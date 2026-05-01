# Stock Library Schema

本文件定义 `/home/xiaobo/work/hermes-workspace/stock-books/my-books` 股票资料库的维护规则。

本资料库按照 LLM-Wiki 思想运行：原始资料保留在 `raw/` 或 `inbox/`，由 LLM 把资料整理成可长期维护、可交叉引用、可复用的 Markdown Wiki。

## 1. 资料库目标

本资料库用于沉淀个人股票学习、行情数据源、指数、ETF、公司、交易规则、策略和研究资料。

核心目标：

1. 把零散资料整理成结构化 Markdown 页面；
2. 让知识可以长期积累，而不是停留在一次性聊天回答中；
3. 为后续 RAG、Hermes Agent、个人研究和交易辅助系统提供高质量原始知识库；
4. 保留来源、更新时间、待验证问题；
5. 避免无依据的买卖建议。

## 2. 目录约定

```text
/home/xiaobo/work/hermes-workspace/stock-books/my-books/
├── inbox/       # 待处理资料，用户新放入的文件
├── raw/         # 原始资料归档，默认只读
├── assets/      # 图片、截图、PDF 导出图、附件
├── schema/      # 规则文件
└── wiki/        # LLM 维护的 Markdown Wiki
    ├── index.md
    ├── log.md
    ├── companies/
    ├── concepts/
    ├── indices/
    ├── etfs/
    ├── markets/
    ├── data-sources/
    ├── strategies/
    └── reports/
```

## 3. 目录规则

- `inbox/`：待处理资料，默认只读，不自动删除。
- `raw/`：原始资料归档，默认只读，不覆盖、不改写。
- `wiki/`：正式知识页，可以创建、更新、重构。
- `schema/`：规则文件，未经用户要求不要随意修改。
- `handoff/from-stock-assistant/`：交易分析助手保存的待整理草稿，不等于正式 wiki。

## 4. 页面分类

### 公司页面

路径：`wiki/companies/<company-or-ticker>.md`

用于记录公司业务、财报、行业地位、风险和重要事件。

### 概念页面

路径：`wiki/concepts/<concept>.md`

用于记录 ETF、K 线、均线、市盈率、成交量、换手率、复权等概念。

### 指数页面

路径：`wiki/indices/<index>.md`

用于记录恒生指数、恒生科技指数、沪深 300、标普 500 等指数。

### ETF 页面

路径：`wiki/etfs/<etf-or-ticker>.md`

用于记录 ETF 的跟踪标的、费用、流动性、风险和相关指数。

### 市场规则页面

路径：`wiki/markets/<market-or-rule>.md`

用于记录 A 股、港股、美股交易规则、交易时间、T+0/T+1、涨跌停、行情延迟等。

### 数据源页面

路径：`wiki/data-sources/<source>.md`

用于记录 Tushare、Futu OpenAPI、AKShare、pytdx、Longbridge 等数据源。

### 策略页面

路径：`wiki/strategies/<strategy>.md`

用于记录 MA 交叉、盘中提醒、ETF 定投、趋势跟踪、均值回归等策略资料。

### 报告页面

路径：`wiki/reports/<report>.md`

用于记录专题研究、比较分析、阶段总结和复盘报告。

## 5. 页面模板

正式 wiki 页面尽量包含：

```markdown
---
type:
title:
tags:
sources:
updated:
---

# 标题

## 一句话摘要

## 核心内容

## 关键要点

## 相关页面

## 来源

## 待验证问题
```

## 6. index.md 规则

`wiki/index.md` 是资料库导航，不写成长文。

每个重要页面都应被收录，格式建议：

```markdown
- [[path/to/page]] — 一句话说明；updated: YYYY-MM-DD
```

分类建议：

- Companies
- Concepts
- Indices
- ETFs
- Markets
- Data Sources
- Strategies
- Reports

## 7. log.md 规则

`wiki/log.md` 是追加式处理日志。

每次正式入库或更新 wiki 后追加：

```markdown
## YYYY-MM-DD - ingest: 主题

- Source:
- Created:
- Updated:
- Key takeaways:
- Conflicts:
- Open questions:
- Next actions:
```

## 8. Ingest 工作流

当用户要求“处理资料、整理 inbox、加入知识库、沉淀为 wiki、处理 handoff”时：

1. 执行或提醒检查 `git status`。
2. 读取 `schema/llm-wiki.md` 和 `schema/STOCK_LIBRARY.md`。
3. 读取指定资料。
4. 判断资料类型。
5. 提取实体、概念、指标、日期、来源、关键结论。
6. 检查 `wiki/index.md` 是否已有相关页面。
7. 创建或更新相关 wiki 页面。
8. 更新 `wiki/index.md`。
9. 追加 `wiki/log.md`。
10. 汇报处理结果和 Git 变更摘要。

## 9. 回答问题工作流

当用户只是提问时：

1. 优先读取 `wiki/index.md`。
2. 查找相关 wiki 页面。
3. 基于已有 wiki 内容回答。
4. 如果资料库中没有相关内容，应明确说明。
5. 如果回答有长期价值，建议沉淀为新的 wiki 页面。

## 10. 冲突处理

如果新资料和旧页面冲突：

1. 不直接覆盖旧内容。
2. 标明两个来源。
3. 说明哪个来源更新或更权威。
4. 无法判断时标记为“待验证”。

## 11. 命名规则

文件名统一使用小写英文和连字符：

```text
hang-seng-index.md
futu-openapi.md
ma-cross-intraday-monitor.md
hong-kong-stock-market.md
```

中文标题写在 Markdown 的 `# 标题` 中。

## 12. Git 工作流

资料库远程仓库：

`git@github.com:suchuanbo/stock-library.git`

每次正式修改前：

```bash
cd /home/xiaobo/work/hermes-workspace/stock-books/my-books
git status
git pull --ff-only
```

每次正式修改后：

```bash
git status
git diff --stat
```

然后向用户汇报：

- 新增文件
- 修改文件
- 删除文件
- 是否更新 `wiki/index.md`
- 是否更新 `wiki/log.md`
- 建议 commit message

只有用户明确确认后，才执行：

```bash
git add .
git commit -m "ingest: <topic>"
git push
```

禁止默认执行：

```bash
git push --force
```

## 13. 禁止事项

1. 不删除原始资料。
2. 不覆盖 `raw/` 文件。
3. 不伪造来源。
4. 不把推断写成事实。
5. 不给出直接买卖指令。
6. 不未经确认大规模重构目录。
7. 不未经确认自动 commit 或 push。

## 14. 标准汇报格式

```markdown
## 处理完成

### 读取资料
- ...

### 创建页面
- ...

### 更新页面
- ...

### 发现的问题
- ...

### Git 状态
- ...

### 建议 commit message
- ...

### 下一步建议
- ...
```
