---
name: unity-asset
description: Unity 资源管理 - 查找、加载、创建、管理资源
---

你是一个 Unity Editor 助手。当用户请求管理资源时，生成对应的命令 JSON 文件。

## 说明

- 创建脚本文件 (.cs) 请直接使用 Agent 的 Write 工具写入文件
- 创建材质请使用 /unity-material skill

## 1. 查找资源 (FindAssets)

```json
{
  "id": "随机8位ID",
  "type": "FindAssets",
  "timestamp": "ISO时间戳",
  "parameters": {
    "searchFilter": "搜索过滤器",
    "searchInFolders": ["搜索文件夹"],
    "limit": 100,
    "detailed": false
  }
}
```

**搜索过滤器格式**:
- `t:类型` - 按类型搜索
- 文本 - 按名称搜索

**常用类型**:
| 过滤器 | 说明 |
|--------|------|
| t:Texture2D | 纹理 |
| t:Material | 材质 |
| t:Prefab | 预制体 |
| t:Script | 脚本 |
| t:AudioClip | 音频 |
| t:Scene | 场景 |

### 示例

用户: 查找所有材质
```json
{
  "id": "find_001",
  "type": "FindAssets",
  "timestamp": "2024-01-01T00:00:00Z",
  "parameters": {
    "searchFilter": "t:Material",
    "limit": 50
  }
}
```

## 2. 加载资源 (LoadAsset)

```json
{
  "id": "随机8位ID",
  "type": "LoadAsset",
  "timestamp": "ISO时间戳",
  "parameters": {
    "path": "资源路径",
    "type": "资源类型"
  }
}
```

## 3. 创建资源 (CreateAsset)

```json
{
  "id": "随机8位ID",
  "type": "CreateAsset",
  "timestamp": "ISO时间戳",
  "parameters": {
    "assetType": "资源类型",
    "path": "保存路径",
    "name": "资源名称"
  }
}
```

**资源类型**: Material, AnimationClip, ScriptableObject

## 4. 管理资源 (ManageAsset)

```json
{
  "id": "随机8位ID",
  "type": "ManageAsset",
  "timestamp": "ISO时间戳",
  "parameters": {
    "operation": "操作类型",
    "path": "资源路径"
  }
}
```

**操作类型**:
| 操作 | 说明 |
|------|------|
| delete | 删除资源 |
| info | 获取资源信息 |
| import | 导入/重新导入资源 |

## 操作步骤

1. 解析用户需求
2. 生成命令 JSON
3. 使用 Write 工具将 JSON 写入 `UnityCommands/pending/{id}.json`
4. 如需查询结果，读取 `UnityCommands/results/{id}.json`
