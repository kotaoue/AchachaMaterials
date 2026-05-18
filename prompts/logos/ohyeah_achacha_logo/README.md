# OhYeah AchaAcha Logo

オーイェーのアチャチャチャンネル用ロゴを ComfyUI で生成する手順書です。

---

## ファイル構成

| パス | 内容 |
| --- | --- |
| `prompts/logos/ohyeah_achacha_logo/ohyeah_achacha_logo_preset.json` | プロンプト・生成パラメータのプリセット |
| `workflows/logos/ohyeah_achacha_logo_txt2img_api.json` | ComfyUI API 用ワークフロー |
| `assets/logos/ohyeah_achacha_logo/` | 生成済み画像の保存先 |

---

## 前提条件

- ComfyUI が起動していること
- アニメ / イラスト系チェックポイントが ComfyUI の `models/checkpoints/` に配置済みであること  
  (例: ToonYou, CounterfeitXL, AnythingXL など)

---

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

---

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

3. **img2img** (denoise 低め) で細部を調整する
2. SaveImage ノードまたは後処理でアルファチャンネル (透過背景) を有効にして書き出す
3. サイズターゲットに合わせてスケール・クロップして納品する
