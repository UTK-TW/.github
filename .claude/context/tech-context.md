---
created: 2025-09-02T18:49:02Z
last_updated: 2025-09-02T18:49:02Z
version: 1.0
author: Claude Code PM System
---

# 技術環境文件

## 專案類型
**GitHub 組織預設儲存庫** - 非程式語言專案，專注於：
- 組織層級配置管理
- Claude Code SuperClaude 框架
- GitHub 自動化工作流程
- 專案管理和文件範本

## 主要技術堆疊

### 組織技術環境
根據 README.md，UTK-TW 組織主要使用：
- **.NET 8.0 / .NET Core** - 主要開發框架
- **ASP.NET Core MVC/API** - Web 應用程式開發
- **Entity Framework Core** - 資料存取層
- **Azure 雲端服務** - 雲端基礎設施
- **Azure SQL** - 資料庫解決方案
- **Windows Server/IIS** - 部署環境
- **工作排程器** - 自動化任務管理

### Claude Code 技術堆疊
- **Claude Code** - AI 驅動開發環境
- **SuperClaude 框架** - 智能路由和協調系統
- **MCP (Model Context Protocol)** - 伺服器整合協議
- **YAML 配置** - 結構化設定管理
- **Markdown** - 文件撰寫和範本系統
- **Bash 腳本** - 自動化工具和工作流程

## 開發工具

### 版本控制
- **Git** - 版本控制系統
- **GitHub** - 程式碼託管和協作平台
- **GitHub CLI (gh)** - 命令列介面工具
  - 版本: 2.76.2 (2025-07-30)
  - 擴充功能: 1 個已安裝 (gh-sub-issue)

### GitHub 自動化
- **GitHub Actions** - CI/CD 和工作流程自動化
- **標籤同步工作流程** - 跨儲存庫標籤統一管理
- **Issue 和 PR 模板** - 標準化工作流程

### Claude Code 工具
- **子代理程式系統**:
  - `code-analyzer` - 程式碼分析和漏洞檢測
  - `file-analyzer` - 檔案內容摘要和分析
  - `parallel-worker` - 平行處理協調
  - `test-runner` - 測試執行和結果分析

## 配置管理

### 權限設定
```json
{
  "permissions": {
    "allow": [
      "Bash(pnpm lint:*)",
      "Bash(pnpm build:*)",
      "Bash(pnpm generate:docs:*)",
      "Bash(git add:*)"
    ],
    "deny": [],
    "ask": []
  }
}
```

### 標籤系統
定義在 `.github/labels.yml` 中的統一標籤：
- **錯誤相關**: `bug`, `critical-bug`, `regression`
- **功能相關**: `enhancement`, `feature-request`, `breaking-change`
- **文件相關**: `documentation`, `api-docs`, `readme`
- **狀態標籤**: `needs-triage`, `in-progress`, `blocked`
- **優先級**: `priority-low/medium/high/critical`
- **技術標籤**: `dotnet`, `csharp`, `azure`, `api`, `database`

## 整合系統

### GitHub 整合
- **ORG_PAT_TOKEN** - 組織個人存取令牌
- **標籤同步** - 自動跨儲存庫標籤管理
- **Issue 模板** - 標準化問題回報流程
- **PR 模板** - 統一程式碼審查流程

### SuperClaude MCP 伺服器
根據框架配置，可整合的 MCP 伺服器：
- **Context7** - 文件和研究整合
- **Sequential** - 複雜分析和思考
- **Magic** - UI 元件和設計
- **Playwright** - 瀏覽器自動化和測試

## 部署和操作

### Git 工作流程
- **主分支**: `main`
- **遠端儲存庫**: https://github.com/UTK-TW/.github.git
- **分支策略**: 直接在主分支上工作
- **提交規範**: 使用表情符號和慣例性提交訊息

### 自動化腳本
- **PM 系統初始化**: `.claude/scripts/pm/init.sh`
- **測試和日誌**: `.claude/scripts/test-and-log.sh`
- **狀態管理**: 多個專案管理腳本

### 監控和日誌
- **Git 狀態監控** - 自動檢查工作樹狀態
- **權限驗證** - GitHub 認證和權限檢查
- **依賴關係檢查** - 必要工具和擴充功能驗證

## 系統需求

### 必要工具
- **Git** - 版本控制
- **GitHub CLI (gh)** - GitHub 操作
- **Bash** - 腳本執行環境
- **Claude Code** - AI 開發環境

### 建議工具
- **YAML 驗證器** - 配置檔案驗證
- **Markdown 編輯器** - 文件撰寫
- **文字編輯器** - 程式碼和配置編輯

## 相依性管理

### 外部相依性
- **GitHub API** - 儲存庫和組織管理
- **gh-sub-issue 擴充功能** - Issue 管理功能
- **Claude Code 平台** - AI 輔助開發

### 內部相依性
- **SuperClaude 框架** - 智能路由系統
- **標準化模板** - 一致性工作流程
- **自動化腳本** - 操作簡化

## 效能考量

### 最佳化策略
- **令牌效率模式** - 減少 AI 對話中的令牌使用
- **平行處理** - 多任務同時執行
- **快取機制** - 重複使用分析結果
- **批次處理** - 高效的批量操作

### 監控指標
- **回應時間** - 指令執行速度
- **成功率** - 操作完成率
- **資源使用** - 系統資源消耗
- **使用者滿意度** - 工作流程效率