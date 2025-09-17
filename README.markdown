# COLLAB LINKS:
#Text_to3d_model:
https://colab.research.google.com/drive/1KxiHZelc3icE-rb9b6ZBa6L6HNjPd5At?usp=sharing

#Quest_generator:
https://colab.research.google.com/drive/1O_9YR7z1k9-UZcZSVo1v4Y7yBG1ofGe3?usp=sharing

# ML Tooling for Game Development: Text-to-3D and Fantasy Quest Generator

This project, developed for the "Hiring Assignment – ML Tooling for Game Development," includes two components: a **Text-to-3D Model Generator** using OpenAI's [Shap-E](https://github.com/openai/shap-e) to create game-ready 3D assets (OBJ, GLB, PLY) with animated GIF visualizations, and a **Fantasy Quest Generator** using Hugging Face's `distilgpt2` to produce quest narratives for game integration. Both tools are CPU-friendly, support parameter experimentation (e.g., seed, guidance scale, temperature), and include interactive interfaces, sample outputs, and metrics for game compatibility, hosted in a GitHub repository with comprehensive documentation.

## Repository Structure
```
ml-game-tooling/
├── README.md
├── requirements.txt
├── writeup.md
├── text_to_3d/
│   ├── generate_3d_interactive.py
│   ├── outputs/
│   │   ├── a_sword_gs15.0_steps64_seed42_0.obj
│   │   ├── a_sword_gs15.0_steps64_seed42_0.glb
│   │   ├── a_sword_gs15.0_steps64_seed42_0.png
│   │   ├── a_sword_gs15.0_steps64_seed42_0.gif
├── nlp_task/
│   ├── ML_Game_Tooling_Assignment_NLP.ipynb
│   ├── quest1.txt
│   ├── quest2.txt
│   ├── experiment_1.txt
│   ├── experiment_2.txt
│   ├── experiment_3.txt
│   ├── experiment_4.txt
│   ├── experiments.md
```

## Features
- **Text-to-3D Generation**:
  - Converts text prompts (e.g., "a sword") into 3D models using Shap-E’s diffusion model.
  - Outputs OBJ, GLB, PLY files for Unity/Blender, plus 128x128 PNG/GIF visualizations (360° views).
  - Interactive CLI for prompts and parameters (guidance scale, steps, seed).
  - Metrics: vertex/face counts, watertight status.
- **Fantasy Quest Generation**:
  - Generates quest narratives using `distilgpt2` for game quest logs or dialogue systems.
  - Outputs text files (~11–200 words) with varied parameters (seed, temperature, max_length).
  - Metrics: word counts, perplexities for coherence.
- **Colab and Local Support**: Runs on CPU (~1–15 min for 3D, ~2–5s for text) or GPU for faster 3D generation.

## Setup
1. **Clone the Repository**:
   ```bash
   git clone <your-repo-url>
   cd ml-game-tooling
   ```
2. **Install Dependencies**:
   Create a virtual environment (optional):
   ```bash
   python -m venv venv
   source venv/bin/activate  # Windows: venv\Scripts\activate
   ```
   Install requirements:
   ```bash
   pip install -r requirements.txt
   ```
   `requirements.txt`:
   ```
   torch==2.0.1
   trimesh
   pillow
   transformers==4.56.1
   numpy==2.0.2
   ```
   The 3D script auto-installs `shap-e`.
3. **Run the Tools**:
   - **Text-to-3D**: `python text_to_3d/generate_3d_interactive.py`
   - **Quest Generator**: Run `nlp_task/ML_Game_Tooling_Assignment_NLP.ipynb` in Colab or locally.

## Usage
### Text-to-3D Generator
1. **Colab**:
   - Open [colab.research.google.com](https://colab.research.google.com), upload `generate_3d_interactive.py`.
   - Enable GPU (Runtime > Change runtime type > GPU) for ~1–2 min generation (vs. 5–15 min on CPU).
   - Run to start the interactive CLI.
2. **Local**:
   - Ensure Python 3.8+ and `git`. Run `python text_to_3d/generate_3d_interactive.py`.
3. **Interactive Prompt**:
   - Enter prompt (e.g., "a sword"), guidance scale (default: 15.0), steps (default: 64), seed (default: 42).
   - Outputs saved in `text_to_3d/outputs/` (OBJ, GLB, PLY, PNG, GIF).
   - Colab displays GIFs inline; locally, view in browser/image viewer.
4. **Exit**: Type `exit`.

### Fantasy Quest Generator
1. **Colab**:
   - Upload `nlp_task/ML_Game_Tooling_Assignment_NLP.ipynb` to Colab.
   - Run cells to install dependencies, generate quests, and run experiments.
2. **Local**:
   - Run the notebook with Jupyter or convert to `.py` for execution.
3. **Outputs**:
   - Two quests (`quest1.txt`, `quest2.txt`) for prompt: "In a mystical forest, a brave warrior embarks on a quest to find a hidden relic guarded by ancient spirits."
   - Four experiments (`experiment_1.txt`–`experiment_4.txt`) with prompt: "A legendary sword hidden in a cursed mountain awaits a hero," varying seed (42, 200), temperature (0.7–1.2), max_length (100, 200).
   - Download `nlp_task.zip` from Colab.

## Sample Outputs
- **Text-to-3D** (prompt: "a sword", guidance=15.0, steps=64, seed=42):
  - `text_to_3d/outputs/a_sword_gs15.0_steps64_seed42_0.obj`
  - `text_to_3d/outputs/a_sword_gs15.0_steps64_seed42_0.glb`
  - `text_to_3d/outputs/a_sword_gs15.0_steps64_seed42_0.png`
  - `text_to_3d/outputs/a_sword_gs15.0_steps64_seed42_0.gif`
- **Quest Generator**:
  - `nlp_task/quest1.txt`, `quest2.txt`: Quest narratives (~11–116 words).
  - `nlp_task/experiment_1.txt`–`experiment_4.txt`: Experiment outputs (~11–180 words).

## Parameter Observations
- **Text-to-3D**:
  - **Guidance Scale (10–15)**: Higher values align models closer to prompts but reduce diversity.
  - **Steps (32–64)**: More steps improve quality but increase runtime.
  - **Seed (e.g., 42, 100)**: Varies model details (e.g., sword ornamentation).
- **Quest Generator**:
  - **Temperature (0.7–1.2)**: Higher values increase creativity but risk incoherence.
  - **Max Length (100–200)**: Longer outputs provide detailed quests but may truncate early.
  - **Seed (42, 200)**: Alters narrative style and details.

## Metrics
- **Text-to-3D**: Vertex/face counts, watertight status via `trimesh`; tested for Unity/Blender import.
- **Quest Generator**: Word counts (~11–180), perplexities (~13–286, lower is more coherent).

## Troubleshooting
- **Text-to-3D**:
  - **Module Errors**: Restart Colab runtime, reinstall `trimesh`, `pillow`:
    ```bash
    pip uninstall trimesh pillow -y && pip install trimesh pillow --no-cache-dir
    ```
  - **Slow Generation**: Use Colab GPU or check internet for `shap-e` clone.
  - **Local Setup**: Install `libjpeg-dev`, `zlib1g-dev` (Ubuntu) or `libjpeg`, `zlib` (Mac).
- **Quest Generator**:
  - **Short Outputs**: Increase `max_length` to 250 or lower `temperature` to 0.6.
  - **Hugging Face Errors**: Clear cache (`!rm -rf ~/.cache/huggingface`) or restart runtime.

## Next Steps
- **Text-to-3D**: Add mesh simplification (~3k faces), API for async generation, Unity import tests.
- **Quest Generator**: Fine-tune `distilgpt2` on fantasy datasets, output JSON for game engines.
- **General**: Side-by-side parameter visualizations, automated metrics scripts.

## Requirements
- Python 3.8+
- `requirements.txt` (see above)
- `git` for `shap-e` cloning
- Optional: GPU for faster 3D generation

## License
MIT License. See [LICENSE](LICENSE).

## Acknowledgments
- [Shap-E](https://github.com/openai/shap-e) by OpenAI for 3D generation.
- [Hugging Face Transformers](https://huggingface.co/docs/transformers) for `distilgpt2`.
- Built for accessible ML tooling in game development.
