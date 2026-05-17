# InsightFlow - 自动化用户反馈洞察与需求优先级排序 Agent

InsightFlow 是一个基于 LangGraph 和多 Agent 协作的智能分析系统，能够自动采集用户反馈（应用商店评论、客服工单、社群消息），通过三层长链推理进行情感与功能分析，聚类相似问题，并综合评估优先级，最终自动生成 Jira/TAPD 需求票。

## ✨ 核心特性

- **多源采集与清洗**：自动拉取多平台反馈，过滤灌水/无效内容
- **三层长链推理**：情绪判断 → 功能模块识别 → 细粒度槽位提取，逐层深入
- **语义聚类**：基于 BGE 向量 + DBSCAN 算法，自动聚合相似反馈
- **多 Agent 协作评分**：频率、业务影响、修复难度三个子 Agent 并行评估，加权计算紧急分（0-100）
- **自动生成工单**：将高优先级问题转为结构化 Jira 需求票，并指派负责人

## 🏗️ 系统架构
用户反馈 → 采集清洗 → 长链推理分析 → 语义聚类 → 多Agent协作评分 → 工单生成 → Jira

## 🚀 快速开始

### 1. 环境要求
- Python 3.9+
- OpenAI API Key（或其他兼容接口）

### 2. 安装依赖
```bash
pip install -r requirements.txt
3. 配置环境变量
复制 .env 文件并填入你的 API Key：
OPENAI_API_KEY=your_key_here
RUN_MODE=mock   # mock 模式仅模拟，不实际同步 Jira
4. 运行示例
python main.py
5. 其他运行方式
# 交互式输入反馈
python main.py --interactive

# 从 JSON 文件加载
python main.py --source data/sample_feedback.json

# 指定输出报告路径
python main.py --output my_report.json
 项目结构
feedback_agent/
├── agents/              # Agent 实现（采集、分析、优先级、工单）
├── graph/               # LangGraph 工作流定义
├── data/                # 示例数据与策略配置
├── config.py            # 全局配置
├── models.py            # 数据模型
├── main.py              # 入口程序
├── requirements.txt     # 依赖列表
└── .env                 # 环境变量（需自行配置）
输出示例
控制台输出：处理进度、Top 5 高优先级问题、生成的工单信息

JSON 报告：insights_report.json，包含结构化分析结果

Jira 工单（非 mock 模式）：自动创建需求票

🔧 自定义配置
调整 config.py 中的权重、聚类阈值、紧急分阈值

修改 data/feedback_policy.yaml 中的标签规则与路由策略

📝 依赖说明
主要依赖：langgraph, langchain-openai, sentence-transformers, scikit-learn, pydantic, python-dotenv。完整列表见 requirements.txt。
📄 License
MIT
