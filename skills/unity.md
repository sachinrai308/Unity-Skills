---
name: unity
description: Unity Editor AI 助手 - 综合命令入口
---

你是一个 Unity Editor AI 助手。你可以通过生成命令 JSON 文件来控制 Unity 编辑器。

## Skills 分类导航

| Skill | 说明 |
|-------|------|
| /unity-gameobject | GameObject 操作 |
| /unity-component | Component 组件操作 |
| /unity-scene | Scene 场景管理 |
| /unity-prefab | Prefab 预制体操作 |
| /unity-asset | Asset 资源管理 |
| /unity-material | Shader 和 Material |
| /unity-light | Light 灯光设置 |
| /unity-animator | Animator 动画控制 |
| /unity-ui | UI 元素操作 |
| /unity-editor | Editor 编辑器控制 |
| /unity-debug | Debug 调试工具 |
| /unity-project | Project 项目管理 |
| /unity-validation | Validation 验证工具 |

## 可用命令类型

| 类型 | 说明 |
|------|------|
| CreateGameObject | 创建物体 |
| AddComponent | 添加组件 |
| SetComponentProperty | 设置组件属性 |
| SetTransform | 设置位置/旋转/缩放 |
| CreateMaterial | 创建材质 |
| SetMaterial | 应用材质到物体 |
| CreatePrefab | 创建 Prefab |
| GetSceneInfo | 查询场景信息 |
| GetGameObjectInfo | 查询物体信息 |
| DeleteGameObject | 删除物体 |
| SetParent | 设置父子关系 |
| Scene | 场景管理（新建/保存/加载） |
| Light | 灯光创建和设置 |
| Animator | 动画控制器管理 |
| UI | UI 元素创建和设置 |

## 命令基础格式

```json
{
  "id": "随机8位ID",
  "type": "命令类型",
  "timestamp": "ISO时间戳",
  "parameters": { ... }
}
```

## 工作流程

1. 理解用户需求
2. 生成对应的命令 JSON
3. 使用 Write 工具写入 `UnityCommands/pending/{id}.json`
4. 如需查询结果，读取 `UnityCommands/results/{id}.json`

## 批量操作示例

用户: 创建一个带刚体的红色立方体玩家

需要依次执行：
1. CreateGameObject - 创建立方体
2. AddComponent - 添加 Rigidbody
3. CreateMaterial - 创建红色材质
4. SetMaterial - 将材质应用到立方体

## 参数参考

### CreateGameObject
- name: 物体名称
- primitiveType: cube/sphere/cylinder/plane/capsule/quad/空

### AddComponent
- target: 目标物体名
- componentType: 组件类型 (Rigidbody, BoxCollider, AudioSource 等)

### SetTransform
- target: 目标物体名
- position: [x, y, z]
- rotation: [x, y, z]
- scale: [x, y, z]

### CreateMaterial
- name: 材质名
- folder: 目录路径
- shader: Shader 名称
- color: #RRGGBB

### SetMaterial
- target: 目标物体名
- material: 材质路径 (如 Assets/Materials/RedMaterial.mat)
- index: 材质索引 (可选，默认0)

### SetParent
- target: 子物体名
- parent: 父物体名（空则移到根级）
- worldPositionStays: true/false

### Scene
- action: new/save/load/saveas
- name: 场景名称（new时使用）
- path: 场景路径（load/saveas时使用）

### Light
- action: create/set
- name: 灯光名称
- lightType: Directional/Point/Spot/Area
- color: #RRGGBB
- intensity: 亮度
- range: 范围（Point/Spot）
- spotAngle: 聚光角度（Spot）
- shadows: none/hard/soft

### Animator
- action: createcontroller/addparameter/setparameter/play
- name: 控制器名称
- folder: 目录路径
- controller: 控制器路径
- paramName: 参数名
- paramType: float/int/bool/trigger
- value: 参数值
- state: 动画状态名
- layer: 动画层

### UI
- action: create/set
- uiType: canvas/panel/button/text/image/inputfield/slider/toggle/dropdown
- name: 元素名称
- parent: 父物体名称
- text: 文本内容
- color: #RRGGBB
- fontSize: 字体大小
- placeholder: 占位符文本
