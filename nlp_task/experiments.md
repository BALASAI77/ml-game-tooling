# Project Write-Up

## Model/Tool Used and Why
Used `distilgpt2` from Hugging Face's `transformers`. It's lightweight (82M parameters), runs fast on CPU (~2-5s per generation in Colab), and suits game text generation (quests, lore). Alternatives like full GPT-2 are too heavy for CPU; fine-tuned fantasy models need more data/setup.

## Input Parameters Tested
- **Seed**: 42 vs. 200 for output variation.
- **Temperature**: 0.7-0.8 (balanced) vs. 1.2 (creative).
- **Max Length**: 100 (short) vs. 200 (detailed).

## Differences Observed
- Higher temperature (1.2) produced more creative but less coherent text (e.g., unusual plot twists vs. baseline's logical quest).
- Different seeds shifted narrative focus (e.g., exploration vs. combat scenarios).
- Longer max_length added detail but risked repetition, runtime increased (~2s to ~5s).
- Metrics: Word counts (80-180 words); perplexity lower (~20-30) for balanced params, higher (~40) for high temp.

## Validation/Metrics
- Word count checked for game UI fit (100-200 words ideal).
- Perplexity as coherence proxy (lower = better).
- Outputs importable as text in Unity/Blender (e.g., via ScriptableObjects).

## What I'd Do Next
Fine-tune on fantasy dataset (e.g., D&D quests from Kaggle). Add keyword extraction for quest objectives. With resources: Implement RQ queue for batch jobs or try CPU-optimized Stable Diffusion for 2D sprites.

## Extras
- Experiments saved in nlp_task/ folder with side-by-side comparisons.
- Validation includes word count and perplexity for game usability.
