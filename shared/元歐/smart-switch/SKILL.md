---
name: smart-switch
description: 智慧切換技能。當使用者上傳圖片、照片、截圖或任何圖形檔案時自動載入，將看圖任務交給 vision sub-agent（qwen3.7-plus）。純文字對話維持預設模型（deepseek-v4-flash）。
---

# 智慧切換 Smart Switch

## 觸發條件

使用者提供以下內容時，啟動此技能：
- 上傳圖片檔（.jpg/.png/.gif/.webp/.bmp）
- 貼上截圖
- 提供照片需要分析
- 問「這張圖是什麼」「幫我看這張圖」等

## 行為

1. 用 `read` 工具讀取圖片檔案
2. 透過 `task` 委派給 vision sub-agent（model: opencode-go/qwen3.7-plus）
3. vision agent 回傳結果後，直接轉達給使用者
4. 純文字對話不需任何切換，維持預設模型

## 注意

- 我（元歐）的預設模型是 deepseek-v4-flash，**不能動態切換**
- vision sub-agent 已在 opencode.json 設定，名稱叫 `vision`
- 使用方式：
  ```
  task("vision", "請分析這張圖片：<file_path>", subagent_type="general")
  ```
- 不需要問使用者「要不要切模型」，直接自動處理
