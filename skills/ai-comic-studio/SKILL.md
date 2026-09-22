---
name: ai-comic-studio
description: Use when planning or generating AI comic character sheets, scene anchors, storyboards, or episode image batches with the bundled JSON templates and image-generation scripts. Do not use this as a semantic character-consistency evaluator or a ComfyUI runner.
metadata:
  version: 0.3.0
  domain: ai-comic-image-workflow
---

# AI 漫剧工作室

用角色锚点、场景锚点和分镜模板组织 AI 漫剧出图。先让角色与场景配置可核对，再生成单图或整集；不要把尚未验证的角色一致性当作已实现能力。

## 工作边界

- 角色的 `seed_prompt` 固定描述脸部和体型；同一角色的变体只描述服装或状态。需要调整镜头、情绪或光影时，不重写这两个锚点。
- `references/characters/`、`references/scenes/` 和 `references/scripts/` 分别保存角色、场景和剧集 JSON。先从其中的中文模板复制并填写，再调用脚本。
- `references/templates/` 说明构图选型：单人用 `full-body` 或 `half-body`，双人对话用 `conversation`，动作镜头用 `fight`，空镜用 `scene-board`，多格叙事用 `comic-grid`。
- 不把角色、客户剧本、生成图片、`manifest.json` 或 `.env` 提交到这个 skills 合集。`.env` 含密钥；即使本地存在，也不要执行 `git add .env`。

## 生成前检查

1. 明确用户要的是配置、分镜、单张图还是整集。只有配置请求时不要触发出图 API。
2. 对剧集逐帧核对 `characters` 中的角色和变体、`scene` 中的场景，以及构图模板是否匹配；缺少依赖时先报告，不能边生成边猜测。
3. 生图会向 AIHubMix 的图像 API 发送提示词并可能消耗额度。运行前确认用户已要求生成、模型与输出位置符合预期。
4. 运行时要求 Node.js 18+。脚本使用内置 `fetch`，没有 npm 依赖；把 `.env.example` 复制为本地 `.env` 后填入 `AIHUBMIX_API_KEY`，但绝不提交这个文件。

## 命令

```bash
# 不需要 API Key；确认角色和变体配置
node scripts/gen-image.mjs --list-chars

# 角色锚点 + 变体 + 构图 + 情绪，默认写入 outputs/
node scripts/gen-image.mjs --char 角色名 --variant casual --composition "全身立绘" --emotion "平静"

# 自由提示词（不会附加角色锚点）
node scripts/gen-image.mjs "雨夜的城市天际线"

# 读取 references/scripts/剧集名.json，逐帧串行生成
node scripts/gen-episode.mjs 剧集名
```

生成后人工抽查输出文件、对应 JSON 和实际提示词。整集生成的 `manifest.json` 只记录运行结果，不能证明角色外观一致。

## 已知限制

- 脚本当前只向 API 发送 `prompt`；剧集 JSON 中的 `size` 字段尚未传给服务端，不能据此承诺图片尺寸。
- `forbidden`、负面提示词、ComfyUI workflow、多项目隔离和基于 CLIP/embedding 的语义一致性检查都未实现。
- 不收录原项目的 `character-checker.mjs`：它只能做全局文件大小异常检查，无法确认某张图属于指定角色。

## 参考资料

- 角色、场景和剧集字段分别见 `references/characters/角色模板.json`、`references/scenes/场景模板.json`、`references/scripts/剧集模板.json`。
- 只在选分镜时读取所需的 `references/templates/*.md`；不要为简单单图请求加载全部模板。
