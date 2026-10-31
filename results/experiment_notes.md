# Experiment notes

- Environment: Kaggle, Tesla T4 GPU.
- Dataset pairs loaded: 50,731.
- After filtering: 50,517.
- Split: 40,443 train / 5,060 validation / 5,014 test.
- Basic Transformer: 15 epochs, 22.37 minutes, best validation loss 4.2985.
- mT5-small: 5,000 training pairs, 1 epoch, 5.06 minutes, validation loss 2.9183.
- LLaMA and Gemma loading failed with HTTP 401 gated-repository access errors; no evaluation was performed.
- Results are reconstructed from the actual outputs recorded during the conversation. No model was rerun during repository packaging.
