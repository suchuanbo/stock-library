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
