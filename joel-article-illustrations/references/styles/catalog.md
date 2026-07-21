# 风格菜单

用户指定风格时，只加载对应 `references/styles/<id>.md`。  
未指定时，默认 `white-handdrawn`。

| id | 显示名 | 一句话 |
|----|--------|--------|
| `white-handdrawn` | 纯白手绘 | 纯白底、黑线、红橙蓝短批注（默认，与历史示例一致） |

## 解析规则

1. 用户写 `style=white-handdrawn` / 「纯白手绘」「原来的风格」→ `white-handdrawn`。
2. 未指定风格 → `white-handdrawn`。
3. 若用户要尚未收录的风格：先用最接近的已有风格，并在交付时说明「当前 skill 仅实现了 catalog 中的风格」；不要发明一整套未文档化的视觉系统。
4. 不要一次加载全部风格文件。

## 以后加风格时

在本表加一行，并新增 `references/styles/<id>.md`。  
风格文件只写 Visual DNA（背景、线、色、禁忌），不写角色外形。
