hpc-learning
|我的 HPC / AI 学习仓库。记录我做过什么、卡在哪里、怎么解决的。

我想做什么
- 目标：先把一个模型亲手写出来，再谈优化——用纯 numpy 实现自动微分和一个多分类器，跑通训练、评估和错误分析。
- 为什么：把「我想学 AI」变成一件能验收的事，有输入、有输出、有基线、有对比。
- 下一步：在这个基础上做一次性能剖析（时间花在哪、数据怎么流动），再尝试把训练切分到多进程。

目前做了什么
experiments/tiny-digits —— 零依赖自动微分框架 + MNIST 子集分类器。
用 numpy 从零实现张量与反向传播，包含 softmax 分类器、SGD 优化器和错误样本分析。38 个行为测试全部通过，训练 9 秒达到测试准确率 99.4%。

我现在的环境
- 操作系统：Windows 11（Build 26300）
- Linux 环境：WSL2 + Ubuntu 24.04（VERSION 2）
- 终端：Windows Terminal → Ubuntu
- Python：3.12.3
- Node.js：v22.22.0（npm 源：npmmirror）
- Git：2.43.0（WSL 内）
- Agent Harness：DeepSeek Harness（Web UI，npx @deepseek-ai/dsh web）
- 学习 Skill：ProMentor

怎么运行
git clone https://github.com/Lyricslll/hpc-learning.git
cd hpc-learning/experiments/tiny-digits

python3 -m unittest discover -s tests -v   # 跑行为测试（38 个）
python3 train.py                            # 训练
python3 evaluate.py                         # 评估
python3 analyze.py                          # 错误样本分析
无第三方依赖，只需要系统自带的 Python 3。

目录约定
hpc-learning/
├── README.md
├── notes/             # 学习笔记、论文摘录
├── experiments/       # 每个实验一个目录：代码 + 结果 + 结论
│   └── tiny-digits/
└── .gitignore

学习日志
2026-10-19　建仓库、装 Git
想给 WSL 里的项目配好版本控制，先在 Windows 侧装 Git。
卡住：PowerShell 报「无法将 git 项识别为 cmdlet」。
解决：winget 的安装源指向 GitHub，被墙；改用华为云镜像下载便携版，手动加进 PATH。
2026-10-20　搭 WSL2 + Ubuntu
第一次 wsl --install 报 HCS_E_HYPERV_NOT_INSTALLED。
解决：BIOS 虚拟化其实是开的，问题在 boot 配置里 HYPERVISORLAUNCHTYPE=OFF，改回 auto 后重启。
2026-10-20　注册 Ubuntu 发行版
wsl --install 拉不到发行版清单（GitHub 上的 DistributionInfo.json 不通）。
解决：从清华镜像下载 rootfs，用 wsl --import 手动导入，版本指定为 2。
2026-10-20　装 DeepSeek Harness
npm 官方源不通，npx 下载失败。
解决：Node 二进制和 npm 源都换成 npmmirror。
2026-10-20　跑第一个实验
用 ProMentor 生成项目骨架，然后逐章自己实现核心逻辑。

注意
- 不提交 API Key、密码、.env，已在 .gitignore 中排除。
- 提交信息用动词开头：docs: ...、feat: ...、fix: ...。
