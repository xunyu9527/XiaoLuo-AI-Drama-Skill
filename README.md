# XiaoLuo AI Drama Skills (Normalized Layout)

小逻 AI 影视 / 短剧创作技能集，**已重构为标准 agent skill 布局**，可直接被
`skills-manager-cli` 及其他遵循 `<dir>/SKILL.md` 约定的 agent 安装与自动更新。

## 原始出处

本仓库是以下项目的 **fork 与结构规范化版本**：

- 原作者仓库：<https://github.com/zhurui0523/XiaoLuo-AI-Drama-Skill>
- 技能内容、作者署名与创作成果均归原作者所有
- 本次改造**未修改任何技能正文**，仅调整目录结构与打包方式

## 为什么要重构

原仓库把 19 个技能以**扁平 `.md` 文件**的形式直接放在仓库根目录：

```
repo/
├── README.md
├── 小逻-场景俯视布局.md
├── 小逻-角色三视图.md
└── …（共 19 个 .md 平铺）
```

这种结构无法被 agent 技能管理器识别，因为标准约定要求每个技能是
**独立目录 + 目录内一个 `SKILL.md`**：

```
repo/
├── README.md
└── skills/
    ├── xiaoluo-scene-top-view-layout/
    │   └── SKILL.md
    ├── xiaoluo-character-orthographic/
    │   └── SKILL.md
    └── …（共 19 个目录）
```

具体报错：

```json
{"ok": false, "code": "COMMAND_FAILED",
 "error": "Repository root is not a skill directory (no SKILL.md); pass --subpath"}
```

因此原仓库无法作为 git 源绑定，技能装上后**不能自动更新**。

## 本次改造内容

1. 每个技能移入 `skills/<name>/` 目录，正文文件重命名为 `SKILL.md`
2. **目录名取技能 frontmatter 里的 `name:` 字段**（而非中文文件名），
   保证纯 ASCII 路径，避免中文路径在 HTTP 拉取和跨平台场景下出问题
3. 技能正文内容**逐字节保持不变**

目录名与技能名对照（左侧目录名即 frontmatter 的 `name`）：

| 目录名 | 原文件名 |
|---|---|
| `xiaoluo-90s-script-to-video` | `xiaoluo-90s-script-to-video.md` |
| `xiaoluo-ai-drama-scene-layout` | `小逻-AI短剧场景布局设计.md` |
| `xiaoluo-vr-panorama` | `小逻-VR场景图.md` |
| `xiaoluo-script-to-video` | `小逻-剧本分镜脚本.md` |
| `design-script-assets` | `小逻-剧本资产-DNA-美术指导.md` |
| `xiaoluo-scene-top-view-layout` | `小逻-场景俯视布局.md` |
| `xiaoluo-scene-turnaround` | `小逻-场景四视图.md` |
| `xiaoluo-film-script-analysis` | `小逻-影视剧本分析.md` |
| `xiaoluo-original-screenplay-adaptation` | `小逻-影视剧本原创改编.md` |
| `xiaoluo-film-screenwriting` | `小逻-影视编剧创作.md` |
| `xiaoluo-storyboard-panel` | `小逻-故事面板.md` |
| `xiaoluo-visual-storyboard-grid` | `小逻-视觉分镜九宫格生成.md` |
| `xiaoluo-video-shot-analysis` | `小逻-视频拉片拆解.md` |
| `xiaoluo-character-orthographic` | `小逻-角色三视图.md` |
| `xiaoluo-character-pose` | `小逻-角色动作设定.md` |
| `xiaoluo-character-costume` | `小逻-角色服装设定.md` |
| `xiaoluo-character-expression` | `小逻-角色表情设定.md` |
| `xiaoluo-character-turnaround` | `小逻-角色设定图.md` |
| `xiaoluo-character-prop` | `小逻-角色道具设定.md` |

## 技能清单

**编剧 / 剧本**
- `xiaoluo-film-screenwriting` — 影视编剧创作
- `xiaoluo-film-script-analysis` — 影视剧本分析
- `xiaoluo-original-screenplay-adaptation` — 影视剧本原创改编

**角色资产**
- `xiaoluo-character-turnaround` — 角色设定图
- `xiaoluo-character-orthographic` — 角色三视图
- `xiaoluo-character-costume` — 角色服装设定
- `xiaoluo-character-expression` — 角色表情设定
- `xiaoluo-character-pose` — 角色动作设定
- `xiaoluo-character-prop` — 角色道具设定

**场景资产**
- `xiaoluo-scene-top-view-layout` — 场景俯视布局
- `xiaoluo-scene-turnaround` — 场景四视图
- `xiaoluo-ai-drama-scene-layout` — AI 短剧场景布局设计
- `xiaoluo-vr-panorama` — VR 场景图

**分镜 / 视频**
- `xiaoluo-script-to-video` — 剧本分镜脚本
- `xiaoluo-90s-script-to-video` — 90 秒剧本转视频
- `xiaoluo-storyboard-panel` — 故事面板
- `xiaoluo-visual-storyboard-grid` — 视觉分镜九宫格生成
- `xiaoluo-video-shot-analysis` — 视频拉片拆解
- `design-script-assets` — 剧本资产 DNA 美术指导

## 安装

```bash
# 单个技能（把 <name> 换成上表中的目录名）
skills-manager-cli skills install \
  https://github.com/xunyu9527/XiaoLuo-AI-Drama-Skill/tree/main/skills/<name>

# 需要 git 源自动更新时
skills-manager-cli skills set-source <name> \
  --git-url https://github.com/xunyu9527/XiaoLuo-AI-Drama-Skill \
  --subpath skills/<name>
```

## 许可证与致谢

技能内容版权归原作者 **zhurui0523** 所有。本 fork 仅做目录结构规范化，
以便技能管理器能够正确安装与更新。若原作者希望合并此改造，欢迎提交 PR 回上游。
