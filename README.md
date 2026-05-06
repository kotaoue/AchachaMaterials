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
comfy install

COMFY_DIR="$(find "$HOME" -type d -name ComfyUI 2>/dev/null | head -n 1)"
echo "$COMFY_DIR"

cp ~/Downloads/model.safetensors "$COMFY_DIR/models/checkpoints/"

```

### Generating Facial Expressions

1. Start ComfyUI.

   ```bash
   comfy launch
   ```

1. Open `http://127.0.0.1:8188` in your browser.
1. Pick a character folder under `assets/characters/` and prepare a reference image if you want the design to inherit an existing icon or avatar.
1. Import a `.json` workflow file from the `workflows/` directory into ComfyUI.

   GUI example:

   - Click `Load` in the top menu.
   - Select a workflow JSON from this repository.
   - Confirm that nodes such as `CheckpointLoaderSimple`, `LoadImage`, `CLIPTextEncode`, and `KSampler` appear on the canvas.

1. Refer to prompts in the `prompts/` directory and adjust the prompt text, seed, CFG, steps, and denoise values.
1. Click `Queue Prompt` to generate an image.
1. Save generated images to the appropriate `assets/characters/<name>/base/` or `assets/characters/<name>/expressions/` folder.

### Example: `chiken`

- Reference image: `assets/characters/chiken/reference/kotaoue-icon.png`
- Prompt guide: `prompts/characters/chiken/chiken_relaxed_yukkuri.md`
- Prompt preset JSON: `prompts/characters/chiken/chiken_relaxed_yukkuri_preset.json`
- Workflow template: `workflows/characters/chiken/chiken_relaxed_yukkuri_img2img_api.json`

Suggested flow:

1. Copy the reference image into the ComfyUI input directory.

   Example:

   ```bash
   cp assets/characters/chiken/reference/kotaoue-icon.png /path/to/ComfyUI/input/
   ```

2. In the ComfyUI browser tab, click `Load` and open `workflows/characters/chiken/chiken_relaxed_yukkuri_img2img_api.json`.
3. Click the `CheckpointLoaderSimple` node and set `ckpt_name` to your installed anime-oriented checkpoint.

   Example values:

   - `anything-v5.safetensors`
   - `meinamix.safetensors`
   - `animagine-xl.safetensors`

4. Click the `LoadImage` node and confirm that `kotaoue-icon.png` is selected. If it is not shown, choose the file manually from the ComfyUI input folder.
5. Open `prompts/characters/chiken/chiken_relaxed_yukkuri_preset.json` and copy the `positive` and `negative` prompt strings into the two `CLIPTextEncode` nodes.
6. In the `KSampler` node, start with the following values.

   - `seed`: `0` for random exploration, then reuse a fixed seed once you get a good base face
   - `steps`: `28`
   - `cfg`: `6.5`
   - `sampler_name`: `dpmpp_2m`
   - `scheduler`: `karras`
   - `denoise`: `0.48`

7. Click `Queue Prompt`.
8. Review the output image.

   - If the face is too different from the icon, lower `denoise` to `0.40` to `0.45`.
   - If the image looks too realistic, lower `cfg` to around `5.5` and add `simple mascot design` to the positive prompt.
   - If the expression is too weak, raise `denoise` to around `0.55` and append one variant such as `cheerful expression` or `wry smile`.

9. When you get a good base portrait, save it to `assets/characters/chiken/base/`.
10. For expression variations, keep the same checkpoint and seed, then append one of the expression variant prompts from `prompts/characters/chiken/chiken_relaxed_yukkuri.md` and save the outputs to `assets/characters/chiken/expressions/`.

## License

See the `LICENSE` file in each directory for the license of individual assets.
