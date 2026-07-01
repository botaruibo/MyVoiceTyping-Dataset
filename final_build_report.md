# final phonetic-aware 构建报告

- 输出：`/Users/bytedance/Documents/py-space/train002/data_final_phonetic/final.jsonl`
- flat：`/Users/bytedance/Documents/py-space/train002/data_final_phonetic/final_flat.jsonl`
- 总数：144085
- 去重前：81472
- 去重移除：7098
- 去重后修正对覆盖：28057
- positive_no_change：10000
- written_csc：71472
- 修正对总数：28057

## 拼音桶分布
- `medium`: 8331
- `close`: 9965
- `same_or_very_close`: 8792
- `far`: 969

## 拼音桶入选样本数
- `medium`: 17252
- `close`: 26532
- `same_or_very_close`: 26669
- `far`: 1019

## 全量候选索引
- 扫描：277337
- 命中修正对行数：166325
- 命中修正对 mentions：205581
- 找到修正对数：28057
- 缺失修正对数：0

## selection_counts
- `positive_no_change_keep`: 10000
- `written_csc_pair_phonetic_keep`: 64374

## 注意
- 修正对清单和命中次数来自 pair_counts.jsonl。
- 候选样本从 written_csc_weak_asr.jsonl 全量重建，不再受 pair_counts.jsonl 中前5条 examples 的限制。
- 每个修正对至少保留1条；近音/同音修正对按拼音相似度和命中次数增加配额；同一修正对内相同主题签名最多保留3条。

## 词长=1 词频样本合并
- 来源：`/Users/bytedance/Documents/py-space/train002/tmp_inspect/unmatched_reasonable_pairs/filtered_no_yue_to_ri/len1_freq_weighted_selection/selected_unique_samples.jsonl`
- 选择样本：14405
- 新增入 final：14404
- 与已有 final 重复跳过：1
- 合并后总数：88778
- 合并后 selection_counts：
  - `positive_no_change_keep`: 10000
  - `written_csc_pair_phonetic_keep`: 64374
  - `len1_freq_weighted_keep`: 14404

## Prompt Rule Review 合并
- 来源：`/Users/bytedance/Documents/py-space/train002/tmp_inspect/asr_unsuitable_large/classified_tags/review/missing_final_punctuation.jsonl`
- 来源：`/Users/bytedance/Documents/py-space/train002/tmp_inspect/asr_unsuitable_large/classified_tags/review/numeric_style_not_normalized.jsonl`
- 合并前 final：88778
- 两类去重 input：79588
- 更新已有 final：21270
- 已存在且 expected 相同：1529
- 新增入 final：56789
- 合并后总数：145567
- flat 备份：`/Users/bytedance/Documents/py-space/train002/data_final_phonetic/final_flat.jsonl.bak_prompt_rule_merge_20260625_005227`
- chat 备份：`/Users/bytedance/Documents/py-space/train002/data_final_phonetic/final.jsonl.bak_prompt_rule_merge_20260625_005227`

## Final Expected Prompt Rule 修正
- 策略：保守修正，只做数字风格规范化与缺失句末标点补齐，不做分段、列表化或句式改写。
- 合并后 final 总数：145567
- 修改 expected：16295
- reason_counts：`{'final_punctuation_added': 1309, 'numeric_style_normalized': 15114}`
- changed 明细：`/Users/bytedance/Documents/py-space/train002/tmp_inspect/final_expected_prompt_rule_fix/changed_20260625_010307.jsonl`
- flat 备份：`/Users/bytedance/Documents/py-space/train002/data_final_phonetic/final_flat.jsonl.bak_final_expected_prompt_rules_20260625_010307`
- chat 备份：`/Users/bytedance/Documents/py-space/train002/data_final_phonetic/final.jsonl.bak_final_expected_prompt_rules_20260625_010307`

## Final Expected Prompt Rule 修正
- 策略：保守修正，只做数字风格规范化与缺失句末标点补齐，不做分段、列表化或句式改写。
- 合并后 final 总数：145567
- 修改 expected：12567
- reason_counts：`{'final_punctuation_added': 1309, 'numeric_style_normalized': 11347}`
- changed 明细：`/Users/bytedance/Documents/py-space/train002/tmp_inspect/final_expected_prompt_rule_fix/changed_20260625_010414.jsonl`
- flat 备份：`/Users/bytedance/Documents/py-space/train002/data_final_phonetic/final_flat.jsonl.bak_final_expected_prompt_rules_20260625_010414`
- chat 备份：`/Users/bytedance/Documents/py-space/train002/data_final_phonetic/final.jsonl.bak_final_expected_prompt_rules_20260625_010414`

## Final Expected Prompt Rule 修正
- 策略：保守修正，只做数字风格规范化与缺失句末标点补齐，不做分段、列表化或句式改写。
- 合并后 final 总数：145567
- 修改 expected：7101
- reason_counts：`{'final_punctuation_added': 1169, 'numeric_style_normalized': 5958}`
- changed 明细：`/Users/bytedance/Documents/py-space/train002/tmp_inspect/final_expected_prompt_rule_fix/changed_20260625_010531.jsonl`
- flat 备份：`/Users/bytedance/Documents/py-space/train002/data_final_phonetic/final_flat.jsonl.bak_final_expected_prompt_rules_20260625_010531`
- chat 备份：`/Users/bytedance/Documents/py-space/train002/data_final_phonetic/final.jsonl.bak_final_expected_prompt_rules_20260625_010531`

## Final Expected Prompt Rule 修正
- 策略：保守修正，只做数字风格规范化与缺失句末标点补齐，不做分段、列表化或句式改写。
- 合并后 final 总数：145567
- 修改 expected：7122
- reason_counts：`{'final_punctuation_added': 1169, 'numeric_style_normalized': 5980}`
- changed 明细：`/Users/bytedance/Documents/py-space/train002/tmp_inspect/final_expected_prompt_rule_fix/changed_20260625_010645.jsonl`
- flat 备份：`/Users/bytedance/Documents/py-space/train002/data_final_phonetic/final_flat.jsonl.bak_final_expected_prompt_rules_20260625_010645`
- chat 备份：`/Users/bytedance/Documents/py-space/train002/data_final_phonetic/final.jsonl.bak_final_expected_prompt_rules_20260625_010645`

## Final Expected Prompt Rule 修正
- 策略：保守修正，只做数字风格规范化与缺失句末标点补齐，不做分段、列表化或句式改写。
- 合并后 final 总数：145567
- 修改 expected：7108
- reason_counts：`{'final_punctuation_added': 1169, 'numeric_style_normalized': 5966}`
- changed 明细：`/Users/bytedance/Documents/py-space/train002/tmp_inspect/final_expected_prompt_rule_fix/changed_20260625_010859.jsonl`
- flat 备份：`None`
- chat 备份：`None`

## 后续 expected 深度修正与最终近重复去重

### expected 深度修正
- 目标：在 `main_prompt_bak.md` 规则基础上，继续修正 final 中 `expected` 字段残留的日期、时间、明显错别词、连接断句和长无标点文本问题。
- 策略边界：保持最小修改；不做大段改写；不改写地域用字如 `计画/报导/作法`；专名和语义不确定样本不凭规则强改。
- 规则类别：
  - `date_month_normalized`：修正 `2019年七月`、`2003年九月` 这类年份后中文月份。
  - `date_month_day_normalized`：修正 `2012年六月21日`、`8月一四日`、`十一月3日起` 等月日混合格式。
  - `date_day_normalized`：修正 `本月十七日` 等相对日期中的中文日。
  - `time_normalized`：修正 `下午二时三十分`、`上午10时三十分` 等时间表达。
  - `time_duration_normalized`：仅在 `总时间...时...分` 场景下修正持续时长，如 `总时间一九四时二十分`。
  - `residual_pair_typo_fixed`：利用样本已有的 `wrong_word/corrected_word` 或 `correction_pairs`，只处理长度大于等于 2 的残留错词，避免单字误伤。
  - `high_confidence_phrase_fixed`：只处理明确坏串或重复词，如 `错误的的示范 -> 错误的示范`、`三个月多久 -> 三个多月`、`性交过成中 -> 性交过程中`。
  - `connector_punctuation_added`：只对高置信连接处加标点，如 `检疫措施菲律宾当局 -> 检疫措施，菲律宾当局`。
  - `long_no_punctuation_segmented`：仅对较长且标点密度极低的文本，按 `建议/因为/所以/如果/但是/期间/这种情况` 等连接词补少量逗号。
- 首轮深度修正：1793 条，明细：`/Users/bytedance/Documents/py-space/train002/tmp_inspect/final_expected_deep_repair/changed_20260625_012620.jsonl`
- 增量补修：87 条，明细：`/Users/bytedance/Documents/py-space/train002/tmp_inspect/final_expected_deep_repair/changed_20260625_012735.jsonl`
- 持续时长补修：3 条，明细：`/Users/bytedance/Documents/py-space/train002/tmp_inspect/final_expected_deep_repair/changed_20260625_012821.jsonl`
- 去除重复触发修正：1 条，明细：`/Users/bytedance/Documents/py-space/train002/tmp_inspect/final_expected_deep_repair/changed_20260625_012901.jsonl`
- 幂等检查：再次运行 `changed_rows=0`，明细：`/Users/bytedance/Documents/py-space/train002/tmp_inspect/final_expected_deep_repair/changed_20260625_012915.jsonl`
- 累计修改操作：1884；去重后涉及样本行：1795。
- 累计 reason_counts：
  - `long_no_punctuation_segmented`: 267
  - `time_normalized`: 1968
  - `time_duration_normalized`: 2
  - `high_confidence_phrase_fixed`: 38
  - `date_month_normalized`: 112
  - `date_month_day_normalized`: 45
  - `date_day_normalized`: 2
  - `connector_punctuation_added`: 3
  - `residual_pair_typo_fixed`: 59
- 三类人工 review 文件：`/Users/bytedance/Documents/py-space/train002/tmp_inspect/final_expected_deep_repair/review_typo_phrase_connector/typo_phrase_connector_review.md`

### input 近重复去重
- 目标：对 final 中 `input` 字段相似度超过 80% 的样本视为同组，每组只保留 1 条。
- 文本归一化：转小写，保留中文、ASCII 字母和数字，移除空白与标点噪声。
- 候选召回：
  - 先处理归一化后完全相同的 exact input。
  - 对长度大于等于 30 的文本计算 3-gram SimHash。
  - 使用 64-bit SimHash 分成 4 个 16-bit band 做桶召回。
  - 每个桶最多回看最近 800 条，避免大桶拖慢和误召回。
- 候选过滤：
  - 长度比低于 0.80 的候选直接跳过。
  - SimHash 汉明距离大于 18 的候选跳过。
  - 3-gram Dice 相似度低于 0.70 的候选跳过。
- 最终确认：使用 `difflib.SequenceMatcher(..., autojunk=False).ratio()` 计算真实相似度，达到 0.80 才合并。
- 分组策略：对相似样本做并查集连通分量聚类；每组保留 final 中行号最靠前的 1 条，其余移除。
- 去重前：145567
- 重复组：1354
- 移除：1482
- 去重后：144085
- 组大小分布：`{2: 1260, 3: 72, 4: 16, 5: 3, 6: 1, 7: 1, 8: 1}`
- 删除明细：`/Users/bytedance/Documents/py-space/train002/tmp_inspect/final_input_similarity_dedupe/removed_20260625_102100.jsonl`
- 重复组明细：`/Users/bytedance/Documents/py-space/train002/tmp_inspect/final_input_similarity_dedupe/groups_20260625_102100.jsonl`
- 摘要：`/Users/bytedance/Documents/py-space/train002/tmp_inspect/final_input_similarity_dedupe/summary_20260625_102100.json`
- 幂等检查：再次运行 `removed_rows=0`，summary：`/Users/bytedance/Documents/py-space/train002/tmp_inspect/final_input_similarity_dedupe/summary_20260625_102207.json`

### 最终统计
- 统计时间：2026-06-30，按当前实际文件重新统计。
- final 总数：144084
- 输出文件：
  - flat：`/Users/bytedance/Documents/py-space/train002/data_final_phonetic/final_flat.jsonl`
  - chat：`/Users/bytedance/Documents/py-space/train002/data_final_phonetic/final.jsonl`

#### source_counts
| source | 数量 | 占比 |
|---|---:|---:|
| `shibing624_CSC` | 115341 | 80.05% |
| `shibing624_chinese_text_correction` | 26050 | 18.08% |
| `ASR-EC-Benchmark` | 1986 | 1.38% |
| `FCGEC` | 367 | 0.25% |
| `ChineseHP` | 340 | 0.24% |

#### category_counts
| category | 数量 | 占比 | 说明 |
|---|---:|---:|---|
| `general_base` | 115475 | 80.14% | 通用错字、错词、音近/形近纠错底座 |
| `grammar_semantic` | 23928 | 16.61% | 语病、句式不顺、语义顺滑、部分标点和数字规则修正 |
| `domain_entity` | 2355 | 1.63% | 领域实体、专名、机构名、地址名等 |
| `asr_entity_phrase` | 1986 | 1.38% | ASR-EC 中实体名词、常用词组、长短文本纠错 |
| `asr_phonetic` | 340 | 0.24% | ChineseHP 中更偏 ASR 音近错误的样本 |

#### selection_counts
| selection_type | 数量 | 占比 | 选择逻辑 |
|---|---:|---:|---|
| `written_csc_pair_phonetic_keep` | 63884 | 44.34% | 从 written_csc_weak_asr 中抽取错词->修正词样本；每种修正对至少保留 1 条；音近修正对按拼音相似度和命中次数增加配额；同一修正对内相同主题签名最多保留 3 条 |
| `prompt_rule_review_keep` | 56044 | 38.90% | 从 `missing_final_punctuation`、`numeric_style_not_normalized` 等 review 类样本中修正 expected 后合并，重点补数字、日期、时间、句末标点和少量断句 |
| `len1_freq_weighted_keep` | 14283 | 9.91% | 从单字错词修正样本中按现代汉语词频表词长=1的高频词加权选择；高频词单词样本最多保留 20 条，并尽量选择不同话题 |
| `positive_no_change_keep` | 9873 | 6.85% | 从无差异正样本中按信息量、长度和去重后保留，用来约束模型不要过度改写 |

#### split_counts
| split | 数量 | 占比 |
|---|---:|---:|
| `train` | 126827 | 88.02% |
| `valid` | 14751 | 10.24% |
| `test` | 2506 | 1.74% |

#### length_bucket_counts
| length_bucket | 数量 | 占比 |
|---|---:|---:|
| `medium` | 81244 | 56.39% |
| `long` | 47758 | 33.15% |
| `short` | 15082 | 10.47% |

#### positive_counts
| is_positive | 数量 | 占比 |
|---|---:|---:|
| `False` | 142177 | 98.68% |
| `True` | 1907 | 1.32% |

说明：`selection_type=positive_no_change_keep` 与 `is_positive=True` 不完全一致。部分原本无差异正样本后续按规则补了句末标点或数字格式，已经不再是严格的 `input == expected`。

#### original_tags 多标签统计
| tag | 数量 | 占比 |
|---|---:|---:|
| `<missing>` | 64989 | 45.10% |
| `written_csc_weak_asr` | 50617 | 35.13% |
| `numeric_style_not_normalized` | 49956 | 34.67% |
| `missing_final_punctuation` | 27212 | 18.89% |
| `grammar_rewrite_weak_asr` | 22799 | 15.82% |
| `positive_no_change` | 13857 | 9.62% |
| `positive` | 2037 | 1.41% |
| `long_no_punctuation_label` | 184 | 0.13% |
| `contains_url_or_markdown` | 9 | 0.01% |
| `expected_keeps_fillers` | 8 | 0.01% |
| `large_rewrite_or_misaligned` | 6 | 0.00% |
| `asr_alignment_noisy_review` | 3 | 0.00% |
| `expected_much_shorter` | 3 | 0.00% |
| `negative` | 1 | 0.00% |
| `expected_much_longer` | 1 | 0.00% |

说明：`original_tags` 是多标签统计，同一条样本可能同时命中 `numeric_style_not_normalized`、`missing_final_punctuation`、`grammar_rewrite_weak_asr` 等，因此各项占比相加会超过 100%。

### 加工策略和约束逻辑汇总
- 不使用 train001 标点断句主数据，避免继续强化单一标点/断句风格。
- ASR-EC、ChineseHP 只小比例加入，作为 ASR 实体、短语、音近错误补充，避免其长文本和噪声分布主导训练。
- `positive_no_change` 从高信息量样本中保留约 1 万条，后续近重复去重后为 9873 条，用来抑制模型过度改写。
- `written_csc_weak_asr` 是主力错字词纠错来源。筛选时不再只看目标词是否在词频表中，而是统计真实 `错词 -> 修正词` 修正对；每个修正对至少保留 1 条。
- 对修正对按拼音相似性加权：同音/近音修正对多保留，明显音远修正对少保留，更贴近语音输入/ASR 转写错误分布。
- 对相同修正对内样本做主题签名限制，相同话题内容最多保留 3 条，减少模板化重复。
- 对单字修正样本使用现代汉语词频表中词长=1的词做频率约束；高频词不超过 20 条，优先保留不同话题。
- `missing_final_punctuation` 和 `numeric_style_not_normalized` 经 `main_prompt_bak.md` 规则做 expected 修正后合并：只做保守的数字、日期、时间、句末标点修正，不做激进改写。
- 对 final 全量 expected 继续做深度修正：日期月份、时间表达、残留错别词、高置信重复坏串、少量连接处断句和长无标点文本补逗号。
- 对 input 相似度超过 80% 的样本做近重复去重，每组只保留 1 条；精确 input 重复和 input+expected 重复均清零。
- 人工安全样本 `artificial_format_guard` 不并入主集；含 URL/Markdown 的样本只保留极少量 review 后样本，避免训练出新增链接或图片的污染行为。

### 分布合理性判断
- 当前分布适合作为“ASR 后中文纠错/格式化”的通用底座版本：`general_base` 约 80%，可以强化错字、错词、音近/形近纠错；`grammar_semantic` 约 16.6%，能补充句式不顺、连接词和轻度语义顺滑；正样本约 6.85% 的选择来源可约束过度改写。
- 风险 1：`shibing624_CSC` 占 80.05%，模型可能更偏 written CSC 的短句错字词修正，而不是纯 ASR 断句、口语冗余、长句整理。训练后需要重点评估长 ASR 文本、口语填充词和断句能力。
- 风险 2：严格 `is_positive=True` 只有 1.32%，如果模型出现“本来正确也想改”的倾向，可以单独补一批真正 `input == expected` 的 ASR 风格正样本，建议提升到 5%-10% 的严格无改写样本。
- 风险 3：ASR-EC 和 ChineseHP 合计约 1.62%，符合“占比要小”的要求，但如果目标更偏语音输入法真实错词，后续可在不增加噪声的前提下适度提高 ASR 音近、实体、专名样本到 3%-5%。
- 风险 4：`prompt_rule_review_keep` 占 38.90%，其中不少来自数字、日期、标点规则修正。这个比例对格式化有帮助，但如果评测发现模型过度数字化或过度补标点，需要降低该类比例或增加“不要改”的反例。
- 训练建议：先按 1000/2000/5000 iter 分阶段训练和评测，不建议直接按 epoch 训练。每轮重点看过度改写率、链接/Markdown 新增率、数字日期格式稳定性、长句断句和实体名词修正。
