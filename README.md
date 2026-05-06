# Bridum

A puzzle game where you draw bridges between tiles to merge their numbers. Built as a Progressive Web App with two distinct modes.

[日本語版は下にあります / Japanese version below](#日本語)

## Features

- **Two game modes** — Classic (turn-based, strategic) and Rapid (real-time tile pressure)
- **Bridge mechanic** — draw a line between two tiles to declare a merge; valid pairs: 1+2=3, or n+n=2n
- **Chain swipe** — drag through multiple tiles in one gesture to build a bridge chain
- **Cascade merges** — a merge can unlock further merges in subsequent waves, scored by wave depth
- **Classic mode** — place bridges freely, then trigger all merges at once; new tiles spawn after each turn
- **Rapid mode** — no merge button; bridges fire on pointer-up; tiles spawn on a timer that accelerates over time
- **Per-mode records** — high score, max tile, play count, and milestone split times tracked separately per mode
- **Auto-save & resume** — both modes save independently; switching modes does not affect the other's save
- **Offline-ready** — full PWA, works without a network after the first load


## Tech Stack

- Vanilla JavaScript (no framework)
- SVG for board rendering and bridge drawing
- Web Audio API for synthesised sound effects
- Service Worker for offline caching
- localStorage for records, settings, and saved games


## Project Structure

```
.
├── index.html              # Game (single-file: HTML + CSS + JS)
├── manifest.json           # PWA manifest
├── sw.js                   # Service worker
├── privacy.html            # Privacy policy (EN/JA)
├── icon_192.png
├── icon_512.png
└── icon_512_maskable.png
```

## Local Development

This is a static site with no build step. To run locally, serve the directory with any static HTTP server:

```bash
# Python
python3 -m http.server 8000

# Node.js
npx serve .
```

Then open `http://localhost:8000` in a browser.

> Service workers require HTTPS or `localhost`. Opening `index.html` directly via `file://` will not register the service worker.


## Configuration

Key constants in `index.html` that are easy to tweak:

| Constant | Default | Description |
|---|---|---|
| `RAPID_INITIAL_SPAWN_INTERVAL` | `2500` | Rapid mode: initial tile spawn interval (ms) |
| `RAPID_MIN_SPAWN_INTERVAL` | `1000` | Rapid mode: minimum spawn interval floor (ms) |
| `RAPID_DECAY_PER_60S` | `200` | Rapid mode: interval reduction per 60 seconds (ms) |
| `TARGET_SCORES` | `[100, 500, 1500, 5000, 15000]` | Score thresholds tracked as milestone split times |


## Cache Versioning

When updating cached assets, bump `CACHE` in `sw.js` so existing clients pick up the new version on next launch.


## License

(c) 2026 SukoyakaStudio. All rights reserved.

---

## 日本語

タイル間に橋を引いて数字を合算するパズルゲーム。2つのゲームモードを持つPWAとして実装。

### 特徴

- **2つのゲームモード** — クラシック（ターン制、戦略的）とラピッド（リアルタイムにタイルが増殖）
- **橋を引くルール** — 2枚のタイルを結ぶとマージを宣言。有効な組み合わせは 1+2=3 または n+n=2n
- **チェーンスワイプ** — 複数タイルを一筆書きでなぞって橋をまとめて配置
- **連鎖合成** — 合成がさらなる合成を引き起こす連鎖。深さ（ウェーブ数）によりスコアが増加
- **クラシックモード** — 橋を自由に配置し、MERGEボタンで一斉発火。ターン終了後に新タイルがスポーン
- **ラピッドモード** — MERGEボタンなし。指を離した瞬間に発火。タイマーでタイルが自動スポーンし、時間経過で加速
- **モード別記録** — ハイスコア・最大タイル・プレイ回数・マイルストーンタイムをモードごとに独立管理
- **自動セーブ・再開** — 両モードのセーブが共存。一方を始めても他方のデータは保持される
- **オフライン動作** — PWAとして初回読み込み後はネット不要


### 技術スタック

- 素のJavaScript（フレームワーク不使用）
- SVGによる盤面描画・橋のレンダリング
- Web Audio APIによるサウンドエフェクト合成
- オフラインキャッシュ用Service Worker
- localStorageによる記録・設定・中断ゲームの保存


### ローカル開発

ビルド工程はありません。任意の静的HTTPサーバーで動作します:

```bash
python3 -m http.server 8000
```

ブラウザで `http://localhost:8000` を開いてください。

> Service Workerは HTTPS または `localhost` が必要です。`file://` で直接開いた場合は登録されません。


### 設定

`index.html` 内の主要な定数は調整可能です（`RAPID_INITIAL_SPAWN_INTERVAL`, `TARGET_SCORES` など）。詳細は英語版の表を参照。


### キャッシュのバージョン管理

キャッシュ対象のリソースを更新した際は、`sw.js` の `CACHE` の値を更新してください。次回起動時に新しいキャッシュが取得されます。
