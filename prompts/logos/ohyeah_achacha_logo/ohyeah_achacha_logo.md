
# OhYeah AchaAcha Logo Prompt

## Character Brief

- Channel: オーイェーのアチャチャチャンネル (OhYeahAchacha)
- Direction: pop-style channel logo with bold outlines for high visibility at any size
- Mood: lively, fun, energetic — fits a variety entertainment YouTube channel
- Keep: thick stroke outlines on all elements, transparent background, simple bold shapes
- Avoid: photorealistic textures, thin hairline strokes, busy backgrounds, drop shadows only (prefer outlines)

## Positive Prompt

```text
masterpiece, best quality, channel logo design, pop art style, bold thick outlines, vibrant colors, high contrast, transparent background, clean vector-like illustration, flat shading, cheerful energetic mood, readable at small size, versatile layout, no background, cutout style, anime-inspired lettering, bright saturated palette
```

## Negative Prompt

```text
photorealistic, realistic texture, 3d render, drop shadow only, thin strokes, busy background, gradient background, white background, black background, watermark, signature, cluttered composition, muted colors, low contrast, blur, noise
```

## Color Variation Targets

| Variant | Description |
| --- | --- |
| `full_color` | Default bright palette (yellow, orange, red accents) |
| `monochrome` | Single-color outline suitable for white or black backgrounds |
| `white_on_dark` | White fill with dark outline for dark overlays |

## Size Targets

| Name | Resolution | Use Case |
| --- | --- | --- |
| `1x` | 512×512 | Small icon / avatar |
| `2x` | 1024×1024 | Standard use |
| `banner` | 1920×480 | YouTube channel art / banner |

## Recommended Settings

- Sampler: DPM++ 2M Karras
- Steps: 28
- CFG: 7.0
- Denoise: 1.0 (txt2img)
- Resolution: 1024×1024 (then scale/crop per size target)
- Seed: random during exploration, lock once the composition is satisfying

## Workflow Notes

- Use txt2img first to explore compositions; switch to img2img for refinement passes.
- Enable alpha channel output (transparent background) in the SaveImage node or via post-processing.
- For LoRA fine-tuning, collect 15–30 reference images with consistent style, then train with `network_dim=32` as a starting point.
- Color variants can be produced by img2img with a low denoise (0.30–0.40) and a palette-specific prompt appended.
- Size variants should be exported from the same seed by changing only the target resolution or via upscale nodes.
