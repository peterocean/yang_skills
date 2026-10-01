# 仪器界面设计简报

在新项目、约束发生变化或需要交接给实现人员时使用本模板。只展示对当前对话有用的字段；内部记录可以保留完整结构。

## 首轮确认卡

```text
设备与用途：
主要读数 / 单位：
关键操作与告警：

1. 屏幕分辨率：____ × ____；横屏 / 竖屏；旋转：____
2. 屏幕类型：TFT / OLED / 单色 LCD / 电子纸 / 其他；触摸：____
3. 像素格式：RGB565 / RGB888 / ARGB8888 / 单色 / 未定
4. 显示风格：____；明暗主题：____；品牌色或参考图：____
5. GUI 中间件：____；版本：____；语言/平台：____
6. 整体布局：主数据区 ____；趋势区 ____；状态区 ____；操作区 ____；导航 ____
7. 图片输出目录：____；允许覆盖同名文件：是 / 否（默认否）

输入方式：触摸 / 物理键 / 旋钮 / 混合
资源限制：RAM ____；Flash ____；帧缓冲 ____；目标刷新率 ____
```

允许用户回答“未知”。对未知项给出基于设备类型的候选方案，并分别说明画质、显存、刷新和实现代价。

## 状态表

| 因素 | 当前值 | 状态 | 影响 / 备注 |
| --- | --- | --- | --- |
| 分辨率 | 800 × 480 横屏 | 已确认 | 决定画布和布局密度 |
| 屏幕类型 | 4.3 英寸 TFT，电容触摸 | 暂定 | 需核对面板型号 |
| 像素格式 | RGB565 | 已确认 | 避免大面积细腻渐变 |
| 显示风格 | 深色工业科技 | 待确认 | 等待风格预览选择 |
| GUI 中间件 | LVGL 9.x | 已确认 | 使用 v9 API |
| 整体布局 | 顶部状态 + 主读数 + 底部导航 | 暂定 | 等待线框确认 |
| 图片输出目录 | `output/instrument-ui/demo` | 已确认 | 自动创建并保存全部预览图 |

状态含义：

- **已确认**：用户明确给出或批准。
- **暂定**：为推进预览而采用的推荐值，必须在最终实现前确认。
- **待确认**：缺少信息，且当前不应推断。

## 可移交 YAML

需要保存为文件、供后续预览或代码生成复用时，使用以下结构；不需要持久化时无需机械输出 YAML。

```yaml
project:
  name: ""
  device_purpose: ""
  operator_context: ""
output:
  image_directory: { value: "output/instrument-ui/demo", status: confirmed }
  overwrite_existing: false
  naming: "stage_variant_version"
display:
  resolution: { width: 800, height: 480, status: confirmed }
  orientation: { value: landscape, status: confirmed }
  technology: { value: tft_lcd, status: provisional }
  shape: rectangular
  touch: capacitive
  pixel_format: { value: rgb565, status: confirmed }
  refresh_constraints: ""
software:
  gui_middleware: { name: lvgl, version: "9.x", status: confirmed }
  platform: ""
visual:
  style: { value: "dark industrial", status: open }
  palette: []
  density: medium
layout:
  selected_variant: ""
  regions: []
  navigation: ""
content:
  primary_readings: []
  alarms: []
interaction:
  inputs: []
locks: []
open_questions: []
```

## 迭代反馈卡

每轮预览优先询问可直接执行的反馈：

```text
选择：方案 A / B / C
保留：
修改：区域 + 具体变化
删除：
新增：
是否锁定布局：是 / 否
是否进入高保真或实现：是 / 否
```
