---
created: 2025-09-02T18:49:02Z
last_updated: 2025-09-02T18:49:02Z
version: 1.0
author: Claude Code PM System
---

# 專案風格指南

## 編碼標準總則

### 核心原則
1. **一致性優先** - 整個專案保持一致的風格和慣例
2. **可讀性重於簡潔** - 程式碼應該易於理解和維護
3. **明確優於隱含** - 明確表達意圖，避免隱含的複雜邏輯
4. **防禦性程式設計** - 總是考慮邊界條件和錯誤處理
5. **文件即程式碼** - 文件與程式碼同等重要，同步更新

### 品質標準
- **零容忍策略** - 對程式碼品質和安全性零容忍
- **自動化優先** - 能自動檢查的規則都應該自動化
- **漸進式改進** - 持續改進現有程式碼品質
- **測試驅動** - 所有功能都必須有對應的測試

## 檔案命名慣例

### Markdown 文件
```yaml
格式: kebab-case.md
範例:
  ✅ project-overview.md
  ✅ tech-context.md
  ✅ system-patterns.md
  ❌ ProjectOverview.md
  ❌ tech_context.md
```

### YAML 配置檔
```yaml
格式: kebab-case.yml 或 snake_case.yaml
範例:
  ✅ labels.yml
  ✅ sync-labels-to-all-repos-fixed.yml
  ✅ settings.local.json
  ❌ labelsConfig.yml
  ❌ SyncLabels.yaml
```

### Shell 腳本
```bash
格式: kebab-case.sh
範例:
  ✅ test-and-log.sh
  ✅ init.sh
  ❌ testAndLog.sh
  ❌ Test_Script.sh
```

### 代理程式和指令檔案
```yaml
代理程式: kebab-case.md
  ✅ code-analyzer.md
  ✅ file-analyzer.md
  
指令檔案: action-target.md 或 category:action.md
  ✅ code-rabbit.md
  ✅ pm:init.md  
  ✅ context:create.md
```

## 目錄結構慣例

### 階層式組織
```
專案根目錄/
├── .claude/                    # Claude Code 配置 (隱藏目錄)
│   ├── agents/                # 代理程式 (複數)
│   ├── commands/              # 指令系統 (複數)
│   ├── context/               # 上下文文件 (單數)
│   ├── scripts/               # 腳本集合 (複數)
│   └── rules/                 # 規則集合 (複數)
├── .github/                   # GitHub 配置 (隱藏目錄)
│   ├── ISSUE_TEMPLATE/        # GitHub 慣例 (大寫)
│   └── workflows/             # GitHub Actions (複數)
└── profile/                   # 組織簡介 (單數)
```

### 命名邏輯
- **功能性目錄** - 使用複數形式 (`agents/`, `commands/`, `scripts/`)
- **內容性目錄** - 使用單數形式 (`context/`, `profile/`)  
- **隱藏配置** - 使用點前綴 (`.claude/`, `.github/`)
- **GitHub 慣例** - 遵循 GitHub 官方慣例 (`ISSUE_TEMPLATE/`)

## 前置資料 (Frontmatter) 標準

### YAML 前置資料格式
```yaml
---
created: 2025-09-02T18:49:02Z           # ISO 8601 格式
last_updated: 2025-09-02T18:49:02Z     # ISO 8601 格式  
version: 1.0                           # 語意化版本
author: Claude Code PM System          # 作者資訊
---
```

### 代理程式特殊前置資料
```yaml
---
name: agent-name                       # 代理程式名稱
description: "詳細功能描述..."          # 功能描述
tools: Glob, Grep, LS, Read            # 可用工具列表
model: inherit                         # 模型設定
color: red                            # 顯示顏色
---
```

### 指令檔案特殊前置資料  
```yaml
---
allowed-tools: Task, Read, Edit        # 允許使用的工具
---
```

## 程式碼註解慣例

### Markdown 文件註解
```markdown
<!-- 這是 Markdown 註解，用於內部說明 -->

## 主要章節
內容說明...

### 子章節  
詳細內容...

> **重要提示**: 使用引用格式標示重要資訊

**粗體** 用於強調關鍵概念
*斜體* 用於強調術語或變數
`程式碼` 用於標示程式碼片段或檔案名
```

### YAML 檔案註解
```yaml
# 這是主要配置區塊
permissions:
  # 明確允許的操作 - 使用最小權限原則
  allow:
    - "Bash(pnpm lint:*)"     # 程式碼品質檢查
    - "Bash(pnpm build:*)"    # 建置操作
  
  # 明確禁止的操作
  deny: []
  
  # 需要詢問使用者的操作  
  ask: []
```

### Shell 腳本註解
```bash
#!/bin/bash
# 腳本名稱: 測試執行和日誌記錄
# 作者: Claude Code PM System
# 用途: 執行測試並記錄完整輸出以供後續分析

# 檢查必要參數
if [ $# -eq 0 ]; then
    echo "使用方式: $0 <test_file> [log_name]"
    exit 1
fi

# 設定變數
TEST_FILE="$1"                    # 測試檔案路徑
LOG_NAME="${2:-default}"          # 日誌名稱 (可選)
```

## 內容撰寫風格

### 中文文件風格  
```markdown
# 標題使用繁體中文，明確簡潔

## 結構化組織
- 使用層次化的標題結構
- 重要資訊使用 **粗體** 強調
- 程式碼和檔案名使用 `反引號`

## 術語一致性
- 專案管理 (非 Project Management)
- 代理程式 (非 Agent)
- 儲存庫 (非 Repository)
- 工作流程 (非 Workflow)

## 語調要求
- 正式但不拘謹
- 清晰且具體
- 避免過度技術性語言
- 包含適當的範例說明
```

### 英文內容風格
```markdown
# Use clear, professional English for technical content

## Technical Terms
- Use consistent terminology throughout
- Avoid unnecessary jargon
- Provide examples where helpful
- Use active voice when possible

## Structure
- Clear hierarchical organization
- Bullet points for lists
- Code blocks for technical examples
- Callouts for important information
```

## 配置檔案格式

### JSON 配置風格
```json
{
  "permissions": {
    "allow": [
      "Bash(pnpm lint:*)",
      "Bash(pnpm build:*)",
      "Bash(pnpm generate:docs:*)"
    ],
    "deny": [],
    "ask": []
  }
}
```

**JSON 規則**:
- 使用 2 空格縮排
- 屬性名稱使用雙引號
- 最後一個屬性後不加逗號
- 陣列和物件保持一致的格式

### YAML 配置風格
```yaml
# 主要配置
name: "GitHub 組織標準標籤"
version: "1.0"

# 標籤定義
labels:
  # 錯誤相關標籤
  - name: "bug"
    color: "d73a4a"
    description: "程式碼中的錯誤或缺陷"
  
  # 功能相關標籤  
  - name: "enhancement"
    color: "a2eeef"
    description: "新功能或功能改進"
```

**YAML 規則**:
- 使用 2 空格縮排 (絕不使用 Tab)
- 陣列項目使用 `- ` 格式
- 字串值使用雙引號 (除非是純數字或布林值)
- 註解使用 `# ` 格式 (空格分隔)

## 錯誤處理和驗證

### 錯誤訊息格式
```yaml
成功訊息: ✅ 操作完成 - 簡短說明
警告訊息: ⚠️ 注意事項 - 具體說明和建議  
錯誤訊息: ❌ 操作失敗 - 具體錯誤原因和解決方法
資訊訊息: ℹ️ 提示資訊 - 有用的補充資訊
```

### 驗證規則
- **檔案存在性** - 在操作前檢查檔案是否存在
- **權限檢查** - 確認有足夠權限執行操作
- **格式驗證** - YAML/JSON 語法正確性檢查
- **內容完整性** - 必要欄位和資訊完整性驗證

## 版本控制慣例

### 提交訊息格式
```
🚀 feat: 新功能簡短描述

詳細說明新功能的內容和影響範圍。

- 新增了 xxx 功能
- 改進了 yyy 效能
- 修正了 zzz 問題

🤖 Generated with [Claude Code](https://claude.ai/code)

Co-Authored-By: Claude <noreply@anthropic.com>
```

### 表情符號使用標準
- ✨ `feat` - 新功能
- 🐛 `fix` - 錯誤修正
- 📝 `docs` - 文件更新
- 🎨 `style` - 程式碼格式
- ♻️ `refactor` - 重構  
- ✅ `test` - 測試相關
- 🔧 `chore` - 工具和設定

### 分支命名慣例
```bash
main                    # 主分支
feature/new-agent      # 功能分支
fix/bug-description    # 修正分支  
docs/update-guide      # 文件分支
```

## 測試和品質保證

### 測試檔案命名
```bash
# 測試檔案
test-component.spec.js
integration-test.js
e2e-workflow.test.js

# 測試資料
mock-data.json
sample-config.yml
test-fixtures/
```

### 品質檢查清單
- [ ] 語法正確性 (YAML/JSON/Markdown)
- [ ] 檔案命名符合慣例
- [ ] 前置資料完整且格式正確
- [ ] 註解清晰且有意義
- [ ] 錯誤處理適當
- [ ] 文件與程式碼同步
- [ ] 測試覆蓋率足夠
- [ ] 安全性考量完整

這份風格指南確保了整個專案的一致性和可維護性，讓團隊成員能夠快速理解和參與專案開發。