# dsh-routing-suite-learn-record

> 学习记录 · 创建于 2026-08-16
> 源笔记：[[scienc-project-repo/Tools/dsh/plugins/routing-suite/dsh-routing-suite-使用说明]]

---

## 学习目标

- 理解 dsh-routing-suite 的两部分构成（注入器 + 路由预置）及其"非界面增强类"定位
- 掌握 dev_* 工具全家桶的插入/卸载/热重载/路由自愈主链路
- 理解 router-standard 三带（spec/mixed/react）与两种路由模式

## 学习过程

### 第一次学习（2026-08-16）

**学习内容：**
- 通读 injector 源码目录结构、README、INSTALL、CHANGELOG、SPEC.md
- 通读 preset/README.md 的三带测量结论与 standard/spec 路由模式
- 实操 dev_plugin_status 解析实时 registry（window.__DSH_BOOT__.entries，54 条）

**关键理解：**
- 注入器 = DSH 生态"BepInEx 式模组注入入口"：官方入口装一次，之后万物可运行时注入（免重启）
- "一切皆插件"：host 工具 + client UI 注入即完整生效，靠 normalizeEntry / 补扫 / 卸载清理
- 路由三带是**实测塌缩区域**而非连续可调：mixed 是 transition trap，不自动选

**实践验证：**
- `dev_plugin_status` 显示 `@dsh-external/dsh-super-injector` 已装配（web bundles 第 6 位）
- 自研 dev_plugin_status.py 复刻 registry 解析成功（rev 2482a5646ef1 / 54 entries）

**疑问：**
- injector 与 preset 是同一仓库两个独立子 git（.gitmodules），preset 需另行装配还是随 injector 走？
- 生产态应走官方装配（重启由 bundles 接管），还是运行时注入仍可持续？

---

## 知识分解

| 知识点 | 理解程度 | 备注 |
|--------|----------|------|
| 注入器心智模型（BepInEx 类比） | 🟢 掌握 | |
| dev_* 工具全家桶（注入/卸载/热重载/自愈） | 🟡 粗浅 | 命名已掌握，个别工具待实操 |
| staging 后侧挂区与转正 | 🟡 粗浅 | dev_stage_* 系列 |
| 路由三带与非连续相位 | 🟢 掌握 | V4 Pro 三带 / V4 Flash 阈值式 |
| 官方装配 vs 运行时注入的取舍 | 🟡 粗浅 | 生产/开发态边界待明确 |

## 查漏补缺

- preset 子项目的装配路径与 routerMode 实际生效位置（agent.cordis.yml 在哪个 profile）
- 待实操：dev_inject_plugin 注入一个真实插件、dev_reload_package 观察 uid 变化

## 总结标记

- [x] 核心概念已理解
- [x] 已实践验证（dev_plugin_status 解析 registry）
- [ ] 已总结归纳（本文档即总结）
- [ ] 可独立复述

---

*最后更新：2026-08-16*
