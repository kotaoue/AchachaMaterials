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

```sh
# install
uv tool install comfy-cli
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.zshrc
source ~/.zshrc
comfy install
```

```sh
# setup. example
export COMFY_DIR="$HOME/ComfyUI"
cp your_model.safetensors "$COMFY_DIR/models/checkpoints/"
cp assets/characters/your_character/reference/your_reference_image.png "$COMFY_DIR/input/"
```

```sh
# launch
comfy launch

```

<http://127.0.0.1:8188>

### Generating Facial Expressions

1. Run the setup commands above.
2. Load a `.json` workflow file from the `workflows/` directory into ComfyUI.
3. Refer to prompts in the `prompts/` directory to adjust generation parameters.
4. Save generated images to the appropriate `assets/characters/<name>/expressions/` folder.

### Generating Logos (ComfyUI)

Logo-specific generation steps live under `prompts/logos/<logo_name>/`.

Current logo guides:

- [OhYeah AchaAcha Logo](prompts/logos/ohyeah_achacha_logo/README.md)

Generated logo images should be stored under `assets/logos/<logo_name>/`, and ComfyUI workflows should be stored under `workflows/logos/`.

## License

See the `LICENSE` file in each directory for the license of individual assets.
