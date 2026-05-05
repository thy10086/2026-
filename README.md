#  基于强化学习的Gazebo模糊测试工具

## 项目简介

GzFuzz是一个基于强化学习的Gazebo模糊测试工具，旨在自动化发现Gazebo仿真环境中的潜在漏洞和崩溃问题。

## 主要功能

- 🤖 **强化学习策略**：基于Actor-Critic算法的智能测试用例生成
- 🧠 **四种优化策略**：优先经验回放、自适应探索、课程学习、N步回报
- 🔍 **多版本支持**：支持测试不同版本的Gazebo
- 📊 **实验对比**：支持与AFL++、RL-based Fuzzer、Rozz等工具对比
- 🛡️ **安全测试**：针对Gazebo 11的安全测试模式

## 目录结构

```
gzfuzz/
├── modules/               # 核心模块
│   ├── __init__.py
│   ├── rl_policy_nn.py    # 神经网络强化学习策略
│   ├── sdf_generator.py   # SDF模型生成器
│   ├── gazebo_runner.py   # Gazebo运行器
│   └── crash_detector_real.py  # 崩溃检测器
├── experiments/           # 实验脚本
│   ├── comprehensive_experiments.py   # 综合实验
│   ├── tool_comparison_experiment.py  # 工具对比
│   ├── multi_version_gazebo_experiment.py  # 多版本测试
│   └── gz11_safe_fuzz_test.py   # Gazebo 11安全测试
├── docs/                  # 文档
│   └── gazebo_crash_exploit_cases.md  # 崩溃案例分析
├── optimized_gzfuzz.py    # 主程序
├── requirements.txt       # 依赖列表
└── README.md              # 项目说明
```

## 安装要求

```bash
# 安装依赖
pip install -r requirements.txt

# 安装Gazebo（Ubuntu）
sudo apt-get install gazebo11 libgazebo11-dev
```

## 快速开始

```bash
# 运行主程序
python optimized_gzfuzz.py

# 运行综合实验
python experiments/comprehensive_experiments.py

# 运行Gazebo 11安全测试
python experiments/gz11_safe_fuzz_test.py
```

## 核心算法

### Actor-Critic神经网络结构

- **Actor网络**：3层全连接（256 → 128 → action_size）
- **Critic网络**：3层全连接（256 → 128 → 1）
- **优化策略**：
  1. 优先经验回放（PER）
  2. 自适应探索率
  3. 课程学习
  4. N步回报计算

## 实验结果

该工具在不同版本的Gazebo上进行了测试，发现了多种类型的崩溃：

| 崩溃类型 | 描述 |
|---------|------|
| 段错误 | 内存访问违规 |
| 断言失败 | 程序断言检查失败 |
| 除零错误 | 除零操作 |
| 空指针 | 空指针解引用 |
| 缓冲区溢出 | 缓冲区越界 |

## 贡献

欢迎提交Issue和Pull Request！

## 许可证

MIT License
