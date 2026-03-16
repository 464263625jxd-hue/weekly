# 知行周刊代码库文件管理规范 v1.0

**生效日期**: 2026-03-16
**适用范围**: 知行周刊所有代码库（weekly、weekly-backup、zhixing-weekly-web）

---

## 📁 标准文件结构

```
zhixing-weekly/
├── data.json              # 主数据文件（所有期数汇总）
├── index.html             # Web展示页面
├── favicon.svg            # 网站图标
├── version.json           # 版本信息
├── README.md              # 项目说明
│
├── sources/               # 资讯源目录
│   ├── issue-67.docx     # 第67期原始资讯源
│   ├── issue-68.docx     # 第68期原始资讯源
│   └── issue-69.docx     # 第69期原始资讯源
│
├── issues/                # 往期数据目录（可选）
│   ├── issue-67/
│   │   └── issue67.json  # 第67期数据
│   ├── issue-68/
│   │   └── issue68.json  # 第68期数据
│   └── issue-69/
│       └── issue69.json  # 第69期数据
│
├── docs/                  # 文档目录
│   ├── STANDARDIZATION.md   # 标准化规范
│   ├── WORKFLOW.md          # 工作流程
│   └── issue-XX-*.md        # 往期相关文档
│
└── archive/               # 归档目录（可选）
    └── scripts/           # 废弃脚本归档
```

---

## 📋 文件分类说明

### 1. 核心文件（必须保留）

| 文件 | 说明 | 更新时机 |
|------|------|----------|
| `data.json` | 主数据文件，包含所有期数 | 每期更新 |
| `index.html` | Web展示页面 | 功能更新时 |
| `favicon.svg` | 网站图标 | 一次性 |
| `version.json` | 版本信息 | 每期更新 |
| `README.md` | 项目说明 | 重要变更时 |

### 2. 资讯源文件（必须上传）

| 文件 | 说明 | 位置 |
|------|------|------|
| `issue-XX.docx` | 第XX期原始资讯源 | `sources/` |

**要求**：每期制作完成后，必须将原始资讯源文件上传到 `sources/` 目录。

### 3. 往期数据（可选保留）

| 文件 | 说明 | 位置 |
|------|------|------|
| `issueXX.json` | 第XX期完整数据 | `issues/issue-XX/` |

**说明**：可在 `data.json` 中获取所有期数，单期文件为备份用途。

### 4. 制作过程文件（必须清理）

| 文件类型 | 示例 | 处理方式 |
|----------|------|----------|
| 中间数据文件 | `issue69_news.json`, `issue69_news_v2.json` | ❌ 删除 |
| 调试脚本 | `fix_issue68.py`, `make_issue68_v2.py` | 📦 归档到 `archive/scripts/` 或删除 |
| 临时文档 | `README-WEB.md`, `REBUILD_PLAN.md` | 📦 归档或合并到 `docs/` |

---

## 🔄 更新流程标准

### 每期更新步骤

```bash
# 1. 清理制作过程文件
rm -f issue*_news*.json
rm -f *.py  # 或归档到 archive/scripts/

# 2. 上传资讯源文件
cp ~/Desktop/知行周刊第XX期.docx sources/issue-XX.docx

# 3. 更新核心文件
# - data.json（自动更新）
# - version.json（自动更新）
# - issueXX.json（可选）

# 4. 更新README（如有重要变更）

# 5. 提交并推送
git add -A
git commit -m "Issue XX: 标题（资讯数）"
git push
```

### 文件检查清单

- [ ] `data.json` 是否更新？
- [ ] `version.json` 是否更新？
- [ ] 资讯源文件是否上传到 `sources/`？
- [ ] 中间文件是否清理？
- [ ] README 是否需要更新？

---

## 🗂️ 文件命名规范

### 资讯源文件
- 格式：`issue-XX.docx`
- 示例：`issue-69.docx`

### 单期数据文件
- 格式：`issueXX.json`
- 示例：`issue69.json`

### 文档文件
- 格式：`UPPERCASE.md` 或 `issue-XX-topic.md`
- 示例：`STANDARDIZATION.md`, `issue-68-push-message.md`

---

## ⚠️ 禁止事项

1. ❌ 禁止提交中间文件（`*_news*.json`, `*_temp.json`）
2. ❌ 禁止提交调试脚本到根目录
3. ❌ 禁止提交包含敏感信息的文件
4. ❌ 禁止删除 `sources/` 目录中的资讯源文件

---

## 📊 当前状态检查

### 需要清理的文件

| 文件 | 状态 | 处理方式 |
|------|------|----------|
| `issue69_news.json` | ❌ 中间文件 | 删除 |
| `issue69_news_v2.json` | ❌ 中间文件 | 删除 |
| `README-WEB.md` | ⚠️ 过时文档 | 归档到 `docs/` |
| `REBUILD_PLAN.md` | ⚠️ 过时文档 | 归档到 `docs/` |
| `scripts/fix_issue68.py` | ⚠️ 过时脚本 | 归档到 `archive/scripts/` |
| `scripts/make_issue68_v2.py` | ⚠️ 过时脚本 | 归档到 `archive/scripts/` |

### 需要补充的文件

| 文件 | 位置 | 状态 |
|------|------|------|
| `issue-69.docx` | `sources/` | ❌ 缺失 |

---

**最后更新**: 2026-03-16
