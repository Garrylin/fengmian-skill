# fengmian-skill

从一句主题开始，让 AI 助手带你制作清楚、醒目的视频封面。默认交付横竖两张独立图片，无需写代码、准备专业照片或先确定账号定位。

这是给 AI 助手读取的工作说明，不是可以双击运行的软件，也不是图像模型。它负责引导、选文案、排版和验收；生成图片需要你使用的助手本身具有生图能力。支持参考图编辑时，才可以把你自己的照片用于封面。所用平台可能有额度或费用，本技能不附带额度。

## 一句话安装

如果你使用的 AI 助手具有联网、GitHub 访问和本地文件写入能力，可以直接复制下面这句话发送给它：

> 请从 https://github.com/Garrylin/fengmian-skill 安装 `fengmian-skill`：先检查仓库内容和当前环境支持的用户级 Skills 目录；如果目标目录已存在，不要覆盖，先比较差异并询问我；安装后验证该 Skill 能被发现，并告诉我调用方式。若当前产品不支持持久安装，请明确说明并改为本次会话读取，不要声称已经安装成功。

这条口令不是绕过权限的“万能安装链接”。它只有在当前助手能够下载文件并写入自己的 Skills 目录时，才会真正完成安装；安装过程中出现下载、写入或覆盖确认时，应由用户决定是否继续。

### 各平台怎么说

**Codex（桌面端或 CLI）**

> 请把 https://github.com/Garrylin/fengmian-skill 安装为当前 Codex 的用户级 Skill，保留完整目录结构；若已有同名目录先不要覆盖。安装后检查 `SKILL.md` 是否能被发现，并告诉我是否需要新开任务。

Codex 能读取 Skill 的名称、描述和完整说明，并在任务匹配或用户明确调用时加载它。安装后建议新开任务，再说“使用 `$fengmian-skill`，帮我做封面”。参见 [OpenAI Skills 说明](https://developers.openai.com/plugins/concepts/skills)。

**Claude Code**

> 请从 https://github.com/Garrylin/fengmian-skill 安装 `fengmian-skill` 到我的 Claude Code 用户级 Skills 目录 `~/.claude/skills/`；若已存在先比较差异，不要直接覆盖。安装后验证 `/fengmian-skill` 可以被发现。

这里指具备终端和文件权限的 Claude Code，不是普通网页聊天。Claude Code 官方支持用户级目录 `~/.claude/skills/<skill-name>/SKILL.md`，也支持项目级 `.claude/skills/`。参见 [Claude Code Skills 文档](https://code.claude.com/docs/en/skills)。

**WorkBuddy**

> 请检查并从 https://github.com/Garrylin/fengmian-skill 安装 `fengmian-skill`。先审查仓库内容和权限；如果当前版本不能直接从 GitHub 安装，请下载完整 ZIP，并告诉我在“技能 → 添加技能 → 上传技能”中导入哪个文件。安装后验证它出现在“已安装”列表中。

WorkBuddy 官方支持上传本地技能包，也支持在产品内查找或创建 Skill；不同版本是否能在对话中直接完成 GitHub 下载与安装，以实际权限提示为准。参见 [WorkBuddy 技能说明](https://www.workbuddy.cn/docs/workbuddy/From-Beginner-to-Expert-Guide/Function-Description/Skills-Market)。

**DeepSeek**

- 在使用 DeepSeek 模型的 Codex 中，按上面的 Codex 方式安装，Skill 由 Codex 承载。
- 在支持 Agent Skills 的 Deep Code 中，可以发送：

> 请从 https://github.com/Garrylin/fengmian-skill 安装 `fengmian-skill` 到用户级目录 `~/.agents/skills/`；若已存在先比较差异，不要覆盖。安装后验证该 Skill 能被发现。

- 普通 DeepSeek 网页或手机对话如果没有本地文件和 Skills 安装入口，就不能永久安装。可以上传 `SKILL.md` 及 `references/` 文件，并说：“请在本次对话中读取并遵循这些封面制作说明”；这只对当前对话生效。Deep Code 的目录规则见 [DeepSeek 官方集成说明](https://api-docs.deepseek.com/quick_start/agent_integrations/deepcode/)。

判断是否真的安装成功，只看三个结果：完整文件夹已经写入正确目录、助手能发现 `fengmian-skill`、新对话中可以正常调用。只回复“我已经理解”、只生成一段提示词或只读取 GitHub 页面，都不算安装完成。

## 开始使用

1. 解压分享包，保留整个 `fengmian-skill` 文件夹及内部目录结构。发布到 GitHub 后，也可从仓库的 **Code → Download ZIP** 下载。找到直接包含 `SKILL.md` 的目录，将其命名为 `fengmian-skill`（去掉 GitHub 下载目录可能带的 `-main` 等分支后缀）。
2. 在支持 Skill 的助手中导入这个文件夹。以本地 Codex 为例，可把整个文件夹放到用户目录的 `.codex/skills/` 下；设置过 `CODEX_HOME` 时使用其下的 `skills/`。再新开任务检查能否找到 `fengmian-skill`。目录应形如 `.codex/skills/fengmian-skill/SKILL.md`，避免多层嵌套。如果产品界面不同，直接把文件夹交给助手，说：“请检查当前环境如何加载这个 Skill。”
3. 如果应用支持读取附件但没有安装 Skill 的入口，也可附上整个文件夹，让助手读取 `SKILL.md` 并遵循其中流程；这只是当前对话使用，不等于已永久安装。
4. 发送下面任意一句。想用自己的人物照片，就同时附上一张清晰照片；没有照片也可以制作。

> 使用 $fengmian-skill，帮我做封面，主题是个人养老金，我第一次用。

> 使用 $fengmian-skill，主标题“个人养老金”，副标题“值不值得买？”，浅色背景，不要人物和 Logo。

> 使用 $fengmian-skill，用我附的照片做封面，标题“先完成，再完美”，不要副标题。

> 使用 $fengmian-skill，主题“开始行动”，只要横版 1440×1080，文字要大。

普通对话加载方式下，把 `$fengmian-skill` 换成“附件里的封面制作说明”即可。若应用不能传文件夹，可分别附上 `SKILL.md` 和 `references/` 内两个文件，并说明原来的目录关系。若助手无法读取文件或没有生图工具，它会说明限制；仅有提示词还不是生成完成。其他助手的安装方式以该产品为准，尚未逐个平台验证兼容性。

## 你会拿到什么

默认两张独立图片：竖版 1080×1440 和横版 1440×1080。也可以只要求其中一张。标题够大、人物可选、Logo 默认不添加；风格可以随主题调整，不要求先确定账号定位。

收到结果先在手机上缩小查看。如果需要调整，直接说“标题再大一点”“去掉右上角图标”“保留人物，只换背景”等。指定文案会保留；无需自己写绘图提示词。

双画幅尺寸是本技能的默认交付约定，不代表所有平台入口的强制要求。成品应是两张可打开的独立图片，文字准确、实际像素符合要求；一张拼图、提示词或工具任务编号都不能代替交付。

## 常见问题

**没有照片可以用吗？** 可以，默认做无人物的大字封面。想用自己，只需一张清晰照片，脸无遮挡，头发和肩部完整，有手势时保留手指。不用重命名或填写素材清单。

**一定要讲 AI 吗？** 不需要。成长、生活、工具教程、观点等都可以，不固定账号定位。

**为什么只有提示词？** 当前助手可能没有生图工具。提示词是待生成方案，需要在具有生图能力的环境继续。

**文字太小或出错怎么办？** 直接指出问题，助手会针对性修正；默认最多自动修正两轮，仍有问题会说明未完成项。

**能保证效果或流量吗？** 不能。模型和素材会影响效果，这套流程侧重清楚表达与可读性。尚未完成跨平台和真实新用户的端到端验证。

## 仓库结构

```text
fengmian-skill/
├── README.md                  使用者的安装与操作说明
├── SKILL.md                   AI 助手的制作流程
├── agents/openai.yaml         Codex 显示信息与默认提示
└── references/
    ├── people.md              人物素材指引
    └── quality-check.md       成品验收要求
```

使用规则以 `SKILL.md` 为准，本页帮助新手开始使用。GitHub 仓库根目录直接放以上文件，不要再套一层同名文件夹。

## 反馈与发布状态

反馈时说明使用的助手、输入、期望结果和卡住的步骤；截图请移除不希望公开的信息，不提交密钥、登录状态或未经许可的肖像。

开源许可证尚未选定，公开发布前由维护者决定并添加 `LICENSE`。公开仓库不自动等于授予开源使用许可。当前没有内置演示图片，后续可添加经授权的成品示例，不使用原作者的私人照片作为公共示例。

## 分享范围

此文件夹不包含原作者的照片、账号资料、Logo 或历史封面。将整个文件夹转发给别人即可；不要把自己的照片和生成结果混入分享包。它是一份可修改的工作流程，不保证所有助手都能执行生图，也不保证播放量或完全相同的生成效果。
