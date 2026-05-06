# Chiken Relaxed Yukkuri Prompt

## Character Brief

- Motif: kotaoue GitHub avatar icon
- Direction: relaxed anime illustration suitable for Yukkuri-style commentary videos
- Mood: low-tension, approachable, slightly blank but friendly expression
- Keep: simple silhouette, rounded face, readable expression at small size
- Avoid: realistic skin texture, complex costume details, sharp edgy lighting

## Positive Prompt

```text
masterpiece, best quality, anime illustration, relaxed mascot character, soft rounded face, simple eyes, small mouth, low-tension expression, friendly smile, fluffy dark hair, slightly messy short hair, casual hoodie, clean lineart, soft cel shading, muted colors, readable silhouette, streamer avatar style, yukkuri commentary friendly, front-facing portrait, upper body, plain background
```

## Negative Prompt

```text
photorealistic, realistic skin, 3d render, extra fingers, extra hands, bad anatomy, detailed wrinkles, overly dramatic lighting, horror, grotesque, text, watermark, logo, signature, cluttered background, sharp jawline, muscular body, old face, glossy latex, noisy details
```

## Expression Variants

### Neutral

```text
blank expression, relaxed eyes, tiny smile, calm mood
```

### Happy

```text
cheerful expression, closed smiling eyes, open smile, upbeat but soft mood
```

### Troubled

```text
wry smile, uneasy eyes, slightly tilted head, comedic awkwardness
```

## Recommended Settings

- Sampler: DPM++ 2M Karras
- Steps: 28
- CFG: 6.5
- Denoise: 0.45 to 0.55
- Resolution: 768x768
- Seed: random until the face shape stabilizes, then lock a seed for variants

## Workflow Notes

- Use the avatar image as the img2img source.
- Keep denoise below 0.6 so the icon motif remains visible.
- If the output becomes too realistic, lower CFG to 5.5 and add `simple mascot design` to the positive prompt.
- If the output loses the original face shape, lower denoise to around 0.4.
