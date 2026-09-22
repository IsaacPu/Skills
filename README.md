# IsaacPu Skills

这是一个面向 Codex 的可复用技能合集。每个 skill 位于 `skills/` 下的独立文件夹，解决一类明确、可验证的工作；不收录一次性的项目文件、客户数据或泛化提示词。

[![skills.sh](https://skills.sh/b/isaacpu/skills)](https://skills.sh/isaacpu/skills)

## 当前技能

| 分类 | Skill | 用途 | 安装命令 | 状态 |
| --- | --- | --- | --- | --- |
| 表格审核 | [CAD Dimension Comparison Table Skill](./skills/cad-dimension-comparison-table/) | 对照正式点位表与 CAD 人工统计表，按明确范围双向核对，并在人工表版式中回写差异。 | `npx skills add https://github.com/IsaacPu/Skills --skill cad-dimension-comparison-table` | 已验证 |
| AI 漫剧 | [AI Comic Studio](./skills/ai-comic-studio/) | 用角色、场景和分镜 JSON 组织 AI 漫剧出图；明确第三方 API、尺寸和一致性检查边界。 | `npx skills add https://github.com/IsaacPu/Skills --skill ai-comic-studio` | 已审核，待 API 实测 |

## 合集约定

- 每个 skill 位于 `skills/` 下一个独立的 `kebab-case` 文件夹，入口文件必须为 `SKILL.md`。
- 目录只收录可复用的工作方法；项目源文件、客户资料、临时输出和密钥不入库。
- 新增或更新 skill 时，同时更新本页目录，并遵循 [贡献规范](./CONTRIBUTING.md)。
- 设计原则、分类方式和质量门槛见 [合集设计](./docs/collection-design.md)。

## 适用边界

本仓库服务于 Codex skill 工作流。每个 skill 的 `SKILL.md` 都会说明何时应该使用、何时不应使用，以及完成任务所需的关键验证步骤。
