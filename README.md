# Financial News Intelligence Dashboard

财经新闻智能采集、分析、可视化与简报生成项目  
Course Project for Data Collection and Visualization

---

## 1. 项目一句话说明

本项目使用 Python 从公开财经新闻网站采集数据，对新闻进行清洗、主题分类、情绪识别、风险事件识别和可视化，并提供一个双语 Streamlit Dashboard、双语图表、双语 Word final report，以及一个用于生成财经新闻简报的 Agent 输入与输出体系。

如果一个人完全没有参与过本项目，可以把它理解为：

> 我们把大量财经快讯从网页上采集下来，整理成结构化数据，再用 Python 统计和可视化，让用户快速看到哪些财经主题最热、哪些主题突然升温、整体新闻情绪如何、高风险新闻集中在哪些事件类型中，最后再生成一份自然语言新闻简报。

---

## 2. 课程要求对应关系

课程 `Course Project.pdf` 的核心要求包括：

1. 使用课堂学习的数据采集和可视化技术解决一个重要商业或社会问题。
2. 使用 Python 从一个或多个网站采集数据。
3. 不允许使用八爪鱼等数据采集工具替代编程。
4. 使用 Python 进行数据可视化。
5. 报告中说明如何采集、存储、预处理、可视化数据。
6. 提交 Word final report、Python 项目代码、爬取的数据和相关文档。

本项目对应如下：

| 课程要求 | 本项目对应内容 | 状态 |
|---|---|---|
| 重要商业或社会问题 | 财经新闻信息过载、热点和风险难以及时判断 | 已满足 |
| Python 采集网页数据 | `src/news/crawl_news.py` | 已满足 |
| 不用采集工具 | 使用 `requests` 等 Python 代码采集公开接口 | 已满足 |
| Python 可视化 | `src/news/visualize_news.py`、`src/news/visualize_news_bilingual.py`、`src/app/streamlit_app.py` | 已满足 |
| 爬取数据 | `data/raw/news/raw_news.csv` 等 CSV 文件 | 已满足 |
| 说明全过程 | 双语 Word 报告和本 README | 已满足 |
| Word final report | `docs/financial_news_intelligence_final_report_bilingual.docx` | 已满足 |
| 额外工作量 | Dashboard、Agent、Coze 知识库、双语图表 | 加分项 |

---

## 3. 项目解决的问题

### 3.1 Business Problem

财经新闻每天更新很快，信息量大、主题分散、风险事件密集。普通读者或分析人员很难在短时间内回答这些问题：

- 今天财经新闻主要集中在哪些主题？
- 哪些主题相对历史水平突然升温？
- 新闻整体情绪偏正面、中性还是负面？
- 高风险新闻主要属于哪些事件类型？
- 能否把复杂图表转成一份自然语言日报？

### 3.2 本项目的解决方案

本项目构建了一条端到端流水线：

```text
公开财经新闻采集
→ 原始数据存储
→ 文本清洗和去重
→ 主题分类
→ 情绪和风险识别
→ 统计分析表
→ Python 图表和 Dashboard
→ Agent 输入 JSON
→ 财经新闻简报
→ Word final report
```

---

## 4. 当前项目主要成果

截至当前版本，项目已经完成：

- 原始新闻数据：`5,000` 条
- 清洗后新闻数据：`4,967` 条
- 分析样本日期：`2026-05-15` 到 `2026-05-24`
- 主题数量：`21` 个
- 已识别高风险新闻：`1,490` 条
- 已生成分析表：`7` 个 CSV
- 已生成原始图表：`8` 个
- 已生成双语图表：`8` 个
- 已生成 Streamlit 双语 Dashboard
- 已生成代码版 Agent 简报
- 已生成 Coze 知识库 Markdown
- 已生成双语 Word final report

---

## 5. 项目根目录

当前项目根目录为：

```text
B:\数据采集与可视化\大作业\financial-news-intelligence
```

后文所有相对路径都以该目录为起点。

---

## 6. 目录结构总览

```text
financial-news-intelligence/
├─ config.yaml
├─ requirements.txt
├─ README.md
├─ data/
│  ├─ raw/news/
│  ├─ interim/news/
│  ├─ processed/news/
│  └─ outputs/
│     ├─ tables/
│     ├─ figures/
│     └─ agent_inputs/
├─ docs/
├─ notebooks/
└─ src/
   ├─ app/
   ├─ news/
   ├─ reports/
   └─ common/
```

---

## 7. 配置文件

### 7.1 `config.yaml`

路径：

```text
config.yaml
```

作用：

- 统一管理项目名称、路径、数据文件名、图表文件名、Agent 输出文件名。
- 配置爬虫参数，例如请求间隔、最大页数、超时时间、重试次数。
- 配置主题关键词、情绪关键词、风险关键词等规则字典。
- 让各个脚本不需要硬编码文件路径，便于复现和维护。

重点配置包括：

```yaml
paths:
  raw_news: "data/raw/news/raw_news.csv"
  cleaned_news: "data/interim/news/cleaned_news.csv"
  topic_labeled_news: "data/processed/news/topic_labeled_news.csv"
  sentiment_risk_news: "data/processed/news/sentiment_risk_news.csv"
  output_tables: "data/outputs/tables"
  figures: "data/outputs/figures"
  agent_inputs: "data/outputs/agent_inputs"
  docs: "docs"
```

双语图表文件也已经同步登记在：

```yaml
output_files:
  figures_bilingual:
```

最终报告登记在：

```yaml
output_files:
  reports:
    final_report_bilingual: "financial_news_intelligence_final_report_bilingual.docx"
```

---

## 8. 依赖文件

### 8.1 `requirements.txt`

路径：

```text
requirements.txt
```

作用：

列出项目运行所需 Python 包，包括：

- 数据采集：`requests`, `beautifulsoup4`, `lxml`
- 数据处理：`pandas`, `numpy`, `pyyaml`
- 中文文本处理：`jieba`
- 机器学习或文本分析辅助：`scikit-learn`
- 可视化：`matplotlib`, `seaborn`, `plotly`, `pyecharts`, `wordcloud`, `networkx`
- Dashboard：`streamlit`
- 表格和文档：`openpyxl`, `python-docx`

安装命令示例：

```powershell
pip install -r requirements.txt
```

本机项目当前主要使用的 Python 环境是：

```text
F:\AnacondaEnvs\financial-news\python.exe
```

---

## 9. 数据文件说明

### 9.1 原始爬取数据

路径：

```text
data/raw/news/raw_news.csv
```

作用：

保存从东方财富 7x24 公开财经快讯采集到的原始新闻数据。

主要字段：

| 字段 | 含义 |
|---|---|
| `news_id` | 新闻 ID |
| `title` | 原始标题 |
| `publish_time_raw` | 原始发布时间 |
| `publish_time` | 初步标准化发布时间 |
| `source` | 新闻来源 |
| `url` | 新闻链接，部分记录可能为空 |
| `raw_text` | 原始正文或摘要 |
| `crawl_time` | 爬取时间 |

用途：

- 作为数据采集结果的原始证据。
- 用于后续清洗脚本输入。
- 可在报告中证明项目确实采集了互联网数据。

---

### 9.2 清洗后新闻数据

路径：

```text
data/interim/news/cleaned_news.csv
```

作用：

保存清洗、解析时间、去重后的中间新闻数据。

主要处理：

- 去除 HTML 标签。
- 处理 `【标题】正文` 这类格式。
- 清理来源前缀。
- 标准化空白字符和标点。
- 解析发布时间。
- 生成 `publish_date` 和 `publish_hour`。
- 根据新闻 ID、清洗标题等去重。
- 过滤过短文本。

主要字段：

| 字段 | 含义 |
|---|---|
| `news_id` | 新闻 ID |
| `title_clean` | 清洗后标题 |
| `text_clean` | 清洗后文本 |
| `publish_time` | 标准化发布时间 |
| `publish_date` | 发布日期 |
| `publish_hour` | 发布小时 |
| `source` | 来源 |
| `is_valid` | 是否有效 |
| `text_length` | 文本长度 |

用途：

- 做数据质量检查。
- 作为主题分类脚本输入。
- 在报告中说明数据预处理过程。

---

### 9.3 主题分类结果

路径：

```text
data/processed/news/topic_labeled_news.csv
```

作用：

保存每条新闻的主题分类结果。

主要方法：

- 基于 `config.yaml` 中的主题关键词字典。
- 对标题和文本进行关键词匹配。
- 给每条新闻分配 `primary_topic`。
- 如果命中多个主题，会记录 `secondary_topics`。

主要字段：

| 字段 | 含义 |
|---|---|
| `primary_topic` | 主主题 |
| `secondary_topics` | 次级主题 |
| `topic_keyword_hit` | 命中的主题关键词 |
| `is_multi_topic` | 是否多主题 |
| `topic_confidence` | 规则分类置信度或命中强度 |

用途：

- 统计主题热度。
- 生成主题热力图。
- 计算主题突发热度。
- 为 Agent 提供主题摘要。

---

### 9.4 情绪和风险识别结果

路径：

```text
data/processed/news/sentiment_risk_news.csv
```

作用：

保存主题分类之后进一步加入情绪标签和风险事件标签的完整分析表。

主要方法：

- 使用正面、负面关键词计算 `sentiment_score`。
- 根据分数生成 `sentiment_label`：
  - `positive`
  - `neutral`
  - `negative`
- 使用风险事件关键词识别 `risk_event_type`。
- 根据关键词强度和事件类型计算 `risk_score`。
- 判断是否属于 `is_high_risk`。

主要字段：

| 字段 | 含义 |
|---|---|
| `primary_topic` | 新闻主主题 |
| `sentiment_label` | 情绪标签 |
| `sentiment_score` | 情绪分 |
| `risk_event_type` | 风险或机会事件类型 |
| `risk_score` | 文本风险分 |
| `keyword_hit` | 情绪或风险关键词命中情况 |
| `is_high_risk` | 是否高风险新闻 |

注意：

`risk_score` 表示文本中的风险表达强度，不代表真实资产价格风险，也不构成投资建议。

用途：

- 生成情绪趋势。
- 生成风险事件分布。
- 筛选高风险新闻。
- 作为 Dashboard 的主要明细数据。

---

## 10. 输出分析表说明

输出表统一放在：

```text
data/outputs/tables
```

### 10.1 `daily_news_volume.csv`

路径：

```text
data/outputs/tables/daily_news_volume.csv
```

用途：

统计每天新闻数量，用于观察新闻总量变化。

字段：

| 字段 | 含义 |
|---|---|
| `publish_date` | 日期 |
| `news_count` | 当日新闻数 |

---

### 10.2 `hourly_news_volume.csv`

路径：

```text
data/outputs/tables/hourly_news_volume.csv
```

用途：

统计一天 24 小时内新闻发布分布，用于观察日内新闻流节奏。

字段：

| 字段 | 含义 |
|---|---|
| `publish_hour` | 小时 |
| `news_count` | 该小时新闻数 |

---

### 10.3 `topic_heatmap_matrix.csv`

路径：

```text
data/outputs/tables/topic_heatmap_matrix.csv
```

用途：

按日期和主题统计新闻数量，生成主题热力图。

结构：

- 行：日期
- 列：主题
- 值：新闻数量

---

### 10.4 `topic_burst_scores.csv`

路径：

```text
data/outputs/tables/topic_burst_scores.csv
```

用途：

计算主题突发热度，判断某个主题是否相对近期历史水平突然升温。

核心字段：

| 字段 | 含义 |
|---|---|
| `date` | 日期 |
| `topic` | 主题 |
| `today_count` | 当日该主题新闻数 |
| `rolling_avg_count` | 历史滚动均值 |
| `burst_score` | 突发热度分 |
| `baseline_status` | 基线状态 |
| `rank` | 当日排名 |

解释：

`burst_score` 越高，说明主题相对历史均值升温越明显。

---

### 10.5 `daily_sentiment_trend.csv`

路径：

```text
data/outputs/tables/daily_sentiment_trend.csv
```

用途：

统计每天正面、中性、负面新闻数量和占比。

核心字段：

| 字段 | 含义 |
|---|---|
| `positive_count` | 正面新闻数 |
| `neutral_count` | 中性新闻数 |
| `negative_count` | 负面新闻数 |
| `positive_share` | 正面占比 |
| `neutral_share` | 中性占比 |
| `negative_share` | 负面占比 |
| `avg_sentiment_score` | 平均情绪分 |

---

### 10.6 `topic_sentiment_matrix.csv`

路径：

```text
data/outputs/tables/topic_sentiment_matrix.csv
```

用途：

统计各主题下正面、中性、负面新闻结构，用于生成主题-情绪热力图。

---

### 10.7 `high_risk_events.csv`

路径：

```text
data/outputs/tables/high_risk_events.csv
```

用途：

保存高风险新闻列表，用于风险事件时间线、Dashboard 高风险新闻表和 Agent 简报。

---

## 11. 图表文件说明

图表统一放在：

```text
data/outputs/figures
```

### 11.1 图表索引

路径：

```text
data/outputs/figures/figure_file_index.md
```

作用：

说明哪些图表是原始版，哪些是双语版。

---

### 11.2 原始图表

原始图表主要由 `src/news/visualize_news.py` 生成。

| 文件 | 用途 |
|---|---|
| `fig_daily_news_volume.png` | 每日新闻量 |
| `fig_intraday_news_flow.png` | 日内新闻流量 |
| `fig_topic_heatmap.html` | 主题热力图，交互式 HTML |
| `fig_topic_burst_ranking.png` | 主题突发热度排名 |
| `fig_sentiment_trend.png` | 情绪趋势 |
| `fig_topic_sentiment_heatmap.html` | 主题-情绪热力图，交互式 HTML |
| `fig_risk_event_distribution.png` | 风险事件类型分布 |
| `fig_high_risk_timeline.html` | 高风险新闻时间线，交互式 HTML |

---

### 11.3 双语图表

双语图表主要用于英文班 presentation 和双语报告，由 `src/news/visualize_news_bilingual.py` 生成。

| 文件 | 用途 |
|---|---|
| `fig_daily_news_volume_bilingual.png` | 每日新闻量，中英双语标题和坐标轴 |
| `fig_intraday_news_flow_bilingual.png` | 日内新闻流量，中英双语 |
| `fig_topic_heatmap_bilingual.html` | 主题热力图，中英双语 |
| `fig_topic_burst_ranking_bilingual.png` | 主题突发热度排名，中英双语 |
| `fig_sentiment_trend_bilingual.png` | 情绪趋势，中英双语 |
| `fig_topic_sentiment_heatmap_bilingual.html` | 主题-情绪热力图，中英双语 |
| `fig_risk_event_distribution_bilingual.png` | 风险事件类型分布，中英双语 |
| `fig_high_risk_timeline_bilingual.html` | 高风险新闻时间线，中英双语 |

---

## 12. Agent 相关文件

Agent 输入和输出统一放在：

```text
data/outputs/agent_inputs
```

### 12.1 JSON 输入文件

这些 JSON 是给代码版 Agent 或 Coze Agent 使用的结构化输入。

| 文件 | 用途 |
|---|---|
| `daily_topic_summary.json` | 当日主题概览、Top 主题、代表新闻 |
| `topic_burst_summary.json` | 突发升温主题及 burst score |
| `sentiment_risk_summary.json` | 情绪结构和风险事件类型分布 |
| `high_risk_events.json` | 高风险新闻列表 |

设计原则：

- Agent 不重新计算数据。
- Agent 只读取 Python 流水线已经生成的结构化 JSON。
- Agent 只做总结、解释和表达。
- Agent 不提供投资建议，不预测市场涨跌。

---

### 12.2 代码版 Agent 输出

路径：

```text
data/outputs/agent_inputs/daily_financial_news_briefing.md
```

作用：

保存中文财经新闻智能简报。

生成脚本：

```text
src/news/generate_news_briefing.py
```

---

### 12.3 双语简报

路径：

```text
data/outputs/agent_inputs/daily_financial_news_briefing_bilingual.md
```

作用：

保存中英双语新闻简报，用于英文班 presentation 和 Dashboard 展示。

---

### 12.4 Coze 知识库文件

路径：

```text
data/outputs/agent_inputs/coze_knowledge_base_financial_news.md
```

作用：

由于 Coze 知识库不一定支持 JSON 文件直接上传，所以本项目把 4 个 JSON 文件整理成 Markdown 知识库文档，便于上传到 Coze。

内容包括：

- 使用边界和免责声明
- 新闻总体概览
- 热点主题
- 主题突发热度
- 情绪结构
- 风险事件分布
- 高风险新闻列表
- Agent 回答结构建议

---

## 13. 文档和报告文件

文档统一放在：

```text
docs
```

### 13.1 Agent 搭建指南

路径：

```text
docs/agent_build_guide.md
```

作用：

说明如何搭建代码版 Agent 和 Coze 版 Agent，包括：

- Agent 输入文件
- 代码版 Agent 运行命令
- Coze Bot 角色设定
- Coze 用户输入模板
- Agent 输出格式
- 不提供投资建议的约束

---

### 13.2 双语 Word final report

路径：

```text
docs/financial_news_intelligence_final_report_bilingual.docx
```

作用：

课程 final report，用英文为主、中文辅助的方式说明：

- 项目摘要
- 业务问题
- 数据来源和采集计划
- 数据采集实现
- 数据存储和预处理
- 分析与可视化方法
- 结果和发现
- AI Briefing Agent 扩展
- 课程要求匹配
- 限制、合规和复现
- 成员贡献占位表
- 结论

注意：

成员姓名和贡献比例需要小组最终提交前自行补充。

---

## 14. 源代码说明

源代码主要放在：

```text
src
```

---

### 14.1 数据采集脚本

路径：

```text
src/news/crawl_news.py
```

作用：

从东方财富 7x24 公开财经快讯采集新闻数据，输出到：

```text
data/raw/news/raw_news.csv
```

主要方法：

- 使用 `requests` 请求公开接口。
- 使用浏览器式请求头。
- 支持 JSON 和 JSONP 解析。
- 使用 `sortEnd` 方式获取更早新闻。
- 设置请求间隔 `request_delay_seconds`。
- 设置超时时间和最大重试次数。
- 不绕过登录、验证码或反爬限制。

运行命令：

```powershell
F:\AnacondaEnvs\financial-news\python.exe src\news\crawl_news.py
```

---

### 14.2 数据清洗脚本

路径：

```text
src/news/clean_news.py
```

作用：

清洗原始新闻数据，输出到：

```text
data/interim/news/cleaned_news.csv
```

主要方法：

- HTML 清理。
- 来源前缀清理。
- 标题和正文标准化。
- 发布时间解析。
- 日期和小时字段生成。
- 新闻去重。
- 文本长度过滤。

运行命令：

```powershell
F:\AnacondaEnvs\financial-news\python.exe src\news\clean_news.py
```

---

### 14.3 主题分类脚本

路径：

```text
src/news/classify_topics.py
```

作用：

基于主题关键词字典给每条新闻打主题标签，输出到：

```text
data/processed/news/topic_labeled_news.csv
```

方法：

- 读取 `config.yaml` 中的主题词典。
- 对新闻标题和文本进行关键词匹配。
- 计算主主题和次级主题。
- 记录命中的关键词。

运行命令：

```powershell
F:\AnacondaEnvs\financial-news\python.exe src\news\classify_topics.py
```

---

### 14.4 情绪和风险识别脚本

路径：

```text
src/news/classify_sentiment_risk.py
```

作用：

在主题分类结果基础上识别情绪和风险事件，输出到：

```text
data/processed/news/sentiment_risk_news.csv
```

方法：

- 使用情绪关键词计算 `sentiment_score`。
- 标注 `positive`、`neutral`、`negative`。
- 使用风险关键词识别风险事件类型。
- 计算 `risk_score`。
- 判断高风险新闻。

运行命令：

```powershell
F:\AnacondaEnvs\financial-news\python.exe src\news\classify_sentiment_risk.py
```

---

### 14.5 统计分析表生成脚本

路径：

```text
src/news/analyze_news.py
```

作用：

从完整新闻分析表生成聚合统计表，输出到：

```text
data/outputs/tables
```

输出包括：

- 每日新闻量
- 每小时新闻量
- 主题热力矩阵
- 主题突发热度
- 每日情绪趋势
- 主题情绪矩阵
- 高风险新闻列表

运行命令：

```powershell
F:\AnacondaEnvs\financial-news\python.exe src\news\analyze_news.py
```

---

### 14.6 原始图表生成脚本

路径：

```text
src/news/visualize_news.py
```

作用：

基于 `data/outputs/tables` 生成原始图表，输出到：

```text
data/outputs/figures
```

使用方法：

- `matplotlib`
- `seaborn`
- `plotly`

运行命令：

```powershell
F:\AnacondaEnvs\financial-news\python.exe src\news\visualize_news.py
```

---

### 14.7 双语图表生成脚本

路径：

```text
src/news/visualize_news_bilingual.py
```

作用：

生成文件名带 `_bilingual` 的双语图表，用于英文班 presentation 和双语报告。

输出位置：

```text
data/outputs/figures
```

运行命令：

```powershell
F:\AnacondaEnvs\financial-news\python.exe src\news\visualize_news_bilingual.py
```

---

### 14.8 Agent 输入生成脚本

路径：

```text
src/news/build_news_agent_inputs.py
```

作用：

把统计表和高风险新闻整理成 Agent 可读取的 JSON 文件。

输出位置：

```text
data/outputs/agent_inputs
```

输出文件：

- `daily_topic_summary.json`
- `topic_burst_summary.json`
- `sentiment_risk_summary.json`
- `high_risk_events.json`

运行命令：

```powershell
F:\AnacondaEnvs\financial-news\python.exe src\news\build_news_agent_inputs.py
```

---

### 14.9 代码版 Agent 简报生成脚本

路径：

```text
src/news/generate_news_briefing.py
```

作用：

读取 Agent JSON 输入，生成财经新闻简报 Markdown。

输出：

```text
data/outputs/agent_inputs/daily_financial_news_briefing.md
```

运行命令：

```powershell
F:\AnacondaEnvs\financial-news\python.exe src\news\generate_news_briefing.py
```

---

### 14.10 Streamlit Dashboard

路径：

```text
src/app/streamlit_app.py
```

作用：

提供一个双语网页 Dashboard，用于展示：

- 总览 Overview
- 主题热力图 Theme Heatmap
- 情绪监测 Sentiment Monitor
- 风险时间线 Risk Timeline
- AI 每日简报 AI Daily Briefing

启动命令：

```powershell
cd "B:\数据采集与可视化\大作业\financial-news-intelligence"
F:\AnacondaEnvs\financial-news\python.exe -m streamlit run src\app\streamlit_app.py --server.port 8501
```

打开地址：

```text
http://localhost:8501
```

如果端口被占用，可以换成：

```powershell
F:\AnacondaEnvs\financial-news\python.exe -m streamlit run src\app\streamlit_app.py --server.port 8502
```

然后打开：

```text
http://localhost:8502
```

---

### 14.11 Word 报告生成脚本

路径：

```text
src/reports/build_bilingual_final_report.py
```

作用：

生成双语 Word final report。

输出：

```text
docs/financial_news_intelligence_final_report_bilingual.docx
```

运行命令：

```powershell
C:\Users\Augus-Yang\.cache\codex-runtimes\codex-primary-runtime\dependencies\python\python.exe src\reports\build_bilingual_final_report.py
```

也可以在装有 `python-docx` 的项目环境中运行：

```powershell
F:\AnacondaEnvs\financial-news\python.exe src\reports\build_bilingual_final_report.py
```

---

## 15. 推荐完整运行顺序

如果要从头到尾重新生成项目结果，建议在项目根目录运行：

```powershell
cd "B:\数据采集与可视化\大作业\financial-news-intelligence"
```

然后按顺序执行：

```powershell
F:\AnacondaEnvs\financial-news\python.exe src\news\crawl_news.py
F:\AnacondaEnvs\financial-news\python.exe src\news\clean_news.py
F:\AnacondaEnvs\financial-news\python.exe src\news\classify_topics.py
F:\AnacondaEnvs\financial-news\python.exe src\news\classify_sentiment_risk.py
F:\AnacondaEnvs\financial-news\python.exe src\news\analyze_news.py
F:\AnacondaEnvs\financial-news\python.exe src\news\visualize_news.py
F:\AnacondaEnvs\financial-news\python.exe src\news\visualize_news_bilingual.py
F:\AnacondaEnvs\financial-news\python.exe src\news\build_news_agent_inputs.py
F:\AnacondaEnvs\financial-news\python.exe src\news\generate_news_briefing.py
```

然后启动 Dashboard：

```powershell
F:\AnacondaEnvs\financial-news\python.exe -m streamlit run src\app\streamlit_app.py --server.port 8501
```

如果需要重新生成 Word 报告：

```powershell
F:\AnacondaEnvs\financial-news\python.exe src\reports\build_bilingual_final_report.py
```

---

## 16. 方法说明

### 16.1 数据采集方法

本项目使用 Python 编写爬虫，从东方财富 7x24 公开财经快讯获取新闻。

方法特点：

- 直接使用 Python 代码采集，不使用八爪鱼等工具。
- 只访问公开页面或公开接口。
- 使用请求头模拟正常浏览器访问。
- 设置请求间隔，避免高频访问。
- 支持失败重试。
- 输出结构化 CSV。

### 16.2 数据清洗方法

主要清洗步骤：

1. 将空值、NaN、None 标准化为空字符串。
2. 去除 HTML 标签。
3. 处理中文新闻常见的 `【标题】正文` 格式。
4. 清理来源前缀。
5. 规范化空白字符。
6. 解析发布时间。
7. 生成日期和小时字段。
8. 去重。
9. 过滤文本过短新闻。

### 16.3 主题分类方法

主题分类使用规则词典法。

优点：

- 可解释性强。
- 适合课程项目展示。
- 方便说明为什么新闻被分到某个主题。
- 不依赖外部大模型或黑箱接口。

缺点：

- 可能漏判没有命中关键词但语义相关的新闻。
- 可能误判关键词出现在非核心语境中的新闻。

主题示例：

- AI
- Semiconductor
- New_Energy
- Real_Estate
- Consumption
- Healthcare
- Financial_Regulation
- Overseas_Macro
- Geopolitical_Risk
- Capital_Market

### 16.4 情绪识别方法

情绪识别使用关键词规则和分数法：

- 正面关键词增加分数。
- 负面关键词降低分数。
- 根据最终分数标注：
  - `positive`
  - `neutral`
  - `negative`

这种方法不等于真实市场预测，只是对新闻文本语气进行近似判断。

### 16.5 风险事件识别方法

风险事件识别使用风险关键词和事件类型词典。

常见风险或机会类型包括：

- `Geopolitical_Risk`
- `Public_Safety_Risk`
- `Regulatory_Risk`
- `Market_Risk`
- `Credit_Risk`
- `Operating_Risk`
- `Policy_Opportunity`
- `Financing_Opportunity`
- `Performance_Opportunity`

注意：

`risk_score` 只是文本风险强度，不是金融资产风险，不构成投资建议。

### 16.6 主题突发热度方法

突发热度使用当日新闻数与历史滚动均值比较。

核心思想：

```text
burst_score = today_count / rolling_avg_count
```

如果历史均值很低但当日新闻数明显增加，说明该主题可能在样本日突然升温。

### 16.7 可视化方法

本项目使用多种 Python 可视化工具：

- `matplotlib`：生成静态 PNG 图。
- `seaborn`：美化统计图。
- `plotly`：生成交互式 HTML 图。
- `streamlit`：搭建交互式 Dashboard。

主要可视化内容：

- 每日新闻量
- 日内新闻流量
- 主题热力图
- 主题突发热度排名
- 情绪趋势
- 主题-情绪热力图
- 风险事件类型分布
- 高风险新闻时间线

---

## 17. Dashboard 页面说明

Dashboard 地址：

```text
http://localhost:8501
```

页面包括：

### 17.1 Overview / 总览

展示：

- 总新闻数
- 筛选后新闻数
- 最新日期新闻数
- 主题数量
- 高风险新闻数量
- Top 热点主题
- 每日新闻量
- 日内新闻流量

### 17.2 Theme Heatmap / 主题热力图

展示：

- 日期-主题热力图
- 主题突发热度排名
- 代表新闻列表

### 17.3 Sentiment Monitor / 情绪监测

展示：

- 每日情绪趋势
- 主题-情绪热力图
- 正面、中性、负面比例
- 主题情绪统计表

### 17.4 Risk Timeline / 风险时间线

展示：

- 高风险新闻时间线
- 风险事件类型分布
- 高风险新闻列表
- 风险分筛选

### 17.5 AI Daily Briefing / AI 每日简报

展示：

- 简报日期
- 当日新闻数
- 高风险新闻数
- 平均情绪分
- Top 热点主题表
- 双语 Agent 简报
- Coze 输入 JSON 预览

---

## 18. Final Report 说明

最终 Word 报告：

```text
docs/financial_news_intelligence_final_report_bilingual.docx
```

报告是 English-first bilingual 格式。

也就是说：

- 英文内容用于满足英文班 final report 要求。
- 中文内容用于组内理解和展示准备。

报告中包括：

- Abstract
- Business Problem
- Data Source and Collection Plan
- Data Collection Implementation
- Data Storage and Preprocessing
- Analysis and Visualization Design
- Results and Findings
- AI Briefing Agent Extension
- Course Requirement Mapping
- Limitations, Ethics, and Reproducibility
- Member Contributions
- Conclusion

注意：

成员贡献表目前是占位表，需要最终提交前填写真实组员姓名和贡献比例。

---

## 19. Coze Agent 使用方式

如果要在 Coze 中制作 Agent，推荐使用：

```text
data/outputs/agent_inputs/coze_knowledge_base_financial_news.md
```

作为知识库文件上传。

原因：

- Coze 可能不支持 JSON 文件直接作为知识库。
- Markdown 更容易被知识库解析。
- 该文件已经把 4 个 JSON 的核心内容整理成自然语言和表格。

如果要手动给 Coze 输入结构化数据，也可以使用这 4 个 JSON：

```text
data/outputs/agent_inputs/daily_topic_summary.json
data/outputs/agent_inputs/topic_burst_summary.json
data/outputs/agent_inputs/sentiment_risk_summary.json
data/outputs/agent_inputs/high_risk_events.json
```

Agent 必须遵守：

- 只能基于提供的数据总结。
- 不能编造新闻标题、数量或事件。
- 不能提供投资建议。
- 不能预测市场涨跌。

---

## 20. 重要结果发现

基于当前处理后的完整数据：

- 原始新闻共 `5,000` 条。
- 清洗后新闻共 `4,967` 条。
- 样本日期为 `2026-05-15` 到 `2026-05-24`。
- 共识别 `21` 个主题。
- 完整数据中高风险新闻共 `1,490` 条。
- 新闻情绪以中性为主。
- 在最新日报日期 `2026-05-24`，地缘风险是最主要主题。
- 公共风险在最新日期出现较明显突发升温。
- 风险事件主要集中在融资机会、业绩机会、监管风险、政策机会、市场风险、地缘风险等类别。

---

## 21. 合规和限制

### 21.1 合规说明

本项目：

- 只采集公开财经新闻。
- 不绕过登录。
- 不绕过验证码。
- 不破解反爬限制。
- 设置请求间隔。
- 仅用于课程项目、信息监测和可视化展示。

### 21.2 方法限制

本项目也有一些限制：

- 主要使用东方财富一个新闻源，不能代表全市场所有财经新闻。
- 规则分类方法可解释，但可能漏判或误判。
- 情绪分和风险分来自文本规则，不代表真实市场方向。
- 高风险新闻是文本风险高，不等于投资风险高。
- Agent 简报是基于结构化输出生成，不应被当成投资建议。

---

## 22. 提交时建议包含的文件

建议最终提交包含：

```text
config.yaml
requirements.txt
README.md
src/
data/raw/news/raw_news.csv
data/interim/news/cleaned_news.csv
data/processed/news/topic_labeled_news.csv
data/processed/news/sentiment_risk_news.csv
data/outputs/tables/
data/outputs/figures/
data/outputs/agent_inputs/
docs/financial_news_intelligence_final_report_bilingual.docx
docs/agent_build_guide.md
```

如果 Canvas 对文件大小有限制，可以优先保留：

- `src/`
- `config.yaml`
- `requirements.txt`
- `README.md`
- `data/raw/news/raw_news.csv`
- `data/processed/news/sentiment_risk_news.csv`
- `data/outputs/tables/`
- `data/outputs/figures/`
- `docs/financial_news_intelligence_final_report_bilingual.docx`

---

## 23. 常见问题

### 23.1 打不开 Dashboard 怎么办？

如果浏览器显示 `ERR_CONNECTION_REFUSED`，说明 Streamlit 服务没有启动。

先运行：

```powershell
cd "B:\数据采集与可视化\大作业\financial-news-intelligence"
F:\AnacondaEnvs\financial-news\python.exe -m streamlit run src\app\streamlit_app.py --server.port 8501
```

然后打开：

```text
http://localhost:8501
```

### 23.2 端口 8501 被占用怎么办？

换一个端口：

```powershell
F:\AnacondaEnvs\financial-news\python.exe -m streamlit run src\app\streamlit_app.py --server.port 8502
```

然后打开：

```text
http://localhost:8502
```

### 23.3 Coze 不支持 JSON 知识库怎么办？

使用已经转换好的 Markdown：

```text
data/outputs/agent_inputs/coze_knowledge_base_financial_news.md
```

### 23.4 Word 报告在哪里？

路径：

```text
docs/financial_news_intelligence_final_report_bilingual.docx
```

### 23.5 双语图表在哪里？

路径：

```text
data/outputs/figures
```

文件名包含：

```text
_bilingual
```

---

## 24. 项目一句话总结

本项目完成了一个可复现的财经新闻数据采集与可视化系统：用 Python 采集公开财经新闻，用规则方法完成主题、情绪和风险识别，用 Python 生成统计表和可视化图表，用 Streamlit 做双语 Dashboard，并通过 Agent 把结构化结果转化为可读的财经新闻简报。
