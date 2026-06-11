# LINE AI Customer Service & Student Care Workflow

這是一個作品集展示版，介紹一套針對美容教育場景設計的 LINE AI 客服與學生關懷 workflow 系統。

> This is a public showcase repo. It does not include production source code, real customer data, private URLs, API keys, tokens, or business-sensitive configuration.

## 一句話介紹

這不是單純 chatbot，而是一個把 LINE Bot、AI 回覆、課程問卷、學生紀錄、課前提醒與課後關懷串在一起的 AI application prototype。

## 專案背景

美容教育或個人服務型事業常遇到幾個重複問題：

- 客戶從 LINE 詢問課程，店家需要重複回答相似問題。
- 課程前需要收集資料、確認狀態、安排提醒。
- 課後需要持續關懷，但人工追蹤容易漏掉。
- 單純 FAQ chatbot 無法連到營運流程與資料紀錄。

這個專案的目標，是把 AI 客服變成可接到後台 workflow 的應用系統，而不是只做一個會聊天的 bot。

## Demo Screenshots

以下截圖皆為匿名 demo 資料，不包含真實姓名、LINE ID、網址、token 或私密紀錄。

| Search workflow | Records workflow |
|---|---|
| ![Admin search demo](assets/screenshots/admin-search-demo.png) | ![Admin records demo](assets/screenshots/admin-records-demo.png) |

## 系統架構

![System architecture](assets/diagrams/system-architecture.svg)

高層流程：

1. 使用者從 LINE 官方帳號進入。
2. LINE webhook 接收訊息並驗證來源。
3. Workflow engine 判斷目前是 AI 回覆、課程問卷、既有流程延續，或 follow-up 任務。
4. OpenAI API 負責受規則限制的 AI 回覆。
5. Supabase 保存客戶狀態、課程紀錄、follow-up tasks 與 admin sessions。
6. Admin UI 讓店家管理學生關懷狀態與提醒任務。
7. Vercel Cron 觸發排程提醒與關懷任務。

## 核心功能

- LINE Bot webhook integration
- AI customer-service replies
- Structured course questionnaire flow
- Student care admin workbench
- Pre-course reminder workflow
- Post-course care workflow
- Supabase-backed state and task storage
- Protected admin API boundary
- Scheduled follow-up task runner
- Portfolio-ready documentation, screenshots, and architecture diagram

## 技術棧

- LINE Messaging API
- OpenAI API
- Supabase Postgres
- Vercel Serverless Functions
- Vercel Cron
- HTML / CSS / JavaScript admin UI
- Git / GitHub
- AI-assisted development with Codex and Claude Code

## AI / Agent Workflow 設計重點

- AI 不直接決定所有流程狀態；重要狀態由 server-side workflow 與 database 管理。
- prompt 只負責約束 AI 回覆方向，不承擔權限、付款或資料寫入判斷。
- 客戶狀態、問卷進度與 follow-up tasks 由 Supabase 保存。
- Admin 操作透過 protected API 進行，避免把敏感 business logic 放在 browser。
- 回覆與提醒流程分開，讓 AI 客服可以接到後續營運工作。

## 專案成果

目前成果定位為可展示的 AI application prototype：

- 已完成 LINE AI 客服與學生關懷 workflow 的整體設計。
- 已建立 admin workbench 的匿名展示畫面。
- 已整理成面試與 GitHub 作品集可讀的架構文件。
- 已完成 private source repo 與 public showcase repo 的分工規劃。

實際商業成效仍需上線後以完成率、回覆效率、提醒成功率與人工節省時間來量測。

## 我的角色與貢獻

我負責從需求拆解到系統整理的完整流程：

- 將美容教育場景中的客服與關懷流程拆解成可實作的 workflow。
- 設計 LINE Bot、AI 回覆、Supabase storage、Admin UI 與排程任務的邊界。
- 使用 Codex / Claude Code 輔助開發、除錯、文件整理與安全檢查。
- 建立作品集 README、架構圖、匿名截圖與面試說明文件。

## Demo 流程展示

目前這份 showcase 可以透過 README、架構圖與匿名截圖理解主要流程。

未來若補上短版 demo video，會展示以下端到端流程：

1. 使用者從 LINE 開始課程諮詢。
2. 後端依照 workflow logic 判斷訊息要進入哪個流程。
3. AI 在產品規則與 prompt 邊界內產生回覆。
4. 學生關懷任務出現在 admin workbench。
5. 店家操作人員查看提醒、紀錄與關懷狀態。

任何 demo video 都只會使用匿名資料，不會顯示真實客戶紀錄、private admin link、environment variables 或 production settings。

## Roadmap

- 補一支短版匿名 demo video。
- 補更清楚的 Agent workflow diagram。
- 補更多匿名 demo case。
- 強化 production hardening，例如 follow-up idempotency、observability、access control 與資料隱私流程。

## 注意事項

- 此 repo 是 public showcase，不是完整開源專案。
- 完整 source code、production secrets、真實客戶資料與商業敏感流程不公開。
- 截圖與案例均使用 demo data。
- 若需要看 source code，可於面試或合作討論時提供 private repo access。
