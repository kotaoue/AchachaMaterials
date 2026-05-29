# Achacha Logo Style Adjust

清書済みの基準ロゴ画像から、色合い、質感、雰囲気のバリエーションを作る workflow です。

## 目的

この段階では字形を作り直さない。基準画像の読みやすさを維持したまま、採用候補を増やす。

- 入力: `01-sketch-cleanup` で作った基準ロゴ画像
- 出力: 色・雰囲気違いのロゴ画像
- 推奨 denoise: `0.18-0.35`
- 字形優先の場合: `0.18-0.25`
- 雰囲気優先の場合: `0.28-0.35`

## Input

ComfyUI の input フォルダに、基準画像を `achacha_logo_base.png` として置く。

基準画像は `01-sketch-cleanup` の採用候補から選ぶ。

## Workflow

- [achacha_logo_style_adjust.json](achacha_logo_style_adjust.json)

処理の流れ:

1. `Load Base Logo` で基準画像を読み込む。
2. `Encode Base Logo` で img2img 用の latent にする。
3. `Style Adjust Sampler` で低 denoise の再生成を行う。
4. `Save Styled Logo` でバリエーションを書き出す。

## Presets

`Positive Prompt` の末尾に追記して使う。

| バリアント | 追記するプロンプト | denoise |
| --- | --- | --- |
| `full_color` | `vibrant yellow orange red palette, saturated pop colors, lively sticker logo` | `0.25-0.32` |
| `retro_tv` | `retro Japanese TV show logo, warm halftone texture, playful broadcast graphics` | `0.28-0.35` |
| `clean_flat` | `clean flat vector logo, crisp outline, limited color palette, print-ready finish` | `0.18-0.26` |
| `monochrome` | `single color logo, monochrome ink, bold readable outline` | `0.18-0.28` |
| `white_on_dark` | `white fill, dark thick outline, high contrast, night mode logo` | `0.22-0.30` |

## 調整メモ

| 症状 | 調整 |
| --- | --- |
| 文字が変形する | `denoise` を下げる、negative prompt に `warped text` を足す |
| 色だけ変えたい | `denoise` を `0.18-0.22` にする |
| 絵柄を強めたい | `denoise` を `0.30-0.35` にする |
| 背景が出る | negative prompt に `background, scene, frame` を足す |

## 採用候補メモ

| 項目 | 値 |
| --- | --- |
| Checkpoint | `CounterfeitXL_V2.5.safetensors` |
| Source image | `achacha_logo_base.png` |
| Seed | |
| Steps | `24` |
| CFG | `5.5` |
| Sampler / Scheduler | `dpmpp_2m / karras` |
| Denoise | `0.26` |
