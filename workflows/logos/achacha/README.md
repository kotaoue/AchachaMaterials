# OhYeah Achacha Logo

オーイェーのアチャチャチャンネル用ロゴを ComfyUI で生成する手順書です。

## 方針

「文字列とフォントを ComfyUI 内で指定し、LoRA やプロンプトでロゴ文字を直接生成する」方針は、このロゴでは採用しない。

理由:

- 日本語の正確な文字列、字間、行間、太さを拡散モデルに任せると、再生成のたびに字形が崩れやすい。
- フォント描画ノードで文字を重ねることはできるが、ロゴとしての手書き感、字形の誇張、文字同士の噛み合わせは別工程で調整が必要になる。
- このロゴの重要部分は「オーイェーのアチャチャチャンネル」という読める文字そのものなので、文字の形は画像入力で固定し、生成モデルは清書と雰囲気調整に使うほうが安定する。

そのため、正式な運用は次の 2 段に分ける。

| 段階 | 目的 | Workflow |
| --- | --- | --- |
| 1 | 手書き下書きを清書して基準画像を作る | [01-sketch-cleanup](01-sketch-cleanup/) |
| 2 | 基準画像の色合いや雰囲気を調整する | [02-style-adjust](02-style-adjust/) |

既存の [achacha_logo.json](achacha_logo.json) は、文字を入れない土台や方向性を探る試作用として残す。

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

### 推奨フロー

1. 紙または画像編集ツールで「オーイェーのアチャチャチャンネル」の下書きを作る。
2. `01-sketch-cleanup` でロゴとして読める基準画像を作る。
3. 採用した基準画像を `02-style-adjust` に入れ、色合い、質感、雰囲気の差分を作る。
4. 採用候補の Seed とパラメータを README に残す。

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
