# xd-code-scan

> **你的项目不是没有架构，是每套架构都想当皇帝。**

**v1.0.2 · AI Ghost Lab · 开源 Skill**

`xd-code-scan` 是一个给软件项目开的**吐槽大会**：先认真读代码、追踪调用链、核对文档和测试，再把确凿的架构矛盾与演化债写成一段能讲出口、能剪成视频、也能让程序员笑着破防的中文 Roast。

**后台是证据驱动（evidence-driven）的项目诊断；台前是有包袱的脱口秀。**

它不是换个语气输出 SonarQube 报告。默认**不写重构建议、不列优先级清单、不把结尾变成咨询方案**。

## 先听个响

> [以下是风格示例，纯属虚构，并非对某个真实项目的诊断。]
>
> 当初说要迁新架构，这话真没毛病。旧的不能一刀切，咱们稳一点。
>
> 结果三年过去，新架构上线了，旧架构还在，两个架构中间又养了个 Adapter。卧槽，你这哪是渐进式迁移？你这是让两届政府同时执政，中间还成立了个协调办公室！
>
> 最绝的是，没人知道什么时候算迁完。临时方案都快熬出退休金了，系统里唯一稳定的东西，叫“过渡期”。

真实吐槽必须以实际仓库里的证据为基础；找不到证据，就不能编段子。

## 安装

使用支持 [Agent Skills](https://agentskills.io/) 的工具，可以通过 Skills CLI 安装：

```bash
npx skills add AI-Ghost-Lab/xd-code-scan --skill diagnose-project-entropy
```

也可以把 [`skills/diagnose-project-entropy`](skills/diagnose-project-entropy) 目录按你所用 Agent 的说明放入 Skills 目录。

## 使用

在目标代码仓库中，让你的 Coding Agent 执行：

```text
使用 $diagnose-project-entropy 对当前项目做一次只读诊断，
把证据确凿的架构问题、历史包袱和代码矛盾讲成一场中文吐槽大会。
要尖锐、荒诞、好笑、有递进和回扣；不要修复建议，不要审计表格。
```

如果 Agent 不能读取项目源码，Skill 会明确要求提供仓库或路径，**不会装作已经扫描过**。

## 它会去挖什么

| 诊断范围 | 典型“喜剧素材” |
| --- | --- |
| **系统与架构** | 说好的核心对象可以被旁路；状态、身份、错误语义各玩各的；过度统一反而制造混乱 |
| **演化债** | 一次性迁移代码成了永久居民；新旧架构长期并行；过时兼容和没有退出条件的临时方案 |
| **代码与模块** | 隐性耦合、牵一发而动全身的函数、名义上模块化却没法独立测试 |
| **反常流程** | 超时、重试、取消、重启、恢复、部分成功时暴露出来的设计矛盾 |
| **文档** | 文档里已经是未来架构，源码还活在上一个朝代 |

不是搜到 `legacy`、`TODO` 就开喷。每个上台的观点都必须经过调用路径、真实契约和合理例外的核对。**该保留的复杂性，不会被强行算成屎山。**

## 吐槽，不等于乱喷

- **只读**：不修改目标项目、不提交代码、不创建 Issue/PR。
- **证据先行**：区分已确认事实、可能性和暂时无法判断的情况。
- **默认只输出节目**：有趣、可理解、有技术含量；修复方案是另一个明确请求才会启动的模式。
- **尊重人和隐私**：吐槽设计与代码决策，不针对开发者个人；不要公开客户私有源码、凭据、敏感路径或未披露漏洞细节。
- **非安全审计**：不能替代专门的漏洞扫描、压测和运行时验证。

## 让你的项目上台

欢迎 [提交一个公开项目参与吐槽](https://github.com/AI-Ghost-Lab/xd-code-scan/issues/new?template=roast-request.yml)。你可以推荐自己的项目，也可以推荐值得研究的公开仓库。

只提交你有权分享的公开仓库；私有项目不要把源码或敏感信息粘到公开 Issue。是否公开制作内容，将另外征求项目相关方的同意。

本项目由 **AI Ghost Lab** 维护。欢迎反馈诊断视角、使用体验和吐槽效果。

## 版本与许可

- 当前版本：**1.0.2**（见 [CHANGELOG](CHANGELOG.md)）
- 许可：**MIT**，允许使用、修改与商业使用；保留原版权声明即可。
- 项目目录：[`skills/diagnose-project-entropy`](skills/diagnose-project-entropy)

English keywords: *AI coding, repository roast, software architecture review, technical debt, evolution debt, legacy migration, architecture drift, codebase diagnosis, evidence-backed software critique.*
