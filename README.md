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
└── workflows/                     # ComfyUI workflow files
    ├── characters/
    └── logos/
```

## Materials

- [Logo](workflows/logos/README.md)

## Environment

| Tool | Purpose |
| --- | --- |
| [ComfyUI](https://github.com/comfyanonymous/ComfyUI) | Node-based image generation UI |
| [Stable Diffusion](https://stability.ai/) | Image generation model |

## Usage

### Install & Launch

```sh
uv tool install comfy-cli
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.zshrc
source ~/.zshrc
comfy install

comfy launch
```

<http://127.0.0.1:8188>
