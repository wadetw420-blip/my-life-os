# My Life OS v9.3

My Life OS 是一個以 **AI 第二大腦、90 天成長實驗、Daily Log、Cloud Brain、Supabase 記憶層** 為核心的個人作戰控制台。

目前版本：**v9.3 Smart Coach + Stats + PWA**  
部署平台：**GitHub Pages**  
主檔案：`index.html`

---

## 系統定位

My Life OS 不是普通筆記頁，也不是待辦清單。

它的目標是把每天的：

- 學習
- 輸出
- 回顧
- 變現行動
- AI 教練判斷

整合成一個可以持續運作的 AI 作戰系統。

核心方向：

- 建立自由收入
- 建立高自主生活
- 累積可保存、可展示、可變現的能力資產
- 避免只學習、不輸出

---

## v9.3 新增內容

### 1. Smart Coach 智慧教練

Dashboard 會根據以下狀態產生更貼近當下的提醒：

- 目前 Day
- 連續完成天數
- 今日進度
- 最近 Daily Logs
- 學習 / 輸出 / 變現訊號

用途：避免每天只看固定文字，讓系統更像真正的 AI 教練。

### 2. Stats Dashboard 數據儀表板

新增更直覺的統計區：

- 雲端 Daily Logs 數量
- 近 7 筆輸出訊號
- 近 7 筆變現訊號
- 當前天數
- 連續完成天數
- 整體進度

用途：讓成長變得可視化。

### 3. PWA App 化基礎

新增：

- `manifest.json`
- `sw.js`
- GitHub Pages 正確路徑 `/my-life-os/`

用途：未來可用手機瀏覽器「加到主畫面」，以接近 App 的方式開啟。

---

## Repo 結構

```txt
my-life-os/
├── index.html       # Dashboard 主檔
├── README.md        # 專案說明
├── manifest.json    # PWA 設定
├── sw.js            # Service Worker
├── .gitignore       # 忽略本機與暫存檔
└── netlify.toml     # 舊 Netlify 備援設定，暫時保留
```

---

## Supabase Schema

目前 Dashboard 對齊以下資料表：

### ai_state

```txt
id
created_at
level
xp
streak
current_day
```

用途：保存目前 Day、連續完成、等級與 XP。

### daily_logs

```txt
id
created_at
day
content
source
```

用途：保存每日紀錄。`content` 為 JSON 字串。

### weekly_reviews

```txt
id
created_at
week
q1
q2
q3
q4
```

用途：保存每週回顧。

### life_core

用途：保存人生主線、系統模式、核心方向、90 天目標等長期 Context。

### system_exports

用途：保存匯出摘要或系統備份紀錄。

---

## 部署方式

目前使用 GitHub Pages：

```txt
Settings → Pages → Deploy from a branch → main → /(root)
```

正式網址：

```txt
https://wadetw420-blip.github.io/my-life-os/
```

---

## 開發規則

修改前先備份：

```txt
index.html → index_backup_xx.html
```

測試順序：

1. 本機打開新版 HTML
2. 測試畫面是否正常
3. 測試 Daily Log 是否同步 Supabase
4. 測試 Day / streak 是否正確更新
5. 測試手機版是否正常
6. 沒問題再覆蓋 GitHub 的 `index.html`

---

## Reset Dev Mode

開發測試前可重置 Supabase：

```sql
TRUNCATE TABLE daily_logs RESTART IDENTITY;
TRUNCATE TABLE ai_state RESTART IDENTITY;

INSERT INTO ai_state (
  current_day,
  streak,
  level,
  xp
)
VALUES (
  1,
  0,
  1,
  0
);
```

---

## 目前狀態

```txt
STATUS: ACTIVE
VERSION: v9.3
DEPLOYMENT: GitHub Pages
DATABASE: Supabase
ROLE: AI 作戰控制台
```

---

## 下一階段 Roadmap

### v9.4

- 更精準的 Cloud Brain 分析
- 自動偵測最近卡點
- 依照 Daily Log 給每日策略建議

### v9.5

- 更完整的週回顧分析
- 週報自動生成
- 成長曲線圖

### v10

- 更完整的第二大腦系統
- 可擴充模組
- 更接近正式個人 AI OS
