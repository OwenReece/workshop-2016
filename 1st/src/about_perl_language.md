# Perlという言語について

## Perlって何?
- 1987年, Larry Wall(右写真)が開発したプログラミング言語です.
<img src="public/image/larry.jpg" align='right'>
    - Ruby, Python, PHPと並ぶLL言語(Lightweight Language)と呼ばれるカテゴリのプログラミング言語の1つです.
        - 後のRubyやPHPに影響を与えました.
    - C言語やsed(せど), awk(おーく)の影響を受けた動的型付け言語です.
    - ｢Perl｣は言語そのもの, ｢perl｣はその処理系を示します.

## Perlの特徴
- [Wikipediaの記事](http://ja.wikipedia.org/wiki/Perl)から重要なものだけ引用します...
    - 強力な文字列処理. 正規表現をサポート.
    - 日本語をはじめとして世界中の言語を処理可能.
    - 自由度の高い文法. 簡潔にプログラムを記述できる.
    - 高い後方互換性を持つ.
    - 数多くのオペレーティングシステムで利用可能.
    - プログラムの実行には事前コンパイルは不要.
    - 有志によって開発された豊富なモジュール.

## TMTOWTDI
- Perlのスローガン. ｢ティムトゥーディー｣と読みます.
    - "There's more than one way to do it."
    - ｢やり方はひとつじゃない｣.
- Larryは｢プログラミング言語は, いろんな対象をシンプルに記述する為に, ある程度複雑でなければならない｣と信じています.
    - Perlは, 同じ意味を持つ処理をいろいろな書き方で表すことができます.
    - これについては, きっとこれからのPerl入学式のカリキュラムの中で実際に体験することが出来ると思います.

## 高い後方互換性
- Perlのバージョンアップによって昔のスクリプトが動かなくなる, ということは**ほとんど**ありません.
- もちろん, Perlもバージョンアップによる細かい機能変更はあります.
    - しかし, 基本的な処理については後方互換性が相当繊細なまでに維持されています.

## 豊富なモジュール
- CPANと呼ばれるアーカイブに, 全世界のPerl Mongerがモジュールを投稿しています.
    - Perl Monger ... Perl使い, Perlを得意とするエンジニアのこと. RubyにおけるRubyist, PythonにおけるPythonistaと同義です.
    - 皆さんも今日からPerl Mongerです!
- 例: Encode ... 文字列のエンコードを処理するモジュール.
- 例: Net::Twitter ... TwitterのAPIを操作するモジュール.
- 例: DBD::SQLite ... Perlから, SQLiteというデータベースを操作するモジュール.

## Perl5 のバージョンの歴史
- Perl 4以前は前史として, 既に周囲に環境が存在しないと思って良いです.
- Perl 5.00x(xは数字)というバージョンでPerl5が登場しました. 1994年のことです.
- Perl 5.6が登場. 2000年. この頃からインターネットやウェブというものが徐々に一般に普及していきます.
- Perl 5.8が登場. 2002年. 国際化対応や今につながる様々な機能が搭載されます. 5.8時代が長かったため, 多くの企業等に長きにわたって使われ続けました.

## Perl5 のバージョンの歴史
- Perl 5.10が登場. 2007年. 後方互換性を損ねない構文拡張等を行います.
- Perl 5.12が登場. 2010年.
- Perl 5.14が登場. 2011年.
- Perl 5.16が登場. 2012年.
- Perl 5.18が登場. 2013年.
- Perl 5.20が登場. 2014年.
- Perl 5.22が登場. 2015年.
- Perl 5.24が登場. 2016年. 現在の最新の安定版です.

## Perl5 のバージョンの歴史
- 5.(偶数) が安定版. 5.(奇数) が開発版です.
- 基本的に最新版の一つ手前の安定版までがサポート対象です.
- Perl 5.8時代が長かったので, 今もPerl 5.8が生き残っている現場はあるものの, 今ならPerl 5.10以降だけを考えれば良いです.
- Perl 5.10以降から5.20まで, Perl初学者にとって大きな違いはあまりありません.

## 余談: Perl6について
- Perl 5とは別に, Perl 6も開発されています.
    - 当初はPerl5の後継となるはずだったが, 後に｢Perl5とは別に開発を進める｣と公式に発表されました.
    - よって, Perl5の開発は継続されます.
    - また, 現在ではPerl 6はPerl 5とは別の言語とみなされている, と解説されることもあるほど互換性はありません.
        - これはPerl5のバージョン間での互換性が最大限に保たれていることの裏返しでもあります.
    - 現在の最新の安定版は5.24.0(2016年5月12日現在), バージョンを確認する `perl -v` では, Perl5のバージョン24, のように表記されています.

## Perlのコミュニティ
- 世界各地にPerl Monger(PM)のコミュニティが存在します.
    - 地域のPerl Mongrerコミュニティは, (地名).pmを名乗ることが多いです.
    - 日本でも, 十数個のコミュニティ, 勉強会が開催されています.

## 地域コミュニティ
- pm.orgに登録されている, 公認のコミュニティ.
    - Hokkaido.pm, Kushiro.pm, Sendai.pm, Niigata.pm, Tokyo.pm, Shibuya.pm, Yokohama.pm, Kamakura.pm, Gotanda.pm, Nagoya.pm, Kansai.pm, Kyoto.pm, Fukuoka.pm, Okinawa.pm
- 非公認のコミュニティ
    - Hachioji.pm ...
- 勉強会/イベント
    - Hokkaido.pm Casual, Perl Casual, Perl入学式, よなべPerl...

## YAPC::Asia Tokyo
- YAPC ... Yet Another Perl Conference
    - 年に一度行われる, 日本最大規模のPerlの祭典です.
- 今年は[北海道で開催予定](http://blog.perlassociation.org/2016/04/japan-perl-associationjpa.html)と告知されています.
- また, [Yet Another Pachimon Conference](http://yapcasia8oji-2016mid.hachiojipm.org/)なるイベントも...

## PerlとCGI
- 一時期, ｢PerlでWebサービスを作るならCGI｣という時代がありましたが, 今はそうではありません.
- 最近は, PSGI(Perl Web Server Gateway Interface)という仕様に対応したWAF(Web Application Framework)を使っての開発が増えています.
    - 2016年現在, Perlの代表的かつ新規採用されやすいWAFとしては, MojoliciousやAmon2などがあります.
- Perl入学式は｢モダンなPerlを教える｣という方針を取っていますので, CGIについては触れません.