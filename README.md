# Sealos Weekly 数据集

## 项目简介
本仓库用于存档 Sealos 相关开源仓库的每周活跃情况，包括代码提交和 Issue 动态。所有数据均为离线导出，便于后续的数据分析、可视化和报告撰写。

## 文件结构
仓库以日期区分不同的周报快照，命名规则如下：

- `YYYY-MM-DD.csv`：某日统计时刻的提交记录。
- `YYYY-MM-DD-issue.csv`：同一时刻的 Issue 汇总（CSV）。
- `YYYY-MM-DD-issue.json`：同一时刻的 Issue 详细信息（JSON）。

以 `2025-10-05` 为例，对应的三类文件为：

- `2025-10-05.csv`
- `2025-10-05-issue.csv`
- `2025-10-05-issue.json`

## 数据字段说明
### 提交数据（`YYYY-MM-DD.csv`）
| 字段名 | 含义 |
| --- | --- |
| `分组ID` | 用于聚合同一项目的提交记录。 |
| `项目名称` | GitHub 仓库名称。 |
| `提交CommitID` | 提交的完整哈希。 |
| `提交日期` | 提交时间，含时区信息。 |
| `提交标题` | 提交时的标题，保留原有引号。 |
| `分支` | 提交所在的分支及其引用。 |
| `提交人` | 提交者署名。 |
| `已提交天数` | 从提交产生到统计时刻的天数。 |
| `报告时间` | 生成本记录的日期。 |

### Issue 汇总数据（`YYYY-MM-DD-issue.csv`）
| 字段名 | 含义 |
| --- | --- |
| `repo` | 仓库名称。 |
| `issue_number` | Issue 编号。 |
| `author` | Issue 创建者。 |
| `title` | Issue 标题。 |
| `closed_at` | Issue 关闭时间，若为空则表示仍开放。 |
| `state` | Issue 当前状态（OPEN/CLOSED 等）。 |
| `is_bot` | 创建者是否为机器人账号。 |
| `exported_at` | 导出本记录的时间戳。 |

### Issue 详情数据（`YYYY-MM-DD-issue.json`）
JSON 文件以仓库为单位聚合 Issue 内容。结构示例如下：

```json
[
  {
    "repo": "labring/sealos",
    "issues": [
      {
        "issue_number": 4764,
        "title": "cloud-port=8443时安装cloud会发生错误...",
        "body": "...",
        "state": "CLOSED",
        "labels": [],
        "updated_at": "2024-06-26T08:32:15Z"
      }
    ]
  }
]
```

字段含义：

- `repo`：仓库名称。
- `issues`：当前仓库下的 Issue 列表。
  - `issue_number`：Issue 编号。
  - `title`：Issue 标题。
  - `body`：Issue 详情内容，保留原始 Markdown。
  - `state`：Issue 状态。
  - `labels`：标签列表（如有）。
  - `updated_at`：最后更新时间。

## 使用建议
1. 将 CSV 文件导入任意数据分析工具（如 Excel、Google Sheets、Pandas）即可快速筛选和统计提交/Issue 状态。
2. JSON 文件适合用于生成更详细的周报，例如提取 Issue 描述中的关键信息或引用外部链接。
3. 建议结合 `报告时间` 与 `exported_at` 字段，判定同一周内的差异和趋势。
4. 如需自动化分析，可按日期遍历文件并合并数据，构建时间序列模型或生成图表。

## 贡献指南
若需新增周报数据或纠正已有内容，请确保文件命名遵循上述约定，并使用同一套字段，便于后续处理。

