# converter_spring

#### 所使用技术
   - Retrofit[^1]
   - springboot

#### 合同下载的反思
   反观过去一周,花了一周的时间做**合同下载**的这一功能(增值服务(基础服务)),主要从三方面造成了工作效率低,一是不熟悉流的使用;二是对spring源码不理解;三是不知道第三方开放的工具类的使用.
   对接第三方源码:
   retrofit - api:
   ```java
    @Streaming
    @POST("api/contract/download")
    @FormUrlEncoded
    @Headers("Content-Type: application/x-www-form-urlencoded")
    Call<ResponseBody> download(@Field("contract_id") String contractId);
   ```
   retrofit - service:
   ```java
   public ResponseBody download(String contractId) throws IOException {
        return contractApi.download(contractId)
                .execute()
                .body();
   }
   ```
   对接业务源码(对外部):
   api:
   ```java
    @PostMapping(value = "/contract/downloads", produces = {MediaType.APPLICATION_OCTET_STREAM_VALUE, MediaType.APPLICATION_JSON_VALUE, "application/zip"})
    ResponseEntity<ResFileResult> downloads(@RequestParam String orderCode);
   ```
   service:
   ```java
   @Override
    public ResponseEntity<ResFileResult> downloads(String orderCode) {
      // 业务逻辑就是把第三方的合同文件保存在本地,然后返回ResponseBody,然后转成ResFileRest返回给业务层
    }
   ```
#### 分析
&emsp;&emsp;在分析之前,需要了解一下Retrofit网络请求框架,和Feign这个差不多,都是为作网络请求而设计的.Retrofit主要包含三部分,一是**OkHttpClient**类;而是**Call<T>**类;三是**ServiceMethod**类.
**OkHttpClient**: 为请求创建一个客户端
**Call<T>**: 
**ServiceMethod**:  
* 设计模式
&emsp;&emsp;已知最多的是构建者模式和策略模式
* 分析
&emsp;&emsp;因为合同下载第三方返回时是两种类型,成功是流;失败是json数据.最后可以得到都是流,只是这个流会根据框架进行转换.我做这个时,最开始返回的数据不是ResponseBody,结果spring框架在转换时不成功.在Retrofit框架时,如果使用了@Streaming注解,它总会去找Retrofit框架中的默认实现去转换,而不会去找自定义的转换(不是很理解),源码中我没找到体现.
源码:
OkHttpCall.java
```java
    ...
Response<T> parseResponse(okhttp3.Response rawResponse) throws IOException {
    ...
    @Override public Response<T> execute() throws IOException {
    ....
     return parseResponse(call.execute());
    }    
    ...
    ExceptionCatchingRequestBody catchingBody = new ExceptionCatchingRequestBody(rawBody);
    try {
      T body = serviceMethod.toResponse(catchingBody);
      return Response.success(body, rawResponse);
    } catch (RuntimeException e) {
      // If the underlying source threw an exception, propagate that rather than indicating it was
      // a runtime exception.
      catchingBody.throwIfCaught();
      throw e;
    }
}
```
ServiceMethod.java
```java
  /** Builds a method return value from an HTTP response body. */
  R toResponse(ResponseBody body) throws IOException {
    return responseConverter.convert(body);
  }
```
BuiltInConverters.java
```java
  ....
  @Override
  public Converter<ResponseBody, ?> responseBodyConverter(Type type, Annotation[] annotations,
      Retrofit retrofit) {
    if (type == ResponseBody.class) {
      return Utils.isAnnotationPresent(annotations, Streaming.class)
          ? StreamingResponseBodyConverter.INSTANCE
          : BufferingResponseBodyConverter.INSTANCE;
    }
    if (type == Void.class) {
      return VoidResponseBodyConverter.INSTANCE;
    }
    return null;
  }

  @Override
  public Converter<?, RequestBody> requestBodyConverter(Type type,
      Annotation[] parameterAnnotations, Annotation[] methodAnnotations, Retrofit retrofit) {
    if (RequestBody.class.isAssignableFrom(Utils.getRawType(type))) {
      return RequestBodyConverter.INSTANCE;
    }
    return null;
  }
  ....
  static final class RequestBodyConverter implements Converter<RequestBody, RequestBody> {
    static final RequestBodyConverter INSTANCE = new RequestBodyConverter();

    @Override public RequestBody convert(RequestBody value) throws IOException {
      return value;
    }
  }

  static final class StreamingResponseBodyConverter implements Converter<ResponseBody, ResponseBody> {
    static final StreamingResponseBodyConverter INSTANCE = new StreamingResponseBodyConverter();

    @Override public ResponseBody convert(ResponseBody value) throws IOException {
      return value;
    }
  }

  static final class BufferingResponseBodyConverter implements Converter<ResponseBody, ResponseBody> {
    static final BufferingResponseBodyConverter INSTANCE = new BufferingResponseBodyConverter();

    @Override public ResponseBody convert(ResponseBody value) throws IOException {
      try {
        // Buffer the entire body to avoid future I/O.
        return Utils.buffer(value);
      } finally {
        value.close();
      }
    }
  }
```
Spring框架中的类型转换源码:
AbatractMessageConverterMethodProcessor.java
```java
  protected <T> void writeWithMessageConverters(@Nullable T value, MethodParameter returnType,
	ServletServerHttpRequest inputMessage, ServletServerHttpResponse outputMessage)
		throws IOException, HttpMediaTypeNotAcceptableException, HttpMessageNotWritableException {
		...
		if (body != null && producibleTypes.isEmpty()) {
			throw new HttpMessageNotWritableException("No converter found for return value of type: " + valueType);
		}
		...
		if (isContentTypePreset || !CollectionUtils.isEmpty(producibleMediaTypes)) {
			throw new HttpMessageNotWritableException("No converter for [" + valueType + "] with preset Content-Type '" + contentType + "'");
		}
		....    
  }
```
主要是报这两个异常,第一个异常是因为在下载合同是返回的**application/zip**的类型,而spring源码中,会自动处理为**\*/\***的类型,自动会处理不了,需要在**@PostMapping**注解中添加*product**属性,表示指定返回类型.而第二个异常的主要原因还是返回过程中实体类虽然是一样的,但多包了一个实体;还有一种情况就是ResponseEntity需要重新构建一个请求和响应的头(HttpHeader).

#### 参考文献
[^1]:https://square.github.io/retrofit/