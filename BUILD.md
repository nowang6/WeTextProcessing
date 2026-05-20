# WeTextProcessing 打包指南

## 项目构建配置

项目使用 **pyproject.toml** 配置构建，基于 **setuptools** 构建后端，版本号由 **setuptools-scm** 从 git 历史自动管理。

### 关键配置项

| 配置 | 说明 |
|------|------|
| `build-backend` | `setuptools.build_meta` |
| `dynamic = ["version"]` | 版本号由 setuptools-scm 动态生成 |
| `tool.setuptools.packages.find` | 自动发现 `tn*` 和 `itn*` 包 |
| `tool.setuptools.package-data` | 包含 `.fst`、`.tsv`、`.far` 数据文件 |

### 依赖项

- **构建依赖**: `setuptools>=45`, `wheel`, `setuptools_scm[toml]>=6.2`
- **运行依赖**: `pynini>=2.1.6,<2.1.7`, `importlib_resources`
- **Python 要求**: `>=3.7`

## 打包步骤

### 1. 创建虚拟环境

```bash
uv venv .venv
```

### 2. 安装构建工具

```bash
source .venv/bin/activate
uv pip install build wheel setuptools setuptools-scm
```

### 3. 构建 wheel

```bash
python -m build --wheel
```

构建完成后，wheel 文件生成在 `dist/` 目录下：

```
dist/wetextprocessing-X.Y.Z-py3-none-any.whl
```

## 安装

```bash
pip install dist/wetextprocessing-X.Y.Z-py3-none-any.whl
```

安装后可用的命令行工具：
- `wetn` — 文本正则化 (TN)
- `weitn` — 逆文本正则化 (ITN)

## 版本号说明

由 `setuptools-scm` 根据 git tag 和 commit 数自动生成：
- 有 tag 时：`1.0.5`（tag 版本）
- tag 后有新 commit：`1.0.6.dev204`（自上次 tag 后 204 个 commit）
- 无 git 时的回退版本：`1.0.5`（在 pyproject.toml 中配置的 `fallback_version`）

版本号文件会写入 `tn/_version.py`。
