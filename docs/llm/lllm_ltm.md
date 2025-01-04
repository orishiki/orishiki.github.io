# ローカルLLMの長期記憶

>TL;DR: コンテキスト トークンの制限が 2048 の AI モデルを使用している場合、1000 トークンのキャラクター定義によって AI の「メモリ」が半分に削減されます。これをわかりやすく説明すると、優れた AI からの適切な応答は、簡単に 200 ～ 300 トークン程度になります。この場合、AI はチャット履歴の約 3 回のやり取りしか「記憶」できません。[SillyTavern Documentation](https://docs.sillytavern.app/usage/core-concepts/characterdesign/)


AIは会話内容をコンテキストに貯め込んでいき、コンテキストに収まりきらなくなると古いものから忘れていく。このコンテキスト制限のオーバーフローは特にメモリサイズに制限のあるローカルLLMにおいて大きな課題である。

AIにコンテキスト長を超える長期記憶(long term memory)を与える仕組みはいくつも提案されてきたが、2025年現在でも解決していない。実用的な方法としては、適宜チャット履歴で覚えておきたい内容を手動でCharacterのMemoryに追記していくという力業がある。

## World info, Lorebooks, Memory Books

>これは、World Info エントリに関連付けられたキーワードがメッセージ テキストに存在する場合にのみ、World Info エントリから関連情報を挿入する動的ディクショナリのように機能します。
[SillyTavern Documentation](https://docs.sillytavern.app/usage/core-concepts/worldinfo/)

固有名詞とその説明などを事前に定義しておくことで、必要な時にだけ登録内容をコンテキストに挿入してくれる便利な仕掛け。便利だが静的なものであり、チャット内で内容を更新していく様なものではない。

## [SillyTavern/Smart Context](https://docs.sillytavern.app/extensions/smart-context/)（廃止）

チャットファイルの全履歴を自動的に取得し、ベクトルデータベースに保管、チャットの入力内容をトリガーに検索を行い、コンテキストに挿入する。自動Lorebookの様なもの。

## [SillyTavern/Chat Vectorization](https://docs.sillytavern.app/extensions/chat-vectorization/)

廃止されたSmart Contextの代替品。やはり自動Lorebookの様なものなので、固有名詞以上のものを求めるのは厳しい？

## [SillyTavern/Summarize](https://docs.sillytavern.app/extensions/summarize/)

チャット内容の要約を作成しコンテキストに挿入してくれる。一見良さそうだが、冷静に考えるとAIに覚えていて欲しいのはチャットの概略でも要約でもなく、印象的な会話とか、ある種の特別な瞬間なのでは？

## [Text Gen Web UI/superbooga](https://github.com/oobabooga/text-generation-webui/tree/main/extensions/superbooga),[superboogav2](https://github.com/oobabooga/text-generation-webui/tree/main/extensions/superboogav2)

本体に取り込まれている機能拡張だが、外部情報がほぼない。SillyTavernのChat Vectorization相当か？

## [Text Gen Web UI/Memoir+](https://github.com/brucepro/Memoir)

>Memoirは、テキスト生成WebUI内の既存のAIコンパニオンを充実させるように設計されたAIを利用したプラグインです。高度な記憶機能と心の知能指数を備えたMemoirは、AIとのインタラクションをよりニュアンスのある人間のような体験に変えます。[Memoir+: Enhanced Persona Extension for Text Generation Web UI](https://github.com/brucepro/Memoir)

良さそうだが、何回チャレンジしても記憶が更新されなかった。

## [Text Gen Web UI/complex_memory](https://github.com/theubie/complex_memory)

World info, Lorebooks機能を追加する。

## [Text Gen Web UI/Long term memory with qdrant vector database](https://github.com/jason-brian-anderson/long_term_memory_with_qdrant)

不明。SillyTavernのChat Vectorization相当か？  

## [Text Gen Web UI/long_term_memory(開発停止)](https://github.com/wawawario2/long_term_memory)
  
不明。SillyTavernのChat Vectorization相当か？  
