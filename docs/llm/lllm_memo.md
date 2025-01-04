# ローカルLLMのメモ

[ChatGPT](https://chatgpt.com/)や[Copilot](https://copilot.microsoft.com/)の様な生成AIをクラウドではなくローカルで使う方法のメモ。

## メリット

* 無料
  
  クラウド生成AIでは一般的に無料版では全ての機能が使えず、高機能なモデルにアクセスするには追加料金が必要になる。例えば、ChatGPT Plusは$20/月、Proは$200/月等。ローカルで動かせば追加料金がかからない。

* 制限なし

  クラウド生成AIでは一般的に検閲済みのモデルしか使用できない。違法、有害、倫理的・政治的に不適切と判断された入力は拒否されてしまう。これでは犯罪小説も、ダークファンタジーも書けない。ローカルで無検閲モデルを動かせば制限はかからない。

* プライベート

  クラウド生成AIでは一般的に無料版では入力内容がモデルの学習に使用される。この為、個人情報やセンシティブな内容の扱いには向かない。ローカルで動かせばデータは外部に出て行かない。

## 使い道

* RP（ロールプレイング）チャット

  自分と相手の名前、容姿(アイコン、立ち絵)、性格などを細かく設定したうえで、チャットを行う。クラウドでも疑似的なパートナー、恋人とのチャットは人気が高く、サービスも多い。マイクで音声入力（STT）→文脈を判断し立ち絵を変更→テキスト読み上げで音声出力（TTS）などの機能も利用される。

* 小説のアイデア出し・執筆補助

  舞台設定やキャラクターを指示したうえで小説のあらすじを生成させる、途中まで書いた文章の続きをそのまま書かせるなど、共同執筆相手として使える。執筆向けに学習されたモデルであれば、中世ファンタジー、剣と魔法の世界などのお約束的な舞台設定は得意なので、細かく指定が不要で手間がかからない。

* テキストアドベンチャーゲーム

  「あなたはドラゴンの巣穴の前に立っている。どうしますか？ 1) 入る　2) 逃げ帰る 3) 入口を埋める」の様な、AIと交互に対話を繰り返す、いわゆるゲームブック的な遊びができる。TRPGのGM役にする、NPCを生成させる、D&D 5e 形式でキャラクターシートを作らせる、等にも使える。

## 用意するもの

* 言語モデル

  [Hugging Face](https://huggingface.co/)から用途に合ったモデルを入手する。日本語の学習有無、検閲の有無、モデルの種類(Base、Instruct等)に注意。ローカルで動かす場合は、パラメータ数8B～12Bで、Q4程度に量子化されたものが扱いやすい。（GPUのVRAMにモデル全体がロードできるととても速い）ソフトによってはモデルの検索、ダウンロード機能を備えるものもある。

* クライアント/サーバーソフト

  両方の機能を持つ自己完結タイプ、クライアント機能だけ持つタイプ、自己完結タイプ＋サーバー機能を持つものがある。自己完結タイプ以外ではOpenAI互換のAPI機能を持つものが主流で、色々組み合わせて使える。


## ソフトの例

はじめは自己完結タイプのソフトを試してみるのがおすすめ。

* [LM Studio](https://lmstudio.ai/)

  自己完結タイプ＋サーバー機能あり。単体でHugging Faceからモデルをダウンロードできて、ChatGPT的な画面でチャットができて、APIサーバー機能もあるので、はじめて使うのにおすすめのソフト。システムプロンプトのプリセットが複数作れるものの、RPチャットや小説執筆向けの機能は無い。（r/LMStudioのメンバーは2.1K）

* [SillyTavern](https://github.com/SillyTavern/SillyTavern)

  クライアント機能のみ。RPチャット特化型で非常に多機能、ユーザーも多い。クライアント機能のみなので、別途OpenAI互換APIサーバーが必要。Persona、Character、LorebookなどRPチャット向けの機能を持ち、さらに複数人チャットや立ち絵の自動変更、ヴィジュアルノベルモード等々、多数のユニークな機能がある。（r/SillyTavernAIのメンバーは32K）

* [KoboldCpp](https://github.com/LostRuins/koboldcpp)

  自己完結タイプ＋サーバー機能あり。RPチャット、ストーリーライティング、テキストゲーム用のシナリオが用意されている。モデルファイルをロードできるので、モデルさえ用意すればすぐに使える。OpenAI互換APIサーバー機能もある。
  Lorebookはあるが、Personaなし、MemoryはあるがCharacterなしなので、RPチャット用途ではSillyTavernよりも弱い。(r/KoboldAIのメンバーは12K)

* [RisuAI](https://risuai.net/)

  クライアント機能のみ。RPチャット特化型で非常に多機能。公開されているキャラクターカードがほぼハングルなので、韓国で人気なのかも？クライアント機能のみなので、別途OpenAI互換APIサーバーが必要。Persona、Character、LorebookなどRPチャット向けの機能を持ち、さらにSillyTavern並みに多数の機能がある。（r/RisuAIのメンバーは359）

* [Backyard AI/faraday](https://backyard.ai/)

  自己完結タイプ。RPチャット特化型。Persona、Character、LorebookなどRPチャット向けの機能を持つ。（r/BackyardAIのメンバーは2K）

* [Text generation web UI](https://github.com/oobabooga/text-generation-webui)

  自己完結タイプ＋サーバー機能あり。Characterはあるが、Personaは一つだけ、Lorebookもないので、RPチャット用途ではSillyTavernよりも弱い。他のソフトはモデルロード時のデフォルトコンテキスト長を4K程度に制限しているが、これはモデルの最大値に設定しているので、Mistral AI系モデルではコンテキスト長1Mでロードしようとして失敗しがち。（r/Oobaboogaのメンバーは15K）

* [AnythingLLM](https://anythingllm.com/)

  自己完結タイプ+クライアント機能あり。見た目はLM Studioに近いがAPIサーバー機能はない。RPチャットや小説執筆向けの機能は無い。（r/anythingllmのメンバーは161人）

* [Open Webui](https://openwebui.com/)

  クライアント機能のみ。見た目はChatGPTクローン。RPチャットや小説執筆向けの機能は無い。（r/OpenWebUIのメンバーは2.7K）

* [EasyNovelAssistant](https://github.com/Zuntan03/EasyNovelAssistant)

  別枠。チャットではなく、指定したシナリオに従って小説を生成する。サンプルはNSFWなものが多いが、もちろんSFWな話も生成できる。


## モデルの例

[日本語ローカルLLM関連のメモWiki](https://local-llm.memo.wiki/d/%a4%aa%a4%b9%a4%b9%a4%e1%a4%ce%c6%fc%cb%dc%b8%ec%c2%d0%b1%fe%a5%ed%a1%bc%a5%ab%a5%eb%c2%e7%b5%ac%cc%cf%b8%c0%b8%ec%a5%e2%a5%c7%a5%eb#content_1_1_1)が詳しい。

パラメータ数8B～12B程度、量子化はQ4以上がおすすめで、それより低いとAIの頭が目に見えて悪くなっていく。
基本的にモデルのサイズが大きければ大きいほどAIの頭は良くなるが、GPUのVRAMにモデルが収まらない場合、メインメモリに振り分けられて、処理速度がガタ落ち（1文字/秒とか）になるので、PC環境と相談して決める。

SFW用途では、
* [Mistral-Nemo-Japanese-Instruct-2408](https://huggingface.co/models?search=Mistral-Nemo-Japanese-Instruct-2408)
* [phi-4](https://huggingface.co/models?search=phi-4)

NSFW用途では、
* [Lumimaid-Magnum-v4-12B](https://huggingface.co/models?search=Lumimaid-Magnum-v4-12B)

前述のEasyNovelAssistantは日本語での執筆に適したモデルをダウンロードする機能があるので参考にできる。