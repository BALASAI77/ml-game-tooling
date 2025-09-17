# ML Tooling for Game Development: Write-Up

## Model and Tool Choices
For the text-to-3D generator, I used OpenAI’s [Shap-E](https://github.com/openai/shap-e), a diffusion-based model chosen for its ability to generate game-ready 3D assets (OBJ, GLB, PLY) from text prompts on CPU, ensuring accessibility without GPU requirements. Its support for visualization (PNG, GIF) and game-compatible formats made it ideal for this assignment. For the fantasy quest generator, I selected Hugging Face’s `distilgpt2`, a lightweight NLP model that balances performance and efficiency, suitable for generating coherent quest narratives (~100–200 words) on CPU in ~2–5 seconds. Both models align with the assignment’s focus on CPU-friendly, game-relevant ML tooling.

## Parameters Tested
- **Text-to-3D (Shap-E)**:
  - **Prompts**: “a sword” vs. “a fantasy sword” to test specificity.
  - **Guidance Scale**: 10.0, 15.0 to balance prompt adherence and diversity.
  - **Steps**: 32, 64 to evaluate quality vs. runtime trade-offs.
  - **Seed**: 42, 100 to explore output variation.
- **Quest Generator (distilgpt2)**:
  - **Prompts**: “In a mystical forest, a brave warrior embarks on a quest to find a hidden relic” and “A legendary sword hidden in a cursed mountain awaits a hero.”
  - **Temperature**: 0.7, 1.2 to adjust creativity vs. coherence.
  - **Max Length**: 100, 200 to control output length.
  - **Seed**: 42, 200 to vary narrative style.

## Observed Differences
- **Text-to-3D**:
  - Higher guidance (15.0) produced models closer to the prompt (e.g., “a fantasy sword” had ornate details) but reduced diversity compared to 10.0. Increasing steps from 32 to 64 improved mesh quality (smoother surfaces, ~10k faces) but doubled runtime (~5 min to ~10 min on CPU). Different seeds (42 vs. 100) altered details like sword hilt design. Specific prompts yielded more detailed models than generic ones.
  - Metrics: Generated meshes had ~8k–12k faces, were watertight, and imported successfully into Blender/Unity.
- **Quest Generator**:
  - Higher temperature (1.2) increased creativity (e.g., vivid but less coherent quests) but risked truncation (~11 words in some cases). Lower temperature (0.7) ensured coherent narratives (~100–180 words). Longer max_length (200) produced detailed quests but occasionally truncated early. Different seeds varied tone (e.g., heroic vs. mysterious).
  - Metrics: Perplexities ranged from ~13 (coherent) to ~286 (short/vague), with word counts suitable for game UI.

## Future Improvements
With more time/resources:
- **Text-to-3D**: Implement mesh simplification using `trimesh` to reduce face count (~3k) for game optimization. Add a FastAPI endpoint for async generation. Automate LOD generation and texture baking for Unity integration.
- **Quest Generator**: Fine-tune `distilgpt2` on a fantasy dataset for richer narratives. Structure outputs as JSON for direct game engine import. Add automated coherence metrics (e.g., BLEU scores).
- **General**: Create side-by-side visualizations of parameter effects and integrate both tools into a unified API with a job queue for scalable generation.

This project demonstrates practical ML tooling for game development, with robust, CPU-friendly solutions and clear parameter impacts, laying a foundation for further optimization and integration.