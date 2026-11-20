# 🤖 Foray · RoboMaster

<p align="center">
  <b>肇庆学院 Foray 战队</b> · 全国大学生机器人大赛 RoboMaster 机甲大师赛
</p>

<p align="center">
  <a href="https://www.robomaster.com"><img src="https://img.shields.io/badge/RoboMaster-2027-blue?style=flat-square" alt="RoboMaster 2027 赛季"></a>
  <img src="https://img.shields.io/badge/ZQU-Foray-2ea44f?style=flat-square" alt="ZQU Foray 战队">
</p>

<!-- 队徽：待定（先占位，不做设计）。
     定稿后把文件放进 profile/assets/（建议 logo.svg 黑色版 + logo-dark.svg 白色版），
     再取消下面这段注释即可自动跟随深浅主题显示：

<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="https://github.com/ZQU-Foray/.github/raw/main/profile/assets/logo-dark.svg">
    <img src="https://github.com/ZQU-Foray/.github/raw/main/profile/assets/logo.svg" alt="Foray 战队队徽" width="180">
  </picture>
</p>
-->

---

## 🎯 战队简介

我们来自 **肇庆学院**，参加全国大学生机器人大赛 **RoboMaster 机甲大师赛**，队名 **Foray**。

战队现有 **算法组**（视觉识别、导航定位）与 **电控组**（嵌入式控制、硬件调试）等技术小组，工作覆盖机械、电控、视觉、导航与运营方向。

战队上位机软件系统统一定名为 **Diesel**（2026-11 经队内投票确定，寓意柴油闪点高、不易燃，取「稳定」之意）；`Foray` 保留为战队名与组织名，`Diesel` 用于上位机各仓的仓名、ROS 包名与 C++ 命名空间。迁移范围与批次见 [foray_docs · Diesel 命名迁移计划](https://github.com/ZQU-Foray/foray_docs/blob/main/diesel_naming_migration.md)。

## 🏆 赛季成绩

| 赛季 | 成绩 | 备注 |
|------|------|------|
| 2027 | 备赛中 | 新赛季筹备 |
| 2026 | 华南赛区八强 | RMUL |

## 🚀 系统命名：Diesel

战队上位机软件控制系统定名 **Diesel**——由 [Discussion #6](https://github.com/orgs/ZQU-Foray/discussions/6)
投票通过（2/2 赞成）。`foray` 是**战队名字**，所以它留在组织名和战队资产上；Diesel 是**系统名字**，
软件栈从仓名到节点名全部叫 `diesel_*`。只有 ROS 生态约定的话题与 tf frame 不动：

| 层 | 管什么 | 记法 | 变不变 |
|------|------|------|------|
| 品牌层 | 战队与战队资产 | `ZQU-Foray` · `foray_docs` · `foray_ml` · `foray_robots` · `foray_ws` | 🔒 不变 |
| 系统层 | 整套上位机 | **Diesel** | 🚀 本次定名 |
| 代码层 | 仓库名 · ROS 包名 · namespace · include 根 · 节点名 | `diesel_<domain>` · `diesel_<domain>_<module>` · `diesel::…` · `include/diesel/…` · `diesel_*` | ✅ 跟随系统层 |
| 生态层 | ROS 话题 · tf frame | `/<module>/<entity>` · `map`/`odom`/`base_link` | 🔒 不变 |

```cpp
#include "diesel/localization/map/grid.hpp"   // 头文件在 include/diesel/localization/map/grid.hpp
namespace diesel::localization::map { }       // 三层 namespace：diesel::<domain>::<module>
```

**为什么话题与 tf frame 不动**：它们已经带有正确的语义（`/localization/state` 说明是哪个模块的什么实体），
加 `diesel` 只是重复系统名，收益为零，却会打断 Nav2 配置、`foray_robots` 的参数文件与别人的 `tf2` 链路。
包名与仓名反过来——它们承载"这是哪个仓、哪个包"的信息，统一之后 `colcon list` 一眼就能看出归属。

- 📖 规范全文与旧→新映射表：[foray_docs / naming.md](https://github.com/ZQU-Foray/foray_docs/blob/main/naming.md)
- ⚙️ 风格配置唯一源：[`config/`](https://github.com/ZQU-Foray/.github/tree/main/config)（clang-format / pyproject / editorconfig）
- 🔄 迁移进度：各仓用仓根 `.diesel-naming` 的 `mode: enforced | migrating | na` 自报状态，CI 按此收紧

## 📂 仓库导航

### Diesel · 上位机软件系统（ROS 2）

> 下列仓名是**改名前的现状**。迁到 Diesel 后对应 `diesel_interfaces` / `diesel_platform` / `diesel_localization` /
> `diesel_vision` / `diesel_auto_aim` / `diesel_navigation` / `diesel_decision` / `diesel_simulation`；
> `foray_ws`（元仓）与 `foray_robots`（战队装配）保留 `foray`。进度见
> [naming.md §6.1](https://github.com/ZQU-Foray/foray_docs/blob/main/naming.md)。

| 仓库 | 说明 |
|------|------|
| [diesel_ws](https://github.com/ZQU-Foray/diesel_ws) | 元仓：`.repos` 依赖锁定 · 集成 CI · 一键脚本（零业务代码） |
| [diesel_interfaces](https://github.com/ZQU-Foray/diesel_interfaces) | 接口契约：msg/srv/action · 机间态势协议 · 裁判系统消息 |
| [diesel_platform](https://github.com/ZQU-Foray/diesel_platform) | 平台基础层：时间 / 数学 / 参数 / 日志基础设施 + 下行 HAL |
| [diesel_localization](https://github.com/ZQU-Foray/diesel_localization) | 定位与地图：内置地图 + 激光配准 · 配准残差动态物体检测 |
| [diesel_vision_frontend](https://github.com/ZQU-Foray/diesel_vision_frontend) | 视觉前端：装甲板检测（双模型 ONNX）· PnP 几何 · 可插拔多目标检测框架 |
| [diesel_vision_backend](https://github.com/ZQU-Foray/diesel_vision_backend) | 视觉后端：多源观测融合 · EKF 装甲板跟踪 · 瞄准解算 · WorldSnapshot 输出 |
| [diesel_navigation](https://github.com/ZQU-Foray/diesel_navigation) | 导航栈（ROS 2 / Nav2） |
| [diesel_decision](https://github.com/ZQU-Foray/diesel_decision) | 决策层：战术层 · 技能层 · 安全门 · 机间协同 · 对局仿真 |
| [diesel_robots](https://github.com/ZQU-Foray/diesel_robots) | 兵种装配根：sentry_bringup / infantry_bringup · 参数 · 场地资产 |
| [diesel_simulation](https://github.com/ZQU-Foray/diesel_simulation) | RMUL 2027 3v3 场地资产与「点云 → 定位 → 寻路」仿真链路（Humble + Fortress） |

### 下位机、工具与文档

| 仓库 | 说明 |
|------|------|
| [foray_mcu](https://github.com/ZQU-Foray/foray_mcu) | 下位机固件：多兵种 × 多开发板（STM32H723 主力 / F407 / TM4C） |
| [foray_mcu_controller](https://github.com/ZQU-Foray/foray_mcu_controller) | 原 ControllerCode：MC02 (H723) 与官方 C 板 (F407) 电控代码 |
| [foray_web](https://github.com/ZQU-Foray/foray_web) | 战队内部信息管理 Web |
| [diesel_ml](https://github.com/ZQU-Foray/diesel_ml) | 视觉 CNN 训练全流程工具集：数据准备 → 标注管理 → 预标注 → 训练 → 推理（私有） |
| [mvs-sdk](https://github.com/ZQU-Foray/mvs-sdk) | 海康机器人 MVS 相机 SDK 二进制分发（私有，组织内可见） |
| [foray_docs](https://github.com/ZQU-Foray/foray_docs) | 组织技术文档：仓库结构 · 算法结构 · 地图资产 · **命名与代码风格（naming.md）** |
| [foray-HelloWorld](https://github.com/ZQU-Foray/foray-HelloWorld) | 新队员 Git 协作练习 |

### 算法与平台参考（Fork）

| 仓库 | 说明 |
|------|------|
| [open_vins-foray-fork](https://github.com/ZQU-Foray/open_vins-foray-fork) | 视觉惯性导航研究平台 |
| [VINS-Fusion-foray-fork](https://github.com/ZQU-Foray/VINS-Fusion-foray-fork) | 基于优化的多传感器状态估计 |
| [ORB_SLAM3-foray-fork](https://github.com/ZQU-Foray/ORB_SLAM3-foray-fork) | 视觉 / 视觉惯性 / 多地图 SLAM |
| [RoboRTS-foray-fork](https://github.com/ZQU-Foray/RoboRTS-foray-fork) | RoboMaster 开源软件栈（参考） |

## 🤝 参与贡献

- 提交代码前请先阅读 [贡献指南](https://github.com/ZQU-Foray/.github/blob/main/CONTRIBUTING.md)
- Issue / PR 模板、贡献指南等**组织默认文件**统一由 [.github](https://github.com/ZQU-Foray/.github) 仓库维护，改一次即对全组织生效
- 新队员可从 [foray-HelloWorld](https://github.com/ZQU-Foray/foray-HelloWorld) 开始熟悉协作流程

## 📮 联系我们

- 邮箱：[zqu_foray@protonmail.com](mailto:zqu_foray@protonmail.com)
- 技术讨论：[GitHub Discussions](https://github.com/ZQU-Foray/.github/discussions)（战队群链接待补充）

---

> **加入我们？** 关注校内招新信息，或直接联系战队队长。
