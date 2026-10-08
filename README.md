# Enterprise Agent Platform

> 企业级 AI Agent 运行时平台，支持 Agent Runtime、Tool/MCP 集成、Evaluation、Observability、Security 与 Model Gateway。

## Features

- **Agent Runtime** — 状态管理、Checkpoint、Retry、Handoff 支持长时间运行的 Agent
- **Tool / MCP Integration** — 统一的工具注册层，支持 MCP 协议与权限策略
- **Memory** — 短期与长期记忆管理，支持 Vector DB 集成
- **Workflow** — Human-in-the-loop 审批流与 Durable Execution
- **Evaluation** — Trajectory 级别的 Agent 评估，支持回归测试
- **Observability** — Trace、Metrics、Logs 全链路可观测性
- **Security** — Agent Identity、RBAC、Tool Permission、Audit
- **Model Gateway** — 多模型路由、负载均衡、成本控制

## Architecture

```
                    Enterprise Agent Platform
                              │
        ┌─────────────────────┼─────────────────────┐
        │                     │                     │
   Agent Runtime         Tool / MCP            Workflow
        │                     │                     │
        ├── State             ├── Registry        ├── Human
        ├── Memory            ├── Permission      ├── Approval
        ├── Retry             ├── Security        └── Durable
        └── Checkpoint        └── Audit
        │
        ├───────────────────────────────────────────┐
        │                                           │
   Evaluation                              Observability
        │                                           │
        ├── Trajectory                         ├── Trace
        ├── Success                            ├── Metrics
        ├── Cost                               └── Logs
        └── Regression
                    │
                    ▼
             Model Gateway
                    │
       ┌────────────┼────────────┐
       ▼            ▼            ▼
    Model A       Model B      Model C
```

## Quick Start

### Installation

```bash
git clone https://github.com/你的用户名/agent-platform.git
cd agent-platform
pip install -e .
```

### Basic Usage

```python
from agent_platform import AgentRuntime

# 初始化运行时
runtime = AgentRuntime()

# 注册工具
@runtime.tool(name="search", description="Search the web")
def search(query: str):
    return f"Results for: {query}"

# 运行 Agent
result = runtime.run(
    goal="Search for the latest AI news",
    tools=["search"]
)
print(result)
```

## Project Structure

```
agent-platform/
├── runtime/           # Agent 执行运行时
│   ├── agent.py       # Agent 核心实现
│   ├── runner.py       # 任务运行器
│   ├── state.py       # 状态管理
│   ├── checkpoint.py  # 检查点与恢复
│   └── execution.py   # 执行引擎
├── tools/             # 工具层
│   ├── registry.py    # 工具注册表
│   ├── mcp.py         # MCP 协议支持
│   └── permission.py  # 权限策略
├── memory/            # 记忆层
│   ├── short_term.py  # 短期记忆
│   └── long_term.py   # 长期记忆
├── workflow/          # 工作流
│   ├── engine.py      # 工作流引擎
│   └── human_task.py  # 人工审批任务
├── evaluation/        # 评估层
│   ├── evaluator.py   # 评估器
│   └── trajectory.py  # 轨迹分析
├── observability/     # 可观测性
├── security/          # 安全与治理
├── gateway/           # 模型网关
└── examples/          # 示例代码
```

## Development

```bash
# 克隆项目
git clone https://github.com/你的用户名/agent-platform.git
cd agent-platform

# 安装开发依赖
pip install -e ".[dev]"

# 运行测试
pytest tests/

# 代码格式检查
black .
ruff check .
```

## License

MIT License
