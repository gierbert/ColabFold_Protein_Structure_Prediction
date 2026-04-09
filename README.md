# ColabFold_Protein_Structure_Prediction
# ColabFold 蛋白质结构预测使用手册
## 项目简介
基于`ColabFold`实现蛋白质结构预测，适配Linux/服务器/本地GPU工作站环境，依托`colabfold_batch`、`MMseqs2`、`JAX+AlphaFold`核心工具，完成从序列输入到三维结构可视化的全流程预测。

## 核心功能
1. 自动检测Python环境、GPU可用性，一键安装缺失依赖
2. 快速生成标准FASTA蛋白序列输入文件
3. 调用GPU加速执行`colabfold_batch`结构预测
4. 自动解析pLDDT、PAE、ptm等关键预测指标
5. 支持Notebook内三维结构可视化展示
6. 自动汇总输出结果文件，便于后续分析

## 环境要求
- 系统：Linux/WSL2（Windows环境易报错）
- 硬件：推荐NVIDIA GPU（CPU可运行但速度极慢）
- Python：3.8及以上版本
- 依赖：colabfold、alphafold、biopython、py3Dmol、matplotlib、pandas

## 快速使用步骤
### 1. 环境检查与依赖安装
运行环境检测代码，自动校验Python版本、GPU状态，缺失依赖会自动安装，同时修复JAX GPU后端问题。

### 2. 准备输入序列
替换代码中的`sequence`为目标蛋白序列，设置`job_name`，自动生成标准FASTA文件。

### 3. 执行结构预测
开启`run_prediction=True`，程序自动调用GPU运行`colabfold_batch`，支持自定义循环精修次数、模型数量、是否启用Amber弛豫。

### 4. 结果解析与可视化
- 自动扫描输出PDB结构文件、JSON评分文件
- 提取pLDDT、ptm等核心指标并排序
- 调用py3Dmol在Notebook内展示最优三维结构

### 5. 结果解读
- **pLDDT（0-100）**：局部结构可信度，＞70较可靠，＞90高可信
- **PAE**：残基相对位置误差，数值越低精度越高
- **ptm/ipTM**：整体拓扑/多聚体界面质量指标
- **rank_001**：综合评分最优模型，为核心分析结果

## 输出文件说明
- `*.pdb`：预测的蛋白质三维结构文件
- `*.json`：包含pLDDT、PAE、ptm等预测评分
- `*.png`：pLDDT、PAE、序列覆盖度可视化图表
- `*.a3m`：多序列比对结果文件
- `log.txt`：预测运行日志
