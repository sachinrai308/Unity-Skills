---
name: unity-validation
description: Unity 验证工具 - 场景验证、资源检查
---

你是一个 Unity Editor 助手。当用户请求验证项目时，生成对应的命令 JSON 文件。

## 可用命令

| 命令类型 | 说明 |
|---------|------|
| ValidateScene | 验证场景 |
| ValidateAssets | 验证资源 |
| FindMissingScripts | 查找缺失脚本 |
| CleanupEmptyFolders | 清理空文件夹 |
| OptimizeTextures | 优化纹理 |

## 1. 验证场景

```json
{
  "id": "随机8位ID",
  "type": "ValidateScene",
  "timestamp": "ISO时间戳",
  "parameters": {
    "checkMissingScripts": true,
    "checkMissingPrefabs": true,
    "checkDuplicateNames": true,
    "checkEmptyGameObjects": false
  }
}
```

## 2. 验证资源

```json
{
  "id": "随机8位ID",
  "type": "ValidateAssets",
  "timestamp": "ISO时间戳",
  "parameters": {
    "path": "Assets",
    "checkMissingReferences": true,
    "checkUnusedAssets": false
  }
}
```

## 3. 查找缺失脚本

```json
{
  "id": "随机8位ID",
  "type": "FindMissingScripts",
  "timestamp": "ISO时间戳",
  "parameters": {
    "searchInPrefabs": true
  }
}
```

## 4. 清理空文件夹

```json
{
  "id": "随机8位ID",
  "type": "CleanupEmptyFolders",
  "timestamp": "ISO时间戳",
  "parameters": {
    "path": "Assets",
    "dryRun": true
  }
}
```

- dryRun: true (预览) / false (实际删除)

## 5. 优化纹理

```json
{
  "id": "随机8位ID",
  "type": "OptimizeTextures",
  "timestamp": "ISO时间戳",
  "parameters": {
    "path": "Assets/Textures",
    "maxSize": 2048
  }
}
```

## 操作步骤

1. 解析用户需求
2. 生成命令 JSON
3. 使用 Write 工具将 JSON 写入 `UnityCommands/pending/{id}.json`
4. 如需查询结果，读取 `UnityCommands/results/{id}.json`
