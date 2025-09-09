---
title: "抓片神器＋轉檔全能：yt-dlp 與 FFmpeg 終極應用！"
date: 2025-09-09T19:00:00+08:00
draft: false
tags: ["yt-dlp", "ffmpeg", "影音工具", "自由軟體", "教學", "Python"]
categories: ["工具筆記"]
cover:
  image: "https://thf.bing.com/th/id/OIP.5FR4S5tojUE6z_fbTu9cWQHaE8?w=220&h=180&c=7&r=0&o=7&cb=thfc1&dpr=2&pid=1.7&rm=3"
  alt: "yt-dlp 和 FFmpeg 的標誌"
---

在日常工作中，不論是尋找影片素材、下載線上課程，或是處理音樂檔案，我們常常會遇到網頁下載器畫質受限、廣告繁多，或根本不支援某些網站的窘境。

其實，你只需要兩個強大且免費的自由軟體，就能乾淨、快速、高效地解決絕大多數的影音下載與處理需求：

- **yt-dlp**：最強大的影片下載器，支援 YouTube、Vimeo、Bilibili 等上千個網站，是 `youtube-dl` 的進化版。
- **FFmpeg**：影音界的瑞士刀，轉檔、壓縮、剪輯、合併、抽取音訊，幾乎無所不能。

這兩個工具搭配使用，堪稱完美組合。本篇將從安裝到實用指令，帶你一次上手。

---

## 為何選擇 yt-dlp + FFmpeg？

- **持續更新**：YouTube 等影音網站會頻繁改版，`yt-dlp` 的社群非常活躍，能快速修正以應對網站變化。
- **功能強大**：能下載 8K 影片、播放清單、指定格式，甚至處理會員限定內容。
- **批次處理**：FFmpeg 能用簡單的指令處理大量檔案，這是許多圖形介面軟體難以企及的。
- **乾淨無廣告**：完全開源，沒有任何廣告或惡意軟體。

---

## 安裝指南 (Windows, macOS, Linux, Android)

`yt-dlp` 需要頻繁更新，因此使用套件管理器來安裝最為方便。以下將針對不同平台提供最佳安裝方式。

### Windows (使用 Python Pip + 手動安裝 FFmpeg)

此方法適合已安裝 Python 或偏好手動管理工具的使用者。`yt-dlp` 本身是 Python 套件，但它依賴 `FFmpeg` 來處理影片合併與轉檔，因此兩者皆須安裝。

#### **第一步：安裝 Python 與 yt-dlp**

1.  **安裝 Python**：
    *   前往 [Python 官方網站](https://www.python.org/downloads/windows/) 下載最新版的安裝程式。
    *   執行安裝程式，**務必勾選 `Add Python to PATH`** 這個選項，這會自動幫你設定好環境變數。
    *   安裝完成後，開啟新的「**Windows 終端機**」或「**命令提示字元 (CMD)**」，輸入 `python --version` 和 `pip --version`，若能看到版本號，代表安裝成功。

2.  **使用 Pip 安裝 yt-dlp**：
    在終端機中輸入以下指令，即可從 Python 套件索引 (PyPI) 安裝 `yt-dlp`。
    ```powershell
    pip install yt-dlp
    ```

3.  **更新 yt-dlp**：
    日後若要更新 `yt-dlp` 至最新版本，只需執行：
    ```powershell
    pip install --upgrade yt-dlp
    ```

#### **第二步：安裝 FFmpeg 並設定環境變數**

`pip` 不會幫你安裝 FFmpeg，我們需要手動下載並設定，這樣 `yt-dlp` 才能找到它。

1.  **下載 FFmpeg**：
    *   前往 [FFmpeg 官方網站的 Windows Builds 頁面](https://www.gyan.dev/ffmpeg/builds/) (推薦 gyan.dev)。
    *   找到最新的 release 版本 (通常標示為 `ffmpeg-release-full.7z`) 並下載。

2.  **解壓縮檔案**：
    *   將下載的 `.7z` 檔案解壓縮 (可能需要安裝 [7-Zip](https://www.7-zip.org/))。
    *   將解壓縮後的資料夾（例如 `ffmpeg-7.0.1-full_build`）移動到一個你不會輕易刪除的位置，例如 `C:\ffmpeg`。

3.  **設定環境變數 (關鍵步驟)**：
    *   在 Windows 搜尋列中，搜尋「**編輯系統環境變數**」並開啟它。
    *   在跳出的「系統內容」視窗中，點擊「**環境變數**」。
    *   在下方的「**系統變數**」區塊中，找到名為 `Path` 的變數，點選它，然後按「**編輯**」。
    *   在「編輯環境變數」視窗中，點擊「**新增**」，然後貼上你剛剛存放 FFmpeg 的 `bin` 資料夾路徑，例如：`C:\ffmpeg\bin`。
    *   點擊所有視窗的「**確定**」來儲存設定。

4.  **驗證安裝**：
    *   **完全關閉**所有終端機視窗，然後**重新開啟一個新視窗** (這一步很重要，為了讓新的環境變數生效)。
    *   分別輸入以下指令：
        ```powershell
        yt-dlp --version
        ffmpeg -version
        ```
    *   如果兩個指令都能成功顯示版本號，恭喜你，所有工具都已安裝並設定完成！

### macOS

macOS 使用者最方便的選擇是 [Homebrew](https://brew.sh/)。

1.  開啟**終端機 (Terminal)**。
2.  透過 Homebrew 安裝：
    ```bash
    brew install yt-dlp ffmpeg
    ```
3.  日後更新指令：
    ```bash
    brew upgrade yt-dlp ffmpeg
    ```

### Linux (Ubuntu/Debian)

雖然許多發行版的套件庫（如 `apt`）有收錄 `yt-dlp`，但版本可能過舊。官方推薦直接從 GitHub 下載最新的二進位檔，並自行更新。

1.  開啟**終端機**。
2.  下載 `yt-dlp` 主程式並設為可執行：
    ```bash
    sudo wget https://github.com/yt-dlp/yt-dlp/releases/latest/download/yt-dlp -O /usr/local/bin/yt-dlp
    sudo chmod a+rx /usr/local/bin/yt-dlp
    ```
3.  安裝 `ffmpeg`（通常套件庫的版本就很夠用了）：
    ```bash
    sudo apt update && sudo apt install ffmpeg
    ```
4.  `yt-dlp` 日後可以**自我更新**，非常方便：
    ```bash
    sudo yt-dlp -U
    ```

---

## 實用指令教學

> ⚠️ **重要提示**：在終端機中，如果網址包含 `&` `?` 等特殊字元，請務必用雙引號 `"` 將網址包起來，避免指令被錯誤解析。

### yt-dlp：影片與音訊下載

- **下載單一影片 (最高畫質)**：
  ```bash
  yt-dlp "影片網址"
  ```

- **下載整個播放清單**：
  ```bash
  yt-dlp "https://www.youtube.com/playlist?list=XXXX"
  ```

- **列出所有可下載的格式**：
  你會看到影片和音訊的格式代碼 (format code)。
  ```bash
  yt-dlp -F "影片網址"
  ```

- **下載指定的影片和音訊格式並合併**：
  例如，選擇代碼 `137` (1080p 影片) + `140` (m4a 音訊)。
  ```bash
  yt-dlp -f 137+140 "影片網址"
  ```

- **只下載最高品質的音訊**：
  `yt-dlp` 會自動選擇最佳音訊並轉成 m4a 格式。
  ```bash
  yt-dlp -x --audio-format m4a "影片網址"
  ```

### FFmpeg：轉檔與基礎處理

- **基本轉檔 (MP4 轉 WAV)**：
  ```bash
  ffmpeg -i input.mp4 output.wav
  ```

- **轉換影片格式 (MOV 轉 MP4)**：
  `-c copy` 表示直接複製影音流，不重新編碼，速度極快且無損畫質。
  ```bash
  ffmpeg -i input.mov -c copy output.mp4
  ```

---

## 常用指令速查表

| 任務 | 指令 |
| :--- | :--- |
| **下載最高畫質影片** | `yt-dlp "[網址]"` |
| **下載整個播放清單** | `yt-dlp "[播放清單網址]"` |
| **列出所有可用格式** | `yt-dlp -F "[網址]"` |
| **下載指定格式** | `yt-dlp -f [影片代碼]+[音訊代碼] "[網址]"` |
| **僅下載最佳音訊 (轉為m4a)** | `yt-dlp -x --audio-format m4a "[網址]"` |
| **影片轉音訊 (如 mp3)** | `ffmpeg -i in.mp4 -vn -b:a 192k out.mp3` |
| **無損合併多個影片**¹ | `ffmpeg -f concat -safe 0 -i filelist.txt -c copy out.mp4` |
| **壓縮影片 (調整 CRF)**² | `ffmpeg -i in.mp4 -vcodec libx264 -crf 23 out.mp4` |

> ¹ **合併影片註解**：需先建立一個 `filelist.txt`，內容為 `file '1.mp4'` `file '2.mp4'`...
>
> ² **壓縮影片註解**：`crf` 值越低，畫質越好，檔案越大。`18` 接近無損，`23` 是預設值，`28` 壓縮率較高。

---

## 結語

學會 `yt-dlp` 和 `FFmpeg` 這兩個指令工具，就像為自己配備了一間數位影音工作室。你將能夠：

-   **自由下載**：從網路獲取高品質的影音資源，不再受限。
-   **輕鬆轉檔**：將檔案轉換成任何你需要的格式。
-   **提升效率**：用指令自動化處理重複性的影音任務。

這兩個工具是開源社群的寶貴資產，一旦學會，受用無窮。現在就動手安裝，體驗它們的強大之處吧！
```