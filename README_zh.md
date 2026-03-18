# MPE Multi-Agent Benchmark 🎮🤖

基于 PettingZoo MPE 环境的多智能体强化学习基准测试套件，集成 LLM API 驱动智能体决策。

[![Python](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/downloads/)
[![PettingZoo](https://img.shields.io/badge/PettingZoo-MPE-green.svg)](https://pettingzoo.farama.org/)
[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)


🌐 **可用语言**: [English](README_en.md) | [中文](README_zh.md) | [日本語](README_ja.md) | [Tiếng Việt](README_vi.md)

## 🌟 项目亮点

- 🎯 **9个经典环境**: 涵盖协作、对抗、通信等多种场景
- 🤖 **LLM集成**: 支持 OpenAI、DeepSeek、Qwen、Gemini
- 📊 **标准化解析**: 将原始观测转换为 LLM 友好的 JSON 格式
- 📝 **完善文档**: 从快速开始到深度开发的完整指南
- 🔧 **模块化设计**: 易于扩展和自定义

## 📁 项目结构

```
MPE_muiltiagent_benchmark/
├── 📄 配置文件
│   ├── requirements.txt          # Python 依赖
│   ├── pyproject.toml           # 项目配置
│   ├── .env.example             # API 密钥模板
│   └── .gitignore               # Git 忽略规则
│
├── 📚 文档 (docs/)
│   ├── README.md                # 📚 文档导航中心
│   ├── getting_started/         # 入门指南
│   │   ├── quickstart.md        # ⭐ 快速开始
│   │   └── overview.md          # 项目概览
│   ├── configuration/           # 配置指南
│   │   └── api_keys.md          # 🔑 API 密钥配置
│   ├── architecture/            # 架构设计
│   │   ├── observation_space.md # 观测解析
│   │   ├── logging_system.md    # 📊 日志系统
│   │   └── models.md            # 🤖 模型使用
│   ├── experiments/             # 实验指南
│   │   ├── reproducibility.md   # 🎲 种子固定
│   │   ├── running_benchmarks.md # Benchmark 运行
│   │   └── benchmark_review.md  # 📈 Benchmark 分析
│   └── dev_notes/               # 开发笔记
│       ├── work_summary.md      # 工作总结
│       ├── workflow_standardization.md # 工作流标准化
│       └── api_keys_refactor.md # API 密钥重构
│
├── 🎮 环境实现（9个完整游戏）
│   ├── spread_API.py            # Simple Spread
│   ├── adv_API.py               # Simple Adversary
│   ├── tag_API.py               # Simple Tag
│   ├── push.py                  # Simple Push
│   ├── crypto.py                # Simple Crypto
│   ├── reference.py             # Simple Reference
│   ├── speaker_listener.py      # Simple Speaker Listener
│   ├── world_comm.py            # Simple World Comm
│   ├── simple.py                # Simple (Basic)
│   └── utils_api.py             # 统一 LLM API 接口
│
├── 🧪 测试与工具
│   ├── benchmark_runner.py      # ✅ 批量测试框架
│   ├── setup_api_keys.py        # ✅ API 密钥配置脚本
│   └── test_unified_api.py      # API 测试
│
├── 🔍 观测解析 (obs/)
│   ├── parse_*_obs.py           # 9个环境的解析器
│   └── utils.py                 # 通用辅助函数
│
├── 💬 提示词工程 (prompt/)
│   └── prompt_for_*.py          # 标准化 Prompt 模块
│
└── 📊 结果输出 (results/)
    └── benchmarks/<env>/        # 各环境的测试结果
        ├── *.mp4                # 视频记录
        └── *.json               # 详细日志
```

## 🚀 快速开始

### 环境要求

- **Python**: 3.8+ (推荐 3.12.3，已测试)
- **操作系统**: Linux / macOS / Windows
- **依赖管理**: pip / conda / uv

### 1. 安装依赖

```bash
# 克隆仓库
git clone https://github.com/HuangShengZeBlueSky/MPE_muiltiagent_benchmark.git
cd MPE_muiltiagent_benchmark

# 方式 A: 使用 venv（推荐）
python -m venv .venv
source .venv/bin/activate  # Linux/Mac
# .venv\Scripts\activate   # Windows
pip install -r requirements.txt

# 方式 B: 使用 conda
conda create -n mpe-bench python=3.12
conda activate mpe-bench
pip install -r requirements.txt

# 方式 C: 直接安装（不推荐）
pip install -r requirements.txt
```

**验证安装**:
```bash
# 运行环境验证脚本
python verify_environment.py
# ✅ 所有检查通过即表示环境配置成功
```

**📖 详细说明**: 查看 [docs/getting_started/environment_setup.md](docs/getting_started/environment_setup.md)

### 2. 配置 API 密钥 🔑

#### 方式 A: 交互式配置（推荐）
```bash
python setup_api_keys.py
```

#### 方式 B: 手动配置
```bash
# 复制模板并编辑
cp .env.example .env
nano .env  # 填入你的 API 密钥
```

#### 方式 C: 环境变量
```bash
export QWEN_API_KEY="sk-your-key"
export DEEPSEEK_API_KEY="sk-your-key"
export OPENAI_API_KEY="sk-your-key"
```

**获取 API 密钥**:
- Qwen (推荐): https://dashscope.console.aliyun.com
- DeepSeek: https://platform.deepseek.com
- OpenAI: https://platform.openai.com/api-keys
- Gemini: https://aistudio.google.com/apikey

**📖 详细配置**: 查看 [docs/configuration/api_keys.md](docs/configuration/api_keys.md)

### 3. 运行测试

#### 单个环境测试
```bash
# 运行单个游戏（默认 Qwen API）
python adv_API.py
python spread_API.py
python tag_API.py
```

#### 批量 Benchmark 测试（推荐）
```bash
# 运行 10 个 episode 的 Adversary 测试（种子 1-10）
python benchmark_runner.py

# 自定义环境和轮数
python -c "from benchmark_runner import run_benchmark; run_benchmark(env_name='spread', provider='qwen', episodes=20, seed_start=1)"
```

**输出**: 自动保存视频 (`*.mp4`) 和日志 (`*.json`) 到 `results/benchmarks/<env>/`

**📖 详细指南**: [docs/getting_started/quickstart.md](docs/getting_started/quickstart.md)

## 🧭 仓库使用流程（Workflow）

- 环境准备：创建虚拟环境并安装依赖（见上）
- 选择模型提供方：通过 `utils_api.get_api_engine(provider)` 统一接口配置模型
    - 可用值：`deepseek`, `qwen`, `gpt`, `gemini`, `transformers`, `ollama`, `vllm`
    - 根据 provider 传入对应参数，例如 `api_key`、`model_name`、`model_path` 等
- 解析观测：使用 `obs/parse_*.py` 对各环境的 `obs` 进行结构化解析（包含自测）
- 构建 Prompt：主程序调用 `prompt/prompt_for_*.py` 的四个模块化函数拼装指令
- 运行环境：执行对应主脚本（如 `reference.py`、`speaker_listener.py`、`world_comm.py`）
- 产出结果：自动保存视频（mp4）与详细日志（json）到仓库根目录

### 运行常用环境（示例命令）

```bash
# 指定 provider 运行（可在脚本文件顶部修改 PROVIDER）
python reference.py
python speaker_listener.py
python world_comm.py

# 运行世界通信环境并解析真实 obs（需要设置 PYTHONPATH）
PYTHONPATH=. python obs/test_parse_world_comm_obs_real.py
```

### 模型配置示例

```python
from utils_api import get_api_engine
provider = "qwen"  # deepseek / gpt / gemini / transformers / ollama / vllm
llm = get_api_engine(provider, api_key="your-key", model_name="qwen3-max")
action, thought = llm.generate_action(system_prompt, user_prompt)
```

### 输出与日志

- 视频：`world_comm_modular_*.mp4` 等（每步一帧，便于回放）
- 日志：`*.json`（含观测、动作、奖励与 LLM 原始响应）

### 注意事项

- PettingZoo `mpe` 未来将迁移到 `mpe2`，当前代码兼容旧路径，后续可平滑升级
- 如使用 Google Gemini，请关注 `google.generativeai` 包的弃用提示，建议迁移到 `google.genai`

## 📖 网页版说明书

- 中文版：docs/index_zh.html（本地打开）
- English: docs/index_en.html（open in browser）

## 🎯 支持的环境

| 环境 | 类型 | 智能体 | 观测解析 | Prompt | 日志 | Seed | 说明 |
|------|------|--------|---------|--------|------|------|------|
| **Simple Spread** | 协作 | N | ✅ | ✅ | ✅ | ✅ | 覆盖所有地标 |
| **Simple Adversary** | 对抗 | N+1 | ✅ | ✅ | ✅ | ✅ | 欺骗与推理博弈 |
| **Simple Tag** | 追逃 | N+1 | ✅ | ✅ | ✅ | ✅ | 捕食者围捕猎物 |
| **Simple Push** | 物理 | 2 | ✅ | ✅ | ✅ | ✅ | 推动物体到目标 |
| **Simple Crypto** | 密码 | 3 | ✅ | ✅ | ✅ | ✅ | Alice/Bob/Eve 博弈 |
| **Simple Reference** | 引用 | 2 | ✅ | ✅ | ✅ | ✅ | 颜色引用协作 |
| **Simple Speaker Listener** | 通信 | 2 | ✅ | ✅ | ✅ | ✅ | 编码解码协作 |
| **Simple World Comm** | 复杂 | N | ✅ | ✅ | ✅ | ✅ | 多地标复杂场景 |
| **Simple (Basic)** | 基础 | 1 | ✅ | ✅ | ✅ | ✅ | 基础协作 |

✅ = 已完成并测试

## 💡 核心功能

### 1. 统一 Benchmark 测试框架 ⭐

批量测试多个环境，支持固定种子的可重现实验：

```python
from benchmark_runner import run_benchmark

# 运行 10 个 episode，使用种子 1-10
result = run_benchmark(
    env_name="adversary",    # 9个环境任选
    provider="qwen",          # qwen/deepseek/gpt/gemini/ollama/transformers
    episodes=10,              # 运行轮数
    seed_start=1,             # 起始种子（保证可重现）
    output_dir="results/benchmarks"
)

# 输出统计
print(f"Mean Reward: {result['mean_reward']:.4f}")
print(f"Std Dev: {result['std_reward']:.4f}")

# 自动生成:
# - results/benchmarks/adversary/adversary_ep1.mp4
# - results/benchmarks/adversary/adversary_ep1.json
# - ... (共 10 个 episode)
```

**特性**:
- ✅ 支持所有 9 个环境
- ✅ 固定种子（1-20），保证可重现性
- ✅ 自动计算平均奖励和标准差
- ✅ 完整日志（obs + action + thought + reward）
- ✅ 自动保存视频和 JSON

### 2. 观测解析器

将原始数值向量转换为语义化的 JSON 格式：

```python
from obs.parse_adv_obs import parse_adversary_obs

# 输入: numpy array [10 维]
obs_raw = np.array([-0.66, -1.32, ...])

# 输出: 结构化 JSON
obs_struct = parse_adversary_obs(obs_raw, 'agent_0', num_good=2)

# {
#   "role": "GOOD_AGENT",
#   "goal": {
#     "relative_position": [-0.66, -1.32],
#     "distance": 1.48,
#     "direction": "DOWN",
#     "description": "⭐ 真正的目标在你的DOWN方向，距离 1.48"
#   },
#   "tactical_hint": "SCORER - 你更接近目标，应该直接冲向目标！"
# }
```

### 3. LLM API 集成

统一的 API 调用接口，支持多种 LLM：

```python
from utils_api import get_api_engine

# 远程 API（自动读取环境变量中的密钥）
llm = get_api_engine("qwen")           # 阿里通义千问
llm = get_api_engine("deepseek")       # DeepSeek
llm = get_api_engine("gpt")            # OpenAI GPT
llm = get_api_engine("gemini")         # Google Gemini

# 本地模型（无需 API 密钥）
llm = get_api_engine("transformers", model_path="Qwen/Qwen2.5-7B-Instruct")
llm = get_api_engine("ollama", model_name="qwen2.5:7b")
llm = get_api_engine("vllm", model_path="meta-llama/Llama-3-8B")

# 调用
action, thought = llm.generate_action(system_prompt, user_prompt)
```

**支持的提供商**:
- ☁️ **远程 API**: OpenAI, DeepSeek, Qwen, Gemini
- 🖥️ **本地模型**: Transformers, Ollama, vLLM
- 🔐 **密钥管理**: 通过 `.env` 文件或环境变量

### 4. 标准化 Prompt 工程框架

每个环境都有模块化的 Prompt 组件（位于 `prompt/` 目录）：

```python
from prompt.prompt_for_adversary import (
    get_task_and_reward,
    get_action_and_response_format,
    get_physics_rules,
    get_navigation_hints
)

def build_full_prompt(agent, step, obs):
    return "\n\n".join([
        f"ENV: Adversary | AGENT: {agent} | STEP: {step}",
        get_task_and_reward(),
        get_physics_rules(),
        get_action_and_response_format(),
        get_navigation_hints(),
        format_obs(obs)  # 来自 obs/parse_adv_obs.py
    ])
```

**标准化结构**（每个环境都遵循）:
1. `get_task_and_reward()` - 任务目标和奖励机制
2. `get_action_and_response_format()` - 动作空间和输出格式
3. `get_physics_rules()` - 物理规则和环境设定
4. `get_navigation_hints()` - 导航提示和策略建议

详见: [docs/dev_notes/workflow_standardization.md](docs/dev_notes/workflow_standardization.md)

## 📊 输出产物

### 单次运行输出
运行单个环境（如 `python adv_API.py`）生成：
- **视频** (`adversary_demo.mp4`): 可视化回放
- **日志** (`adversary_demo.json`): 完整轨迹

### Benchmark 批量输出
运行 `benchmark_runner.py` 生成：
```
results/benchmarks/adversary/
├── adversary_ep1.mp4
├── adversary_ep1.json
├── adversary_ep2.mp4
├── adversary_ep2.json
...
└── adversary_ep10.json
```

### JSON 日志格式
每条记录包含：
```json
{
  "step": 0,
  "agent": "agent_0",
  "obs": {...},              // 结构化观测
  "action": [0.8, 0.2, ...], // 动作向量
  "thought": "LLM原始响应",   // 思考过程
  "reward": 0.15             // 奖励值
}
```

最后追加汇总：
```json
{
  "final_summary": true,
  "total_rewards": {"agent_0": 12.5, "agent_1": 8.3},
  "mean_reward": 10.4,
  "steps": 50
}
```

详见: [docs/architecture/logging_system.md](docs/architecture/logging_system.md)

## 🔬 研究应用

本项目可用于研究：

### 已支持的实验
- ✅ **可重现实验**: 固定种子 1-20，保证初始状态一致
- ✅ **模型对比**: 统一接口测试不同 LLM（Qwen/DeepSeek/GPT/Gemini）
- ✅ **Prompt 工程**: 模块化 Prompt 便于消融实验
- ✅ **性能评估**: 自动计算平均奖励和标准差
- ✅ **行为分析**: 完整日志记录每步决策过程

### 研究方向
- 🔬 LLM 作为多智能体策略的可行性
- 🔬 Prompt 工程对协作行为的影响
- 🔬 零样本 vs Few-shot 多智能体学习
- 🔬 自然语言通信协议的涌现
- 🔬 不同模型规模的性能-成本权衡

### 示例研究流程
```python
# 1. 使用相同种子测试不同模型
for provider in ["qwen", "deepseek", "gpt"]:
    result = run_benchmark(
        env_name="adversary",
        provider=provider,
        episodes=20,
        seed_start=1  # 相同的初始状态
    )
    print(f"{provider}: {result['mean_reward']:.3f}")

# 2. 参数搜索（温度、prompt 变体等）
# 3. 分析 JSON 日志中的决策模式
```

## 📚 文档导航

**完整文档索引**: [docs/README.md](docs/README.md) 📖

### 🚀 新手入门
- [快速开始](docs/getting_started/quickstart.md) - 5分钟快速上手
- [项目概览](docs/getting_started/overview.md) - 项目全景图

### ⚙️ 配置指南
- [API 密钥配置](docs/configuration/api_keys.md) - LLM API 密钥安全管理

### 🏗️ 架构设计

- [观测空间解析](docs/architecture/observation_space.md) - 观测解析开发流程
- [日志系统](docs/architecture/logging_system.md) - 完整日志格式规范
- [模型使用指南](docs/architecture/models.md) - 支持的 7 种 LLM

### 🧪 实验与测试
- [可重现实验](docs/experiments/reproducibility.md) - 种子固定指南
- [基准测试指南](docs/experiments/running_benchmarks.md) - 批量测试流程
- [基准测试评估](docs/experiments/benchmark_review.md) - 多角色日志分析

### 🛠️ 开发者笔记
- [工作总结](docs/dev_notes/work_summary.md) - v1.0 完整开发历程
- [工作流标准化](docs/dev_notes/workflow_standardization.md) - 模块化设计原则
- [API 密钥重构](docs/dev_notes/api_keys_refactor.md) - 安全迁移日志

## 🛠️ 开发状态

### 已完成 ✅ (Version 1.0)
- [x] **9个环境完整实现**（spread, adversary, tag, push, crypto, reference, speaker_listener, world_comm, simple）
- [x] **统一 LLM API 接口**（远程: qwen/deepseek/gpt/gemini, 本地: transformers/ollama/vllm）
- [x] **观测解析器**（9个环境的标准化 JSON 输出）
- [x] **Prompt 标准化**（4个模块化函数 × 9个环境）
- [x] **日志系统**（obs + action + thought + reward + final_summary）
- [x] **Benchmark 测试框架**（批量测试 + 统计分析）
- [x] **种子固定机制**（1-20 可重现实验）
- [x] **API 密钥管理**（.env 文件 + 交互式配置脚本）
- [x] **完善文档体系**（15+ 个 Markdown 文档）
- [x] **视频录制**（每个 episode 自动生成 mp4）

### 测试覆盖 ✅
- [x] 所有 9 个环境可独立运行
- [x] Benchmark 框架可测试所有环境
- [x] 种子固定验证通过
- [x] 日志格式统一且完整
- [x] API 密钥安全管理

### 计划中 📅 (Version 1.1+)
- [ ] 性能基准数据库（存储历史测试结果）
- [ ] 交互式可视化 Dashboard
- [ ] Few-shot 示例库
- [ ] 多进程并行测试
- [ ] 更多本地模型支持

## 🤝 贡献

欢迎贡献！步骤：

1. Fork 本仓库
2. 创建你的特性分支 (`git checkout -b feature/AmazingFeature`)
3. 提交更改 (`git commit -m 'Add some AmazingFeature'`)
4. 推送到分支 (`git push origin feature/AmazingFeature`)
5. 开启 Pull Request

**贡献方向**:
- 实现新环境的解析器
- 改进 Prompt 工程模板
- 添加新的评估指标
- 完善文档和示例

## 📄 许可证

本项目采用 MIT 许可证 - 详见 [LICENSE](LICENSE) 文件

## 🙏 致谢

- [PettingZoo](https://pettingzoo.farama.org/) - 多智能体环境库
- [OpenAI](https://openai.com/) - LLM API
- 所有贡献者


## ⭐ Star History

如果这个项目对你有帮助，请给一个 Star ⭐！

---

**最后更新**: 2026-01-26  
**版本**: 1.0.0 - 所有核心功能完成  
**状态**: ✅ 生产就绪
