# IsaacPu Skills

这是一个面向 Codex 的个人可复用技能合集。每个 skill 解决一类明确、可验证的工作，而不是把一次性的项目文件、客户数据或泛化提示词放进仓库。

## 下载与安装

### 在 Codex 中安装（推荐）

在 Codex 对话中输入以下请求，让内置安装器从本仓库下载指定 skill：

```text
请使用 $skill-installer 从 GitHub 仓库 IsaacPu/Skills 安装 cad-dimension-comparison-table。
```

安装完成后，可在下一轮 Codex 对话中使用；若未显示，再重启 Codex。安装器会把指定 skill 安装到本机的 skills 目录；不会把整个仓库误当成一个 skill。

### 下载源码

- 网页下载：在 GitHub 仓库点击 **Code → Download ZIP**，或直接下载 [main 分支 ZIP](https://github.com/IsaacPu/Skills/archive/refs/heads/main.zip)。
- Git 克隆：`git clone https://github.com/IsaacPu/Skills.git`

下载源码适合查看、审核或二次开发。若要在 Codex 中调用某个 skill，优先使用上面的安装器；手动安装时，应复制单个 skill 文件夹（例如 `cad-dimension-comparison-table`）及其全部内容，而不是只复制 `SKILL.md`。

### 调用示例

安装 `cad-dimension-comparison-table` 后，可以在请求中写：

```text
使用 $cad-dimension-comparison-table 对照我的 CAD 人工数图表与正式点位表，按指定建筑范围审核并输出原表内差异工作簿。
```

## 当前技能

| 分类 | Skill | 用途 | 状态 |
| --- | --- | --- | --- |
| 表格审核 | [CAD Dimension Comparison Table Skill](./cad-dimension-comparison-table/) | 对照正式点位表与 CAD 人工统计表，按明确范围双向核对，并在人工表版式中回写差异。 | 已验证 |
| AI 漫剧 | [AI Comic Studio](./ai-comic-studio/) | 用角色、场景和分镜 JSON 组织 AI 漫剧出图；明确第三方 API、尺寸和一致性检查边界。 | 已审核，待 API 实测 |

## 合集约定

- 每个 skill 是仓库根目录下一个独立的 `kebab-case` 文件夹，入口文件必须为 `SKILL.md`。
- 目录只收录可复用的工作方法；项目源文件、客户资料、临时输出和密钥不入库。
- 新增或更新 skill 时，同时更新本页目录，并遵循 [贡献规范](./CONTRIBUTING.md)。
- 设计原则、分类方式和质量门槛见 [合集设计](./docs/collection-design.md)。

## 适用边界

本仓库服务于 Codex skill 工作流。每个 skill 的 `SKILL.md` 都会说明何时应该使用、何时不应使用，以及完成任务所需的关键验证步骤。
