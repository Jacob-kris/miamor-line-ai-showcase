# Architecture Overview

## 設計目標

這個系統的重點不是讓 AI 自由聊天，而是把 AI 回覆接到一個可維護的商業 workflow。

核心設計原則：

- LINE 負責入口與訊息互動。
- Serverless webhook 負責事件接收與驗證。
- Workflow engine 負責流程判斷。
- OpenAI API 負責受限制的文字回覆。
- Supabase 負責保存客戶狀態、課程紀錄與 follow-up tasks。
- Admin UI 只負責操作介面，不承擔信任邊界。
- Protected API 負責權限檢查與資料寫入。

## 高層架構圖

![System architecture](../assets/diagrams/system-architecture.svg)

## 主要元件

### LINE User

客戶從 LINE 官方帳號開始互動，可以詢問課程、填寫問卷或接收提醒。

### LINE Webhook

後端接收 LINE message events，並驗證 signature，避免未授權來源直接觸發流程。

### Workflow Engine

根據目前使用者狀態判斷下一步：

- 是否交給 AI 回覆。
- 是否進入課程問卷。
- 是否更新既有問卷進度。
- 是否建立 follow-up task。

### OpenAI API

負責客服回覆，但不負責最終資料真相或權限判斷。

### Supabase

保存系統狀態與任務：

- `line_customers`
- `student_course_records`
- `followup_tasks`
- `admin_sessions`

### Admin UI

提供店家搜尋學生、查看關懷狀態、管理提醒與紀錄整理的工作台。

### Protected API

處理 admin 操作與資料寫入，避免 browser 直接承擔敏感邏輯。

### Vercel Cron

定期觸發提醒與關懷任務。

## 為什麼這樣設計

這個架構讓 AI、資料、權限和操作介面分工清楚：

- AI 負責語意與客服回覆。
- Database 負責狀態。
- Server-side API 負責權限與資料寫入。
- Admin UI 負責人可以理解與操作的流程。

這樣比單純把所有邏輯放在 chatbot prompt 裡更安全，也更容易維護。
