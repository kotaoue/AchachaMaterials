# AchachaMaterials

A repository for managing materials used in the [OhYeahAchacha](https://www.youtube.com/@OhYeahAchacha) YouTube channel.

---

## Directory Structure

```text
AchachaMaterials/
├── assets/
│   ├── characters/
│   │   └── <character_name>/
│   │       ├── base/
│   │       └── expressions/
│   ├── logos/
│   ├── backgrounds/
│   └── props/
├── workflows/
├── prompts/
```

- `assets/`: Root directory for all assets
- `characters/`: Character assets
- `base/`: Base images
- `expressions/`: Facial expression variants
- `logos/`: Logo assets
- `backgrounds/`: Background assets
- `props/`: Prop assets
- `workflows/`: ComfyUI workflow JSON files
- `prompts/`: Stable Diffusion prompts

---

## Usage

### Generating Facial Expressions

1. Set up [ComfyUI](https://github.com/comfyanonymous/ComfyUI).
2. Load a `.json` workflow file from the `workflows/` directory into ComfyUI.
3. Refer to prompts in the `prompts/` directory to adjust generation parameters.
4. Save generated images to the appropriate `assets/characters/<name>/expressions/` folder.

---

## Environment

| Tool | Purpose |
| --- | --- |
| [ComfyUI](https://github.com/comfyanonymous/ComfyUI) | Node-based image generation UI |
| [Stable Diffusion](https://stability.ai/) | Image generation model |

---

## License

See the `LICENSE` file in each directory for the license of individual assets.
