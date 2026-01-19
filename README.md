# Unity Skills

Unity Editor AI 助手技能库 - 通过 JSON 命令文件控制 Unity 编辑器

## 项目简介

Unity Skills 是一个为 AI 助手设计的 Unity 编辑器控制系统。通过生成标准化的 JSON 命令文件，AI 可以自动化执行各种 Unity 编辑器操作，包括场景管理、GameObject 创建、组件配置、材质设置等。

## 作者信息

**Cool 浩**

- B站主页: [https://space.bilibili.com/228962838](https://space.bilibili.com/228962838?spm_id_from=333.1007.0.0)
- 演示视频: [Unity Skills 演示](https://www.bilibili.com/video/BV1HAkwB7ED2/?spm_id_from=333.1387.upload.video_card.click)

## 工作原理

AI 助手通过以下流程与 Unity 编辑器交互：

1. **理解用户需求** - 解析用户的自然语言指令
2. **生成命令 JSON** - 根据需求生成标准化的命令文件
3. **写入待处理队列** - 将命令写入 `UnityCommands/pending/{id}.json`
4. **Unity 执行命令** - Unity 编辑器监听并执行命令
5. **返回结果** - 执行结果写入 `UnityCommands/results/{id}.json`

## 技能分类

本仓库包含以下 Unity 操作技能：

| 技能文件 | 说明 |
|---------|------|
| [unity.md](skills/unity.md) | 综合命令入口和导航 |
| [unity-gameobject.md](skills/unity-gameobject.md) | GameObject 创建、删除、查询 |
| [unity-component.md](skills/unity-component.md) | 组件添加和属性设置 |
| [unity-scene.md](skills/unity-scene.md) | 场景管理（新建/保存/加载） |
| [unity-prefab.md](skills/unity-prefab.md) | Prefab 预制体操作 |
| [unity-asset.md](skills/unity-asset.md) | 资源管理和导入 |
| [unity-material.md](skills/unity-material.md) | 材质和 Shader 设置 |
| [unity-light.md](skills/unity-light.md) | 灯光创建和配置 |
| [unity-animator.md](skills/unity-animator.md) | 动画控制器管理 |
| [unity-ui.md](skills/unity-ui.md) | UI 元素创建和设置 |
| [unity-editor.md](skills/unity-editor.md) | 编辑器控制（播放/暂停等） |
| [unity-debug.md](skills/unity-debug.md) | 调试工具 |
| [unity-project.md](skills/unity-project.md) | 项目管理 |
| [unity-validation.md](skills/unity-validation.md) | 验证工具 |

## 命令格式

所有命令遵循统一的 JSON 格式：

```json
{
  "id": "随机8位ID",
  "type": "命令类型",
  "timestamp": "ISO时间戳",
  "parameters": {
    // 命令特定参数
  }
}
```

## 使用示例

### 示例 1: 创建一个立方体

```json
{
  "id": "abc12345",
  "type": "CreateGameObject",
  "timestamp": "2026-01-19T10:30:00Z",
  "parameters": {
    "name": "MyCube",
    "primitiveType": "cube"
  }
}
```

### 示例 2: 添加刚体组件

```json
{
  "id": "def67890",
  "type": "AddComponent",
  "timestamp": "2026-01-19T10:30:01Z",
  "parameters": {
    "target": "MyCube",
    "componentType": "Rigidbody"
  }
}
```

### 示例 3: 创建并应用材质

```json
{
  "id": "ghi11111",
  "type": "CreateMaterial",
  "timestamp": "2026-01-19T10:30:02Z",
  "parameters": {
    "name": "RedMaterial",
    "folder": "Assets/Materials",
    "shader": "Standard",
    "color": "#FF0000"
  }
}
```

```json
{
  "id": "jkl22222",
  "type": "SetMaterial",
  "timestamp": "2026-01-19T10:30:03Z",
  "parameters": {
    "target": "MyCube",
    "material": "Assets/Materials/RedMaterial.mat"
  }
}
```

## 快速开始

### 对于 AI 助手开发者

1. 克隆本仓库
2. 将 `skills/` 目录配置到 AI 助手的技能路径
3. 配置 AI 读取 `CLAUDE.md` 获取使用说明
4. 实现命令文件的写入和结果读取逻辑

### 对于 Unity 开发者

1. 在 Unity 项目中实现命令监听器
2. 监听 `UnityCommands/pending/` 目录
3. 解析并执行 JSON 命令
4. 将结果写入 `UnityCommands/results/` 目录

## 支持的命令类型

- **GameObject 操作**: CreateGameObject, DeleteGameObject, SetTransform, SetParent, SetActive
- **组件管理**: AddComponent, SetComponentProperty
- **场景管理**: Scene (new/save/load/saveas)
- **资源管理**: CreateMaterial, SetMaterial, CreatePrefab
- **灯光系统**: Light (create/set)
- **动画系统**: Animator (createcontroller/addparameter/setparameter/play)
- **UI 系统**: UI (create/set)
- **查询操作**: GetSceneInfo, GetGameObjectInfo

## 许可证

本项目采用 [Apache License 2.0](LICENSE) 许可证。

## 贡献

欢迎提交 Issue 和 Pull Request 来改进技能定义和文档。

## 相关项目

- Unity Editor - https://unity.com/
- Claude AI - https://claude.ai/

---

**注意**: 本项目需要配合支持文件系统操作的 AI 助手和相应的 Unity 编辑器插件使用。
