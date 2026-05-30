# GPU Undervolt Navigator

> アーキテクチャ別の定番アンダーボルト開始点を提示し、試行ログから「安定性フロンティア」と次の探索点を描く単一HTMLツール。
> A single-file HTML tool that suggests architecture-specific GPU undervolt starting points and plots a stability frontier from your own test logs.

NVIDIA RTX 40/50（Ada / Blackwell）、AMD RX 7000（RDNA3）、AMD RX 9000（RDNA4）に対応。インストール不要・常駐なし・オフライン動作。

---

## ✨ 特徴

- **アーキテクチャ別の最適アプローチ提示**
  - NVIDIA … MSI Afterburner での VFカーブ平坦化（プラトー方式）
  - RDNA3 … Adrenalin での最大電圧（mV）絶対値指定
  - RDNA4 … Adrenalin での電圧オフセット（-200〜0mV）指定
- **3つのチューニングモード**：省電力重視 / バランス / 性能重視で値が連動
- **安定性ログ & フロンティア可視化**：電圧 × クロック平面に試行を散布表示し、二分法で次の探索点を提案
- **ステップ手順・安定性テスト・トラブル切り分け**をGPUごとに自動生成
- **JSONエクスポート / インポート** によるログのバックアップと移行
- **単一HTMLファイル**：依存パッケージなし、ローカルでもGitHub Pagesでも動作

---

## 🖥️ 対応GPU

| メーカー | 世代 | モデル例 |
|---|---|---|
| NVIDIA | Blackwell (RTX 50) | 5090 / 5080 / 5070 Ti / 5070 / 5060 Ti |
| NVIDIA | Ada Lovelace (RTX 40) | 4090 / 4080(S) / 4070 Ti(S) / 4070(S) / 4060 Ti / 4060 |
| AMD | RDNA4 (RX 9000) | 9070 XT / 9070 / 9060 XT |
| AMD | RDNA3 (RX 7000) | 7900 XTX / 7800 XT / 7700 XT / 7600 |

---

## 🚀 使い方

### オンライン（GitHub Pages）

```
https://ytty-pc.github.io/gpu-undervolt-navigator/
```

### ローカル

`index.html` をダウンロードしてブラウザで開くだけです。記録はブラウザの保存領域に自動保存されます。

> ⚠️ サンドボックス内のプレビューでは保存（localStorage）が無効になる場合があります。確実に記録を残すにはローカルで開くか、JSONエクスポートでバックアップしてください。

### 基本フロー

1. **ナビゲーター**タブで自分のGPUとモードを選び、表示された開始点・手順に従って設定を適用
2. ベンチ／実プレイで安定性を確認（FFXVベンチ → Steel Nomad → 実プレイ）
3. **安定性ログ**タブに結果（電圧・クロック・判定）を記録
4. 散布図と「次の探索点」を見ながら、1回につき1変数だけ動かして詰める

---

## 📊 データ出典

開始点の目安は以下を基にした集計値です（無保証）。

- MSI 公式 OC/UV ガイド（2025）
- Esports Tales: RTX 5070 Ti 実測（2025）
- RDNA4 UV レポート: HWCooling / Tom's Hardware / der8auer・Alva Jonathan（2025）
- 各GPUの定番開始点の集計（2026）

---

## ⚠️ 免責事項

- 表示値は**目安**です。個体差（シリコンロータリー）で安定値は±50mV前後変動します。**必ず自分の環境でテストしてください。**
- 本ツールは設定を**自動適用しません**。値の提示と記録のみを行います。
- 電圧不足によるクラッシュは再起動でデフォルトに戻り、**ブート不能・恒久的故障は発生しません**。
- このアンダーボルトはGPUのVFテーブル/電圧のみを操作し、**VBS/HVCI・コア隔離等のOSセキュリティ機構には影響しません**。
- 本ツールの利用によって生じたいかなる損害についても、作者は責任を負いません。自己責任でご利用ください。

---

## 🛠️ 技術メモ

- 純粋なHTML/CSS/JavaScript（フレームワーク・ビルド不要）
- フォント: IBM Plex Sans JP / IBM Plex Mono / Chakra Petch（Google Fonts、オフライン時はフォールバック）
- 散布図はインラインSVGで描画
- 永続化: `localStorage`（try/catchでフォールバック）+ JSON入出力

---

## 🤝 コントリビュート

対応GPUの追加、開始点データの補正、不具合報告は Issue / Pull Request でお願いします。

---

## 📄 ライセンス

[MIT License](./LICENSE)
