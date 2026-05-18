# OhYeah AchaAcha Logo

**チャンネル:** オーイェーのアチャチャチャンネル (OhYeahAchacha)

YouTube チャンネルロゴを AI 生成するためのプリセットおよびワークフロー一式です。

---

## ディレクトリ構成

| ファイル | 内容 |
| --- | --- |
| `ohyeah_achacha_logo_preset.json` | 生成パラメータのプリセット (ComfyUI API 向け) |
| `ohyeah_achacha_logo.md` | プロンプト仕様書 (各項目の詳細説明) |

---

## デザイン方針

- **スタイル:** ポップアート・太いアウトライン・高コントラスト
- **ムード:** 明るく元気、バラエティ系 YouTube に合うエネルギッシュな雰囲気
- **背景:** 透過 (transparent background)
- **避けること:** フォトリアル、細い線、ごちゃついた背景、ドロップシャドウのみ

---

## プロンプト

### Positive

```
masterpiece, best quality, channel logo design, pop art style, bold thick outlines,
vibrant colors, high contrast, transparent background, clean vector-like illustration,
flat shading, cheerful energetic mood, readable at small size, versatile layout,
no background, cutout style, anime-inspired lettering, bright saturated palette
```

### Negative

```
photorealistic, realistic texture, 3d render, drop shadow only, thin strokes,
busy background, gradient background, white background, black background,
watermark, signature, cluttered composition, muted colors, low contrast, blur, noise
```

---

## 生成設定

| パラメータ | 値 |
| --- | --- |
| モデル推奨 | アニメ / イラスト系チェックポイント (ToonYou, CounterfeitXL, AnythingXL など) |
| Sampler | DPM++ 2M Karras |
| Steps | 28 |
| CFG | 7.0 |
| Denoise | 1.0 (txt2img) |
| 解像度 | 1024×1024 (その後サイズ別にスケール・クロップ) |
| Seed | 探索中はランダム、構図が決まったら固定 |

---

## カラーバリエーション

| バリアント | 追加プロンプト |
| --- | --- |
| `full_color` | vibrant yellow orange red palette, saturated colors |
| `monochrome` | single color, monochrome, grayscale outline |
| `white_on_dark` | white fill, dark thick outline, high contrast |

カラーバリエーションは img2img で denoise 0.30–0.40 にし、上記プロンプトを追記して生成します。

---

## サイズターゲット

| 名称 | 解像度 | 用途 |
| --- | --- | --- |
| `1x` | 512×512 | 小アイコン / アバター |
| `2x` | 1024×1024 | 標準使用 |
| `banner` | 1920×480 | YouTube チャンネルアート / バナー |

同一シードで解像度のみ変更するか、アップスケールノードで出力します。

---

## 調整ガイド

| 目的 | 対処法 |
| --- | --- |
| よりポップに | `pop art, halftone dots, bold comic style` を追加、CFG を 7.5 に上げる |
| アウトラインを強調 | `thick black outline, stroke border, outlined art style` を追加 |
| 透過処理 | アルファ出力が使えない場合は rembg 等で後処理 |
| LoRA 学習 | `network_dim=32`, `lr=1e-4`, 1500 steps、スタイル統一した参照画像 15〜30 枚 |

---

## ワークフロー手順

1. **txt2img** で構図を探索する
2. 気に入ったシードが出たら固定する
3. **img2img** (denoise 低め) で細部を調整する
4. SaveImage ノードまたは後処理でアルファチャンネル (透過背景) を有効にして書き出す
5. サイズターゲットに合わせてスケール・クロップして納品する
