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
├── workflows/                     # ComfyUI workflow JSON files
└── prompts/                       # Stable Diffusion prompts
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

**Setup:**

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

## License

See the `LICENSE` file in each directory for the license of individual assets.
