# 📊 Steam 玩家硬體趨勢分析報告 — AI 自動化數據管線系統

> **商業痛點解決方案：** 一句指令完成「網頁爬蟲 → 資料清洗 → ETL 整合 → AI 商業洞察撰寫 → 產出雙語互動式簡報」，將原本需要 2–3 小時的跨部門例行性手動報告作業，壓縮至秒級自動化觸發。

![Claude Code](https://img.shields.io/badge/Built_with-Claude_Code-green?logo=anthropic)
![Python](https://img.shields.io/badge/Python-3.10+-blue?logo=python&logoColor=white)
![LLM Integration](https://img.shields.io/badge/LLM-Prompt_Engineering-green)
![Data Pipeline](https://img.shields.io/badge/Data_Pipeline-ETL_/_Pandas-orange)
![Bilingual Support](https://img.shields.io/badge/Language-Traditional_Chinese_/_EN-purple)
![Data Source](https://img.shields.io/badge/Data_Source-Steam_Hardware_Survey-black?logo=steam)

---

## 🎯 專案核心價值與背景

在數據分析師的日常工作中，跨部門的例行性報告（如月報、季報）往往佔用大量時間。本專案為其中之一實際工作產出，針對全球指標性遊戲平台 **Steam 的硬體調查報告** 建立自動化管線（Data Pipeline）。

本系統不僅完成資料的採集與清洗，更串接 **LLM (Claude API)**，以專業數據分析師的視角自動撰寫**中英雙語的深度商業洞察 (Business Insights)**，最終輸出單一檔案、零依賴、具備即時切換語系的互動式 HTML 簡報（共 12 頁），直接滿足管理階層與跨國團隊的決策需求。

---

## ✨ 數據分析師核心職能與技術棧

本專案展現了現代數據分析師（Data Analyst）必備的四大核心能力：**數據工程（ETL）**、**商業洞察（BI）**、**AI 應用落地（LLM Ops）** 與 **前端視覺化溝通**。

| 職能面向 | 核心技術 / 工具 | 具體實現內容 |
|------|------------|------------|
| **資料採集與清洗 (ETL)** | `Python` / `requests` / `BeautifulSoup` | 自動化網頁爬蟲，精準解析 Steam 官網結構並建立防呆機制。 |
| **數據處理與倉儲** | `Pandas` / `openpyxl` | 歷史數據縱向合併、自動 GPU 型號分類（Vendor/Series/DT）、異常值與重複導入查核。 |
| **AI 洞察與自動化** | `Claude Code` / `Prompt Engineering` | 結合 `takeaways.md` 趨勢信號，驅動 AI 進行「非單純複述數字」的深度趨勢成因解讀。 |
| **商業視覺化 (BI)** | `HTML5` / `Vanilla JS` / `CSS3` | 打造無外部依賴（Zero-dependency）的互動簡報，支援雙語即時切換、圖表動態高亮。 |
| **軟體工程素養** | `Git` / `GitHub` | 完備的專案目錄結構、欄位規格書（Schema）與設計系統（Design System）文件管理。 |

---

## 🔄 數據自動化管線流程

```
[觸發指令]
│
▼
refresh_steam_data.py  ──► 網路爬蟲：自動抓取最新月份 Steam 官網數據
│                     ──► 資料清洗：GPU 欄位正規化、AMD 集顯整合、自動補齊分類
▼
build_data.py          ──► ETL 整合：讀取 Excel 歷史數據庫，進行增量更新 (Incremental Update)
│                     ──► 品質控管：防呆機制攔截重複資料，自動偵測未知型號觸發人工檢查
▼
build_dashboard.py     ──► AI 洞察分析：調用 Claude API 讀取趨勢信號，生成雙語 Insights
│                     ──► 簡報注入：將結構化數據 const D 與 AI 洞察注入 template.html
▼
[產出終端報告]         ──► 自動產出：steam-dashboard-YYYY-MM.html (雙語、互動、免安裝)
```

### 🛠️ 關鍵資料處理決策 (Data Governance)
* **月份慣例 (Month Convention)**：嚴格遵循業務邏輯，N 月執行腳本時自動抓取並標記為 N-1 月數據（因 Steam 於每月初發布上月完整調查）。
* **維度過濾 (Data Filtering)**：精準鎖定市場焦點，過濾並僅保留獨立桌機顯示卡（DT=1），涵蓋最新的 NVIDIA RTX 50/40 系列及主流世代，確保分析不被筆電或內顯雜訊干擾。
* **指標標準化**：將原始資料之小數點份額統一轉換為標準百分比（Market Share %），並在 `takeaways.md` 中自動重算跨月增減率（MoM Changes）。

---

## 📁 專案架構與規範文件

良好的專案結構與文件化，是團隊協作與系統可維護性的基石：

```
steam-hw-dashboard/
├── scripts/
│   ├── refresh_steam_data.py   # 階段一：爬蟲、資料清洗與 Excel 寫入
│   ├── build_data.py           # 階段二：歷史資料庫整合與未知型號查核
│   └── build_dashboard.py      # 階段三：串接 LLM API 與自動化簡報生成
├── assets/
│   └── template.html           # 前端 UI：中英雙語 i18n 互動式簡報模板（12 slides）
├── reference/
│   ├── data-schema.md          # 數據治理：Excel 倉儲欄位規格與型號定義文件
│   └── design-system.md        # 視覺規範：色彩、字型、圖表層次與 UI 設計系統
├── SKILL.md                    # LLM 運作手冊：Prompt Engineering 架構與 AI 調整指引
└── WORKFLOW.md                 # 系統營運手冊：自動化排程與維護流程說明
```

---

## 🖥️ 終端報告視覺與互動亮點

* **零外部依賴 (Zero-dependency)**：封裝為單一 HTML 檔案，內建所有樣式與邏輯，跨平台離線即開即用，免除 Node.js 環境配置。
* **國際化支持 (i18n)**：全頁面支援 **繁體中文 ↔ 英文** 點擊即時切換，所有數據指標與 AI 洞察同步變更。
* **聚焦視覺化 (Data Visualization UX)**：歷史趨勢圖表中，Top 4 核心類別使用品牌色著色，其餘自動歸類為灰階，創造極佳的視覺層次；點擊圖例可動態高亮特定序列，並提供「⟲ 顯示全部」重置按鈕。

---
💡 *資料來源：[Steam Hardware Survey](https://store.steampowered.com/hwsurvey/) — Valve 官方每月公開調查數據。*
