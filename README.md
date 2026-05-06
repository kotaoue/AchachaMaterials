# AchachaMaterials

YouTube チャンネル [OhYeahAchacha](https://www.youtube.com/@OhYeahAchacha) で使用する素材を管理するリポジトリです。

A repository for managing materials used in the [OhYeahAchacha](https://www.youtube.com/@OhYeahAchacha) YouTube channel.

---

## 概要 / Overview

ComfyUI + Stable Diffusion を使って、動画に登場するキャラクターの表情差分などを作成・管理します。

This repository manages character assets and facial expression variations (表情差分) created with ComfyUI + Stable Diffusion for use in YouTube videos.

---

## ディレクトリ構成 / Directory Structure

```text
AchachaMaterials/
├── characters/
│   └── <character_name>/
│       ├── base/
│       └── expressions/
├── workflows/
├── prompts/
└── assets/
```

- `characters/`: キャラクター素材 / Character assets
- `base/`: ベース画像 / Base images
- `expressions/`: 表情差分 / Facial expression variants
- `workflows/`: ComfyUI ワークフロー / ComfyUI workflow JSON files
- `prompts/`: プロンプト集 / Stable Diffusion prompts
- `assets/`: その他の素材 / Other assets (backgrounds, props, etc.)

---

## 使い方 / Usage

### 表情差分の生成 / Generating Facial Expressions

1. [ComfyUI](https://github.com/comfyanonymous/ComfyUI) をセットアップする  
   Set up [ComfyUI](https://github.com/comfyanonymous/ComfyUI).

2. `workflows/` 内の `.json` ファイルを ComfyUI にロードする  
   Load a `.json` workflow file from the `workflows/` directory into ComfyUI.

3. `prompts/` 内のプロンプトを参考にパラメータを調整する  
   Refer to prompts in the `prompts/` directory to adjust generation parameters.

4. 生成した画像を対応する `characters/<name>/expressions/` に保存する  
   Save generated images to the appropriate `characters/<name>/expressions/` folder.

---

## 環境 / Environment

| ツール / Tool | 用途 / Purpose |
| --- | --- |
| [ComfyUI](https://github.com/comfyanonymous/ComfyUI) | ノードベースの画像生成 UI / Node-based image generation UI |
| [Stable Diffusion](https://stability.ai/) | 画像生成モデル / Image generation model |

---

## ライセンス / License

各素材のライセンスはそれぞれのディレクトリ内の `LICENSE` ファイルを参照してください。  
See the `LICENSE` file in each directory for the license of individual assets.
