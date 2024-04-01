# Experiments with TinyLlama

## Training Data Options

### Interesting HF Organizations with Data

- [Argilla](https://huggingface.co/argilla)
- [Hugging Face H4](https://huggingface.co/HuggingFaceH4)
- [Intel](https://huggingface.co/Intel)

### SFT Data

- [teknium/OpenHermes-2.5](https://huggingface.co/datasets/teknium/OpenHermes-2.5)
- [HuggingFaceH4/ultrachat_200k](https://huggingface.co/datasets/HuggingFaceH4/ultrachat_200k)
- [HuggingFaceH4/no_robots](https://huggingface.co/datasets/HuggingFaceH4/no_robots) - CC BY-NC 4.0
- [Open-Orca/OpenOrca](https://huggingface.co/datasets/Open-Orca/OpenOrca) - MIT
- [Anthropic/hh-rlhf](https://huggingface.co/datasets/Anthropic/hh-rlhf) - MIT
- [berkeley-nest/Nectar](https://huggingface.co/datasets/berkeley-nest/Nectar) - Apache 2.0
- [openbmb/UltraFeedback](https://huggingface.co/datasets/openbmb/UltraFeedback) - MIT

### DPO Data

- [argilla/OpenHermes2.5-dpo-binarized-alpha](https://huggingface.co/datasets/argilla/OpenHermes2.5-dpo-binarized-alpha)
- [HuggingFaceH4/ultrafeedback_binarized](https://huggingface.co/datasets/HuggingFaceH4/ultrafeedback_binarized)
- [argilla/dpo-mix-7k](https://huggingface.co/datasets/argilla/dpo-mix-7k)

## Benchmarks and Leaderboards

  - <https://huggingface.co/spaces/mlabonne/Yet_Another_LLM_Leaderboard>
  - <https://github.com/mlabonne/llm-autoeval>
  - <https://github.com/huggingface/lighteval>

## Own Datasets

### PhilipMay/ultrachat_200k_convert_2048

This dataset is created with [`01_convert_ultrachat_200k.ipynb`](https://github.com/PhilipMay/TinyLlama-experiments/blob/main/01_convert_ultrachat_200k.ipynb) and
[`02_convert_ultrachat_200k_test.ipynb`](https://github.com/PhilipMay/TinyLlama-experiments/blob/main/02_convert_ultrachat_200k_test.ipynb)
based on [HuggingFaceH4/ultrachat_200k](https://huggingface.co/datasets/HuggingFaceH4/ultrachat_200k)
(train_sft and test_sft).

The dataset can be found on Hugging Face:
[PhilipMay/ultrachat_200k_convert_2048](https://huggingface.co/datasets/PhilipMay/ultrachat_200k_convert_2048)

Main changes:

- convert to conversations format which is supported by [Axolotl](https://github.com/OpenAccess-AI-Collective/axolotl) - see [sharegpt](https://github.com/OpenAccess-AI-Collective/axolotl?tab=readme-ov-file#conversation)
- clean invisible characters and strip - see
[`mltb2.text.clean_all_invisible_chars_and_strip()`](https://telekom.github.io/mltb2/api-reference/text.html#mltb2.text.clean_all_invisible_chars_and_strip)
- remove rows with empty text
- remove conversations longer than 2048 TinyLlama tokens

### PhilipMay/berkeley_nest_nectar_convert_2048

This dataset is created with [`04_convert_nectar.ipynb`](https://github.com/PhilipMay/TinyLlama-experiments/blob/main/04_convert_nectar.ipynb) based on
[berkeley-nest/Nectar](https://huggingface.co/datasets/berkeley-nest/Nectar).

Main changes:

- convert to conversations format which is supported by [Axolotl](https://github.com/OpenAccess-AI-Collective/axolotl) - see [sharegpt](https://github.com/OpenAccess-AI-Collective/axolotl?tab=readme-ov-file#conversation)
- only use rank 1 answers
- clean invisible characters and strip - see
[`mltb2.text.clean_all_invisible_chars_and_strip()`](https://telekom.github.io/mltb2/api-reference/text.html#mltb2.text.clean_all_invisible_chars_and_strip)
- remove rows with empty text
- remove rows from multiple sources (see `source` column)
- remove conversations longer than 2048 TinyLlama tokens

## Axolotl Setup

TODO: add docker command

After docker startup I do:

```bash
git -C /workspace/axolotl fetch origin
git -C /workspace/axolotl checkout 5cf226e
pip install -U -e /workspace/axolotl
export BNB_CUDA_VERSION=
export WANDB_API_KEY=_MY_API_KEY_
```

Start the training (example):

```bash
accelerate launch -m axolotl.cli.train ./persist/training_01/tiny_llama_02.yml
```

## Licensing

Copyright (c) 2024 [Philip May](https://may.la/)

Licensed under the **MIT License** (the "License"); you may not use this file except in compliance with the License.
You may obtain a copy of the License by reviewing the file
[LICENSE](https://github.com/PhilipMay/TinyLlama-experiments/blob/main/LICENSE) in the repository.
