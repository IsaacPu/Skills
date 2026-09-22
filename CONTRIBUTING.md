# 新增与维护 Skill

## 新增前的判断

仅当一个方法能在多个类似任务中复用，并且存在需要保留的非显而易见约束、判断规则或验收步骤时，才新增 skill。一次性的项目说明、样例数据和临时脚本不应包装成 skill。

## 目录规范

```text
skill-name/
├── SKILL.md                 # 必需：YAML frontmatter 和工作说明
├── agents/openai.yaml        # 可选：面向 Codex 界面的名称和默认提示
├── references/               # 可选：按需读取的细节
├── scripts/                  # 可选：可重复执行的确定性工具
└── assets/                   # 可选：生成结果所需的资源
```

skill 文件夹使用小写、数字和连字符。`SKILL.md` 的 `name` 必须与文件夹名一致，`description` 要能准确说明适用场景和边界。

## 入库检查

1. 以一个真实或接近真实的请求检查 skill 是否会被正确选择。
2. 用 Codex 自带 `skill-creator` 的 `quick_validate.py` 校验 `SKILL.md` 的 frontmatter、命名和未完成占位符。
3. 若新增脚本，执行一次与其职责相符的测试；若涉及产物，检查实际产物而不只检查日志。
4. 在 `README.md` 的“当前技能”中登记名称、用途和状态。
5. 通过目的明确的分支和中文 PR 提交，说明本次修改、验证方式、风险与边界。

## 文档边界

仓库级介绍、设计与贡献说明放在根目录或 `docs/`。不要给每个 skill 重复创建 README、安装说明或变更日志，除非该资源确实是使用该 skill 的必要条件。
