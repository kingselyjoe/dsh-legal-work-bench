# dsh-legal-work-bench

> DSH 原生律师办公工作台 —— 办案用 work-bench，发内容用 legal-ip（[dsh-legal-ip](https://github.com/kingselyjoe/dsh-legal-ip)）

基于 DeepSeek Harness（DSH）的律师办公工作台：preset + 技能 + 工作流，覆盖合同审查、诉讼仲裁、劳动用工等领域，内置**双闸门验证**（事实核验 + 合规审查）与**审计链**。

> 设计参考：CSlawyer1985/claude-for-legal-ZH（Apache 2.0）的领域覆盖地图与画像机制（方法借鉴，内容全部重写）。详见《dsh-legal-work-bench-设计方案》。

## 定位

| 维度 | claude-for-legal-ZH | dsh-legal-work-bench |
|---|---|---|
| 本质 | 法律技能插件集 + 多端适配 | DSH 原生 preset + 工作流 + 验证 + 审计 |
| 人设 | 无专属 persona | **法律执业人设** |
| 验证 | 引用标"未验证" | **双闸门**（Fail-Closed） |
| 审计 | 无 | **审计链**（版本/来源/审批/时间戳） |
| 内容生产 | ❌ | ✅ 联动 dsh-legal-ip |

## 安装

```bash
cp -R preset ~/.dsh/.agent-presets/dsh-legal-work-bench
# 新建会话，预设选择器选「律师工作台（Legal Work Bench）」
```

## 目录结构

```
dsh-legal-work-bench/
├── preset/
│   ├── preset.yml           # 预设元数据
│   ├── agent.cordis.yml     # 法律执业人设 + 工具行 + skills 挂载
│   └── skills/
│       ├── 00-cold-start-interview/   # 画像机制（核心，先用它）
│       ├── 01-commercial-legal/       # 商事合同审查
│       ├── 02-litigation-legal/       # 诉讼仲裁
│       ├── 03-employment-legal/       # 劳动用工
│       ├── 04-legal-fact-check/       # 事实核验闸门（双闸门第一道）
│       └── 05-legal-compliance-review/ # 合规质量审查闸门（双闸门第二道）
├── LICENSE / README.md / .gitignore
```

## 阶段状态

- ✅ 阶段 0：preset 骨架 + 画像机制 + 3 核心域
- ✅ 阶段 1：**双闸门验证**（04 事实核验 + 05 合规质量审查，Fail-Closed）
- 🚧 阶段 2：13 领域全覆盖 + 5 托管工作流 + 审计链
- 🚧 阶段 3：案件管理（借鉴 dsh-law）+ 与 dsh-legal-ip 联动 + 付费层

## 使用流程

1. 新建会话选「律师工作台」预设
2. **先运行画像访谈**（`cold-start-interview`）：告诉我你的执业角色、场景、风险偏好，或提供 5-10 份已签合同，我从中反推你的真实条款立场
3. 之后直接丢工作：审查合同 / 分析案件 / 起草文书

## 核心铁律

- **先溯源，再下结论**：每条法律结论必须能回答"从哪来"
- **绝不编造**：法条/案号/判决/金额不知道就用【待核实：…】
- **保密优先**：客户材料本地处理，不泄露
- **对外动作必须人批**：发函、提交文件、签署默认禁止自动执行
- **审计留痕**：每次产出记录来源/版本/审批/时间戳

## License

MIT © dsh-legal-work-bench contributors
