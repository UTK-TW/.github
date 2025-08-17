# 環友科技 GitHub 組織預設儲存庫 🌐

<div align="center">

![環友科技 Logo](https://www.utk.com.tw/Content/images/logo_blue.svg)

**專業的 GitHub 組織預設設定檔案與模板**

[![GitHub](https://img.shields.io/badge/GitHub-UTK--TW-black?style=for-the-badge&logo=github)](https://github.com/UTK-TW)
[![官方網站](https://img.shields.io/badge/官方網站-utk.com.tw-blue?style=for-the-badge&logo=internet-explorer)](https://www.utk.com.tw/)
[![授權條款](https://img.shields.io/badge/授權-MIT-green?style=for-the-badge)](LICENSE)

</div>

## 📋 專案概述

這是環友科技股份有限公司的 GitHub 組織預設儲存庫，包含了組織層級的設定檔案、Issue 和 Pull Request 模板、社群健康檔案以及組織簡介頁面。這些檔案將自動套用到組織內所有沒有相應檔案的儲存庫。

### 🎯 主要功能

- **🏢 組織簡介頁面** - 在 `github.com/UTK-TW` 顯示的專業形象頁面
- **📝 Issue 和 PR 模板** - 標準化的問題回報和程式碼貢獻流程
- **📚 社群健康檔案** - 貢獻指南、支援說明、安全政策等
- **🏷️ 標籤管理** - 統一的標籤系統和自動同步
- **⚙️ 工作流程** - 自動化的標籤同步和品質檢查

## 📁 檔案結構

```
.
├── profile/
│   └── README.md                    # 組織簡介頁面
├── .github/
│   ├── ISSUE_TEMPLATE/
│   │   ├── bug_report.yml          # 錯誤回報模板
│   │   ├── feature_request.yml     # 功能請求模板
│   │   ├── question.yml            # 問題諮詢模板
│   │   ├── documentation.yml       # 文件改進模板
│   │   └── config.yml              # Issue 模板設定
│   ├── PULL_REQUEST_TEMPLATE/
│   │   └── pull_request_template.md # Pull Request 模板
│   ├── workflows/
│   │   └── sync-labels.yml         # 標籤同步工作流程
│   └── labels.yml                  # 共用標籤定義
├── CONTRIBUTING.md                  # 貢獻指南
├── SUPPORT.md                      # 支援說明
├── SECURITY.md                     # 安全政策
├── LICENSE                         # MIT 授權條款
└── README.md                       # 本檔案
```

## 🚀 快速開始

### 1. 設定組織預設

如果您是組織管理員，這個儲存庫已經自動作為組織預設設定生效。組織內的新儲存庫將自動繼承這些設定。

### 2. 套用到現有專案

對於現有的專案，您可以選擇性地複製需要的檔案：

```bash
# 複製貢獻指南
cp CONTRIBUTING.md your-project/

# 複製支援說明  
cp SUPPORT.md your-project/

# 複製安全政策
cp SECURITY.md your-project/

# 複製授權條款
cp LICENSE your-project/
```

### 3. 自訂專案特定內容

根據專案需求調整檔案內容：

- 更新 Issue 模板的選項和欄位
- 調整 Pull Request 模板的檢查項目  
- 新增專案特定的標籤
- 修改貢獻流程以符合專案需求

## 🛠️ 使用指南

### 🏷️ 標籤管理

本儲存庫包含標準化的標籤系統：

| 類型 | 標籤範例 | 用途 |
|------|---------|------|
| **錯誤相關** | `bug`, `critical-bug`, `regression` | 標記問題和缺陷 |
| **功能相關** | `enhancement`, `feature-request`, `breaking-change` | 功能開發和改進 |
| **文件相關** | `documentation`, `api-docs`, `readme` | 文件改善 |
| **狀態標籤** | `needs-triage`, `in-progress`, `blocked` | 工作流程狀態 |
| **優先級** | `priority-low/medium/high/critical` | 工作優先順序 |
| **技術標籤** | `dotnet`, `csharp`, `azure`, `api`, `database` | 技術分類 |

### 📝 Issue 和 PR 流程

#### 建立 Issue
1. 選擇適當的 Issue 模板
2. 填寫必要資訊
3. 選擇相關標籤
4. 指派負責人（如需要）

#### 提交 Pull Request  
1. 使用 PR 模板
2. 詳細描述變更內容
3. 連結相關 Issue
4. 完成代碼審查檢查清單

## 🤝 參與貢獻

我們歡迎社群的參與和改進建議！

- 📖 **閱讀貢獻指南**: [CONTRIBUTING.md](CONTRIBUTING.md)
- 🐛 **回報問題**: [建立 Issue](../../issues/new/choose)
- 💡 **功能建議**: [功能請求](../../issues/new?template=feature_request.yml)
- 🔒 **安全回報**: 請參考 [SECURITY.md](SECURITY.md)

## 🆘 獲得支援

如果您需要協助：

- 📚 **查閱文件**: [SUPPORT.md](SUPPORT.md)
- 💬 **社群討論**: [GitHub Discussions](../../discussions)
- 📧 **聯絡我們**: sen@utk.com.tw
- 🌐 **官方網站**: [https://www.utk.com.tw/](https://www.utk.com.tw/)

## 🔒 安全政策

我們重視軟體安全性。如果您發現安全漏洞，請參考我們的 [安全政策](SECURITY.md) 進行負責任的揭露。

## 🛡️ 技術棧

我們的主要技術領域：

- ![.NET](https://img.shields.io/badge/.NET_Core-512BD4?style=flat-square&logo=dotnet&logoColor=white) .NET Core / C#
- ![ASP.NET Core](https://img.shields.io/badge/ASP.NET_Core-512BD4?style=flat-square&logo=dotnet&logoColor=white) Web API 開發
- ![Azure](https://img.shields.io/badge/Microsoft_Azure-0078D4?style=flat-square&logo=microsoft-azure&logoColor=white) 雲端部署
- ![SQL Server](https://img.shields.io/badge/Azure_SQL-CC2927?style=flat-square&logo=microsoft-sql-server&logoColor=white) 資料庫設計

## 📋 最佳實務

### 🔄 定期維護

- 定期檢查和更新 Issue 模板
- 根據回饋改進貢獻流程  
- 更新安全政策和聯絡資訊
- 同步最新的標籤定義

### 🎯 品質保證

- 所有變更都需要經過代碼審查
- 遵循一致的程式碼風格
- 確保文件與實際流程同步
- 定期測試模板和工作流程

## 📄 授權條款

本專案採用 [MIT 授權條款](LICENSE)。

---

<div align="center">

**🌟 感謝您對環友科技的關注與支持！ 🌟**

*讓我們一起建立更好的開發體驗*

[🏠 返回組織首頁](https://github.com/UTK-TW) • [📧 聯絡我們](mailto:sen@utk.com.tw) • [🌐 官方網站](https://www.utk.com.tw/)

</div>