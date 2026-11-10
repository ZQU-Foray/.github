# config/ —— 组织风格配置的唯一源

这里的三个文件是**全组织 canonical**：各仓复制到自己的仓库根目录，不再各自定义。

| 文件 | 作用 | 各仓怎么用 |
|---|---|---|
| [`.clang-format`](.clang-format) | C/C++ 风格（4 空格 · 100 列 · 指针左靠） | 复制到仓根；`clang-format -i` 一把梭 |
| [`pyproject.toml`](pyproject.toml) | `ruff` + `black` 配置（py310 / 88 列） | 复制到仓根；`ruff check .` / `black --check .` |
| [`.editorconfig`](.editorconfig) | 缩进 / 换行 / 编码的编辑器兜底 | 复制到仓根 |

## 为什么要集中

2026-11-03 盘点时，同一个 `.clang-format` 在组织内出现了三个状态：34 行组织版（3 个仓）、
10 行精简版（`foray_localization`，缺 `AllowShortIfStatements` 等，导致格式化结果与别人不同）、
缺失（2 个仓）。配置一致之前，"跑过格式化工具"这件事本身不保证任何东西。

## 校验

各仓 CI 复制组织模板 `workflows/ci-template.yml` 后，`style-config` 作业会拿本目录的文件
与仓根同名文件逐字节比对。严格程度由仓根 `.diesel-naming` 的 `mode` 决定：

```yaml
mode: enforced   # 不一致即失败
mode: migrating  # 只告警（迁移期默认）
mode: na         # 跳过（非 C++ / 非 Python 仓）
```

## 改这里的流程

1. 在 `.github` 提 PR，改本目录文件；
2. 同一 PR 里更新 `foray_docs` 的 `naming.md`（§5 与映射表），两个仓必须同步；
3. 合并后各仓再把 canonical 拉一遍，`mode: enforced` 的仓会在 CI 里被点名。

顺带建议（不强制、不做比对）：各仓根放 `.gitattributes` 写 `* text=auto eol=lf`，
防止 Windows 机器把 CRLF 带进来——`.editorconfig` 管不住已经提交进库的文件。
