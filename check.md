<p align="center">
  <h2>Dexora：面向高自由度双臂双手灵巧操作的开源 VLA 系统</h2>
</p>

<p align="center">
  <a href="#"><img src="https://img.shields.io/badge/arXiv-2026.xxxxx-B31B1B.svg" alt="arXiv"></a>
  <a href="#"><img src="https://img.shields.io/badge/Project-Page-blue.svg" alt="Project Page"></a>
  <a href="LICENSE"><img src="https://img.shields.io/badge/License-MIT-green.svg" alt="License"></a>
</p>

<p align="center">
  <img src="assets/teaser.gif" alt="Dexora Teaser" width="80%">
</p>

---

## 摘要（Abstract）

**Dexora** 是一个面向 **36 自由度双臂双手灵巧操作** 的开源 **视觉-语言-动作（Vision-Language-Action, VLA）系统**。相比以往以机械夹爪为主的抓取数据集与策略，Dexora 直接面向在仿真与真实世界中的 **高自由度双臂协同灵巧操作**，支持诸如手内重定向、工具使用、多步装配等复杂任务。我们的系统结合了大规模仿真数据（**10 万条轨迹、650 万帧图像**）与精心采集的真实数据（**1 万条轨迹、320 万帧图像**），真实数据通过 **外骨骼 + Vision Pro** 组成的混合远程操作系统采集完成。为使高自由度操作研究更具 **可复现性与可扩展性**，Dexora 采用 **LIBERO-2.0 数据标准**，并公开了带有购买链接的 **详细物品清单**，便于其他实验室以较低成本复现我们的实验环境。

---

## 🔥 新闻与更新（News & Updates）

- **2025-11-03**：发布完整的 **真实世界物品清单**（**347 个物体，17 个类别**），附带购买链接，便于可复现实验。
- **2025-12-01**：在 Hugging Face 上正式发布完整的 **真实世界数据集**（**10K 条轨迹**）与 **仿真数据集**（**100K 条轨迹**）。

---

## 📊 数据集总览（Dataset Overview）

Dexora 语料库由两部分组成：一是 **高保真真实世界远程操作数据**，二是与真实机器人形态一致的 **大规模仿真数据集**。

### A. Dexora 真实世界数据集（高保真）

Dexora 真实世界数据集包含 **10K 条远程操作轨迹**、**3.2M 帧图像** 和 **177.5 小时** 的示教数据。演示通过一个 **混合远程操作系统** 采集：使用 **外骨骼** 控制机械臂、使用 **Vision Pro** 控制灵巧手，从而在真实硬件上实现精确的 36 自由度双臂双手操作。

<p align="center">
  <img src="assets/image/real-data.JPG" alt="Dexora Real-World Dataset Mosaic" width="90%">
</p>

<p align="center">
  <i>图 1. <b>高保真真实场景。</b> 数据通过混合远程操作系统采集（外骨骼控制手臂 + Vision Pro 控制灵巧手），覆盖 <b>347 个物体</b>，分布在多种环境中。数据呈现丰富的光照变化、背景杂乱度与精确的双手协同交互，这些细节对于训练鲁棒的策略至关重要。</i>
</p>

<p align="center">
  <img src="assets/image/Categorized%20Robot%20Task%20Trajectory%20Distribution.png" alt="Dexora Task Taxonomy" width="48%">
  <img src="assets/image/Robot%20Arm%20Task%20Trajectory%20Distribution.png" alt="Dexora Robot Arm Trajectory Distribution" width="48%">
</p>

<p align="center">
  <i>图 2. <b>任务分类与动作分布。</b> 与标准夹爪数据集不同，Dexora 强调高自由度灵巧操作。真实世界数据中包含 <b>Dexterous Manipulation（20%）</b>，例如 <i>Twist Cap</i>（拧瓶盖）、<i>Use Pen</i>（使用笔）、<i>Cut Leek</i>（切葱），以及 <b>Assembly（15%）</b>，例如 <i>Separate Nested Bowls</i>（分离嵌套碗）、<i>Stack Ring Blocks</i>（叠环形积木），此外还包括 Articulated Objects（10%） 和 Pick-and-Place（55%）。</i>
</p>

所有轨迹与标注均遵循 **LIBERO-2.0 标准**，包括同步的 **RGB(-D) 观测**、**机器人本体状态（proprioception）**、**控制动作** 与 **语言指令**。

### B. Dexora 仿真数据集（大规模）

Dexora 仿真数据集在 **MuJoCo** 中生成，共包含 **100K 条轨迹**，并采用与真实机器人一致的 **36 自由度双臂双手** 形态。该数据集提供大规模、与实体机器人形态匹配的经验，重点覆盖 **抓取与放置（pick-and-place）**、**装配（assembly）** 与 **关节物体操作（articulation）** 等核心技能，可用于先在仿真中预训练基础能力，再在真实世界数据上进行精调。

### 仿真与真实数据统计对比

| **数据划分（Split）** | **轨迹数（Episodes）** | **帧数（Frames）** | **时长（约）（Hours）** | **任务类型（Task Types）**                                                         |
| :-------------------- | ---------------------: | -----------------: | ----------------------: | :--------------------------------------------------------------------------------- |
| **Simulated**         | **100K**               | **6.5M**           | TBD                     | Pick-and-place, assembly, articulation, dexterous manipulation, long-horizon      |
| **Real-World**        | **10K**                | **3.2M**           | **177.5**               | Teleoperated bimanual tasks with high-DoF hands, cluttered scenes, fine-grain interactions |

---

## 📦 物品清单与可复现性（Object Inventory & Reproducibility）

可复现性是 Dexora 的 **核心原则** 之一。为了让其他实验室与团队可以 **忠实复现** 我们的实验环境，我们发布了一份与真实实验场景一一对应的 **物体清单**。

- **规模（Scale）**：共 **347 个物体**，覆盖 **17 个语义类别**（如工具、容器、关节物体、可变形物体、日用品等）。
- **覆盖面（Coverage）**：物体选择侧重于考察 **灵巧操作能力**、**双手协同** 以及 **长时程操作**。
- **采购（Procurement）**：每个物体都提供 **淘宝 / 亚马逊** 等平台的购买链接，便于快速复现与补货。

<p align="center">
  <a href="https://docs.google.com/spreadsheets/d/1L2cgqvIukVziXc0OwpqNkb5j8c3bzC_K/edit?usp=sharing">
    <b>📑 打开 Dexora 真实世界物品清单（Google Sheet）</b>
  </a>
</p>

### 物品清单元数据结构

公开的 Google Sheet 遵循如下字段结构：

| 列名（Column）           | 描述（Description）                                                                |
| :---------------------- | :--------------------------------------------------------------------------------- |
| **Object Name (EN & CN)** | 中英文双语物体名称，便于全球研究者统一引用。                                        |
| **Task Type**           | 任务类型之一：`pick-and-place`、`assemble`、`articulation`、`dexterous`。          |
| **Purchase Link**       | 指向 **淘宝 / 亚马逊** 的购买链接，便于快速采购与补货。                               |

研究者可以根据 **任务类型、物体类别或电商平台** 进行过滤，从而基于 Dexora 构建更细粒度的基准任务或扩展任务集。

---

## 📂 数据结构（Data Structure）

Dexora 完全遵循 **LIBERO-2.0 数据集标准**。每个轨迹（episode）都以独立文件形式存储，包含：

- **观测（Observations）**：多视角 RGB（以及可选的深度）、可用时的分割掩码等。
- **机器人状态（Robot State）**：双臂与双手的关节位置 / 速度，以及夹爪 / 手的开合或接触状态。
- **动作（Actions）**：与 36 自由度双臂双手控制兼容的底层控制指令。
- **语言（Language）**：高层任务描述以及（在可用时）步骤级子目标注释。

示例目录结构如下：

```text
dexora/
  sim/
    tasks/
      pick_and_place/
        episodes/
          episode_000001.h5
          episode_000002.h5
          ...
      assembly/
        episodes/
          episode_000001.h5
          ...
  real/
    tasks/
      dexterous/
        episodes/
          episode_000001.h5
          ...
      articulation/
        episodes/
          episode_000001.h5
          ...
  metadata/
    object_inventory.csv        # 物品清单（可由 Google Sheet 导出）
    task_taxonomy.yaml          # 任务名称到类别的映射
    camera_calibration.json     # 各相机的内参与外参
```

> **注**：公开版本在文件夹命名与具体格式上可能会有微调，但整体会保持 **基于 episode 的 LIBERO-2.0 结构** 不变。

---

## 📥 使用说明（Usage）

### 1. 环境配置（Environment Setup）

推荐使用 **conda** 管理 Python 环境与依赖：

```bash
conda create -n dexora python=3.10 -y
conda activate dexora

# 克隆仓库
git clone <your-dexora-repo-url>.git
cd Dexora

# 安装 Python 依赖（示例）
pip install -r requirements.txt
```

如需训练或微调 VLA 模型，请确保根据本机硬件正确安装 **PyTorch**、**CUDA** 以及相应的仿真后端（如 Isaac、Mujoco 等）。

### 2. 数据下载（Downloading the Dataset）

- **仿真数据（Simulated Dexora）**：下载链接将在 **项目主页（Project Page）** 上提供（参见顶部 badge）。
- **真实数据（Real-World Dexora）**：高分辨率的远程操作数据（RGB、proprio、actions 等）将托管在公开存储服务上（如学术服务器或云存储）。

典型使用方式：

```bash
# 设定本地数据存放路径
export DEXORA_DATA=/path/to/dexora

# （可选）将数据软链接到当前仓库
ln -s $DEXORA_DATA data
```

### 3. 轨迹读取示例（Loading Episodes）

下面是一个最小示例，展示如何遍历 Dexora 中符合 LIBERO-2.0 规范的 episode 文件：

```python
import h5py
from pathlib import Path

root = Path("/path/to/dexora/real/tasks/dexterous/episodes")

for episode_path in sorted(root.glob("episode_*.h5")):
    with h5py.File(episode_path, "r") as f:
        rgb = f["observations/rgb_front"][:]      # (T, H, W, 3)
        qpos = f["robot_state/qpos"][:]           # (T, 36)
        actions = f["actions"][:]                 # (T, 36)
        language = f["language/instruction"][()]  # 标量字符串

        # 在此编写你的训练 / 评估代码
        ...
```

该接口与 **LIBERO-2.0 工具链** 自然兼容，因此你可以在最小改动下复用现有的数据加载器与训练流程。

---

## 📜 引用（Citation）

如果 Dexora 对你的研究有所帮助，欢迎引用我们的论文：

```bibtex
@misc{dexora2026,
  title         = {Dexora: Open-Source VLA for High-DoF Bimanual Dexterity},
  author        = {Dexora Team},
  year          = {2026},
  archivePrefix = {arXiv},
  eprint        = {xxxx.xxxxx},
  primaryClass  = {cs.RO}
}
```

---

如有问题、合作意向或任何反馈，欢迎在仓库中提交 issue，或通过项目主页与维护者取得联系。


