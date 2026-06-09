# Steam 玩家硬體趨勢報告 — 自動化流程
一句話觸發（例如「**更新最新的 Steam report**」），AI 助理即完成
**爬取官網 → 合併資料 → 數據分析 → 產出雙語簡報**的完整流程。

```mermaid
flowchart LR
    subgraph P1[" "]
        direction TB
        P1_Title["階段一：自動取得資料"] ~~~ A
        A["👤 觸發指令\n『更新 Steam report』"] --> B["🌐 爬取 Steam 官網\n（取得最新月份數據）"] --> C["🧹 數據清洗與分類\n（自動補齊規格欄位）"]
    end
    subgraph P2[" "]
        direction TB
        P2_Title["階段二：Excel 數據合併與查核"] ~~~ E
        E{"❓ 發現全新顯卡？"} -- "是" --> F["🙋 詢問確認 DT 桌機值\n（自動更新 Reference）"]
        F --> G{"❓ 該月份數據\n是否已存在？"}
        E -- "否" --> G
        G -- "否" --> H["📊 併入歷史資料庫\n（自動生成 takeaways.md）"]
        G -- "是" --> Z["⏭️ 數據已存在\n（跳過避免重複導入）"]
    end
    subgraph P3[" "]
        direction TB
        P3_Title["階段三：分析與簡報生成"] ~~~ P3_R1
        subgraph P3_R1[" "]
            direction LR
            I["⚙️ 提取關鍵指標\n（重算趨勢數據）"] --> J["🧩 數據注入模板\n（生成雙語簡報檔案）"] --> K["✍️ 分析師觀點撰寫\n（生成雙語 Insight 內容）"]
        end
        subgraph P3_R2[" "]
            direction LR
            L["🔍 瀏覽器自動驗證\n（檢查排版與圖表）"] --> M["✅ 報告發佈完成\n（提供下載連結）"]
        end
        P3_R1 --> P3_R2
    end
    C --> E
    H --> P3_R1
    classDef auto fill:#F4FBF7,stroke:#10B981,color:#064E3B,stroke-width:1.5px;
    classDef human fill:#FFF5F5,stroke:#EF4444,color:#991B1B,stroke-width:2px;
    classDef decision fill:#F8FAFC,stroke:#64748B,color:#334155,stroke-width:1.5px;
    classDef done fill:#EFF6FF,stroke:#3B82F6,color:#1E3A8A,stroke-width:2px;
    class A,F human;
    class B,C,H,I,J,K,L auto;
    class E,G decision;
    class M,Z done;
    style P1 fill:#FAFAFA,stroke:#E2E8F0,stroke-width:1px;
    style P2 fill:#FAFAFA,stroke:#E2E8F0,stroke-width:1px;
    style P3 fill:#FAFAFA,stroke:#E2E8F0,stroke-width:1px;
    style P1_Title fill:none,stroke:none,color:#064E3B,font-weight:bold;
    style P2_Title fill:none,stroke:none,color:#064E3B,font-weight:bold;
    style P3_Title fill:none,stroke:none,color:#064E3B,font-weight:bold;
    style P3_R1 fill:none,stroke:none;
    style P3_R2 fill:none,stroke:none;
```

> 🟩 綠色 = 全自動　🟧 橘色 = 需要你介入　🟦 藍色 = 結束 / 產出

## 重點說明
- **月份慣例**：N 月執行 → 抓 N-1 月（最新公布的調查）。Steam 通常每月頭幾天才公布上月數據。
- **唯一需人工的環節**：只有當出現對照表沒收錄的「全新顯卡型號」時，AI 才會詢問該卡是否為桌機卡（DT 值）；多數月份完全自動。
- **防呆**：同一個月不會重複併入，避免資料倉被污染。
- **資料來源**：[Steam Hardware Survey](https://store.steampowered.com/hwsurvey/)（官方公開調查）。
