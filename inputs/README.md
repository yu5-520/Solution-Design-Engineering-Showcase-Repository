# Inputs Module

## 模块定位
`inputs/` 用于承接方案设计前的原始输入整理。

目标不是直接生成方案，
而是先把输入信息做成可判断、可检查、可补全的结构。

## 核心任务
本模块主要完成四件事：

1. 提取需求重点
2. 识别缺失字段
3. 标记信息冲突
4. 生成补充提问清单

## 适用输入来源
原始输入可来自：

- 用户聊天记录
- 会议纪要
- 邮件需求
- 项目简报
- 表单信息
- 历史文档
- AI 整理后的草稿

输入允许混乱，
但进入框架层之前，必须先被整理。

## 进入下一层前必须回答的问题
在进入 Framework 之前，至少要回答：

- 用户到底想解决什么问题
- 当前输入里已经明确了什么
- 还缺哪些关键字段
- 哪些信息之间存在冲突或不一致

## 本模块输出
每次输入整理后，统一输出四部分：

- A. 需求重点
- B. 缺失字段
- C. 信息冲突
- D. 补充提问清单

---

### E. 条件输入数据
把“补充信息”从自然语言说明，升级为可继续流转的数据。

每条条件统一记录为：

- **condition_id**：
- **stage**：input
- **condition_type**：constraint / assumption / conflict / decision / exception
- **content**：
- **source**：用户 / 文档 / 会议 / 人工补充 / AI整理
- **owner**：谁提供、谁确认
- **priority**：high / medium / low
- **required**：yes / no
- **status**：pending / confirmed / rejected / overridden
- **impact_module**：check / framework / output / review / case
- **next_action**：
- **timestamp**：

说明：
- `constraint`：约束条件，如预算、时限、组织限制
- `assumption`：当前先按某个假设继续推进
- `conflict`：存在冲突但尚未确认真值
- `decision`：人工已经确认的判断口径
- `exception`：允许偏离默认流程的例外条件

---

### F. 已确认条件
列出已经被确认、可直接进入后续模块的条件。

示例格式：

- **condition_id**：COND-001
- **condition_type**：constraint
- **content**：本次方案只覆盖试点，不做全量上线设计
- **owner**：需求方
- **status**：confirmed
- **impact_module**：framework / output

---

### G. 待确认条件
列出尚未确认、但会影响后续判断的条件。

示例格式：

- **condition_id**：COND-002
- **condition_type**：conflict
- **content**：上线时间存在两个版本：5月15日 / 6月1日
- **source**：会议纪要 / 聊天记录
- **status**：pending
- **impact_module**：check / framework
- **next_action**：转人工确认

## 文件说明
- `template.md`：标准输入整理模板
- `examples/`：真实输入整理样例