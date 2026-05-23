# OhYeah Achacha Logo

オーイェーのアチャチャチャンネル用ロゴを ComfyUI で生成する手順書です。

## 前提条件

ComfyUI のセットアップ手順は [リポジトリ README](../../../README.md#comfyui-setup-commands) を参照してください。

## チェックポイントのおすすめDL方法

このワークフローは 1024×1024 生成前提なので、まずは SDXL 系のアニメ / イラスト向けチェックポイントを 1 つ入れるのがおすすめです。

### 推奨: CounterfeitXL を Hugging Face CLI でDLする

`uv` が使える環境なら、`hf` コマンドを常設インストールせず `uvx hf` でDLできます。

```sh
uvx hf download Simplicity-Ai/CounterfeitXL \
  CounterfeitXL_V2.5.safetensors \
  --local-dir "$COMFY_DIR/models/checkpoints"
```

DL後、ComfyUI を再起動するかブラウザを更新し、**Load Checkpoint** ノードで
`CounterfeitXL_V2.5.safetensors` を選択してください。

### 代替: AnythingXL をブラウザでDLする

Civitai から AnythingXL の `fp16 SafeTensor` をDLし、以下に配置します。

```sh
export COMFY_DIR="$HOME/ComfyUI"
mkdir -p "$COMFY_DIR/models/checkpoints"
cp ~/Downloads/*.safetensors "$COMFY_DIR/models/checkpoints/"

comfy launch
```

チェックポイントは `.ckpt` より `.safetensors` を優先してください。

## 生成手順

### 1. ワークフローを読み込む

ComfyUI の **Load** ボタンから以下を読み込む。

```
workflows/logos/ohyeah_achacha_logo_txt2img_api.json
```

### 2. チェックポイントを設定する

ワークフロー内の **Load Checkpoint** ノードで、使用するモデルファイル名を選択する。

> デフォルト値は `put_your_anime_checkpoint_here.safetensors` (プレースホルダー)

### 3. 生成を実行する

**Queue Prompt** を押して実行する。  
生成された画像は ComfyUI の output フォルダ内 `ohyeah_achacha_logo/` に保存される。

### 4. 構図を確定する

気に入った結果が出たら **KSampler** ノードの seed 値を固定する。

### 5. 成果物を配置する

生成画像を `assets/logos/ohyeah_achacha_logo/` にコピーして管理する。

推奨ファイル名:

- `assets/logos/ohyeah_achacha_logo/ohyeah_achacha_logo_v001.png`
- `assets/logos/ohyeah_achacha_logo/ohyeah_achacha_logo_v002.png`
- `assets/logos/ohyeah_achacha_logo/ohyeah_achacha_logo_final.png`

### 6. 再現性メモを残す

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

## コミット前チェック

- ワークフローJSONが `workflows/logos/ohyeah_achacha_logo_txt2img_api.json` に保存されている。
- プリセットJSONが `prompts/logos/ohyeah_achacha_logo/ohyeah_achacha_logo_preset.json` に保存されている。
- 最終候補のロゴ画像が `assets/logos/ohyeah_achacha_logo/` に保存されている。
- README の生成手順が実際のワークフローと一致している。
