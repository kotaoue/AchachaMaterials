# AchachaMaterials

A repository for managing materials used in the [OhYeahAchacha](https://www.youtube.com/@OhYeahAchacha) YouTube channel.

## Directory Structure

```text
AchachaMaterials/
├── assets/                        # Root directory for all assets
│   ├── characters/                # Character assets
│   │   └── <character_name>/
│   │       ├── base/              # Base images
│   │       └── expressions/       # Facial expression variants
│   ├── logos/                     # Logo assets
│   ├── backgrounds/               # Background assets
│   └── props/                     # Prop assets
├── workflows/                     # ComfyUI workflow files
│   ├── characters/
│   └── logos/
└── prompts/                       # Stable Diffusion prompts
 └── logos/
```

## Environment

| Tool | Purpose |
| --- | --- |
| [ComfyUI](https://github.com/comfyanonymous/ComfyUI) | Node-based image generation UI |
| [Stable Diffusion](https://stability.ai/) | Image generation model |

## Usage

### ComfyUI Setup Commands

Install `comfy-cli` and initialize ComfyUI:

```sh
uv tool install comfy-cli
export PATH="$HOME/.local/bin:$PATH"
comfy install
```

Set your ComfyUI directory (the folder created by `comfy install`) and place required files.
For `your_model.safetensors`, use an SD model checkpoint file that matches your workflow:

```sh
export COMFY_DIR="/home/<user>/ComfyUI"
cp sdxl_base.safetensors "$COMFY_DIR/models/checkpoints/"
cp assets/characters/<character>/reference/<reference_image>.png "$COMFY_DIR/input/"
```

Launch ComfyUI:

```sh
comfy launch
```

### Generating Facial Expressions

1. Run the setup commands above.
2. Load a `.json` workflow file from the `workflows/` directory into ComfyUI.
3. Refer to prompts in the `prompts/` directory to adjust generation parameters.
4. Save generated images to the appropriate `assets/characters/<name>/expressions/` folder.

### Generating Logos (ComfyUI)

1. Prepare model files in ComfyUI.
2. Open ComfyUI and load your logo workflow JSON.
3. Set logo concept prompts (main prompt and negative prompt).
4. Fix reproducibility parameters before generation:
    - Seed
    - Steps
    - CFG
    - Sampler / Scheduler
    - Image size
5. Generate draft variations and pick candidates.
6. Refine selected candidates by adjusting prompt, denoise strength, and style-related nodes.
7. Export final images and store them under `assets/logos/`.
8. Save reproducibility artifacts to this repository:
    - Workflow JSON: `workflows/logos/<logo_name>.json`
    - Prompt text: `prompts/logos/<logo_name>.txt`
    - Optional notes (seed, model, sampler): append to the same prompt file.

Recommended output naming:

- `assets/logos/<logo_name>/<logo_name>_v001.png`
- `assets/logos/<logo_name>/<logo_name>_v002.png`
- `assets/logos/<logo_name>/<logo_name>_final.png`

Checklist before commit:

- Workflow JSON is included in `workflows/logos/`.
- Prompt text is included in `prompts/logos/`.
- Final selected logo exists in `assets/logos/`.
- README instructions still match the actual generation flow.

## License

See the `LICENSE` file in each directory for the license of individual assets.
