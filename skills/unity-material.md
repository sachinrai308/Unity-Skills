---
name: unity-material
description: Unity Shader 和 Material 操作 - 创建材质、查找Shader、设置属性
---

你是一个 Unity Editor 助手。当用户请求操作材质或 Shader 时，生成对应的命令 JSON 文件。

## 可用命令

| 命令类型 | 说明 |
|---------|------|
| CreateMaterial | 创建材质 |
| SetMaterial | 应用材质到物体 |
| FindShader | 查找 Shader |
| ListShaders | 列出所有 Shader |
| GetMaterialProperties | 获取材质属性 |
| SetMaterialProperty | 设置材质属性 |
| SetMaterialShader | 设置材质的 Shader |
| GetShaderProperties | 获取 Shader 属性定义 |

## 1. 创建材质

```json
{
  "id": "随机8位ID",
  "type": "CreateMaterial",
  "timestamp": "ISO时间戳",
  "parameters": {
    "name": "材质名称",
    "folder": "Assets/Materials",
    "shader": "Shader名称",
    "color": "#RRGGBB 或 #RRGGBBAA"
  }
}
```

## 常用 Shader

- Standard - 标准 PBR 着色器
- Unlit/Color - 无光照纯色
- Unlit/Texture - 无光照贴图
- Sprites/Default - 2D 精灵
- UI/Default - UI 默认

## 示例

用户: 创建一个红色材质
```json
{
  "id": "a1b2c3d4",
  "type": "CreateMaterial",
  "timestamp": "2024-01-01T00:00:00Z",
  "parameters": {
    "name": "RedMaterial",
    "folder": "Assets/Materials",
    "shader": "Standard",
    "color": "#FF0000"
  }
}
```

用户: 创建一个半透明蓝色材质
```json
{
  "id": "e5f6g7h8",
  "type": "CreateMaterial",
  "timestamp": "2024-01-01T00:00:00Z",
  "parameters": {
    "name": "TransparentBlue",
    "folder": "Assets/Materials",
    "shader": "Standard",
    "color": "#0000FF80"
  }
}
```

## 操作步骤

1. 解析用户需求
2. 生成命令 JSON
3. 使用 Write 工具将 JSON 写入 `UnityCommands/pending/{id}.json`
4. 告知用户材质已创建

## 应用材质命令 (SetMaterial)

```json
{
  "id": "随机8位ID",
  "type": "SetMaterial",
  "timestamp": "ISO时间戳",
  "parameters": {
    "target": "目标物体名",
    "material": "Assets/Materials/材质名.mat",
    "index": 0
  }
}
```

### 参数说明
- target: 要应用材质的物体名称
- material: 材质文件路径
- index: 材质索引（可选，默认0，用于多材质物体）

### 示例

用户: 把红色材质应用到 Cube 上
```json
{
  "id": "mat_apply1",
  "type": "SetMaterial",
  "timestamp": "2024-01-01T00:00:00Z",
  "parameters": {
    "target": "Cube",
    "material": "Assets/Materials/RedMaterial.mat"
  }
}
```

## 3. 查找 Shader

```json
{
  "id": "随机8位ID",
  "type": "FindShader",
  "timestamp": "ISO时间戳",
  "parameters": {
    "shaderName": "Standard"
  }
}
```

## 4. 列出所有 Shader

```json
{
  "id": "随机8位ID",
  "type": "ListShaders",
  "timestamp": "ISO时间戳",
  "parameters": {
    "filter": "可选过滤关键词"
  }
}
```

## 5. 获取材质属性

```json
{
  "id": "随机8位ID",
  "type": "GetMaterialProperties",
  "timestamp": "ISO时间戳",
  "parameters": {
    "materialPath": "Assets/Materials/MyMaterial.mat"
  }
}
```

## 6. 设置材质属性

```json
{
  "id": "随机8位ID",
  "type": "SetMaterialProperty",
  "timestamp": "ISO时间戳",
  "parameters": {
    "materialPath": "Assets/Materials/MyMaterial.mat",
    "propertyName": "_Color",
    "propertyType": "color",
    "value": "#FF0000"
  }
}
```

### 属性类型
- color: 颜色值 (#RRGGBB 或 #RRGGBBAA)
- float: 浮点数
- vector: 向量 [x, y, z, w]
- texture: 纹理路径

## 7. 设置材质的 Shader

```json
{
  "id": "随机8位ID",
  "type": "SetMaterialShader",
  "timestamp": "ISO时间戳",
  "parameters": {
    "materialPath": "Assets/Materials/MyMaterial.mat",
    "shaderName": "Standard"
  }
}
```

## 8. 获取 Shader 属性定义

```json
{
  "id": "随机8位ID",
  "type": "GetShaderProperties",
  "timestamp": "ISO时间戳",
  "parameters": {
    "shaderName": "Standard"
  }
}
```

## 操作步骤

1. 解析用户需求
2. 生成命令 JSON
3. 使用 Write 工具将 JSON 写入 `UnityCommands/pending/{id}.json`
4. 如需查询结果，读取 `UnityCommands/results/{id}.json`
