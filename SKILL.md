---
name: decision-council
version: 0.1.0
description: >
  决策会诊：重大/不可逆/多方案取舍前，组织 2-4 个不同立场视角（保守工程、极简、风险合规、性能）
  各自独立出题作答，再用对抗校验收敛成一个带理由的决定。
  触发词：会诊、council、多视角、方案比较、该不该、怎么选、决策、adversarial review。
  与内建 debate/chain 配合：本技能管流程与收敛，不替用户拍高危节点。
license: MIT
metadata:
  category: reasoning
  replaces: council-of-high-intelligence
---
# decision-council（决策会诊）

替代原 council-of-high-intelligence（该仓已删，本地备份见 SMS tmp/skill-backup-20261009）。
只保留 SMS 里真正需要的三件事：**多视角出方案 → 互相挑刺 → 收敛并落链**。

## 流程（≤4 轮，全程不超一次任务表）

1. **定题**：把决策改写成一句可判定真伪的论断（claim）。
2. **出视角**：按上式取 2-4 个立场（默认：保守工程 / 极简 / 风险合规 / 性能成本），
   每个立场独立给「建议 + 主要论据 + 我会在什么条件下改主意」，彼此不得先看对方答案。
   实操＝同一条回复里并列 `debate`（claim/pro/con）或多个 `ask` 子问答，禁止串行等待。
3. **对抗验收**：把各方案的两两冲突列成表（收益/代价/可逆性/失效场景）；
   任何方案拿不出「如何被证伪」就降级为备选。
4. **收敛**：输出唯一推荐 + 为什么 + 放弃了什么 + 回退办法；
   用 `chain append` 写入 logic 链（frm=候选,to=决定,why=判据），高危不可逆节点仍交用户拍板。

## 边界

- 不生成对外发布物、不代投票/代点赞、不改他人 session 的任务表。
- 简单二选一或纯知识问答不开会诊，直接 `debate` 自辩即可。
