---
icon: image
date: 2025-01-11T00:00
---
# ローカル画像生成AIのメモ

[Midjourney](https://www.midjourney.com/)や[DALL·E 3](https://openai.com/index/dall-e-3/)の様な画像生成AIをクラウドではなくローカルで使う方法のメモ。

!!!warning Warning
2025年現在、NVIDIA GeForce/AMD RadeonシリーズのGPUを使っているのであれば、Windowsでも実用的な速度で画像生成ができる。Google検索では「Radeonは画像生成に使えない」「ROCmはLinuxにしか対応していない」等の古い情報ばかりがヒットするので参考にならない。生成AI関連の情報はすぐに賞味期限が切れるので、2024年前半以前の情報は無視してよい。
!!!

[Stability Matrix](https://lykos.ai/)をインストールして、ComfyUI(GeForceの場合)かComfyUI-Zluda(Radeonの場合)をバックエンドに選択し、Inferenceから生成するのがおすすめ。

Radeon RX7900XTの場合、特に高速化手法を用いない素の状態で、1024x1024、20 Stepsの画像が1枚あたり7.5秒程度で生成できる。SD1時代は同一プロンプトで何枚も画像を生成して当たりを探す方法だったので生成速度が重要だったが、今はガチャは不要になったので、この程度でも十分実用的と言える。

5枚連続して画像生成した場合の例
```
got prompt
100%|██████████| 20/20 [00:06<00:00,  2.94it/s]
Prompt executed in 7.35 seconds
got prompt
100%|██████████| 20/20 [00:06<00:00,  2.92it/s]
Prompt executed in 7.46 seconds
got prompt
100%|██████████| 20/20 [00:06<00:00,  2.92it/s]
Prompt executed in 7.52 seconds
got prompt
100%|██████████| 20/20 [00:06<00:00,  2.91it/s]
Prompt executed in 7.42 seconds
got prompt
100%|██████████| 20/20 [00:06<00:00,  2.91it/s]
Prompt executed in 7.53 seconds
```

モデルはPony系がおすすめ。Flux系は負荷が重く、2D/2.5D系の得意なモデルもまだ少ないので、様子見。

![Prefect Pony XL](/img/ppxl_01.webp)

## ローカル画像生成AIの使い道

* カスタムポートレイトが使用可能なゲーム用のポートレイト画像

  [RimWorld](https://steamcommunity.com/app/294100)ではModを使用してカスタムポートレイトを表示することができる。[Really Custom Portraits](https://steamcommunity.com/sharedfiles/filedetails/?id=2956572955)、[Bottom Left Portrait](https://steamcommunity.com/sharedfiles/filedetails/?id=2887600947)等。

* チャット用キャラクターのアイコン用画像、立ち絵

  [SillyTavern](https://github.com/SillyTavern/SillyTavern)ではペルソナやキャラクターにアイコン用画像が設定でき、[キャラクターカード](https://aicharactercards.com/)として画像のメタデータに設定を埋め込むことができる。また、Extensionの[Expression Images](https://docs.sillytavern.app/extensions/expression-images/)を使用する事でノベルゲームの様にキャラクターの立ち絵を切り替えることができる。
