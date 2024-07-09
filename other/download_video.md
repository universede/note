# download_video

### ffmpeg
```shell
ffmpeg  -headers  "Referer: https://v.qq.com/x/cover/mzc00200eyaedxh/v00416jh7p8.html"  -i  "https://apd-ed790218a18afc03fb7e865bae13a2a5.v.smtcdns.com/vipts.tc.qq.com/ALY-KlnqV7D2y1P2hSVDOY9Xrh9jPPKNGv8E0pCGgI8o/uwMROfz2r57AoaQXGdGnC2de6448_15NlFLR-6JgreBXkPz2/svp_50112/Nh3TN1mwqMlox2x3bcjxpb_Br_WslglIxTV9M2zK1mpkA3-3UAWT5jdD7J4PiBn-qYxC8ez0uLLoMluSexrvOfQ8GTr6f2LKG1pnaGa4fYq3Obmlvvulpc-mH7JIxEX5u1fkP5HneSkvzdlDKWpeDMCHRr7jvg2Bxb28y7rjFEnOGBwXQG3wzA/0325_gzc_1000102_0b53fyaacaaaqiagcz6yxnq4alwdaeraabka.f321002.ts.m3u8?ver=4" -c copy xx.mp4
```

### lux
```shell
./lux -c c.txt https://v.qq.com/x/cover/mzc00200eyaedxh/v00416jh7p8.html
```
注意：x.txt里面是cookies的值，在m3u8链接中（F12-> network-> 搜索m3u8）

