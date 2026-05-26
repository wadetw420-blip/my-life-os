[README.md](https://github.com/user-attachments/files/28260194/README.md)
# My Life OS v8.9

My Life OS 是一個以 **AI 第二大腦、90 天成長實驗、Daily Log、Cloud Brain、Supabase 記憶層** 為核心的個人作戰控制台。

目前版本：**v8.9 State Reset**  
部署平台：**GitHub Pages**  
主檔案：`index.html`

---

## 系統定位

My Life OS 不是單純筆記頁，也不是一般待辦清單。

它的目標是把每天的學習、輸出、回顧與變現行動整合成一個可持續運作的 AI 作戰系統。

核心方向：

- 建立自由收入
- 建立高自主生活
- 建立可累積能力資產
- 用 AI 加速學習、輸出與變現
- 透過 Supabase 保存長期狀態與每日紀錄

---

## 線上網址

GitHub Pages：

```txt
https://wadetw420-blip.github.io/my-life-os/
```

---

## Repo 結構

```txt
my-life-os/
├── README.md        # 專案說明
├── index.html       # My Life OS Dashboard 主檔
├── manifest.json    # PWA / 手機安裝設定
└── netlify.toml     # 舊 Netlify 部署設定，暫時保留
```

---

## 目前版本功能

### 1. AI 作戰控制台

顯示目前狀態：

- Day 進度
- Supabase 連線狀態
- 連續完成天數
- 角色等級
- 目前階段

---

### 2. 今日唯一主線

每天只聚焦一個最重要任務，避免陷入：

- 一直整理系統
- 一直研究工具
- 一直學習但沒有輸出

---

### 3. 今日執行面板

包含：

- 今日主題
- AI 雲端主腦建議
- 今日避免事項
- 今日輸出目標
- 今日變現相關行動
- 固定時間表
- 今日附加目標

---

### 4. Daily Log 每日紀錄

每日填寫：

- 今天學到什麼
- 今日成果
- 遇到的問題
- 下一步

按下「同步今日紀錄」後，資料會寫入 Supabase 的 `daily_logs`。

---

### 5. Cloud Brain / Supabase 記憶層

目前使用 Supabase 作為主雲端資料層。

主要資料表：

```txt
ai_state
- id
- created_at
- level
- xp
- streak
- current_day

daily_logs
- id
- created_at
- day
- content
- source

life_core
- version
- life_goal
- system_mode
- current_day
- core_direction
- ninety_day_goal
- current_focus
- decision_rules
- fallback_strategy
- source_markdown

weekly_reviews
- week
- q1
- q2
- q3
- q4

system_exports
- export_type
- summary
```

---

## v8.9 修正重點

v8.9 主要修正狀態同步問題：

- 勾選固定時間表不會跳 Day
- 勾選今日附加目標不會跳 Day
- 只有「同步今日紀錄」成功後才會進入下一天
- 同步成功後 Daily Log 欄位會清空
- 同步成功後固定時間表勾選會重置
- 同步成功後今日附加目標勾選會重置
- `ai_state.streak` 與 Supabase 真實 schema 對齊
- 重新整理後優先讀取 Supabase `ai_state`
- `daily_logs` 不再反推 Day，避免測試資料污染狀態

---

## 正確使用流程

每日使用流程：

```txt
1. 打開 Dashboard
2. 看今日唯一主線
3. 完成今日主線任務
4. 填寫 Daily Log 四欄
5. 按「同步今日紀錄」
6. 成功後系統自動進入下一天
```

平常操作以「同步今日紀錄」為主。

其他功能：

- 「同步主腦狀態」：需要更新長期系統狀態時使用
- 「匯出 MD 備份」：需要備份或交給其他 AI 時使用

---

## 測試 / Reset Dev Mode

開發或測試新版前，可以用以下 SQL 將 Supabase 回到乾淨 Day 1 狀態：

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

重置後應為：

```txt
Day 1
streak 0
level 1
xp 0
daily_logs empty
```

---

## 部署方式

目前使用 GitHub Pages。

設定：

```txt
Source: Deploy from a branch
Branch: main
Folder: /root
```

只要更新 `index.html` 並 commit 到 `main`，GitHub Pages 會自動部署。

---

## 檔案更新規則

### 更新 Dashboard

只需更新：

```txt
index.html
```

### 更新 PWA / 手機安裝資訊

更新：

```txt
manifest.json
```

### 更新專案說明

更新：

```txt
README.md
```

### Netlify

`netlify.toml` 目前為舊 Netlify 部署備援設定。  
因 Netlify 帳號曾被暫停，現在主要部署已改為 GitHub Pages。

建議保留一段時間，確認 GitHub Pages 穩定後再刪除。

---

## Roadmap

後續版本可考慮：

- v9：更完整的 Cloud Brain 分析
- v9.5：自動產生今日唯一主線
- v10：真正的 AI 教練回饋系統
- PWA 手機安裝優化
- Weekly Review 視覺化
- 90 天進度圖表
- 匯出完整 Markdown 報告

---

## 原則

```txt
系統是工具，不是成果。
```

真正目標是：

```txt
輸出
成長
變現
自由收入
人生主線推進
```
