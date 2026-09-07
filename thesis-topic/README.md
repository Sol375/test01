# 论文项目总览

> 一句话说明这个仓库是做什么的（选题方向 + 目标产出）。

## 1. 研究问题

- **研究问题（RQ）**：
  - RQ1：
  - RQ2：
- **研究假设**：
- **贡献点**：

## 2. 目录结构

| 目录 | 用途 | 是否入 Git |
| --- | --- | --- |
| `docs/` | 论文正文、大纲、文献笔记、会议记录 | 是 |
| `data/raw/` | 原始数据，**只读，禁止手工修改** | 否（体积大时） |
| `data/processed/` | 清洗/转换后的数据 | 否（可由脚本重建） |
| `src/` | 数据处理、模型、分析代码 | 是 |
| `notebooks/` | 探索性分析笔记本 | 是 |
| `results/` | 表格、统计结果 | 是 |
| `figures/` | 论文/汇报用图 | 是 |
| `experiments/` | 每次实验的配置与记录 | 是 |
| `references/` | BibTeX 与文献管理 | 是 |

## 3. 如何运行

```bash
# 1. 创建环境
conda env create -f environment.yml
conda activate thesis

# 2. 数据预处理（原始 -> 处理后）
python src/preprocess.py --input data/raw --output data/processed

# 3. 跑实验
python src/train.py --config experiments/exp-001-baseline.md

# 4. 出图与结果表
python src/analyze.py --results results/
```

## 4. 命名与记录约定

- 实验记录：`experiments/exp-<三位编号>-<简述>.md`，编号递增不复用。
- 结果文件：`results/<实验编号>_<内容>.<ext>`，例如 `exp-001_metrics.csv`。
- 每次实验必须记录：日期、改动点、超参、随机种子、环境版本、结果、结论。
- 会议记录：`docs/meeting-notes/YYYY-MM-DD-<主题>.md`。

## 5. 复现性检查清单

- [ ] 随机种子固定
- [ ] 依赖版本锁定（environment.yml）
- [ ] `data/raw/` 未被改动（可用校验和核对）
- [ ] 从原始数据到最终结果可一键重跑
