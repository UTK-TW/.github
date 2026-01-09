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

## 標籤系統 (RPG 風格)

專案使用遊戲化的標籤命名系統 (參考 [CONTRIBUTING.md](../CONTRIBUTING.md))：

### 優先級 (Priority)
| 標籤 | 代號 | 說明 |
|-----|------|------|
| P0 | 世界毀滅 (World Boss) | 生產環境停機，全體動員 |
| P1 | 主線劇情 (Main Quest) | Sprint 必須完成 |
| P2 | 支線任務 (Side Quest) | 排入下次 Sprint |
| P3 | 彩蛋 (Easter Egg) | 有資源再處理 |

### 複雜度 (Complexity)
| 標籤 | 代號 | 說明 |
|-----|------|------|
| XS | 史萊姆 (Slime) | 簡單任務，無需討論 |
| S | 哥布林 (Goblin) | 適合 Junior 開發者 |
| M | 菁英怪 (Elite) | 主力任務，佔 Sprint 60% |
| L | 地下城首領 (Boss) | 需 Senior 帶隊 |
| XL | 上古巨龍 (Ancient) | 禁止直接開發，需先拆解 |

## 工作流程自動化

### 自動標籤分配
- **Issue**: 根據標題關鍵字 (`[bug]`, `[feature]`, `[security]`) 和內容自動標籤
- **PR**: 根據 emoji 前綴 (🐛, ✨, 📚) 和變更檔案類型自動標籤
- **PR 大小**: 自動依變更行數標記 `size/XS` ~ `size/XL`

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
