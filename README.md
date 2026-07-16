# Chinese ASR Post-Correction Dataset

这是一个面向中文语音输入/ASR 转写后处理的纠错、格式化和轻度改写数据集。数据目标不是做开放式润色，而是训练模型在保持原意的前提下，对 ASR 或语音输入法输出文本进行必要的最小修正。

主要覆盖能力：

- 错字、错词、音近词、形近词纠错
- 实体名词、专名、常用词组纠错
- 数字、日期、时间格式规范化
- 缺失句末标点补齐
- 长句轻度断句和必要标点补齐
- 语病、连接词、功能词和局部句式不顺修正
- 抑制过度改写，避免新增 URL、Markdown 链接和图片地址

## 与 MyVoiceTyping 的关系

这个数据集用于调优 [MyVoiceTyping](https://github.com/botaruibo/MyVoiceTyping) 的本地文本润写 / ASR 后处理模型。主项目是一个面向 macOS 中文 / 中英混合语音输入的开源工具，目标是把“口述 → 转写 → 标点 / 轻量纠错 / 润写 → 用户确认后粘贴”这条输入链路做得更可控。

配套资源：

- App 主仓库：<https://github.com/botaruibo/MyVoiceTyping>
- 本地润写模型：<https://modelscope.cn/models/botaruibo/MyVoiceTyping-1.5b-q4>
- 30 秒试用任务：<https://github.com/botaruibo/MyVoiceTyping/blob/main/docs/TRIAL_TASKS.zh-CN.md>
- 中文工具对比：<https://github.com/botaruibo/MyVoiceTyping/blob/main/docs/ALTERNATIVES.zh-CN.md>

这个数据集重点不是训练通用聊天能力，而是让语音输入后的文本更可用：修正常见中文 ASR 错词、补标点和断句、保留代码词 / 产品名 / 文件路径 / 中英混合短语，并尽量不改变用户原意。

如果你是从数据集页面进入、想体验完整语音输入工具，可以先做一条 30 秒试用任务；如果方向对你有用，欢迎给 App 主仓库 Star，Star 会帮助决定后续是否优先投入中文语音输入、AI Coding prompt、本地隐私和 self-evaluation 个性化调优。

## 文件结构

```text
.
├── final.jsonl
├── final_flat.jsonl
├── final_build_report.md
├── final_build_report.json
├── pair_selection_report.jsonl
├── README.md
└── splits
    ├── final.train.jsonl
    ├── final.valid.jsonl
    ├── final.test.jsonl
    ├── final_flat.train.jsonl
    ├── final_flat.valid.jsonl
    ├── final_flat.test.jsonl
    └── split_summary.json
```

## 数据规模

当前版本总计 **144,084** 条。

| split | 数量 | 占比 |
|---|---:|---:|
| train | 126,827 | 88.02% |
| valid | 14,751 | 10.24% |
| test | 2,506 | 1.74% |

## 数据格式

### ChatML 格式

`final.jsonl` 和 `splits/final.*.jsonl` 是训练用 ChatML 格式，每行一条 JSON。

```json
{
  "messages": [
    {
      "role": "system",
      "content": "你是ASR和中文文本后处理纠错助手..."
    },
    {
      "role": "user",
      "content": "<ASR_POST><MIN_EDIT><CORRECT><NO_NEW_LINKS><PRESERVE_EXISTING_LINKS>\n场景：general_csc\n原文：..."
    },
    {
      "role": "assistant",
      "content": "..."
    }
  ],
  "metadata": {
    "id": "...",
    "source": "...",
    "category": "...",
    "domain": "...",
    "scene": "...",
    "split": "train"
  }
}
```

训练时通常使用：

- `splits/final.train.jsonl`
- `splits/final.valid.jsonl`
- `splits/final.test.jsonl`

### Flat 格式

`final_flat.jsonl` 和 `splits/final_flat.*.jsonl` 是便于分析、过滤和评测的扁平格式。

```json
{
  "id": "...",
  "source": "shibing624_CSC",
  "category": "general_base",
  "domain": "general_csc",
  "scene": "general_csc",
  "split": "train",
  "input": "原始文本",
  "expected": "修正后文本",
  "is_positive": false,
  "length_bucket": "medium",
  "selection_type": "written_csc_pair_phonetic_keep",
  "selection_score": 123,
  "selection_reason": "...",
  "metadata": {}
}
```

核心字段说明：

| 字段 | 说明 |
|---|---|
| `id` | 样本唯一标识，通常包含来源数据集和原始样本编号 |
| `source` | 数据来源 |
| `category` | 任务类别 |
| `domain` | 领域或子集 |
| `scene` | 训练提示中的场景标识 |
| `split` | `train`、`valid` 或 `test` |
| `input` | 原始待修正文本 |
| `expected` | 期望输出文本 |
| `is_positive` | 是否严格无修改样本，即 `input == expected` |
| `length_bucket` | 文本长度桶，`short`、`medium`、`long` |
| `selection_type` | 样本进入 final 的筛选路径 |
| `selection_reason` | 样本保留原因 |
| `metadata` | 原始标签、修正过程和审查信息 |

## 来源分布

| source | 数量 | 占比 |
|---|---:|---:|
| `shibing624_CSC` | 115,341 | 80.05% |
| `shibing624_chinese_text_correction` | 26,050 | 18.08% |
| `ASR-EC-Benchmark` | 1,986 | 1.38% |
| `FCGEC` | 367 | 0.25% |
| `ChineseHP` | 340 | 0.24% |

## 任务类别分布

| category | 数量 | 占比 | 说明 |
|---|---:|---:|---|
| `general_base` | 115,475 | 80.14% | 通用错字、错词、音近/形近纠错底座 |
| `grammar_semantic` | 23,928 | 16.61% | 语病、句式不顺、语义顺滑、部分标点和数字规则修正 |
| `domain_entity` | 2,355 | 1.63% | 领域实体、专名、机构名、地址名等 |
| `asr_entity_phrase` | 1,986 | 1.38% | ASR-EC 中实体名词、常用词组、长短文本纠错 |
| `asr_phonetic` | 340 | 0.24% | ChineseHP 中更偏 ASR 音近错误的样本 |

## 筛选类型分布

| selection_type | 数量 | 占比 | 说明 |
|---|---:|---:|---|
| `written_csc_pair_phonetic_keep` | 63,884 | 44.34% | 按真实“错词 -> 修正词”修正对筛选，音近修正对加权保留 |
| `prompt_rule_review_keep` | 56,044 | 38.90% | 数字、日期、时间、句末标点和少量断句规则修正后合并 |
| `len1_freq_weighted_keep` | 14,283 | 9.91% | 单字错词按现代汉语词频表加权抽样 |
| `positive_no_change_keep` | 9,873 | 6.85% | 无差异正样本，用于约束模型不要过度改写 |

## 长度分布

| length_bucket | 数量 | 占比 |
|---|---:|---:|
| `medium` | 81,244 | 56.39% |
| `long` | 47,758 | 33.15% |
| `short` | 15,082 | 10.47% |

## 构建策略

### 1. 数据来源选择

本数据集不继续使用 train001 的标点断句主数据，避免模型过度学习单一标点和断句风格。

ASR-EC 和 ChineseHP 只保留小比例样本，用作 ASR 实体、短语和音近错误补充，避免其长文本噪声主导训练。

### 2. 通用纠错样本

`written_csc_weak_asr` 是主要错字词纠错来源。筛选时以真实修正对为中心，而不是只统计修正后的目标词。

例如：

```text
名着 -> 名著
名住 -> 名著
```

这两个样本会被统计为两个不同的修正对，但修正后的目标词都指向 `名著`。

筛选原则：

- 每个修正对至少保留 1 条样本
- 同音、近音修正对多保留
- 音差明显的修正对少保留
- 同一修正对下，主题或句式接近的样本最多保留 3 条
- 优先保留句式、主题差异更大的样本

### 3. 拼音相似性加权

因为目标场景是语音输入/ASR 后处理，音近错误比纯书面形近错误更重要。构建时按拼音相似性对修正对加权。

示例：

```text
宫员 -> 官员
莫国 -> 美国
```

这类音近样本更符合 ASR 错误分布，优先保留更多。

```text
豪国 -> 美国
玫击 -> 攻击
```

这类发音差异较大的修正对保留较少。

### 4. 单字修正样本

对单字错词样本，使用现代汉语词频表中词长=1的词做频率约束：

- 高频词样本最多保留 20 条
- 相同词优先选择不同话题、不同句式
- 去除明显不合理样本，例如 `曰 -> 日` 类高风险误伤样本

### 5. 数字、日期、时间和标点规则

对 `missing_final_punctuation` 和 `numeric_style_not_normalized` 类样本，按规则保守修正 expected：

- 年份、日期、时间转为更适合输入法输出的格式
- 体育比分、明确数值优先使用阿拉伯数字
- `几百万到上千万` 这类模糊数量不强制改为阿拉伯数字
- 补齐明显缺失的句末标点
- 对长无标点文本只做少量必要断句，不做大段改写

### 6. expected 深度修正

在全量 final 上继续检查并修正：

- `2019年七月` 这类月份漏规范问题
- 时间表达混用问题
- 残留高置信错别词
- 明显重复坏串，例如三字异常叠词
- 少量连接词前后的断句和标点
- 语病、句式不顺、连接词/功能词错误候选

修正边界：

- 保持原意
- 最小修改
- 不做开放式扩写
- 不强行改写地域用字，如 `计画`、`报导`、`作法`
- 专名或语义不确定样本不凭规则强改

### 7. 去重

对 `input` 做近重复去重：

- 文本归一化后去除空白和标点噪声
- 使用 3-gram SimHash 召回候选
- 使用 `SequenceMatcher` 做最终相似度确认
- `input` 相似度超过 80% 的样本视为同组
- 每组只保留 1 条

最终精确 `input` 重复为 0，精确 `input + expected` 重复为 0。

### 8. 链接和 Markdown 污染控制

训练目标明确禁止新增 URL、Markdown 链接、Markdown 图片或图片地址。

构建时：

- 人工 format guard 样本不并入主训练集
- 含 URL、Markdown、图片地址的样本只保留极少量 review 后样本
- system/user prompt 中加入 `NO_NEW_LINKS` 和 `PRESERVE_EXISTING_LINKS` 控制符
- 保留原文已有链接时，要求原样保留，不新增、不删除、不改写

## 当前分布评估

当前分布适合作为 ASR 后中文纠错/格式化的通用底座版本。

优势：

- 通用错字词纠错样本充足
- 近音、音近修正对经过加权，贴近语音输入错误
- 语病、连接词、轻度句式修正有一定比例
- 正样本可抑制模型过度改写
- 数字、日期、时间、句末标点规则已有覆盖

风险：

- `shibing624_CSC` 占 80.05%，模型可能偏 written CSC 的短句错字词纠正
- 严格 `input == expected` 的样本只有 1.32%，如果模型出现过度改写，建议补充更多真实 ASR 风格无改写样本
- ASR-EC 和 ChineseHP 合计约 1.62%，符合小占比要求，但真实 ASR 错误覆盖仍偏少
- `prompt_rule_review_keep` 占 38.90%，如果评测出现过度数字化或过度补标点，需要降低该类比例或补充反例

## 推荐训练方式

建议使用固定 step/iter 训练，而不是按 epoch 训练。

推荐实验：

```text
1000 iter: 快速验证数据质量
2000 iter: 推荐主实验
5000 iter: 加强实验，观察是否继续提升
```

不建议直接训练完整 epoch。当前数据量 144,084 条，如果 batch size 为 16，1 epoch 约为 9,006 step，训练成本和过拟合风险都明显增加。

评测重点：

- 字符级 edit distance / similarity
- expected 命中率
- 过度改写率
- 新增 URL、Markdown、图片链接比例
- 数字、日期、时间格式稳定性
- 长 ASR 文本断句和标点质量
- 实体名词、专名、常用词组修正效果

## 注意事项

本数据集由多个公开中文纠错、语病修正、ASR 后处理相关数据源整理而来。单独发布、再分发、商业训练或公开发布模型前，应确认并遵守各原始数据集的许可证、引用要求和使用边界。

授权和使用边界说明见：

- [DATA_LICENSE.md](DATA_LICENSE.md)
- [docs/SOURCES.md](docs/SOURCES.md)

如果用于商业训练或公开发布模型，建议在仓库中补充：

- 原始数据集来源链接
- 各来源许可证
- 数据清洗脚本
- 构建命令
- 评测脚本
- 模型训练配置
# Chinese ASR Post-Correction Dataset

这是一个面向中文语音输入/ASR 转写后处理的纠错、格式化和轻度改写数据集。数据目标不是做开放式润色，而是训练模型在保持原意的前提下，对 ASR 或语音输入法输出文本进行必要的最小修正。

主要覆盖能力：

- 错字、错词、音近词、形近词纠错
- 实体名词、专名、常用词组纠错
- 数字、日期、时间格式规范化
- 缺失句末标点补齐
- 长句轻度断句和必要标点补齐
- 语病、连接词、功能词和局部句式不顺修正
- 抑制过度改写，避免新增 URL、Markdown 链接和图片地址

## 文件结构

```text
.
├── final.jsonl
├── final_flat.jsonl
├── final_build_report.md
├── final_build_report.json
├── pair_selection_report.jsonl
├── README.md
└── splits
    ├── final.train.jsonl
    ├── final.valid.jsonl
    ├── final.test.jsonl
    ├── final_flat.train.jsonl
    ├── final_flat.valid.jsonl
    ├── final_flat.test.jsonl
    └── split_summary.json
```

## 数据规模

当前版本总计 **144,084** 条。

| split | 数量 | 占比 |
|---|---:|---:|
| train | 126,827 | 88.02% |
| valid | 14,751 | 10.24% |
| test | 2,506 | 1.74% |

## 数据格式

### ChatML 格式

`final.jsonl` 和 `splits/final.*.jsonl` 是训练用 ChatML 格式，每行一条 JSON。

```json
{
  "messages": [
    {
      "role": "system",
      "content": "你是ASR和中文文本后处理纠错助手..."
    },
    {
      "role": "user",
      "content": "<ASR_POST><MIN_EDIT><CORRECT><NO_NEW_LINKS><PRESERVE_EXISTING_LINKS>\n场景：general_csc\n原文：..."
    },
    {
      "role": "assistant",
      "content": "..."
    }
  ],
  "metadata": {
    "id": "...",
    "source": "...",
    "category": "...",
    "domain": "...",
    "scene": "...",
    "split": "train"
  }
}
```

训练时通常使用：

- `splits/final.train.jsonl`
- `splits/final.valid.jsonl`
- `splits/final.test.jsonl`

### Flat 格式

`final_flat.jsonl` 和 `splits/final_flat.*.jsonl` 是便于分析、过滤和评测的扁平格式。

```json
{
  "id": "...",
  "source": "shibing624_CSC",
  "category": "general_base",
  "domain": "general_csc",
  "scene": "general_csc",
  "split": "train",
  "input": "原始文本",
  "expected": "修正后文本",
  "is_positive": false,
  "length_bucket": "medium",
  "selection_type": "written_csc_pair_phonetic_keep",
  "selection_score": 123,
  "selection_reason": "...",
  "metadata": {}
}
```

核心字段说明：

| 字段 | 说明 |
|---|---|
| `id` | 样本唯一标识，通常包含来源数据集和原始样本编号 |
| `source` | 数据来源 |
| `category` | 任务类别 |
| `domain` | 领域或子集 |
| `scene` | 训练提示中的场景标识 |
| `split` | `train`、`valid` 或 `test` |
| `input` | 原始待修正文本 |
| `expected` | 期望输出文本 |
| `is_positive` | 是否严格无修改样本，即 `input == expected` |
| `length_bucket` | 文本长度桶，`short`、`medium`、`long` |
| `selection_type` | 样本进入 final 的筛选路径 |
| `selection_reason` | 样本保留原因 |
| `metadata` | 原始标签、修正过程和审查信息 |

## 来源分布

| source | 数量 | 占比 |
|---|---:|---:|
| `shibing624_CSC` | 115,341 | 80.05% |
| `shibing624_chinese_text_correction` | 26,050 | 18.08% |
| `ASR-EC-Benchmark` | 1,986 | 1.38% |
| `FCGEC` | 367 | 0.25% |
| `ChineseHP` | 340 | 0.24% |

## 任务类别分布

| category | 数量 | 占比 | 说明 |
|---|---:|---:|---|
| `general_base` | 115,475 | 80.14% | 通用错字、错词、音近/形近纠错底座 |
| `grammar_semantic` | 23,928 | 16.61% | 语病、句式不顺、语义顺滑、部分标点和数字规则修正 |
| `domain_entity` | 2,355 | 1.63% | 领域实体、专名、机构名、地址名等 |
| `asr_entity_phrase` | 1,986 | 1.38% | ASR-EC 中实体名词、常用词组、长短文本纠错 |
| `asr_phonetic` | 340 | 0.24% | ChineseHP 中更偏 ASR 音近错误的样本 |

## 筛选类型分布

| selection_type | 数量 | 占比 | 说明 |
|---|---:|---:|---|
| `written_csc_pair_phonetic_keep` | 63,884 | 44.34% | 按真实“错词 -> 修正词”修正对筛选，音近修正对加权保留 |
| `prompt_rule_review_keep` | 56,044 | 38.90% | 数字、日期、时间、句末标点和少量断句规则修正后合并 |
| `len1_freq_weighted_keep` | 14,283 | 9.91% | 单字错词按现代汉语词频表加权抽样 |
| `positive_no_change_keep` | 9,873 | 6.85% | 无差异正样本，用于约束模型不要过度改写 |

## 长度分布

| length_bucket | 数量 | 占比 |
|---|---:|---:|
| `medium` | 81,244 | 56.39% |
| `long` | 47,758 | 33.15% |
| `short` | 15,082 | 10.47% |

## 构建策略

### 1. 数据来源选择

本数据集不继续使用 train001 的标点断句主数据，避免模型过度学习单一标点和断句风格。

ASR-EC 和 ChineseHP 只保留小比例样本，用作 ASR 实体、短语和音近错误补充，避免其长文本噪声主导训练。

### 2. 通用纠错样本

`written_csc_weak_asr` 是主要错字词纠错来源。筛选时以真实修正对为中心，而不是只统计修正后的目标词。

例如：

```text
名着 -> 名著
名住 -> 名著
```

这两个样本会被统计为两个不同的修正对，但修正后的目标词都指向 `名著`。

筛选原则：

- 每个修正对至少保留 1 条样本
- 同音、近音修正对多保留
- 音差明显的修正对少保留
- 同一修正对下，主题或句式接近的样本最多保留 3 条
- 优先保留句式、主题差异更大的样本

### 3. 拼音相似性加权

因为目标场景是语音输入/ASR 后处理，音近错误比纯书面形近错误更重要。构建时按拼音相似性对修正对加权。

示例：

```text
宫员 -> 官员
莫国 -> 美国
```

这类音近样本更符合 ASR 错误分布，优先保留更多。

```text
豪国 -> 美国
玫击 -> 攻击
```

这类发音差异较大的修正对保留较少。

### 4. 单字修正样本

对单字错词样本，使用现代汉语词频表中词长=1的词做频率约束：

- 高频词样本最多保留 20 条
- 相同词优先选择不同话题、不同句式
- 去除明显不合理样本，例如 `曰 -> 日` 类高风险误伤样本

### 5. 数字、日期、时间和标点规则

对 `missing_final_punctuation` 和 `numeric_style_not_normalized` 类样本，按规则保守修正 expected：

- 年份、日期、时间转为更适合输入法输出的格式
- 体育比分、明确数值优先使用阿拉伯数字
- `几百万到上千万` 这类模糊数量不强制改为阿拉伯数字
- 补齐明显缺失的句末标点
- 对长无标点文本只做少量必要断句，不做大段改写

### 6. expected 深度修正

在全量 final 上继续检查并修正：

- `2019年七月` 这类月份漏规范问题
- 时间表达混用问题
- 残留高置信错别词
- 明显重复坏串，例如三字异常叠词
- 少量连接词前后的断句和标点
- 语病、句式不顺、连接词/功能词错误候选

修正边界：

- 保持原意
- 最小修改
- 不做开放式扩写
- 不强行改写地域用字，如 `计画`、`报导`、`作法`
- 专名或语义不确定样本不凭规则强改

### 7. 去重

对 `input` 做近重复去重：

- 文本归一化后去除空白和标点噪声
- 使用 3-gram SimHash 召回候选
- 使用 `SequenceMatcher` 做最终相似度确认
- `input` 相似度超过 80% 的样本视为同组
- 每组只保留 1 条

最终精确 `input` 重复为 0，精确 `input + expected` 重复为 0。

### 8. 链接和 Markdown 污染控制

训练目标明确禁止新增 URL、Markdown 链接、Markdown 图片或图片地址。

构建时：

- 人工 format guard 样本不并入主训练集
- 含 URL、Markdown、图片地址的样本只保留极少量 review 后样本
- system/user prompt 中加入 `NO_NEW_LINKS` 和 `PRESERVE_EXISTING_LINKS` 控制符
- 保留原文已有链接时，要求原样保留，不新增、不删除、不改写

## 当前分布评估

当前分布适合作为 ASR 后中文纠错/格式化的通用底座版本。

优势：

- 通用错字词纠错样本充足
- 近音、音近修正对经过加权，贴近语音输入错误
- 语病、连接词、轻度句式修正有一定比例
- 正样本可抑制模型过度改写
- 数字、日期、时间、句末标点规则已有覆盖

风险：

- `shibing624_CSC` 占 80.05%，模型可能偏 written CSC 的短句错字词纠正
- 严格 `input == expected` 的样本只有 1.32%，如果模型出现过度改写，建议补充更多真实 ASR 风格无改写样本
- ASR-EC 和 ChineseHP 合计约 1.62%，符合小占比要求，但真实 ASR 错误覆盖仍偏少
- `prompt_rule_review_keep` 占 38.90%，如果评测出现过度数字化或过度补标点，需要降低该类比例或补充反例

## 推荐训练方式

建议使用固定 step/iter 训练，而不是按 epoch 训练。

推荐实验：

```text
1000 iter: 快速验证数据质量
2000 iter: 推荐主实验
5000 iter: 加强实验，观察是否继续提升
```

不建议直接训练完整 epoch。当前数据量 144,084 条，如果 batch size 为 16，1 epoch 约为 9,006 step，训练成本和过拟合风险都明显增加。

评测重点：

- 字符级 edit distance / similarity
- expected 命中率
- 过度改写率
- 新增 URL、Markdown、图片链接比例
- 数字、日期、时间格式稳定性
- 长 ASR 文本断句和标点质量
- 实体名词、专名、常用词组修正效果

## 注意事项

本数据集由多个公开中文纠错、语病修正、ASR 后处理相关数据源整理而来。单独发布、再分发、商业训练或公开发布模型前，应确认并遵守各原始数据集的许可证、引用要求和使用边界。

授权和使用边界说明见：

- [DATA_LICENSE.md](DATA_LICENSE.md)
- [docs/SOURCES.md](docs/SOURCES.md)

如果用于商业训练或公开发布模型，建议在仓库中补充：

- 原始数据集来源链接
- 各来源许可证
- 数据清洗脚本
- 构建命令
- 评测脚本
- 模型训练配置
