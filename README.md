# 《人月神话》读书笔记与软件开发原则

从《人月神话》二十周年纪念版出发，结合个体开发中的实际教训，整理一份完整读书笔记、一套程序员开发原则 skill，以及一份长期协作偏好的 memory 示例。

这套材料关注开发者怎样作决定：如何定义交付、控制功能膨胀、维护概念一致性、保存可恢复版本，以及让验证支撑实际承诺。原则首先面向程序员，尤其是个体开发者；使用 AI 编程时，也可以由 AI 协助提醒和检查。

## 从哪里开始

| 材料 | 内容与用途 |
| --- | --- |
| [完整读书笔记 Markdown](notes/人月神话_完整读书笔记.md) | 直接在 GitHub 阅读；覆盖全部19章、序言与结束语，约3万字 |
| [完整读书笔记 Word](notes/人月神话_完整读书笔记_20261107.docx) | 下载后批注、编辑和打印；本地排版检查为37页 |
| [离线 HTML 阅读版](notes/人月神话_完整读书笔记_20261107.html) | 下载后用浏览器打开，提供目录跳转；无需联网 |
| [开发原则 Skill](skills/software-development-principles/SKILL.md) | 15项原则及其危险迹象、行动建议、适用条件和章节依据 |
| [来源与取舍](skills/software-development-principles/references/source-and-reconciliation.md) | 解释原经验中的绝对表达如何依据本书得到修正 |
| [决策工作表与案例](skills/software-development-principles/references/decision-worksheets.md) | 项目启动、重要改动、验收、版本提醒和复盘的辅助材料 |
| [个人协作约定](skills/software-development-principles/references/personal-conventions.md) | Windows、Python、版本与授权习惯；使用前按自己的情况调整 |
| [Memory 示例](memory/software-development-principles.md) | 将核心原则与主动提醒方式保存为长期协作偏好 |

HTML 链接在 GitHub 中通常显示文件内容或下载入口；下载后用本地浏览器阅读。此仓库没有部署 GitHub Pages。

## 阅读笔记包含什么

- 全书的结构、论证主线与四个时间层次。
- 原版十五章与纪念版增补四章的逐章精读：论证、案例、概念、局限、实践转化及复盘问题。
- 跨章节概念辨析，以及作者保留、修正和限制的观点对照。
- 对证据、适用条件与历史经验的批判性评价。
- 项目开发、跨电脑分发、研究软件与 AI 辅助开发的实践框架。
- 重要术语、关键短引及解释、复习问答、进一步阅读线索与电子文本勘误。

笔记区分作者主张、作者后期修正和整理者的应用推论。引用以章号、小节和语境定位，不补造纸本页码。原文中的历史比例、生产率数据和组织方案均保留适用条件。

## 原则怎样避免走向另一个极端

“做到最好”需要明确用途、范围、质量和资源约束，允许通过原型与增量发现问题。它不要求第一次设计就预知一切，也不允许把未完成的产品化工作包装成已经交付。

几项关键取舍：

| 容易绝对化的要求 | 这里采用的做法 |
| --- | --- |
| 一次做对，不能返工 | 提前检验关键未知，保留反馈与必要修正的空间 |
| 全部 UI 确认后再编码 | 尽早验证交互，同时检验关键技术、性能和分发风险 |
| 失败必须修好再汇报 | 在授权内主动修复，及时说明持续影响、阻塞与风险变化 |
| 每次存档都必须分支、推送、打标签 | 按恢复、协作、备份与发布的不同目的选择动作 |
| 文档和测试越多越好 | 让记录与验证对应真实决策、变更风险和用户承诺 |
| 项目延期后绝对不能加人 | 检查工作可分性、学习、协调与整合成本 |

二十周年版第19章对信息隐藏、开发过程和“为舍弃而计划”的修正，是理解这些原则的重要依据。全书并不是一套脱离项目条件的强制流程。

## 使用 Skill

技能目录为 `skills/software-development-principles`。整个目录包含 `SKILL.md`、界面元数据和三个参考文件，应一起复制到宿主支持的技能目录。

以支持 `~/.agents/skills` 的 Codex 环境为例，在仓库根目录用 PowerShell 执行以下命令。目标已存在时命令停止，避免覆盖已有定制：

```powershell
$source = Join-Path (Get-Location) 'skills\software-development-principles'
$skillRoot = Join-Path $env:USERPROFILE '.agents\skills'
$destination = Join-Path $skillRoot 'software-development-principles'

if (-not (Test-Path -LiteralPath $source -PathType Container)) {
    throw '请先进入本仓库根目录。'
}
if (Test-Path -LiteralPath $destination) {
    throw '目标技能已存在，请先比较差异，再决定如何更新。'
}
New-Item -ItemType Directory -Path $skillRoot -Force | Out-Null
Copy-Item -LiteralPath $source -Destination $destination -Recurse
Write-Output "已复制到：$destination"
```

不同宿主和版本的技能目录可能不同；例如本项目最初使用的本地环境支持 `~/.codex/skills`。请以自己环境的说明为准，不要在多个发现目录重复安装同名技能。Codex 的技能发现和显式调用机制见 [官方文档](https://learn.chatgpt.com/docs/build-skills)。

明确调用示例：

```text
请用 $software-development-principles 检查我当前的软件开发计划。
结合实际材料，指出最重要的行为风险、适用条件、建议动作和验收方式。
```

其他适用场景包括：准备大规模重构、反复修复同类问题、功能持续膨胀、长期缺少版本检查点，以及准备向其他用户交付。

技能保留正常的自动匹配能力，但自动匹配不保证每次触发。它也不是后台监控软件，不会持续观察开发者在编辑器中的所有行为。

## AI 应怎样提供帮助

每次根据当前证据选择少数关键问题，通常聚焦一至三个，采用以下方式提醒：

> 观察到的事实 → 可能后果 → 建议动作 → 怎样判断已经改善。

例如，准备继续重构时，AI 应先核对现有修改与版本状态，解释为什么需要可恢复检查点，并说明“新建分支”不能保存未提交文件。对于一个局部路径错误，则应定位问题、作相称的修复和验证，无需启动全套项目评审。

相同问题在同一批次不重复说教。已经授权的常规工作继续完成；产品目标、重大取舍及未授权的高后果操作由开发者决定。个人约定中的确认要求不因启用技能而失效，也不应扩大为所有程序员的通用规范。

## 使用 Memory

[Memory 文件](memory/software-development-principles.md) 是可阅读、可修改的长期偏好示例。它保存核心原则和主动提醒方式，并指向完整 skill。**将这个文件放入 Git 仓库，不会自动安装到任何 AI 的记忆系统。**

建议先阅读并修改与你不相符的内容，再明确要求使用的助手将这些偏好写入其支持的长期记忆机制。例如：

```text
请阅读这份 memory，并把其中适合我的开发协作偏好保存为长期记忆。
重点是在相关开发任务中主动提醒工程风险，不需要每次等待我点名调用技能。
不要把个人偏好变成绝对规则，保持提醒与任务风险相称。
```

如果宿主不提供可确认的长期记忆，可以将精简后的原则写入自己使用的项目指令文件。实际加载范围、时机和持久性由宿主决定；仓库中的相对路径只用于查阅资料，复制到其他位置后需要调整。

## 文件结构

```text
README.md
notes/
  人月神话_完整读书笔记.md
  人月神话_完整读书笔记_20261107.docx
  人月神话_完整读书笔记_20261107.html
skills/software-development-principles/
  SKILL.md
  agents/openai.yaml
  references/
    source-and-reconciliation.md
    decision-worksheets.md
    personal-conventions.md
memory/
  software-development-principles.md
```

## 来源与公开版本

书籍为 Frederick P. Brooks, Jr. 的 *The Mythical Man-Month: Essays on Software Engineering* 二十周年纪念版。本仓库的笔记依据提供的中文电子文本整理，并结合个人开发经验，由 Codex 辅助阅读、组织和撰写。它不是作者或出版社的官方资料。

仓库提供阅读笔记、少量带定位的短引及实践分析，不提供原书 EPUB、完整提取文本或原书扫描图。技能中的工具操作约定与个体开发应用不应被当作 Brooks 的逐字主张。

公开副本将个人机器的绝对路径替换为仓库相对路径，并清除了 Word 的个人作者元数据；本地原件保持不变。Memory 与个人约定仅代表这份材料的使用场景，请按自己的工作方式审视后采用。

本仓库未附统一的开源许可证。原书及其引文的权利归相应权利人所有；如需明确的再分发或改编授权，请联系仓库维护者。

## 验证范围

读书笔记已核对章节覆盖、正文与表格完整性、目录链接，并完成37页的本地 Word 排版检查；其他设备的字体与分页可能不同。Skill 已检查格式、引用文件和界面元数据。原则的实际提醒效果仍需在真实项目中验证和修订，不是经过软件项目对照实验得出的效果保证。
