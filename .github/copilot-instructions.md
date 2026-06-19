# GitHub Copilot 指引 - 環友科技 (UTK) GitHub 組織預設儲存庫

## 專案概述

這是 **環友科技 (UTK-TW)** 的 GitHub 組織預設儲存庫 (`.github` repository)，包含組織層級的：
- Issue/PR 模板與自動化工作流程
- 社群健康檔案 (CONTRIBUTING, SECURITY, SUPPORT)
- 標籤系統定義與同步機制
- 組織簡介頁面 (`profile/README.md`)

此儲存庫的設定會自動套用到組織內所有沒有對應檔案的專案。

## 技術棧

環友科技主要使用的技術：
- **後端**: .NET 8 / C# 12 / ASP.NET Core 8 / Entity Framework Core 8
- **雲端**: Microsoft Azure (Container Apps, Functions, App Service, SQL)
- **DevOps**: GitHub Actions, Docker, Kubernetes, Azure DevOps
- **資料庫**: SQL Server 2022, Azure SQL, Redis, Cosmos DB

## 目錄結構

```
.github/                    # GitHub 特定設定
├── ISSUE_TEMPLATE/        # Issue 模板 (bug_report.yml, new_quest_spec.yml)
├── PULL_REQUEST_TEMPLATE/ # PR 模板
├── workflows/             # GitHub Actions 自動化工作流程
└── labels.yml             # 統一標籤定義
profile/                   # 組織首頁顯示內容
scripts/                   # 開發輔助腳本
```

## 標籤系統

標籤的單一來源為 [`labels.yml`](labels.yml)，共 **45 個全正體中文標籤**，採「中文前綴 + 半形冒號空格」格式（如 `類型: 錯誤`）。八大維度：

| 維度 | 前綴 | 標籤值 |
|-----|------|------|
| 類型 | `類型:` | 錯誤、功能、重構、效能、安全、測試、文件、建置、雜務、相依套件、設計、資料遷移 |
| 領域 | `領域:` | 前端、後端 API、資料庫、身分驗證、排程作業、基礎設施與部署、監控與日誌、設定組態、金流與結帳、第三方整合、通知與訊息 |
| 優先 | `優先:` | P0、P1、P2、P3（未貼即視為未排程） |
| 狀態 | `狀態:` | 待分類、進行中、等待審查、受阻、待補資訊、停滯 |
| 環境 | `環境:` | 開發、測試、正式 |
| 無效 | `無效:` | 重複、不成立、不修正 |
| 討論/協作 | `討論:` / `協作:` | 問題詢問、徵求協助 |
| 特殊標記 | `標記:` | 破壞性變更、回歸、線上事故、緊急修補 |

> [CONTRIBUTING.md](../CONTRIBUTING.md) 以「冒險者公會」風格描述 `優先:` 系列（P0 世界毀滅、P1 主線劇情…）。**難度/規模不使用標籤**，改記錄於 GitHub Projects 的 Estimate 數字欄位（已移除 `size:*` 與 `risk:*`）。

## 工作流程自動化

### 自動標籤分配
- **Issue**: 根據標題關鍵字 (`[bug]`, `[feature]`, `[security]`) 和內容自動貼上對應的 `類型:`／`領域:`／`優先:`／`狀態:` 標籤
- **PR**: 根據 emoji 前綴 (🐛, ✨, 📚) 和變更檔案類型自動貼上 `類型:`／`領域:` 標籤
- **PR 大小**: 僅於 PR 留言提示變更規模，**不再貼 `size/*` 標籤**（規模改用 Projects Estimate）

### 關鍵 Workflows
- `issue-labeler.yml` - Issue 自動分類
- `pr-automation.yml` - PR 自動標籤與大小檢查
- `sync-labels-to-all-repos-fixed.yml` - 同步標籤到所有儲存庫
- `stale-issues.yml` - 過期 Issue 自動處理

## 貢獻規範

### Commit 訊息格式
使用 Conventional Commits，搭配 emoji 前綴：
- 🐛 `fix:` 錯誤修復
- ✨ `feat:` 新功能
- 📚 `docs:` 文件更新
- 🔒 `security:` 安全修復
- 🧪 `test:` 測試相關

### PR 提交流程
1. 建立分支進行開發
2. PR 描述中使用 `Fixes #123` 連結 Issue
3. 完成 PR 模板中的檢查清單 (目標 80%+)
4. PR 合併後，連結的 Issue 自動關閉

## 安全回報

**重要**: 安全漏洞請勿透過公開 Issue 回報！

- 安全聯絡: `sen@utk.com.tw`
- 回應時間: 24 小時內確認，72 小時內提供修復計畫
- 詳見 [SECURITY.md](../SECURITY.md)

## 編輯指引

修改此儲存庫時請注意：
1. **YAML 格式**: 工作流程使用 GitHub Actions 語法，標籤顏色為 6 位 hex (不含 #)
2. **Markdown 模板**: Issue/PR 模板支援 YAML frontmatter 定義欄位
3. **同步影響**: `labels.yml` 變更會同步到組織內所有儲存庫
4. **雙語支援**: 文件同時支援中英文關鍵字識別

## 有用的資源

- [CONTRIBUTING.md](../CONTRIBUTING.md) - 完整貢獻指南 (冒險者公會風格)
- [SUPPORT.md](../SUPPORT.md) - 支援管道與 SLA
- [profile/README.md](../profile/README.md) - 組織首頁內容
