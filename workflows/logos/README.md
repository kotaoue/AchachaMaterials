# OhYeah Achacha Logo

オーイェーのアチャチャチャンネル用ロゴを ComfyUI で生成する手順書です。

## Install

### Fonts

```sh
comfy env
export COMFY_DIR="$HOME/Documents/comfy/ComfyUI"

mkdir -p "$COMFY_DIR/fonts"
curl -L "https://fonts.google.com/download?family=RocknRoll+One" -o ./rocknroll.zip
unzip -j ./rocknroll.zip "RocknRollOne-Regular.ttf" -d "$COMFY_DIR/fonts/"
rm ./rocknroll.zip
```

### Model

```sh
comfy env
export COMFY_DIR="$HOME/Documents/comfy/ComfyUI"

uvx hf download Simplicity-Ai/CounterfeitXL CounterfeitXL_V2.5.safetensors --local-dir "$COMFY_DIR/models/checkpoints"
```

## 生成手順

### 再現性メモを残す

採用候補が決まったら、以下の値を `ohyeah_achacha_logo_preset.json` またはこの README に反映する。

- チェックポイント名
- Seed
- Steps
- CFG
- Sampler / Scheduler
- Image size

## バリエーション生成

### カラーバリエーション

気に入った seed を固定した状態で img2img に切り替え、denoise を `0.30–0.40` に下げ、  
**Positive Prompt** の末尾に以下を追記して再生成する。

| バリアント | 追記するプロンプト |
| --- | --- |
| `full_color` | `vibrant yellow orange red palette, saturated colors` |
| `monochrome` | `single color, monochrome, grayscale outline` |
| `white_on_dark` | `white fill, dark thick outline, high contrast` |

### サイズバリエーション

同一 seed のまま **Empty Latent Image** ノードの解像度を変更して再生成する。

| 用途 | 解像度 |
| --- | --- |
| アイコン / アバター | 512×512 |
| 標準 | 1024×1024 |
| バナー | 1920×480 |
