# LVGL 样式提取输出模板

仅在用户要求结构化评审或需要核对提取结果时使用。

## 控件与样式清单

| ID | 推断控件 | 缩放后边界 | 关键样式 | 证据等级 | 资源/说明 |
| --- | --- | --- | --- | --- | --- |
| header_title | `lv_label` | x, y, w, h | 文字色、字号、对齐 | 图片可直接确认 | 字体待确认 |

## C 宏定义

```c
#define UI_COLOR_BG           0x002B52
#define UI_CARD_BORDER_WIDTH  1
#define UI_CARD_RADIUS        0
```

颜色宏保存 `0xRRGGBB`，在 LVGL 代码中以 `lv_color_hex(UI_COLOR_BG)` 使用。

## 待确认项

| 项目 | 原因 | 建议 |
| --- | --- | --- |
| 图标资源 | 截图无法提供原始矢量或位图 | 提供 SVG、PNG 或 LVGL 图片资源 |
