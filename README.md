# Comparative Evaluation of English-to-Kannada Neural Machine Translation

This repository contains the code and currently available results for an academic comparison of encoder-decoder and decoder-only generative models for English-to-Kannada translation.

## Project status

Two model experiments completed in the Kaggle T4 environment:
- Basic Transformer (trained from scratch)
- mT5-small (fine-tuned)

LLaMA 3.2 1B Instruct and Gemma 3 1B IT were attempted but **not evaluated** because their Hugging Face repositories required gated access approval/authentication. No scores are reported for these models.

## Recorded results

| Model | Parameters | BLEU | chrF | Training time | Inference time |
|---|---:|---:|---:|---:|---:|
| Basic Transformer | 13,738,624 | 7.8193 | 30.5407 | 22.37 min | 70.25 sec |
| mT5-small | 300,176,768 | 1.2137 | 15.1282 | 5.06 min | 105.8 sec |
| LLaMA 3.2 1B Instruct | approx. 1.23B | — | — | — | — |
| Gemma 3 1B IT | approx. 1.0B | — | — | — | — |

**Evaluation note:** The Basic Transformer and mT5 values above were recorded from the same-subset evaluation cell in the Kaggle run. Inference times are the totals reported by that cell; they are not normalized per sentence.

## mT5 temperature analysis

| Temperature | BLEU | chrF |
|---:|---:|---:|
| 0.2 | 1.7609 | 17.3329 |
| 0.7 | 1.8810 | 21.9894 |
| 1.0 | 0.8287 | 18.9962 |

Temperature 0.7 produced the highest BLEU and chrF among the three tested settings.

## Dataset

The experiment used the Anuvaad Parallel Corpus, PIB English-Kannada data for 2017–2020 (government/news domain). The raw dataset is not included in this repository. Add or download it separately according to the dataset's source terms and the assignment instructions.

The recorded Kaggle preprocessing counts were:
- Original aligned sentence pairs: 50,731
- Retained after heuristic filtering: 50,517
- Removed: 214
- Train / validation / test: 40,443 / 5,060 / 5,014
- Shared SentencePiece BPE vocabulary: 16,000

## Basic Transformer configuration

- Encoder-decoder Transformer
- `d_model=256`, 4 attention heads
- 3 encoder layers and 3 decoder layers
- Feed-forward dimension 1,024
- Dropout 0.1
- 13,738,624 parameters
- 15 epochs; recorded training time 22.37 minutes
- Best validation loss: 4.2985

## mT5 configuration

- `google/mt5-small`
- 300,176,768 parameters
- Fine-tuned on 5,000 training pairs for one epoch
- Validation subset: 500 pairs
- Recorded training time: 5.06 minutes
- Mean training loss: 8.8338
- Validation loss: 2.9183

## Repository structure

```text
.
├── notebooks/
│   └── English_Kannada_MT_Kaggle.ipynb
├── results/
│   ├── model_comparison.csv
│   ├── mt5_temperature_analysis.csv
│   └── plots/
│       ├── bleu_comparison.png
│       ├── chrf_comparison.png
│       └── mt5_temperature_analysis.png
├── reports/
└── README.md
```

## Reproducing the experiment

1. Open the Kaggle notebook in `notebooks/`.
2. Attach the PIB English-Kannada dataset to the Kaggle notebook.
3. Enable a GPU accelerator.
4. Run the notebook cells in order.
5. For gated model experiments, first obtain access to the relevant Hugging Face model repositories and configure a Hugging Face read token as a Kaggle Secret named `HF_TOKEN`.

## Limitations and responsible reporting

- The dataset is limited to PIB/government-news language and should not be treated as representative of all English-Kannada translation.
- The reported mT5 metrics are substantially lower than the Basic Transformer metrics in this run. The generated translations should be manually inspected before drawing qualitative conclusions.
- LLaMA and Gemma are included in the intended comparison but were not evaluated because access was unavailable. They must not be assigned fabricated scores.
- The mT5 run used a 5,000-example training subset and a 500-example validation subset.
- Automatic metrics such as BLEU and chrF do not fully capture fluency, adequacy, cultural nuance, or factual correctness.

## Current artifact completeness

This is a starter repository assembled from the notebook and experiment outputs available at packaging time. The DOCX/PDF assignment report, raw dataset, trained checkpoints, and generated sample-translation file have not been added here. Add them only when those files are available.
