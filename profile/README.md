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

## 🏆 赛季成绩

| 赛季 | 成绩 | 备注 |
|------|------|------|
| 2027 | 备赛中 | 新赛季筹备 |
| 2026 | 华南赛区八强 | RMUL |

## 📂 仓库导航

### 上位机（ROS 2）

| 仓库 | 说明 |
|------|------|
| [foray_ws](https://github.com/ZQU-Foray/foray_ws) | 元仓：`.repos` 依赖锁定 · 集成 CI · 一键脚本（零业务代码） |
| [foray_interfaces](https://github.com/ZQU-Foray/foray_interfaces) | 接口契约：msg/srv/action · 机间态势协议 · 裁判系统消息 |
| [foray_platform](https://github.com/ZQU-Foray/foray_platform) | 平台基础层：时间 / 数学 / 参数 / 日志基础设施 + 下行 HAL |
| [foray_localization](https://github.com/ZQU-Foray/foray_localization) | 定位与地图：内置地图 + 激光配准 · 配准残差动态物体检测 |
| [foray_vision](https://github.com/ZQU-Foray/foray_vision) | 视觉与态势：装甲板检测跟踪 · 多源态势融合 · WorldSnapshot 生成 |
| [foray_auto_aim](https://github.com/ZQU-Foray/foray_auto_aim) | 自瞄：弹道解算 · 多源目标融合 · 装甲板跟踪 |
| [foray_navigation](https://github.com/ZQU-Foray/foray_navigation) | 导航栈（ROS 2 / Nav2） |
| [foray_decision](https://github.com/ZQU-Foray/foray_decision) | 决策层：战术层 · 技能层 · 安全门 · 机间协同 · 对局仿真 |
| [foray_robots](https://github.com/ZQU-Foray/foray_robots) | 兵种装配根：sentry_bringup / infantry_bringup · 参数 · 场地资产 |
| [foray_simulation](https://github.com/ZQU-Foray/foray_simulation) | RMUL 2027 3v3 场地资产与「点云 → 定位 → 寻路」仿真链路（Humble + Fortress） |

### 下位机、工具与文档

| 仓库 | 说明 |
|------|------|
| [foray_mcu](https://github.com/ZQU-Foray/foray_mcu) | 下位机固件：多兵种 × 多开发板（STM32H723 主力 / F407 / TM4C） |
| [foray_mcu_controller](https://github.com/ZQU-Foray/foray_mcu_controller) | 原 ControllerCode：MC02 (H723) 与官方 C 板 (F407) 电控代码 |
| [foray_web](https://github.com/ZQU-Foray/foray_web) | 战队内部信息管理 Web |
| [foray_ml](https://github.com/ZQU-Foray/foray_ml) | 视觉 CNN 训练全流程工具集：数据准备 → 标注管理 → 预标注 → 训练 → 推理（私有） |
| [mvs-sdk](https://github.com/ZQU-Foray/mvs-sdk) | 海康机器人 MVS 相机 SDK 二进制分发（私有，组织内可见） |
| [foray_docs](https://github.com/ZQU-Foray/foray_docs) | 组织技术文档：仓库结构 · 算法结构 · 地图资产 |
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
