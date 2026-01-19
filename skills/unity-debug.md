---
name: unity-debug
description: Unity 调试工具 - 日志、暂停、偏好设置
---

你是一个 Unity Editor 助手。当用户请求调试功能时，生成对应的命令 JSON 文件。

## 可用命令

| 命令类型 | 说明 |
|---------|------|
| DebugLog | 写入日志 |
| GetLogs | 获取日志 |
| PauseEditor | 暂停编辑器 |
| ResumeEditor | 恢复编辑器 |
| GetEditorPrefs | 获取编辑器偏好 |
| SetEditorPrefs | 设置编辑器偏好 |
| ClearConsole | 清空控制台 |

## 1. 写入日志

```json
{
  "id": "随机8位ID",
  "type": "DebugLog",
  "timestamp": "ISO时间戳",
  "parameters": {
    "message": "测试消息",
    "logType": "Log"
  }
}
```

**日志类型**: Log, Warning, Error

## 2. 获取日志

```json
{
  "id": "随机8位ID",
  "type": "GetLogs",
  "timestamp": "ISO时间戳",
  "parameters": {
    "count": 50,
    "types": ["Error", "Warning"]
  }
}
```

## 3. 暂停编辑器

```json
{
  "id": "随机8位ID",
  "type": "PauseEditor",
  "timestamp": "ISO时间戳",
  "parameters": {}
}
```

恢复编辑器:
```json
{
  "id": "随机8位ID",
  "type": "ResumeEditor",
  "timestamp": "ISO时间戳",
  "parameters": {}
}
```

## 4. 编辑器偏好设置

获取偏好:
```json
{
  "id": "随机8位ID",
  "type": "GetEditorPrefs",
  "timestamp": "ISO时间戳",
  "parameters": {
    "key": "MyCustomSetting",
    "defaultValue": "default"
  }
}
```

设置偏好:
```json
{
  "id": "随机8位ID",
  "type": "SetEditorPrefs",
  "timestamp": "ISO时间戳",
  "parameters": {
    "key": "MyCustomSetting",
    "value": "newValue"
  }
}
```

## 5. 清空控制台

```json
{
  "id": "随机8位ID",
  "type": "ClearConsole",
  "timestamp": "ISO时间戳",
  "parameters": {}
}
```

## 操作步骤

1. 解析用户需求
2. 生成命令 JSON
3. 使用 Write 工具将 JSON 写入 `UnityCommands/pending/{id}.json`
4. 如需查询结果，读取 `UnityCommands/results/{id}.json`
