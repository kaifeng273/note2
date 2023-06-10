# Line bot + ChatGPT
## 下載open-ai translator 並開啟庫聰功能
下載 openai-translator-chrome-extension 並解壓縮\n
(https://github.com/yetone/openai-translator/releases/tag/v0.0.13)\n
於chrome 開啟擴充功能，並並載入為封裝項目
## ChatGPT整合line
### 1. 註冊 LINE 免費開發者帳號
### 2. fork GPT人工智能助手\n(https://github.com/memochou1993/gpt-ai-assistant)
### 3. 環境設定(使用vercel)
```
【 OpenAI Keys 設定】
Name：OPENAI_API_KEY
Value：值設置貼上 OpenAI 網站產生的 ChatGPT Keys(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)

【 LINE channel access token 設定】
Name：LINE_CHANNEL_ACCESS_TOKEN
Value：將值設置為 LINE 頻道 channel access token

【  LINE channe 設定】
Name：LINE_CHANNEL_SECRET
Value：將值設置為 LINE 頻道 channel secret
```

### 4. 套用到line messageing API
