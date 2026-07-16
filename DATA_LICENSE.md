# Dataset License and Usage Notes

This repository contains a derived dataset for Chinese ASR post-correction, Chinese text correction, punctuation restoration, and light text cleanup.

The dataset is built from multiple public upstream datasets. Unless explicitly stated otherwise, each sample remains subject to the license, citation requirements, and usage restrictions of its original source.

This file is a usage boundary note, not a replacement for upstream dataset licenses.

## What this means

Before using this dataset for training, redistribution, publication, commercial use, or model release, please verify:

- the upstream license of each source;
- whether redistribution is allowed;
- whether commercial use is allowed;
- whether attribution or citation is required;
- whether additional dataset-specific restrictions apply.

The source-level verification table is tracked in [docs/SOURCES.md](docs/SOURCES.md).

## Current status

The dataset README documents the current source distribution, but source-level license verification is still in progress.

Until each upstream source is verified, please treat the dataset as suitable for research, evaluation, and reproducible experimentation only, and do not assume that the entire derived dataset can be redistributed or used commercially under a single permissive license.

## Relationship to MyVoiceTyping

This dataset was prepared to support the MyVoiceTyping local text cleanup model:

- App: <https://github.com/botaruibo/MyVoiceTyping>
- Model: <https://modelscope.cn/models/botaruibo/MyVoiceTyping-1.5b-q4>

The app code, model artifacts, and dataset may have different license or usage terms.

## Reporting license issues

If you are an upstream dataset author or notice an incorrect source / license entry, please open an issue with:

- the source name;
- the relevant upstream link;
- the license or usage term that should be reflected;
- any citation or redistribution requirement.
