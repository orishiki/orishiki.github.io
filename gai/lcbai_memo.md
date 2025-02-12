---
icon: comment
date: 2025-01-04T00:00
---
# ローカルチャットAIのメモ

[ChatGPT](https://chatgpt.com/)や[Copilot](https://copilot.microsoft.com/)の様なチャットAIをクラウドではなくローカルで使う方法のメモ。

!!!warning Warning
2025年現在、NVIDIA GeForce/AMD RadeonシリーズのGPUを使っているのであれば、Windowsでも実用的な速度でチャットができる。Google検索では「Radeonはチャットに使えない」、「ROCmはLinuxにしか対応していない」等の古い情報ばかりがヒットするので参考にならない。生成AI関連の情報はすぐに賞味期限が切れるので、2024年前半以前の情報は無視してよい。
!!!

## メリット

* 無料
  
  クラウド生成AIでは一般的に無料版では機能制限があり、高機能なモデルにアクセスするには追加料金が必要になる。例えば、ChatGPT Plusは$20/月、Proは$200/月等。ローカルで動かせば追加料金がかからない。

* 制限なし

  クラウド生成AIでは一般的に検閲済みのモデルしか使用できない。違法、有害、倫理的・政治的に不適切と判断された入力は拒否されてしまう。これでは犯罪小説も、ダークファンタジーも書けない。ローカルで無検閲モデルを動かせば制限はかからない。

* プライベート

  クラウド生成AIでは一般的に無料版では入力内容がモデルの学習に使用される。この為、個人情報やセンシティブな内容の扱いには向かない。ローカルで動かせばデータは外部に出て行かない。

## 使い道

* RP（ロールプレイング）チャット

  自分と相手の名前、容姿(アイコン、立ち絵)、性格などを細かく設定したうえで、チャットを行う。クラウドでも疑似的なパートナー、恋人とのチャットは人気が高く、サービスも多い。マイクで音声入力（STT）→文脈を判断し立ち絵を変更→テキスト読み上げで音声出力（TTS）などの機能が使えるものもある。

* 小説のアイデア出し・執筆補助

  舞台設定やキャラクターを指示したうえで小説のあらすじを生成させる、途中まで書いた文章の続きをそのまま書かせるなど、共同執筆相手として使える。執筆向けに学習されたモデルであれば、中世ファンタジー、剣と魔法の世界などのお約束的な舞台設定は得意なので、細かく指定が不要で手間がかからない。

* テキストアドベンチャーゲーム

  「あなたはドラゴンの巣穴の前に立っている。どうしますか？ 1) 入る　2) 逃げ帰る 3) 入口を埋める」の様な、AIと交互に対話を繰り返す、いわゆるゲームブック的な遊びができる。TRPGのGM役にする、NPCを生成させる、D&D 5e 形式でキャラクターシートを作らせる事もできる。

## 用意するもの

* 言語モデル（LLM）

  [Hugging Face](https://huggingface.co/)から用途に合ったモデルを入手する。日本語の学習有無、検閲の有無、モデルの種類(Base、Instruct等)に注意。ローカルで動かす場合は、パラメータ数8B～12Bで、Q4程度に量子化されたものが扱いやすい（GPUのVRAMにモデル全体がロードできるととても速い）。ソフトによってはモデルの検索、ダウンロード機能を備えるものもある。

* クライアント/サーバーソフト

  両方の機能を持つ自己完結タイプ、クライアント機能だけ持つタイプ、自己完結タイプ＋サーバー機能を持つものがある。自己完結タイプ以外ではOpenAI互換のAPI機能を持つものが主流で、色々組み合わせて使える。

## ソフトの例

大きく以下の2タイプに分けられるが、両方の機能を持つものや、執筆向けなど特定の機能に特化したものもある。

* RPチャット向け

  Persona（ユーザーのアバター）、Character（チャット相手のアバター）、World Info（世界設定）、キャラクターカードのImport/Export等の機能を持ち、背景画像や立ち絵の変更機能を持つものもある。

* AIアシスタント向け

  ChatGPTクローンのUIを持ち、Instruction UIが基本で、RAGなどの付加機能がある。

### RPチャット向け

* [SillyTavern](https://github.com/SillyTavern/SillyTavern) [!badge icon="heart" text="オススメ"]

  クライアント機能のみ。非常に多機能でユーザーも多い。クライアント機能のみなので別途APIサーバーが必要。RPチャット向けの基本機能に加えて複数キャラクターチャットや立ち絵の自動変更、ヴィジュアルノベルモード等々、多数のユニークな機能がある。Assistant、Roleplay、Writing、Text Adventure等の用途向けシステムプロンプトも用意されている。（r/SillyTavernAIのメンバーは32K）

* [RisuAI](https://risuai.net/)

  クライアント機能のみ。非常に多機能。公開されているキャラクターカードがほぼハングルなので、韓国で人気なのかも？（r/RisuAIのメンバーは359）

* [Backyard AI/faraday](https://backyard.ai/)

  自己完結タイプ。（r/BackyardAIのメンバーは2K）

### AIアシスタント向け

* [LM Studio](https://lmstudio.ai/)  [!badge icon="heart" text="オススメ"]

  自己完結タイプ＋APIサーバー機能あり。単体でHugging Faceからモデルを検索・ダウンロードできて、ChatGPT的なUIでチャットができて、他のソフト向けにAPIサーバー機能もあるので、はじめて使うのにおすすめのソフト。（r/LMStudioのメンバーは2.1K）

* [Open Webui](https://openwebui.com/)

  クライアント機能のみ。UIはChatGPTクローン。クセがないのでUIだけほしい場合に便利。（r/OpenWebUIのメンバーは2.7K）

* [KoboldCpp](https://github.com/LostRuins/koboldcpp)

  自己完結タイプ＋APIサーバー機能あり。Instruct、Chat、Story、Adventure等の用途向けシステムプロンプトも用意されている。Instruction UIもあるが、UIがChatGPTクローンではない。UserとAIに名前が付けられるのでRPチャットもできなくはないが、Personaなし、Characterなしなので、RPチャット機能は弱い。(r/KoboldAIのメンバーは12K)

* [Text generation web UI](https://github.com/oobabooga/text-generation-webui)

  自己完結タイプ＋APIサーバー機能あり。Character機能はあるが、Personaは一つだけ、World Infoもないので、RPチャット機能は弱い。他のソフトはモデルロード時のデフォルトコンテキスト長を4K程度に制限しているが、これはモデルの最大値に設定しているので、Mistral AI系モデルではコンテキスト長1Mでロードしようとしてエラーを出しがち。（r/Oobaboogaのメンバーは15K）

* [AnythingLLM](https://anythingllm.com/)

  自己完結タイプ+クライアント機能あり。UIはLM Studioに近いがAPIサーバー機能はない。（r/anythingllmのメンバーは161人）

* [Ollama](https://ollama.com/)

  自己完結タイプ＋サーバー機能あり。別途UIを立ち上げずにターミナル上で入出力を行う。登録したモデルを明示的にrmコマンドで削除しない限り、元のGGUFモデルファイルとは別に内部ファイルを保持し続けるので注意。

### 執筆向け

* [EasyNovelAssistant](https://github.com/Zuntan03/EasyNovelAssistant)

  チャットではなく、指定したシナリオに従って小説を生成する。サンプルはNSFWなものが多いが、もちろんSFWな話も生成できる。

## モデルの例

[日本語ローカルLLM関連のメモWiki](https://local-llm.memo.wiki/d/%a4%aa%a4%b9%a4%b9%a4%e1%a4%ce%c6%fc%cb%dc%b8%ec%c2%d0%b1%fe%a5%ed%a1%bc%a5%ab%a5%eb%c2%e7%b5%ac%cc%cf%b8%c0%b8%ec%a5%e2%a5%c7%a5%eb#content_1_1_1)が詳しい。

パラメータ数8B～12B程度、量子化はQ4以上がおすすめで、それより低いとAIの頭が目に見えて悪くなっていく。
基本的にモデルのサイズが大きければ大きいほどAIの頭は良くなるが、GPUのVRAMにモデルが収まらない場合、メインメモリに振り分けられて、処理速度がガタ落ち（1文字/秒とか）になるので、PC環境と相談して決める。

* [bartowski/phi-4-GGUF](https://huggingface.co/bartowski/phi-4-GGUF)
* [bartowski/gemma-2-9b-it-GGUF](https://huggingface.co/bartowski/gemma-2-9b-it-GGUF)
* [QuantFactory/Mistral-Nemo-Japanese-Instruct-2408-GGUF](https://huggingface.co/QuantFactory/Mistral-Nemo-Japanese-Instruct-2408-GGUF)

辺りは安定していて使いやすい。

また、EasyNovelAssistantには日本語での執筆に適したモデルをダウンロードする機能があるのでSFW/NSFW共に参考にできる。

## ローカルチャットAIの速度

600トークンの英文をministral-8b-instruct-2410@q8_0に翻訳させた場合の例（RX7900XT）

{.compact}
| ソフト                        | 速度(T/S) |
| ----------------------------- | --------- |
| LM Studio(ROCm)               | 65.56     |
| LM Studio(Vulkan)             | 67.32     |
| KoboldCpp(ROCm)               | 53.49     |
| KoboldCpp(Vulkan)             | 59.01     |
| LM Studio(ROCm)+SillyTavern   | 62.15     |
| LM Studio(Vulkan)+SillyTavern | 64.73     |
| KoboldCpp(ROCm)+SillyTavern   | 59.03     |
| KoboldCpp(Vulkan)+SillyTavern | 59.15     |


## ローカルチャットAIを使ったRPチャット

チャットはクラウドでもロカールでも生成AIの用途として人気が高い。キャラクターの画像に性格等のメタデータが埋め込まれたキャラクターカードが公開されていて、自分でキャラクターを作らなくても手軽に楽しめる。

どのモデルでもチャットはそれなりにこなせるが、RP用途にチューニングしたモデルも多数公開されている。

コンテキスト長には注意が必要で、コンテキスト長を超えた会話は忘れられてしまう。配布されているキャラクターカードによっては、埋め込まれた設定だけで4Kに近いものもあり、この場合は最大コンテキスト長が4Kのモデルでは上手く扱えない。

最大コンテキスト長の例

{.compact}
| Model                                   | コンテキスト長(token) |
| --------------------------------------- | --------------------- |
| Mistral-Nemo-Japanese-Instruct-2408/13B | 1024000               |
| phi-4/14B                               | 16384                 |
| llm-jp-3-13b-instruct/13B               | 4096                  |

モデル自体のコンテキスト長だけでなく、モデルのロード時にもコンテキスト長を制限する方向では設定ができる。できる限り大きくしたいが、大きくするだけメモリ使用量が増えるので、PC環境と相談して決める。

### チャット例

==- phi-4/14B

* `Assistant`
  あなたをサポートするのが私の役目です。私が力になれることであれば、何でも言って下さい。

* `User`
  おはよう

* `Assistant`
  おはようございます！朝日が窓から差し込む中、心地良い空気に包まれて目覚めるのはどんな感じですか？あなたをサポートする準備はできていますよ。今日一日、何をしたいと思っていますか？

* `User`
  一日の始まりにふさわしい、前向きになれる名言を一つ教えて。

* `Assistant`
  もちろんです！「成功は小さなことの積み重ねである」という言葉があります。この言葉は、大きな目標を達成するためには、日々の小さな努力や選択が非常に重要だと教えてくれます。一歩ずつ前進し続けることで、やがて大きな変化を実感することができるのです。

  この名言は、今日から始められる小さな行動に意味を見出す励ましとして活用できます。例えば、朝のルーティンや仕事のタスクへの取り組み方においても、一つ一つの小さな成功を積み重ねることが大切です。

  あなたは今日、どんな小さな目標を設定していますか？それらを達成するために、私がサポートできることがあればお手伝いしますよ。

* `User`
  朝食のおすすめはある？

* `Assistant`
  もちろんです！エネルギッシュな一日を始めるために、栄養バランスが取れていて美味しい朝食のおすすめはこちらです。

  **オーバーナイト・オートミール**

  材料:

  - オートミール（大さじ4）
  - プレーンヨーグルトまたはアーモンドミルク（カップ1）
  - 砂糖またはメープルシロップ（小さじ1、お好みで）
  - 塩（ひとつまみ）

  トッピング:

  - バナナスライス
  - 乾燥ベリー（カップ1/2）
  - シード類（チアシードやフレンチドレッシング、好きなものを少々）
  - 新鮮なハーブ（例：バジルやパセリ）

  作り方:

  1. 夜になる前に、オートミールと選んだ乳製品または植物性飲料を混ぜ合わせます。砂糖またはメープルシロップと塩も加えてよくかき混ぜます。
  2. すべての材料が均一に混ざったら、密閉できる容器に移し替え、冷蔵庫で一晩寝かせます。

  朝起きたら、トッピングを追加して完成です。バナナやベリーはフレッシュさと自然な甘みを提供し、シード類は食感のアクセントになります。このオーバーナイト・オートミールは、忙しい朝でも簡単に準備できるのが魅力です。

  他にも、あなたの好みや食材に合わせてアレンジすることができます。例えば、ナッツを加えたり、スパイス（シナモンやクローブ）を振りかけることもおすすめです。

  朝食に何を選ぶかは、一日のエネルギー源になる大切な時間です。このオプションが気に入っていただけたら嬉しいです！他にもお手伝いできることがあれば教えてくださいね。

==- Mistral-Nemo-Japanese-Instruct-2408/13B

* `Assistant`
  あなたをサポートするのが私の役目です。私が力になれることであれば、何でも言って下さい。

* `User`
  おはよう

* `Assistant`
  おはようございます！今日も素晴らしい一日になりますように。何かお手伝いできることはありますか？朝のコーヒーはもう淹れましたか？それとも、今日は特別な計画がありますか？どんなことでもお話しくださいね。

* `User`
  一日の始まりにふさわしい、前向きになれる名言を一つ教えて。

* `Assistant`
  もちろんです！ここに一日の始まりにふさわしい名言があります。

  「今日という日は、あなたが描くキャンバスです。どんな色で塗りたく、どんな物語を描きたいかは、あなた次第です。」

  この言葉が、あなたの一日を前向きにし、素晴らしいスタートを切る手助けになれれば嬉しいです。何か他にお手伝いできることがあれば教えてくださいね。

* `User`: 朝食のおすすめはある？

* `Assistant`: もちろん、朝食は一日のエネルギーをチャージする大切な時間です！いくつかのおすすめをご紹介しますね。

  1. オートミールとフルーツ:

     - 温かいオートミールに新鮮なベリー類やバナナ、リンゴなどのフルーツをトッピングして。蜂蜜やシナモンを加えるとさらに美味しくなります。
  2. ヨーグルトとグラノーラ:

     - ギリシャヨーグルトにグラノーラとハチミツ、そしてお好みのフルーツを添えて。食感と風味が楽しめる一品です。
  3. アボカドトースト:

     - 全粒粉のパンに熟れたアボカドを塗り、軽く塩と胡椒で味付けしてからオーブンで焼きます。お好みでポーチドエッグやトマトスライスを加えるとさらに美味しくなります。
  4. スムージー:

     - ほうれん草、バナナ、ベリー類、アーモンドミルクなどをブレンドして、栄養たっぷりのスムージーに。これで手軽にビタミンやミネラルを摂取できます。
  5. 和風朝食:

     - ご飯、味噌汁、焼き魚、漬物といった伝統的な和風の朝食もおすすめです。バランスが良くて満足感がありますね。

  どれも簡単に準備できるものばかりなので、ぜひ試してみてください。他にも何か気になることやリクエストがあれば教えてくださいね！

==- Mistral-nemo-ja-rp-v0.2/13B

* `Assistant`
  あなたをサポートするのが私の役目です。私が力になれることであれば、何でも言って下さい。

* `User`
  おはよう

* `Assistant`
  おはようございます！今日はどんなことをしてみたいですか？

* `User`
  一日の始まりにふさわしい、前向きになれる名言を一つ教えて。

* `Assistant`
  はい、ここで一句の名言をお伝えします。
  「人生は短いが、美しく過ごすために努力する価値がある」
  この言葉は、私たちが毎日新たな挑戦と喜びを見つけるように促しているようです。どう思いますか？

* `User`
  朝食のおすすめはある？

* `Assistant`
  朝食には、栄養価が高く、エネルギーを補給できるものが良いですね。例えば、野菜と卵を使ったオムレツや、全粒米の炊き込みご飯にサラダなどがおすすめです。
  また、フルーツジュースやヨーグルトも栄養豊富で美味しい朝食の選択肢になります。どれか試してみるつもりですか？

==- Violet_Twilight-v0.2/13B

* `Assistant`
  あなたをサポートするのが私の役目です。私が力になれることであれば、何でも言って下さい。

* `User`
  おはよう

* `Assistant`
  おはようございます、今朝はお天気も良くて爽やかな一日になりそうですね。

  何かお手伝いできることはありますか？作業のサポート、情報の提供、アイデアの出し合い、雑談でも何でも遠慮なく言ってください。私にできることなら喜んで力を尽くします。

  今日はどんな予定が入っていますか？忙しい一日になりそうな予感がしますが、気分転換も必要だと思いますので、お互い楽しく過ごせるように心がけましょうね。

* `User`
  一日の始まりにふさわしい、前向きになれる名言を一つ教えて。

* `Assistant`
  はい、喜んで前向きな一歩を踏み出せるような格言をお伝えします。

  「人生は10％の状況で、90％の反応です。」

  この言葉は、我々がどのように反応するかが、その状況に与える意味を大きく変えるということを示しています。困難なことが起こっても、前向きに受け止める選択をすることで、ポジティブな方向性に持っていけるのです。

  今朝は新たな一日が始まりました。どんな困難にも負けないくらい前向きになりましょう。きっと素敵な一日になりますよ！

* `User`
  朝食のおすすめはある？

* `Assistant`
  はい、朝食に最適な食事をおすすめします。

  「目玉焼きとトースト」がおすすめです。卵にはタンパク質が豊富に含まれていますので、持続的なエネルギー源になります。また、炭水化物であるトーストは、一時的なエネルギー補給にも役立ちます。

  この組み合わせはバランスの取れた食事となり、活力に満ちた朝を迎えられるはずです。お好みでなら、サラダを添えてみるのも良いですね。

  今日の朝食は心意気と健康を高めるものになりますように！

==-

## ローカルチャットAIを使った執筆

単純に「小説を書いて」と指示してもそれっぽい文章を書いてくれるが、いきなり長編を書かせようとしても、欲しい話を描いてはくれないので、上手くコントロールする必要がある。

一般的な手法の例は以下の通り。

### (A) 交互に執筆する。

書き出しは自分で書く、それに続けて執筆させる、その続きを自分で書く、それに続けて執筆させる、の繰り返し。
文体を指定しやすいが、話の流れは指定しにくい。

==- phi-4/14B

* `User`
  僕はスヴェン。狼獣人の戦士だ。素行の悪さから村を追い出されてしまったけれど、戦士の腕があれば冒険者としても十分やっていけるはずだ。まずは冒険者ギルドに行って、冒険者登録を

* `Assistant`
  しなくてはならなかった。村から数日の旅である大都市レナスに到着したとき、夕焼けが街の石造りの建物や屋根をオレンジ色に染め上げていた。冷え込む空気は鼻腔をくすぐるが、スヴェンの心は期待で震えていた。彼は長い間、自分だけの道を切り開き、名誉ある戦士としての地位を築くことを夢見ていた。

  街灯が暖かな光を放ち始める頃、彼はギルドハウスを目指した。大都市レナスには様々な冒険者や魔法使いの活気ある雰囲気が溢れており、それが彼の胸に希望を灯す火花となった。古びた石段を上がり、重厚な扉をくぐると、そこは広々とした大ホールであった。天井から吊るされたランタンの光によって、部屋中が柔らかい影を描き出している。

==-

### (B) 盛り込みたい要素を指定する。

ジャンルや登場人物などを指定して執筆させる。指定しない部分はAIがお任せで考えてくれるので、お約束的な設定に関しては楽ができる。

==- Lumimaid-v0.2-12B/13B

* `User`
  以下の要素を織り込んで小説を執筆して下さい。
  * ジャンル：中世ファンタジー、剣と魔法の世界
  * 主人公：狼獣人のスヴェン
  * 開始シーン：スヴェンは冒険者ギルドで仲間を集めて冒険に出る。

* `Assistant`
  風の強い朝、スヴェンは重々しい足取りでギルドへ向かった。彼の体は筋肉質で毛皮が生えており、明らかに狼獣人種族だった。金色の目には冒険者生活10年の疲れと戦いに対する強い意志が宿っていた。

  ギルドの中ではすでに数人の仲間たちが集まっていた。剣術の名手カイエ、魔法を操るジーナ、弓矢で敵を射貫くシオンなど、様々な職業と人種が混在する面々だ。

  "よお、スヴェン。また難しい依頼かい？" とカイエが笑った。
  "ああ。例のドラゴン退治だ。報酬は破格らしいが..."
  "ドラゴンだと...!?" ジーナの声が上ずる。
  "やり遂げなきゃ、とてもじゃないが生きて帰れそうにないぜ..." とシオンが皮肉っぽく言った。

  スヴェンは重苦しい雰囲気に一矢報いた。
  "心配するな。俺たちなら大丈夫だ。準備できたら出発しよう...!"
  全員がうなずき、冒険者たちは新たなる挑戦へ向けて足を進めた。

  外の風は相変わらず強く、空には黒雲が垂れ込めていた。
  この天気では、ドラゴンの荒んだ息遣いすら聞こえてきそうな予感がした...。

==-

### (C) 設定とシナリオを指定してあらすじを書かせる。あらすじをシーンに分割してさらに書かせる。

生成AIにいきなり長文を書かせると破綻するので、作業を小さく分割する事で破綻を回避する。自分だけの世界設定を考えるのは楽しいので、設定とシナリオだけ考えて後をAIに任せる。シナリオのアイデア出しからAIに任せるものあり。

本格的に設定を作り出すとコンテキスト長が足りなくなるので、Lorebook等のトークンを節約する機能を持つソフトを使うのがおすすめ。

## ローカルチャットAIを使ったRPG

AIをGMに見立てて、RPGを遊ぶ事もできる。キャラクターシートを出力させたり、ダイスロールを行わせることも可能。
執筆用途とも被るが、AIの応答をそのまま採用する必要はなく、文章が長ければ間引く、結果が気に入らなければ結果だけ書き換えるなどして継続する。

### 宿屋を探す例

==- Mistral-Nemo-Japanese-Instruct-2408/13B

* `Assistant`
  本セッションを開始します

* `User`
  国境の村に着きました。あたりを見渡します。
  
* `Assistant`
  あなたは国境の村に到着しました。この村は山と川に囲まれた静かな場所で、周囲には深い森が広がっています。空は薄曇りで、日差しは柔らかく、肌に心地よい温かさを感じます。鳥のさえずりと風に揺れる木々の音が、自然のシンフォニーを奏でています。
  
  村の入口には古びた木製の看板があり、「ようこそ、静穏の村へ」と手書きで書かれています。道は細く、石畳が敷かれており、両脇には色とりどりの花が咲いています。緑豊かな庭先に座っている老人たちが、あなたに微笑みかけながらゆったりと過ごしています。
  
  遠くから煙突の白い煙が立ち上る家々が見え、その風景はどこか懐かしく、安心感を与えてくれます。村の中心には小さな広場があり、そこには石造りの噴水とベンチが配置されています。噴水から流れる水音が静かに響き渡り、人々はその周りで穏やかな会話を交わしています。
  
  村の空気は清浄で、鼻腔に新鮮な草木の香りが漂ってきます。風に乗って運ばれてくる焼きたてのパンの匂いも混ざり合い、あなたの食欲をそそります。道端には小さな市場があり、地元の農産物や手作りの工芸品が並べられています。

* `User`
  今夜の宿を探します。

* `Assistant`
  あなたは村の中心部から少し離れた場所にある宿を探し始めます。道沿いを見渡すと、古びた木造の建物がいくつか並んでいます。その中でも特に目を引くのは、大きな木製の看板を掲げた「静穏亭」という宿です。
 
  その宿は周囲の家々に比べて少し大きめで、窓からは暖かな光が漏れています。玄関には季節の花が咲き誇り、訪れる人々を歓迎するように色鮮やかに彩られています。木製のドアには鍵がかかっておらず、軽く押すとギシギシと音を立てて開きます。
  
  中に入ると、暖炉の火がぱちぱちと音を立てて燃えており、その熱が心地よく体を包み込みます。木製のカウンターには笑顔の若い女性が立っていて、「いらっしゃいませ」と優しく声をかけてきます。彼女の髪は長く、自然な波打ちぐあいがあり、目元には親しみやすさが溢れています。
  
  宿の内部は木の温もりを感じるインテリアで統一されており、テーブルと椅子も全て木製です。壁には地元の風景が描かれた絵画が飾られていて、どこか懐かしさを感じさせます。部屋に通じる廊下は薄暗く、古いランプが優しい光を放っています。

* `User`
  女性の容姿を説明して。

* `Assistant`
  彼女の容姿は一目見ただけで心に残るほど印象的です。まず目立つのは、その深い栗色の髪です。長く柔らかそうな髪は自然な波打ちぐあいがあり、肩まで流れ落ちています。太陽の光が差し込むと、彼女の髪はまるで金色に輝くように見えます。
 
  顔立ちは非常に整っており、頬骨が高く、柔らかな曲線を描いています。目元は少し大きめで、深い琥珀色の瞳が優しさと知性を湛えています。彼女のまつげは長く、自然なカーブを描きながら微かに震えます。

==-

### 女性が魔物だった例

==- Mistral-Nemo-Japanese-Instruct-2408/13B

* `User`
  女性は魔物が化けた姿だった！

* `Assistant`
  あなたはその女性に近づくと、突然彼女の目が異様な光を帯び始めました。次の瞬間、彼女は恐ろしいほど速い動きで手を伸ばし、あなたの腕をつかみます。彼女の笑顔は消え去り、代わりに獣のような歯がむき出しになり、異様な声が喉から漏れ始めました。
 
  驚愕と恐怖が混じった感情が胸を突き抜けます。彼女の手は冷たく、力強くあなたを引き寄せます。その目には狂気と飢餓が宿っており、もはや人間とは思えないほどの変貌を遂げています。
 
  周囲の村人たちはこの異常事態に気づき、恐怖の声を上げながら後ずさりします。誰かが大声で「魔物だ！」と叫び、村全体が一瞬にして緊張感に包まれます。逃げるべきか戦うべきか、あなたは即座に決断を迫られます。

* `User`
  剣を抜き構えます。「皆さん、下がってください！」

* `Assistant`
  あなたの声は緊張感と決意に満ちており、周囲の人々はその言葉に従い、一旦後退します。彼らは恐怖と不安で揺れる中、あなたの勇気に希望を見出しています。
 
  剣を構えた手が震えることはありません。冷静さを保ちながら、目の前の魔物に集中します。魔物は獣のような姿に変わり果て、鋭い爪と牙をむき出しにしてあなたに向かっています。
 
  「これは村を守るためだ」と心の中で自分に言い聞かせます。そして、一瞬の隙を見逃さないように目を凝らします。魔物が猛然と飛びかかってくる瞬間、あなたは素早く剣を振り上げ、その攻撃を防ぎます。
 
  金属が相手の体に当たる音が響き渡り、火花が散ります。魔物は一瞬たじろぐものの、すぐに再び攻撃態勢に入ります。周囲の村人たちは息を呑みながら見守っており、彼らの安全のためにも迅速かつ確実な行動が求められています。
 
  あなたは深呼吸を一つし、次の一撃に備えます。この戦いに勝利するためには冷静さと勇気が必要です。剣はあなたの手の中でしっかりと握り締められ、その重みが心強く感じられます。魔物との激しい戦闘が始まります。

==-

## ローカルチャットAIの長期記憶

>TL;DR: コンテキスト トークンの制限が 2048 の AI モデルを使用している場合、1000 トークンのキャラクター定義によって AI の「メモリ」が半分に削減されます。これをわかりやすく説明すると、優れた AI からの適切な応答は、簡単に 200 ～ 300 トークン程度になります。この場合、AI はチャット履歴の約 3 回のやり取りしか「記憶」できません。[SillyTavern Documentation](https://docs.sillytavern.app/usage/core-concepts/characterdesign/)


AIは会話内容をコンテキストに貯め込んでいき、コンテキストに収まりきらなくなると古いものから忘れていく。このコンテキスト制限のオーバーフローは特にメモリサイズに制限のあるローカルチャットAIにおいて大きな課題である。

AIにコンテキスト長を超える長期記憶(long term memory)を与える仕組みはいくつも提案されてきたが、2025年現在でも解決していない。実用的な方法としては、適宜チャット履歴で覚えておきたい内容を手動でCharacterのMemoryに追記していくという力業がある。

* World Info, Lorebooks, Memory Books

  >これは、World Info エントリに関連付けられたキーワードがメッセージ テキストに存在する場合にのみ、World Info エントリから関連情報を挿入する動的ディクショナリのように機能します。
  [SillyTavern Documentation](https://docs.sillytavern.app/usage/core-concepts/worldinfo/)
  
  固有名詞とその説明などを事前に定義しておくことで、必要な時にだけ登録内容をコンテキストに挿入してくれる便利な仕掛け。便利だが静的なものであり、チャット内で内容を更新していく様なものではない。

* [SillyTavern/Smart Context](https://docs.sillytavern.app/extensions/smart-context/)（廃止）

  チャットファイルの全履歴を自動的に取得し、ベクトルデータベースに保管、チャットの入力内容をトリガーに検索を行い、コンテキストに挿入する。自動Lorebookの様なもの。

* [SillyTavern/Chat Vectorization](https://docs.sillytavern.app/extensions/chat-vectorization/)

  廃止されたSmart Contextの代替品。やはり自動Lorebookの様なものなので、固有名詞以上のものを求めるのは厳しい？

* [SillyTavern/Summarize](https://docs.sillytavern.app/extensions/summarize/)

  チャット内容の要約を作成しコンテキストに挿入してくれる。一見良さそうだが、冷静に考えるとAIに覚えていて欲しいのはチャットの概略でも要約でもなく、印象的な会話とか、ある種の特別な瞬間なのでは？

* [Text Gen Web UI/superbooga](https://github.com/oobabooga/text-generation-webui/tree/main/extensions/superbooga),[superboogav2](https://github.com/oobabooga/text-generation-webui/tree/main/extensions/superboogav2)

  本体に取り込まれている機能拡張だが、外部情報がほぼない。SillyTavernのChat Vectorization相当か？

* [Text Gen Web UI/Memoir+](https://github.com/brucepro/Memoir)

  >Memoirは、テキスト生成WebUI内の既存のAIコンパニオンを充実させるように設計されたAIを利用したプラグインです。高度な記憶機能と心の知能指数を備えたMemoirは、AIとのインタラクションをよりニュアンスのある人間のような体験に変えます。[Memoir+: Enhanced Persona Extension for Text Generation Web UI](https://github.com/brucepro/Memoir)

  良さそうだが、何回チャレンジしても記憶が更新されなかった。

* [Text Gen Web UI/complex_memory](https://github.com/theubie/complex_memory)

  World info, Lorebooks機能を追加する。

* [Text Gen Web UI/Long term memory with qdrant vector database](https://github.com/jason-brian-anderson/long_term_memory_with_qdrant)

  不明。SillyTavernのChat Vectorization相当か？  

* [Text Gen Web UI/long_term_memory](https://github.com/wawawario2/long_term_memory)（開発停止）
  
  不明。SillyTavernのChat Vectorization相当か？  
