# 生产级 AI Agent CLI 工具

一个完整的、可用于生产环境的 AI Agent 命令行工具框架。包含系统提示词、工具管理、执行循环、记忆管理等核心组件。

## 🎯 项目目标

本项目提供了一个**可直接用于生产环境**的 AI Agent CLI 工具参考实现，包括：

- ✅ 完整的架构设计文档
- ✅ 核心组件的源代码实现
- ✅ 优化的系统提示词
- ✅ 生产级的错误处理
- ✅ 详细的使用示例
- ✅ 性能优化建议

## 📁 项目结构

```
CLI-AI/
├── docs/                          # 详细文档
├── src/                           # 源代码
│   ├── agent/                     # Agent 核心
│   ├── tools/                     # 工具系统
│   ├── llm/                       # LLM 集成
│   ├── cli/                       # CLI 入口
│   └── utils/                     # 工具函数
├── examples/                      # 使用示例
├── tests/                         # 测试套件
├── config/                        # 配置文件
├── requirements.txt               # Python 依赖
└── setup.py                       # 安装脚本
```

## 🚀 快速开始

### 1. 安装依赖

```bash
git clone https://github.com/gimmy-z/CLI-AI.git
cd CLI-AI
pip install -r requirements.txt
```

### 2. 配置环境变量

```bash
cp .env.example .env
# 编辑 .env，填入你的 API 密钥
```

### 3. 运行示例

```bash
python examples/basic_usage.py
```

## 📚 文档导航

- **[01_architecture.md](docs/01_architecture.md)** - 完整的架构设计
- **[02_system_prompts.md](docs/02_system_prompts.md)** - 系统提示词详解
- **[03_tool_system.md](docs/03_tool_system.md)** - 工具系统设计
- **[04_memory_management.md](docs/04_memory_management.md)** - 记忆管理实现
- **[05_execution_loop.md](docs/05_execution_loop.md)** - 执行循环原理
- **[06_error_handling.md](docs/06_error_handling.md)** - 错误处理策略
- **[07_production_checklist.md](docs/07_production_checklist.md)** - 上线检查清单
- **[08_optimization.md](docs/08_optimization.md)** - 性能优化指南

## 🔧 核心特性

### 1. 灵活的工具系统
- 简单的工具注册机制
- 自动工具描述生成
- 支持同步和异步工具
- 工具参数自动验证

### 2. 智能的执行循环
- 逐步推理（Chain-of-Thought）
- 自动工具选择
- 结果反馈机制
- 无限循环检测

### 3. 强大的记忆管理
- 短期对话记忆
- 长期知识库
- 自动上下文压缩
- 执行历史追踪

### 4. 生产级的可靠性
- 详细的错误处理
- 日志和调试支持
- 性能监控
- 故障恢复机制

## 💡 使用示例

### 基础使用

```python
from src.agent import AIAgent
from src.tools import ToolRegistry
from src.llm import OpenAIClient

# 初始化
llm = OpenAIClient(api_key="your-key")
tools = ToolRegistry()
tools.register_builtin_tools()

agent = AIAgent(llm=llm, tools=tools)

# 运行
result = agent.run("帮我写一个 Python 脚本处理 CSV 文件")
print(result)
```

### 自定义工具

```python
from src.tools import Tool

class MyCustomTool(Tool):
    name = "my_tool"
    description = "My custom tool description"
    
    def execute(self, **kwargs):
        # 实现你的工具逻辑
        return "result"

tools.register(MyCustomTool())
```

## 🎓 学习路径

1. **入门**：从 [01_architecture.md](docs/01_architecture.md) 了解整体架构
2. **理解**：学习 [05_execution_loop.md](docs/05_execution_loop.md) 中的执行流程
3. **实践**：运行 `examples/` 目录下的示例代码
4. **扩展**：根据 [03_tool_system.md](docs/03_tool_system.md) 添加自己的工具
5. **优化**：参考 [08_optimization.md](docs/08_optimization.md) 优化性能
6. **上线**：检查 [07_production_checklist.md](docs/07_production_checklist.md)

## 🔑 关键概念

### Agent Loop（Agent 循环）

Agent 的核心是一个循环：

```
1. 读取用户输入和记忆
2. 调用 LLM 进行推理
3. LLM 决定调用哪个工具
4. 执行工具获得结果
5. 把结果反馈给 LLM
6. 判断是否完成，循环或结束
```

### System Prompt（系统提示词）

系统提示词定义了 AI 的行为：
- 角色和身份定义
- 可用工具列表
- 工作流程和约束
- 输出格式要求

### Tools（工具集）

工具是 Agent 与外界交互的方式：
- 文件操作（读、写、删除）
- 命令执行（Shell、Python）
- API 调用（HTTP、REST）
- 数据处理（查询、分析）

## 📊 性能指标

典型场景下的性能数据（仅供参考）：

- **平均响应时间**：2-5 秒（不含 LLM API 调用时间）
- **工具执行成功率**：>95%（取决于工具实现）
- **记忆管理开销**：<50ms（每次操作）
- **最大并发请求**：支持同时处理 10+ 独立会话

## 🛠️ 常见问题

### Q: 如何添加自定义工具？
A: 参考 [03_tool_system.md](docs/03_tool_system.md) 的"自定义工具"章节。

### Q: 如何优化 Agent 的性能？
A: 查看 [08_optimization.md](docs/08_optimization.md) 获取详细建议。

### Q: 支持哪些 LLM 服务？
A: 目前支持 OpenAI 和 Claude，可轻松扩展其他服务。

### Q: 如何在生产环境部署？
A: 按照 [07_production_checklist.md](docs/07_production_checklist.md) 逐项检查。

## 📝 许可证

MIT License

## 🤝 贡献

欢迎提交 Issue 和 Pull Request！

## 📧 联系方式

有问题？在 GitHub Issues 中提出。
