# Data Sources and License Verification

This dataset is built from multiple public Chinese text correction, grammar correction, and ASR post-processing datasets.

Please check and comply with each upstream dataset's license, citation requirements, and redistribution terms before using this dataset for training, redistribution, publication, commercial use, or model release.

Status values:

- `needs_verification`: upstream license / citation / redistribution terms still need to be confirmed.
- `verified`: source-level license and usage boundaries have been checked and documented.

## Source table

| Source | Samples | Share | Upstream link | License | Citation required | Commercial use | Redistribution | Status | Notes |
|---|---:|---:|---|---|---|---|---|---|---|
| `shibing624_CSC` | 115,341 | 80.05% | TODO | TODO | TODO | TODO | TODO | needs_verification | General Chinese spelling correction base. Highest priority because it is the largest source. |
| `shibing624_chinese_text_correction` | 26,050 | 18.08% | TODO | TODO | TODO | TODO | TODO | needs_verification | Chinese text correction / grammar-semantic source. |
| `ASR-EC-Benchmark` | 1,986 | 1.38% | TODO | TODO | TODO | TODO | TODO | needs_verification | ASR entity / phrase correction samples. |
| `FCGEC` | 367 | 0.25% | TODO | TODO | TODO | TODO | TODO | needs_verification | Grammar correction benchmark samples. |
| `ChineseHP` | 340 | 0.24% | TODO | TODO | TODO | TODO | TODO | needs_verification | ASR phonetic correction samples. |

## Notes for users

This repository documents a derived training dataset for MyVoiceTyping. The source table above is intentionally conservative: unknown license or redistribution terms are marked as `TODO` / `needs_verification` rather than treated as allowed.

Until each source is verified, do not assume that the entire derived dataset can be redistributed or used commercially under a single permissive license.

## How to contribute verification

If you can help verify a source, please open an issue or pull request with:

1. the source name;
2. the official upstream URL;
3. the license URL or license text;
4. citation requirements, if any;
5. whether commercial use is allowed;
6. whether redistribution or derived dataset publication is allowed;
7. any additional notes from the dataset card, paper, or repository.

Please prefer official dataset cards, repositories, papers, or competition pages over third-party mirrors.
