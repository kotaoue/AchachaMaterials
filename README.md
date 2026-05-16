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

### Setup Comfy

```sh
uv tool install comfy-cli

export PATH="$HOME/.local/bin:$PATH"
comfy install
```

### Generating Facial Expressions

1. Setup.

   Example (`chiken`):

   ```bash
   export COMFY_DIR="/Users/kotaoue/Documents/comfy/ComfyUI"
   cp assets/characters/chiken/reference/kotaoue-icon.png "$COMFY_DIR/input/"
   ```

```sh
comfy launch
```

Open <http://127.0.0.1:8188>.

1. Click `Load` and open the workflow JSON from `workflows/characters/<character>/`.
2. Click the `CheckpointLoaderSimple` node and set `ckpt_name` to your installed checkpoint (e.g., `anything-v5.safetensors`, `meinamix.safetensors`, `animagine-xl.safetensors`).
3. Click the `LoadImage` node and confirm that your reference image is selected.
4. Open the prompt preset JSON from `prompts/characters/<character>/` and copy the `positive` and `negative` strings into the two `CLIPTextEncode` nodes.

**Generation:**

1. In the `KSampler` node, adjust the parameters:

   - `seed`: `0` for exploration, then fix once satisfied
   - `steps`: `28`
   - `cfg`: `6.5`
   - `sampler_name`: `dpmpp_2m`
   - `scheduler`: `karras`
   - `denoise`: `0.48`

2. Click `Queue Prompt`.

**Review & Adjust:**

1. Review the output image and adjust if needed:

   - Too different from reference → lower `denoise` to `0.40–0.45`
   - Too realistic → lower `cfg` to `5.5` and add `simple mascot design` to positive prompt
   - Expression too weak → raise `denoise` to `0.55` and append `cheerful expression` or similar

2. Save base portrait to `assets/characters/<character>/base/`.
3. For expressions, keep the same checkpoint and seed, append variant prompts from the prompt guide, and save to `assets/characters/<character>/expressions/`.

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

## Links

- [ComfyUI](https://github.com/comfyanonymous/ComfyUI)
- [huggingface](https://huggingface.co/)
