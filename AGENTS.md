# StevenCloud47 个人主页维护约定

## 项目与工作方式

本仓库是 Yunrui Jiao（焦云锐）的英文科学研究个人主页，基于 AcadHomepage / Jekyll，通过 GitHub Pages 发布。

- 远程：`https://github.com/StevenCloud47/StevenCloud47.github.io.git`
- 分支：`main`；预期跟踪 `origin/main`。
- 主页：`https://stevencloud47.github.io/`
- 本机当前仓库：`D:\个人发展\myself\StevenCloud47.github.io`。命令和文件引用优先相对当前仓库编写，以便再次迁移。
- 本文件是当前维护约定，不依赖全局 OpenCode skill。历史流程文档及旧 skill 的旧路径不作为当前工作入口。
- 用户提出具体主页更新后，默认完成定位、修改、检查、commit 和 push；若本轮要求只读、草稿或暂不上传，以本轮要求为准。
- 对已授权的修改与上传持续执行，不增加逐步确认。仅在关键信息无法合理推断、出现无法安全处理的冲突、需要用户重新登录或出现超出授权的高影响操作时询问。

## 修改地图

| 需求 | 主要位置 |
| --- | --- |
| 简介、News、Publications、Honors and Awards、Educations、Activities、Academic Service、Internships、Social Works | `_pages/about.md` |
| 姓名、头像、邮箱、地点、学术主页链接、站点全局配置 | `_config.yml` |
| 顶部导航名称和锚点 | `_data/navigation.yml` |
| 头像、主页图片 | `images/` |
| 其他静态资源 | `assets/` |
| 模板、组件、样式 | `_layouts/`、`_includes/`、`_sass/`，仅按用户要求修改 |
| Scholar 引用更新 | `.github/workflows/google_scholar_crawler.yaml`、`google_scholar_crawler/`，日常内容更新不修改 |

## 内容约定

- 只修改本次要求的内容，保持原有英文风格、HTML/Markdown 混排、颜色、emoji、编码和换行，不进行无关格式化或重构。
- 用户提供中文主页内容时，默认翻译为自然、简洁的英文；中文官方名称可依既有格式保留。
- News 位于 `# 🔥 News`，按日期倒序插入，沿用 `- **YYYY.MM.DD:** ...` 和 Markdown 链接格式。
- Publications 位于 `# 📝 Publications`，保留期刊、会议、摘要、专利分区和现有 HTML 列表；新增条目保证 `JP-Pub*`、`CP-Pub*` 等 id 唯一，按相应分区现有顺序插入。
- 保留 co-first / corresponding author 标记和本人姓名高亮。作者、顺序、年份、论文状态、题目、链接以用户材料为依据，不推断录用或正式发表，不编造 DOI。
- 论文从 under review 更新为 accepted/published 时，仅在用户材料支持后移除 `(Under Review)` 并添加实际链接。
- Honors and Awards 保持 Master / Undergraduate 分区，分区内日期倒序。沿用现有颜色：`#ccab00` 奖项名、`#80704c` 名次、`#27a4a4` 普通荣誉、`#dc143c` 突出奖项。
- 更新图片时核对引用路径和文件存在性；没有要求时保留旧图片。
- 导航调整需同时核对目标锚点；不要顺便修复本次范围以外的旧问题。

## Git 工作流

1. 在实际仓库内先执行 `git status --short --branch`、`git remote -v`、`git branch --show-current`，确认路径、远程、分支和已有改动。
2. 保留用户已有修改与暂存内容，不覆盖、不回退、不混入本次提交。可独立完成的任务继续执行；只有相关冲突或提交边界不能明确时才询问。
3. 修改前执行 `git fetch origin main`，确认远程变化；工作区允许时用 `git merge --ff-only origin/main` 同步。不要自动重写历史、强制推送或制造不必要的 merge commit。
4. 定位并完成用户要求的最小修改，检查 `git diff --check`、`git diff -- <本次文件>` 和 `git status --short`；新文件也必须检查内容。避免整文件换行变化。
5. 只使用 `git add -- <本次文件>` 明确暂存；同文件已有用户修改时按实际 diff 仅暂存本任务部分。提交前检查 `git diff --cached`，不得默认 `git add .`。
6. 复用仓库已有 Git 身份与凭据，使用准确、简洁的英文 commit message，不擅自改全局配置或创建 token。
7. 执行 `git push origin main`。失败时先根据实际网络、认证或远程变更诊断；不要把认证失败当作网络错误反复重试。
8. 上传后执行 `git status --short --branch`、`git rev-parse HEAD`、`git ls-remote origin refs/heads/main`，核对远程实际提交与本地一致。若仍有其他任务的原有改动，单独说明。

### 本机网络

2026-10-22 已验证本机一次性代理可用于 fetch/push：

```powershell
git -c http.proxy=http://127.0.0.1:1080 -c https.proxy=http://127.0.0.1:1080 fetch origin main
git -c http.proxy=http://127.0.0.1:1080 -c https.proxy=http://127.0.0.1:1080 push origin main
git -c http.proxy=http://127.0.0.1:1080 -c https.proxy=http://127.0.0.1:1080 ls-remote origin refs/heads/main
```

这些参数仅用于当次命令，不写入全局 Git 配置。代理不可用时核实当前网络后再选择直连，不假定历史端口永久有效。认证复用现有 Git Credential Manager；若必须重新登录、2FA 或输入秘密，由用户完成，不读取本地恢复码文件。

## 验证与完成标准

- 普通内容更新检查变更范围、日期顺序、链接、HTML 标签、图片引用以及提交范围，不为简单文案建立测试框架。
- 只有需要本地页面预览且环境已具备时才运行 Jekyll；先检查 Ruby/Bundler。环境缺失时如实说明，不为普通内容更新自动安装整套环境。
- `AGENTS.md` 是维护文档，在 `_config.yml` 的 `exclude` 中保留其排除项。
- 默认完成标准：本次修改已检查、commit 成功、push 成功、远程实际 `main` 与本地 HEAD 一致；原本干净的工作区应保持干净。
- push 成功不等于 GitHub Pages 已部署成功。除非用户要求验证线上效果，不等待网页刷新；报告中明确是否实际验证部署和显示效果。
- 完成时用中文说明：修改内容与文件、commit id、push 结果、本地/远程同步情况、验证范围。
- 用户要求撤销已上传修改时优先 `git revert`；不默认 `reset --hard` 或 force push。
