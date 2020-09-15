---
title: 4种音频格式转单声道wav.md
date: 2019-06-20 16:16:05
tags: ["sox","ffmpeg","mp3","pcm","m4a","wav"]
---

1. pcm 转 wav  
   system("sox -t raw -c 1 -s -b 16 -r 16000 $pcmpath -c 1 -s -r 16000 $wavpath", \$return);

2. wav 转 wav  
   system("ffmpeg -i $sourcepath -acodec pcm_s16le -ac 1 -ar 16000 $wavpath", \$return);

3. mp3 转 wav  
   system("sox " . $wavpatht . " -r 16000 -c 1 " . $wavpath, \$return);

4. m4a 转 wav  
   system("ffmpeg -i $pcmpath -acodec pcm_s16le -ac 1 -ar 16000 $wavpath", \$return);
