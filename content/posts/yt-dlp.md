---
title: "抓片神器＋轉檔全能：yt-dlp 和 FFmpeg 實用筆記"
date: 2025-09-09T19:00:00+08:00
draft: false
tags: ["yt-dlp", "ffmpeg", "影音工具", "自由軟體"]
categories: ["工具筆記"]
cover:
  image: "img/yt-dlp-ffmpeg-cover.png"
  alt: "yt-dlp 和 FFmpeg"
---

平常在找影片素材或處理音樂時，光靠網頁下載器常常畫質受限、廣告一堆。其實只要兩個自由軟體，就能乾淨又快速地完成工作：

- **yt-dlp**：幾乎所有影片網站都能下載  
- **FFmpeg**：轉檔、壓縮、拼接、處理聲音的萬能工具  

---

## 安裝

### Linux（Ubuntu 為例）

> sudo apt install yt-dlp ffmpeg

macOS

先裝 Homebrew，再輸入：

> brew install yt-dlp ffmpeg

Windows

一般使用者可以直接去官網下載：

yt-dlp

FFmpeg


想省事的人，也能用 Chocolatey：

choco install yt-dlp ffmpeg


---

yt-dlp：影片與音訊下載

> **影片網址的前後需要有" "不然沒辦法正常運行**

下載單一影片：

yt-dlp [影片網址]

下載整個播放清單：

yt-dlp "https://www.youtube.com/playlist?list=XXXX"

列出可抓的格式：

yt-dlp -F [影片網址]
記得列出來的所有數字

只抓音訊（例如 m4a）：

yt-dlp -f 140 [影片網址]

支援網站超過一千種，YouTube、Vimeo、Twitch、Bilibili… 幾乎想得到的都能下載。


---

FFmpeg：轉檔與處理

基本轉檔：

ffmpeg -i [輸入檔] [輸出檔]

例如把 MP4 轉成 WAV：

ffmpeg -i demo.mp4 demo.wav

它不只轉檔，還能壓縮影片、合併檔案、裁切、加濾鏡。專業剪輯軟體做不到的批次處理，用 FFmpeg 幾乎都能解決。


---

常用指令速查表

下載影片：yt-dlp [網址]

下載播放清單：yt-dlp [清單網址]

列出格式：yt-dlp -F [網址]

指定格式下載：yt-dlp -f [代碼] [網址]

影片轉音訊：ffmpeg -i in.mp4 out.wav

合併影片：ffmpeg -i "concat:1.mp4|2.mp4" -c copy out.mp4

壓縮影片：ffmpeg -i in.mp4 -vcodec libx264 -crf 23 out.mp4



---

結語

學會 yt-dlp + FFmpeg，就能：

把影片或音訊抓下來

輕鬆轉成需要的格式

提高處理效率，不靠雜七雜八的軟體


這兩個工具，安裝一次，受用無窮。


