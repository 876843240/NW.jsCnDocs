# Enable Proprietary Codecs
---
[TOC]

## Supported Codecs in Prebuilt NW.js Binary
 已经支持预编译NW.js的二进制格式
As NW.js is based on Chromium, the media components are essentially the same.
NW.js是基于Chromium的，这个media组件也基本上是基于chromium的
In the pre-built NW.js, following codecs are supported:
在预编译NW.js时,如下的解码方式是支持的：
```none
theora,vorbis,vp8,pcm_u8,pcm_s16le,pcm_s24le,pcm_f32le,pcm_s16be,pcm_s24be
```

and following demuxers are supported:
并且如下的分配器也是被支持的
```none
ogg,matroska,wav
```

## Enable Proprietary Codecs in NW.js

!!! warning "License and Patent Fee"
    MP3 and H.264 codecs are licensed under the GPL in `ffmpeg` used by NW.js. Make sure your app are released with compatible license of GPL. And you also have to pay patent licensing royalties for using them. Consult a lawyer if you do not understand the licensing constraints and using patented media formats in your application.
警告，“许可 和 专利费”
   MP3和H.264解码器在nw.js中是基于GPL的‘ffmpeg’许可胡，确保你的app能够兼容GPL许可，并且你在使用的时候必须要付专利使用的费用。相关问题，请咨询律师，确保获得许可再使用。
In order to use MP3 and H.264, you'll need to compile ffmpeg with patch and corresponding options.
为了使用MP3和H.264,在编译ffmpeg的时候，你需要一些补丁和相应的配置选项;
**Step 1.** Apply following patch to `third_party/ffmpeg/ffmpeg.gyp` to make `ffmpeg` include the codecs:
 第一步、将如下的补丁打到 `third_party/ffmpeg/ffmpeg.gyp`,让`ffmpeg`能包含解码器：
```diff
diff --git a/ffmpeg.gyp b/ffmpeg.gyp                   
index 294dd2e..7dfcd3a 100755                          
--- a/ffmpeg.gyp                                       
+++ b/ffmpeg.gyp                                       
@@ -72,7 +72,7 @@                                      
       ['chromeos == 1', {                             
         'ffmpeg_branding%': '<(branding)OS',          
       }, {  # otherwise, assume Chrome/Chromium.      
-        'ffmpeg_branding%': '<(branding)',            
+        'ffmpeg_branding%': 'Chrome'                  
       }],                                             
     ],                                                
```

**Step 2.** Setup `GYP_DEFINES` to `proprietary_codecs=1` to turn on codecs support on Chromium side.
第二步、安装 `GYP_DEFINES`到 `proprietary_codecs=1`，这是为了让解码器支持chromium。
**Step 3.** Regenerate the gyp files again with `gclient runhooks`.
第三步、 用`gclient runhooks`更新gyp文件。
**Step 4.** Rebuild NW.js with `ninja -C out/Release nwjs`.
第四步、用`ninja -C out/Release nwjs`重新编译nw.js
