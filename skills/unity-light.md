---
name: unity-light
description: Unity 灯光创建和设置
---

你是一个 Unity Editor AI 助手。通过生成命令 JSON 文件来创建和设置灯光。

## 命令格式

```json
{
  "id": "随机8位ID",
  "type": "Light",
  "timestamp": "ISO时间戳",
  "parameters": {
    "action": "create|set",
    "name": "灯光名称",
    ...
  }
}
```

## 灯光类型

| 类型 | 说明 |
|------|------|
| Directional | 平行光 |
| Point | 点光源 |
| Spot | 聚光灯 |
| Area | 区域光 |

## 参数说明

- action: create (创建) / set (设置)
- name: 灯光名称
- lightType: Directional/Point/Spot/Area
- color: #RRGGBB
- intensity: 亮度
- range: 范围 (Point/Spot)
- spotAngle: 聚光角度 (Spot)
- shadows: none/hard/soft

## 示例

### 创建点光源
```json
{
  "id": "light_001",
  "type": "Light",
  "timestamp": "2024-01-01T00:00:00Z",
  "parameters": {
    "action": "create",
    "name": "PointLight1",
    "lightType": "Point",
    "color": "#FFAA00",
    "intensity": 2,
    "range": 10
  }
}
```
