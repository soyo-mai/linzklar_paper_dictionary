# 燐字紙辞書組版

## PDF を見たい人のための注意

リポジトリ内の `言将机戦人等定引之字言集.pdf` は多少古いことがある。最新は [Actions の workflow runs](https://github.com/sozysozbot/linzklar_paper_dictionary/actions) の最新を選んで Artifacts の pdf-output をダウンロードして見ること。

## 全体の流れ

- main_indexes.txt の行に書いてある名前で `entries_*.tsv` を作る
- `entries_*.tsv` に書く
- ビルドには柱見出しの情報が必要なので、`GUIDE_WIRDS_*.json` にダミーとして一旦 `{}` とか書いておく
- `node build.js` により、`vivliostyle/*.html` を作る
- `cd vivliostyle; npx vivliostyle build -m` により、`言将机戦人等定引之字言集.pdf` が出来上がる。トリムマークが要らないなら `-m` を削る。
- 満足したら、柱見出しを手動で割り当てるために `GUIDE_WORDS_*.json` を編集し、ビルド作業をもう一度行う

`cd vivliostyle; npx vivliostyle build -m` は vivliostyle/build.bat でできる。

なお、vivliostyle/preview.bat を使ってプレビューを立ち上げておくと、「`node build.js` により、`vivliostyle/*.html` を作る」をトリガーにしてプレビューが更新されるので作業しやすい。

どちらのバッチファイルも、エクスプローラーから起動すること。（カレントディレクトリの関係）

## TSV の書き方

1 列目は燐字表記。

2 列目と 3 列目は、「品詞 + 語釈」と「例文(燐字) + 和訳」を区別せず記載するフォーマットとしている。

### 「品詞 + 語釈」

こちらとして解釈される条件は、「2 列目の先頭が `[` である」または「2 列目が空であり、3 列目が空ではない」に該当するとき。

「品詞欄が空」は、直前の語釈に対する備考として用いることを意図している。

### 「例文(燐字) + 和訳」

こちらとして解釈される条件は、それ以外のとき。

ひとつの例文について複数の和訳を書く際には、間に `|`（半角パイプ文字）を置いて区切る。

例文に対して備考をつける方法は提供していないが、備考をあたかも例文のように扱って半角パイプ文字で解決してほしい。

