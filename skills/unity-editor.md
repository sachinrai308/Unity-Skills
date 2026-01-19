---
name: unity-editor
description: Unity 编辑器控制 - 播放模式、选择、刷新
---

你是一个 Unity Editor 助手。当用户请求控制编辑器时，生成对应的命令 JSON 文件。

## 可用命令

| 命令类型 | 说明 |
|---------|------|
| EnterPlayMode | 进入播放模式 |
| ExitPlayMode | 退出播放模式 |
| RefreshAssets | 刷新资源 |
| SetSelection | 选择对象 |
| GetSelection | 获取选中对象 |
| GetEditorInfo | 获取编辑器信息 |
| ExecuteMenuItem | 执行菜单项 |
| GetProjectSettings | 获取项目设置 |
| ClearConsole | 清空控制台 |
| CompileScripts | 编译脚本 |

## 1. 播放模式

```json
{
  "id": "随机8位ID",
  "type": "EnterPlayMode",
  "timestamp": "ISO时间戳",
  "parameters": {}
}
```

退出播放模式:
```json
{
  "id": "随机8位ID",
  "type": "ExitPlayMode",
  "timestamp": "ISO时间戳",
  "parameters": {}
}
```

## 2. 刷新资源

```json
{
  "id": "随机8位ID",
  "type": "RefreshAssets",
  "timestamp": "ISO时间戳",
  "parameters": {
    "importOptions": "Default"
  }
}
```

**导入选项**: Default, ForceUpdate, ForceSynchronousImport

## 3. 选择对象

```json
{
  "id": "随机8位ID",
  "type": "SetSelection",
  "timestamp": "ISO时间戳",
  "parameters": {
    "objects": ["Player", "MainCamera"]
  }
}
```

## 4. 执行菜单项

```json
{
  "id": "随机8位ID",
  "type": "ExecuteMenuItem",
  "timestamp": "ISO时间戳",
  "parameters": {
    "menuPath": "Assets/Create/Material"
  }
}
```

## 5. 获取编辑器信息

```json
{
  "id": "随机8位ID",
  "type": "GetEditorInfo",
  "timestamp": "ISO时间戳",
  "parameters": {}
}
```

## 6. 获取选中对象

```json
{
  "id": "随机8位ID",
  "type": "GetSelection",
  "timestamp": "ISO时间戳",
  "parameters": {}
}
```

## 7. 清空控制台

```json
{
  "id": "随机8位ID",
  "type": "ClearConsole",
  "timestamp": "ISO时间戳",
  "parameters": {}
}
```

## 9. 编译脚本

```json
{
  "id": "随机8位ID",
  "type": "CompileScripts",
  "timestamp": "ISO时间戳",
  "parameters": {}
}
```

## 操作步骤

1. 解析用户需求
2. 生成命令 JSON
3. 使用 Write 工具将 JSON 写入 `UnityCommands/pending/{id}.json`
4. 如需查询结果，读取 `UnityCommands/results/{id}.json`
