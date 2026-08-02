# 🤝 贡献指南

欢迎为战队代码库贡献！无论你是新队员还是老队员，请先阅读本指南。

---

## 📋 目录

1. [入门](#入门)
2. [开发工作流](#开发工作流)
3. [Commit 规范](#commit-规范)
4. [代码风格](#代码风格)
5. [Pull Request 流程](#pull-request-流程)
6. [文档约定](#文档约定)

---

## 入门

### 新队员 Checklist

- [ ] 阅读本贡献指南
- [ ] 配置 Git 用户名和邮箱（使用学校邮箱）
- [ ] 了解 [RoboMaster 比赛规则](https://www.robomaster.com)
- [ ] 阅读对应方向的技术文档（见各仓库 README）
- [ ] 开始开发

### 环境准备

```bash
# 配置 Git
git config --global user.name "你的姓名"
git config --global user.email "你的邮箱"
```

---

## 开发工作流

> 一定千万牢记不要在main分支进行任何push和merge操作，违者打死。

```
main          ← 稳定版本，经过测试和 Review
  └─ dev      ← 开发分支，所有更改在此分支进行调试
       └─ feat/xxx   ← 功能分支
       └─ fix/xxx    ← 修复分支
       └─ docs/xxx   ← 文档分支
```

### 标准流程

```bash
# 1. 从 dev 创建功能分支
git checkout dev
git pull origin dev
git checkout -b feat/你的功能名

# 2. 开发 & 提交
git add .
git commit -m "feat(scope): 功能描述"

# 3. 推送到远端
git push origin feat/你的功能名

# 4. 在 GitHub 上创建 Pull Request → dev
```

### 同步上游

```bash
# 开发过程中 dev 分支可能有新提交，定期同步
git checkout dev
git pull origin dev
git checkout feat/你的功能名
git rebase dev
```

---

## Commit 规范

采用 [Conventional Commits](https://www.conventionalcommits.org/) 规范：

```
<type>(<scope>): <简短描述>

<详细描述>（可选）

<关联 Issue>（可选）
```

### Type 类型

| Type | 说明 |
|------|------|
| `feat` | 新功能 |
| `fix` | Bug 修复 |
| `docs` | 文档更新 |
| `style` | 代码格式（不影响功能） |
| `refactor` | 代码重构 |
| `perf` | 性能优化 |
| `test` | 测试相关 |
| `chore` | 构建/工具/依赖 |

### Scope 范围

根据仓库模块划分，例如：

- 视觉仓库: `detector` / `classifier` / `preprocess`
- 电控仓库: `chassis` / `gimbal` / `shooter` / `comm`
- 公共: `ci` / `docs` / `config`

### 示例

```
feat(detector): 添加装甲板灯条检测

使用传统视觉方法提取灯条特征，通过颜色和形状匹配定位装甲板。
测试集准确率 92%。

Closes #12
```

```
fix(chassis): 修复底盘右转时电机卡顿问题

PID 参数在急转工况下积分饱和，添加积分限幅解决。
```

---

## 代码风格

### 通用规则

- **缩进**: 统一使用 4 空格
- **换行符**: LF (`\n`)
- **文件末尾**: 保留一个空行
- **编码**: UTF-8

### 按语言

| 语言 | 格式化工具 | 配置 |
|------|-----------|------|
| Python | `ruff` + `black` | 见仓库 `pyproject.toml` |
| C/C++ | `clang-format` | 见仓库 `.clang-format` |
| YAML/JSON | `prettier` | 默认配置 |

### Python 命名

- 变量/函数: `snake_case`
- 类: `PascalCase`
- 常量: `UPPER_SNAKE_CASE`
- 私有成员: 前缀 `_`

### C/C++ 命名

- 变量/函数: `snake_case`
- 结构体/类: `PascalCase`
- 宏/枚举: `UPPER_SNAKE_CASE`

---

## Pull Request 流程

### 提交前自查

- [ ] 本地编译/运行通过
- [ ] 代码符合风格规范（运行了格式化工具）
- [ ] 添加了必要的注释和文档
- [ ] 不包含调试代码、临时文件和密钥

### PR 标题

同 Commit 规范，使用 Conventional Commits 格式。

### PR 描述模板

见 [PULL_REQUEST_TEMPLATE.md](PULL_REQUEST_TEMPLATE.md)

### Review 要求

- 至少 **1 人** Review 并通过后才可以合并
- 视觉/电控方向代码建议由**组长** Review
- Review 关注：逻辑正确性、代码可读性、潜在的 Bug

---

## 文档约定

### 每个仓库必须包含

- `README.md` — 项目介绍、快速开始、依赖说明
- 必要时包含 `docs/` 目录存放详细文档

### 代码注释

- **公共 API/函数**: 必须有 Docstring / Doxygen 注释
- **关键算法**: 注释说明原理和参考来源
- **魔法数字**: 必须注释解释来源（如规则手册页码、标定值）

```
// PID 参数来源于 2024 赛季标定，对应 RM3510 电机
#define KP_VEL 0.5f
```

---

## 求助

- 📖 技术文档：[docs 仓库](https://github.com/ZQU-Foray/docs)
- 💬 技术讨论：战队飞书群
- 🐛 问题反馈：对应仓库的 Issues

> 💡 **不确定该怎么做？** 先看别人怎么做的，或者直接问组长。没有人一开始就什么都会！
