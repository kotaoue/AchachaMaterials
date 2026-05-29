# Achacha Logo Sketch Cleanup

手書きの「オーイェーのアチャチャチャンネル」下書きを清書し、後続工程の基準画像を作る workflow です。

## 目的

この段階では、色や雰囲気の追い込みよりも「読める字形」と「ロゴ全体の構図」を固定する。

- 入力: 手書き下書き画像
- 出力: 清書済みの基準ロゴ画像
- 推奨 denoise: `0.55-0.70`
- 推奨 ControlNet strength: `0.75-0.95`

## Install

### Model

親ディレクトリの README にある `CounterfeitXL_V2.5.safetensors` を使う。

### ControlNet

下書きの線を維持するため、SDXL 用の scribble ControlNet を使う。

```sh
comfy env
export COMFY_DIR="$HOME/Documents/comfy/ComfyUI"

uvx hf download xinsir/controlnet-scribble-sdxl-1.0 diffusion_pytorch_model.safetensors --local-dir "$COMFY_DIR/models/controlnet"
mv "$COMFY_DIR/models/controlnet/diffusion_pytorch_model.safetensors" "$COMFY_DIR/models/controlnet/xinsir-sdxl-scribble.safetensors"
```

## Input

ComfyUI の input フォルダに、下書き画像を `achacha_logo_sketch.png` として置く。

下書きの作り方:

- 白背景に濃い線で描く。
- 文字は「オーイェーの」「アチャチャ」「チャンネル」のように、行単位で読みやすく分ける。
- 線が細すぎる場合は、画像編集ツールで少し太らせてから入れる。
- 仕上げたい比率に近いキャンバスで描く。標準は `1344x832`。

## Workflow

- [achacha_logo_sketch_cleanup.json](achacha_logo_sketch_cleanup.json)

処理の流れ:

1. `Load Sketch` で下書き画像を読み込む。
2. `Sketch ControlNet` で線と構図を固定する。
3. `img2img Sampler` で清書する。
4. `Save Clean Base Logo` で基準画像を書き出す。

## 調整メモ

| 症状 | 調整 |
| --- | --- |
| 文字が崩れる | `ControlNet strength` を上げる、`denoise` を下げる |
| 下書きの粗さが残る | `denoise` を上げる、positive prompt に `clean polished outline` を足す |
| 絵柄が強すぎる | positive prompt から装飾語を減らす |
| 色が不要に変わる | `simple warm base colors` を `flat neutral logo colors` に変える |

## 採用候補メモ

| 項目 | 値 |
| --- | --- |
| Checkpoint | `CounterfeitXL_V2.5.safetensors` |
| ControlNet | `xinsir-sdxl-scribble.safetensors` |
| Seed | |
| Steps | `32` |
| CFG | `6.5` |
| Sampler / Scheduler | `dpmpp_2m / karras` |
| Denoise | `0.62` |
