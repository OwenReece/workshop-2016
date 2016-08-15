# Perl入学式
### 第4回 サブルーチン/正規表現編

___
## 諸注意
- 会場について
    - 飲食・喫煙・トイレetc
- 写真撮影について
    - 写真撮影NGな方はお手数ですが申し出てください

___
## 紹介
- 講師・サポーター紹介

___
## 本日の内容
- リファレンスの復習
- サブルーチン
- サブルーチンとリファレンス
- 正規表現
- 正規表現と置換
- 正規表現とメタ文字
- 正規表現のオプション

___
## 皆さんで自己紹介

---
# リファレンスの復習

- [前回の復習問題](https://github.com/perl-entrance-org/workshop-2015-03/blob/master/practice.md)の｢score.pl｣の一部の問題を解きながら, リファレンスを復習してみましょう.
- [こちら](https://github.com/perl-entrance-org/workshop-2015-03/blob/master/code/score.pl)にサンプルデータがあります.

---
# サブルーチン

___
## サブルーチンとは?
- プログラムの中で, 意味や内容がまとまっている作業をひとかたまりにしたものを｢サブルーチン｣と呼びます.
- Perlにおける｢サブルーチン｣は, ｢関数｣とほぼ同義です.

___
## 組み込み関数
- Perlには, これまで使ってきた`print`や`join`など, Perlが提供する関数(組み込み関数)が用意されています
- サブルーチンを使うことで, `print`や`join`のように, ｢特定の処理をするコード｣をひとかたまりにして, 簡単に呼ぶことが出来るようになります.

___
## サブルーチンの定義
- それでは, 早速サブルーチンを定義していきましょう.
- 今回は, 末尾に自動的に改行(`\n`)を付与しながら文字列を表示する`say`というサブルーチンを定義してみます.

___
## サブルーチンの定義

    sub say {
        my $str = shift @_;
        print "$str\n";     
    }
    say("hello, world!"); # => hello, world![改行]

- それでは, 詳しく見て行きましょう.

___
## サブルーチンの定義
    sub say { ... }

- Perlでサブルーチンを定義する為には, `sub サブルーチン名 { ... }`と書きます.
- 末尾の`}`の後に, `;`を書く必要はありません.
- サブルーチン名として使える文字は大文字･小文字の英数字と, アンダースコア(`_`)です.
    - 但し, サブルーチン名の先頭は英文字か`_`でなければなりません.

___
## サブルーチンの定義

    sub output_data { ... }

- 複数の単語でサブルーチン名を構築する時は, このように単語どうしを`_`で繋げる(スネークケース)場合が多いです.

___
## クイズ

    sub hoge!    { ... }
    sub _hoge    { ... }
    sub 1hoge    { ... }
    sub hoge_123 { ... }

- この中で, サブルーチン名として正しいものはどれでしょうか ?

___
## 正解は?

    sub hoge!    { ... } # => '!'はサブルーチン名に使えない
    sub _hoge    { ... }
    sub 1hoge    { ... } # => 先頭は英字or'_'
    sub hoge_123 { ... }

- 正解は`_hoge`と`hoge_123`です.

___
## サブルーチンの呼び出し

    say('hoge');

- 定義したサブルーチンは, 定義したサブルーチン名の後ろに`()`を付けることで呼び出せます.
- サブルーチンに値(引数)を渡したい場合, `()`の中に書きます.
- `()`を使わずに, 先頭に`&`を付けて`&say`で呼びだすこともできますが, 古い書き方なので使わないようにしましょう.

___
## サブルーチンの引数
    sub say {
        my $str = shift @_; # @_ => ('hoge')
        ...
    }
    say('hoge');

- サブルーチンに与えられた引数は, `@_`という配列(無名配列)に格納されます.
- 2行目では, `shift`を使って, この`@_`の先頭の要素を取得しています.
- このサブルーチンを`say('hoge');`のように呼んだ場合, `@_`の中身は`('hoge')`になるので, `$str`には`hoge`という文字列が入ります.

___
## サブルーチンの引数
    sub say {
        my $str = shift;
        ...
    }

- サブルーチンに与えられた引数が格納されている`@_`は, 省略することができます.
- その為, 2行目の`my $str = shift;`は, `my $str = shift @_;`と同じ意味になります.

___
## サブルーチン｢add｣

    sub add {
        my ($left, $right) = @_;
        return $left + $right;
    }
    my $result = add(2, 5);

- 次に, 2つの引数を受け取り, その和を返すサブルーチン`add`を考えてみることにします.
- `add`サブルーチンの定義と呼び出しは, このように書くことができます.

___
## サブルーチンの引数

    sub add {
        my ($left, $right) = @_;
        ...
    }
    my $result = add(2, 5);

- サブルーチンに複数の引数が与えられた場合(この場合は`2`と`5`), サブルーチン側ではこのようにして受け取ることができます.
    - サブルーチンに複数の引数を与える時は, (配列のように)`,`で区切って渡します.

___
## サブルーチンの引数

    sub add {
        my $left  = shift;
        my $right = shift;
        ...
    }

- 先程の引数の受け取り方は, 上記のコードと同じ意味になります.

___
## サブルーチンの返り値

    sub add {
        my ($left, $right) = @_;
        return $left + $right;
    }
    my $result = add(2, 5);

- サブルーチンは, `return`を使うことで, 任意のデータを呼び出し元へ返すことができます.
    - この場合, `$left + $right`の計算結果が, 呼び出し元へ返され, `$result`に格納されます.

___
## 複数個のreturn

    sub same {
        my ($i, $j) = @_;
        if ($i == $j) {
            print "true\n"; # $i == $jなら表示
            return 1;
        } else {
            print "false\n"; # $i != $jなら表示
            return 0;
        }
        print "!?\n"; # 絶対に表示されない!
        return undef;
    }

- `return`はサブルーチンの中に複数個書くことができますが, `return`に到達した場合, それ以降の処理は一切行われず, すぐさま値を返してサブルーチンの実行を終了します.

___
## 複数の返り値

    sub calc {
        my ($left, $right) = @_;
        return ($left + $right, $left - $right);
    }
    my ($add, $min) = calc(5, 4);

- サブルーチンは, このようにリストを返すことで, 複数個の値を返すこともできます.

___
## returnがない場合の返り値

    sub add {
        my ($left, $right) = @_;
        $left + $right;
    }

- サブルーチンの中に`return`がない場合, サブルーチンの返り値は, 最後に評価された処理の結果(この場合, `$left + $right`の計算結果)を返します.

___
## 練習問題
- 次のような機能を持つコードを, `simple_calc.pl`という名前で作成しよう.
    - 2つの引数の和を計算する`add`と同様に, 2つの引数の差を計算する`min`, 積を計算する`mul`, 商を計算する`div`というサブルーチンを作ってみよう.
    - これらのサブルーチンが正しく実装できているか(与えた2つの引数に対して, 適切な値を返すか)を確認するコードを書いてみよう.

---
# サブルーチンと<br>リファレンス

___
## 配列を引数に
    my @hoge = qw/ hoge fuga /;
    my @foo  = qw/ foo bar baz /;
    sub output {
        my (@array1, @array2) = @_;
        print '@array1 = ' . join(',', @array1) . "\n";  
        print '@array2 = ' . join(',', @array2) . "\n";  
    }
    output(@hoge, @foo);

- サブルーチンの引数として, 2つの配列を与えてみましょう.
    - この時, 実行結果はどうなると思いますか? 考えてみましょう.

___
## 配列を引数に

    @array1 = hoge,fuga,foo,bar,baz
    @array2 =

- 実行結果はこのようになります!

___
## 配列を引数に

    @array1 = hoge,fuga
    @array2 = foo,bar,baz

- このようになる, と予測した方は多いのではないでしょうか?

___
## なぜ!?

    my @array1 = qw/ hoge fuga /;
    my @array2 = qw/ foo bar baz /;
    my @array  = (@array1, @array2);
    # @array = ('hoge', 'fuga', 'foo', 'bar', 'baz');

- これは, 複数の配列をリストで評価すると, 展開されて元の配列の区別がなくなってしまう為です.
- 先程の場合, `@_`の中身は`('hoge', 'fuga', 'foo', 'bar', 'baz')になります.
    - Perlは元の配列の`@hoge`と`@foo`の境目が`@_`のどこにあるかわからないので, 全て`@array1`に突っ込もうとします.

___
## そこで!

- この問題を解決する為に, リファレンスを利用することができます!

___
## リファレンス渡し

    my @hoge = qw/ hoge fuga /;
    my @foo  = qw/ foo bar baz /;
    sub output {
        my ($array1, $array2) = @_;
        print '@$array1 = ' . join(',', @$array1) . "\n";  
        print '@$array2 = ' . join(',', @$array2) . "\n";  
    }
    output(\@hoge, \@foo);

- 8行目で配列のリファレンスを渡しているので, 4行目では2つのスカラ変数で引数を受け取っています.

___
## リファレンス渡し

    @$array1 = hoge,fuga
    @$array2 = foo,bar,baz

- 実行してみると, 期待通りの結果を取得することができました.

___
## リファレンス渡し

- 配列と同様に, ハッシュもリファレンスで渡すことができます.
- 更に, リファレンスで渡す場合, 配列をそのまま渡した時のように, データのコピーが発生しません.
- 引数として与えた配列･ハッシュの構造をそのままサブルーチンに渡すことができ, データのコピーが発生しない｢リファレンス渡し｣ですが, 1つ注意点があります.

___
## 中身の書き換え

    my %hash = ( papix => 'dame' );
    print $hash{papix}; # => dame
    fix(\%hash);
    print $hash{papix}; # => perfect
    sub fix {
        my $hash = shift;
        $hash->{papix} = 'perfect';
    }

- サブルーチンに渡される配列･ハッシュのリファレンスは, サブルーチンの外側にある配列･ハッシュの実体(この場合, `%hash`)を指しているので, サブルーチンの中でデータ構造を書き換えると, 外側の実体にも影響が出てしまいます.

___
## 練習問題
- 配列とハッシュをそれぞれ1つずつ定義してから, 第1引数に配列のリファレンス, 第2引数にハッシュのリファレンスを受け取り, その中身を出力する(for文などを利用して...), `output_array_and_hash`というサブルーチンを書いてみよう.
- このコードは, `output_array_and_hash.pl`という名前で保存するようにしましょう.

---
# 正規表現

___
## 正規表現
- ここでは, データ処理の強い味方｢正規表現｣を取り上げます.
    - 正規表現を使うことで, 文字列を自由自在に検出したり, 置き換えたりすることができます.
- 正規表現は非常に複雑なので(正規表現だけで分厚い1冊の技術書が書けるほどです), Perl入学式で全てを紹介することはできませんが, コードを書く上でよく使う｢基本的な部分｣を中心に, 紹介していきます.

___
## パターンマッチ
    my $str = 'papix loves perl!';
    if ($str =~ /perl/) {
        print "'$str'は'perl'を含みます.";
    }

- `$str =~ /perl/`は, `$str`の中に｢perl｣という文字列が含まれるなら真, そうでないなら(含まれないなら)偽, になります.
- この, `/`に囲まれた, 文字列のパターンを表現するものが｢正規表現｣です.

___
## パターンマッチ

    my $str = 'papix loves perl!';
    if ($str eq 'perl') {
        print "'$str'は'perl'です.";
    }
    if ($str =~ /perl/) {
        print "'$str'は'perl'を含みます.";
    }

- `eq`は完全一致か否かしか判定できません. しかし正規表現とパターンマッチを活用することで, ｢xxxという文字列を含む｣や, その逆の｢xxxという文字列を含まない｣といった複雑な判定を行うことができます.

___
## パターンマッチ
    my $str = 'papix loves perl!';
    if ($str !~ /ruby/) {
        print "'$str'は'ruby'を含みません.";
    }

- `$str !~ /ruby/`と書くことで, `$str`の中に｢ruby｣という文字列を含まないなら真, そうでないなら(含むなら)偽, になります.

___
## 任意の1文字
    my $ans = 'y';
    if($ans =~ /[yY]/) {
        print "文字列にはyないしYが含まれています.\n";
    }

- `[`と`]`で文字をくくると, []の中の任意の1文字にマッチします.
- よって`/[yY]/`は, `y`ないし`Y`にマッチします.

___
## 任意の1文字(否定)
    my $ans = 'n';
    if($ans =~ /[^yY]/) {
        print "文字列にはyないしY以外の文字が含まれています.\n";
    }

- `[`と`]`で文字をくくり, その先頭に`^`を置くと, []の中にない任意の1文字にマッチします.
- よって`/[^yY]/`は, `y`ないし`Y`以外の文字にマッチします.
- `^`は, 必ず`[`の後に置いて, `[^`の形で用います.

___
## 任意の1文字(連続)
    my $ans = 'b';
    if($ans =~ /[a-c]/) {
        print "文字列にはa, b, cのいずれかが含まれています.\n";
    }

- `[`と`]`の中で, 文字の間に`-`を挟むことによって, 文字列の範囲を表現できます.
- この場合, `[a-c]`は`[abc]`と同じ意味になります. `[1-5]`のように, 数値に対しても利用できます.

___
## ワイルドカード
    my $ans = 'get';
    if($ans =~ /g.t/) {
        print "マッチ!\n";
    }

- `.`は, 改行文字(`\n`)を除く, 任意の1文字にマッチします.
- よって`/g.t/`は, `get`や`got`など, `g+任意の1文字+t`にマッチします.
    * `.`がマッチするのは1文字だけなので, `goat`などはマッチしません.
    * また, `gt`にもマッチしません.

___
## 量指定子'?'
    my $ans = 'gt';
    if($ans =~ /g.?t/) {
        print "マッチ!\n";
    }

- `?`は, その直前の要素が0個または1個の場合にマッチします.
    * 例えば`ab?`は, `a`または`ab`にマッチします.
- よって`/g.?t/`は, `g+任意の1文字+t`に加え, `gt`にもマッチします.

___
## 量指定子'+'
    my $ans = 'get';
    if($ans =~ /g.+t/) {
        print "マッチ!\n";
    }

- `+`は, その直前の要素が1個以上の場合マッチします.
    * 例えば`ab+c`は, `abc`や`abbbbc`などにマッチしますが, `ac`にはマッチしません.
- よって, `/g.+t/`は, `g+任意の1文字以上+t`にマッチします.

___
## 量指定子'*'
    my $ans = 'great';
    if($ans =~ /g.*t/) {
        print "マッチ!\n";
    }

- `*`は, その直前の要素が0個以上の場合マッチします.
    * 例えば`ab*c`は, `ac`や`abc`, `abbbbbc`などにマッチします.
- よって`/g.*t/`は, `g`で始まり`t`で終わる全てのフレーズとマッチします(`great`など).

___
## 柔軟な量指定子
    my $str = 'Gyaaaaaaaaa!';
    print "マッチ!\n" if $str =~ /a{5,}/;
    # マッチする
    my $str2 = 'Gyaa!';
    print "マッチ!\n" if $str2 =~ /a{5,}/;
    # マッチしない

- `{m,n}` ... その直前の要素がm回以上, n回以下繰り返す場合マッチ
- `{m,}` ... その直前の要素がm回以上繰り返す場合マッチ
- `{m}` ... その直前の要素がm回繰り返す場合マッチ

___
## 練習問題

- 引数として文字列を受け取り, その文字列に`perl`ないし`Perl`が含まれるなら｢Perl Monger!｣と表示するサブルーチン`perl_checker`を書いてみましょう.
- コードは, `perl_checker.pl`という名前で保存するようにしましょう.

___
## マッチした文字列の取得
    my $str = '私は perl が好きです.';
    if($str =~ /私は (.+) が好き/) {
        print "彼は, $1 が好きです.\n";
        # => 彼は, perl が好きです
    }

- 正規表現のパターンを`()`を囲むと, そのパターンに一致する文字列を取得することができます.
- 例えばこの場合, $1には`perl`が入り, `彼は, perl が好きです.`と表示されるはずです.

___
## マッチした文字列の取得
    my $str = '私は perl と 旅行 が好きです.';
    if($str =~ /私は (.+) と (.+) が好き/) {
        print "彼は, $1 と $2 が好きです.\n";
        # => '彼は, perl と 旅行 が好きです.'と表示.
    }

- 複数の`()`が存在する場合, 先頭から`$1`, `$2`... で取得することができます.

___
## マッチングの原則
    my $str = 'Hello hoge! Hello fuga!';
    if($str =~ /Hello (.+)!/) {
        print "Nice to meet you, $1!\n";
    }

- `hoge`を抜き出して`Nice to meet you, hoge!`としたいので, このようなコードを書きました.
- しかしながら, 実際には`Nice to meet you, hoge! Hello fuga!`と表示されます.

___
## マッチングの原則
    my $str = 'Hello hoge! Hello fuga!';
    if($str =~ /Hello (.+?)!/) {
        print "Nice to meet you, $1!\n";
    }

- これは, 正規表現が｢なるべく長くマッチする(最長マッチ)｣ようになっている為です.
- このように, 量指定子のあとに`?`を付けて, 最短マッチにすれば, `Nice to meet you, hoge!`と出力されるはずです.

___
## 練習問題
    my $words_ref = [
        'papix loves meat!',
        'boolfool loves sushi!',
    ];

- このような配列のリファレンスを受け取り, リファレンスに格納された文字列について, ｢loves｣の後に記述されている好きな食べ物の単語を正規表現で取得し, ｢papix -> meat｣, ｢boolfool -> sushi｣のように表示するサブルーチン, `love_food`を書いてみよう.
- このコードは, `love_food.pl`という名前で保存するようにしましょう.

---
# 正規表現と置換

___
## 置換
	my $str = 'abc def ghi';
	$str =~ s/abc/ABC/;
	# $str = 'ABC def ghi';

- `s/PATTERN/REPLACE/`で, `PATTERN`を`REPLACE`に置換します.
    - `PATTERN`を記述する為に, 正規表現を利用することができます.
- `$str`に含まれる全ての`PATTERN`を置換したい場合, `s/PATTERN/REPLACE/g`と表記します.
    - 最後にオプションとして`g`を付けることで, 繰り返し評価･置換します.

___
## 変数の使用

	my $str = 'perl ruby python';
	my $pattern = 'perl';
	if($str =~ /$pattern/) {
		print "'$str'には'$pattern'が含まれます.\n";
	}

- このように, 正規表現として変数を利用することもできます.

___
## 練習問題
    my $str = 'I love ruby';

- この`$str`に格納された文字列を, 置換を利用して, ｢I love perl｣に書き換えるようなコードを書いてみましょう.
    - コードは, `regexp_replace.pl`という名前で保存しましょう.

---
# 正規表現とメタ文字

___
## メタ文字
- メタ文字を使うと, ｢数字とマッチ｣や｢アルファベットとマッチ｣などといった正規表現を, より簡単に表現することができます.
- ここでは, よく使うメタ文字を紹介します.

___
## メタ文字(1)

- `\w` ... アルファベット, 数字, アンダーバーの1文字
	* `[a-zA-Z0-9_]`と同じ意味です.

- `\W` ... アルファベット, 数字, アンダーバー以外の1文字
	* `[^a-zA-Z0-9_]`と同じ意味です.

- `\d` ... 数字の1文字
	* `[0-9]`と同じ意味です.

- `\D` ... 数字以外の1文字
	* `[^0-9]`と同じ意味です.

___
## メタ文字(1)
- `\s` ... 空白文字にマッチ
	* `[ \n\r\f\t]`と同じ意味です.

- `\S` ... 空白文字以外にマッチ
	* `[^ \n\r\f\t]`と同じ意味です.

___
## メタ文字(1) 使い方

	my $str1 = '2012年7月22日';
	if($str1 =~ /(\d+)年(\d+)月(\d+)日/) {
		print "$1/$2/$3";
		# "2012/7/22"と表示される.
	}
	my $str2 = "この    文章  は\n 読みにく\nい    で  \t    す\n";
	$str2 =~ s/\s+//g;
	# $str2 = "この文章は読みにくいです";

- `\s`を使えば, 余分な空白や改行を抜き取ることができます.

___
## メタ文字(2)
- `|` ... 選択一致（OR検索）
	* 例えば, `abc|def|ghi`は, `abc`, `def`, `ghi`のいずれかにマッチします.
- `(x)` ... グループ化
	* 正規表現をグループ化します.
	* 先に説明したように, `()`の中のパターンにマッチした文字列は記憶され, `$1`や`$2`のように後で参照することができます(後方参照).
- `(?:x)` ... 後方参照しないグループ化
	* 正規表現をグループ化しますが, `()`の中のパターンにマッチした文字列は記憶されません.

___
## メタ文字(2) 使い方
	my $str = 'perl is good!';
	if($str =~ /(?:perl|ruby|python) is (good|bad)!/) {
		print "評価は $1 です!\n";
		# "評価は good です!"と表示される.
	}

- `perl`, `ruby`, `python`を`|`でつなぎ, `(`と`)`で囲うことで, 選択一致をグループ化しています.
- 更に, `(?:`とすることで, 後方参照しないようにしています.
	* その為, $1は`(good|bad)`のパターンにマッチした文字列となります.

___
## 正規表現のメタ文字(3)
	my $str = 'john is dead.';
    if ($str =~ /dead\./) {
        print "match!\n";
    }

- `\` ... メタ文字を無効化する
	- 正規表現の中で特殊な意味を持つ文字(例えば`/`や`.`など)を無効化します.
- この場合. `$str =~ /dead./`は, `john is dead!`などでもマッチしてしまう(`.`は任意の1文字とマッチ, なので).
- `\.`のようにすれば `.`そのものとのマッチができます.

___
## アンカー
- アンカーは, 行頭や行末など, 文字列の特定の位置とマッチします.
    - `^` ... 行頭
    - `$` ... 行末

___
## アンカー 使い方
	my $str = 'john is great';
	# 行頭に'john'がある場合のみマッチ
    if ($str =~ /^john/) {
        print "match!\n";
    }

___
## 区切り記号の変更(1)
	my $str = '/usr/local/bin/perl';
    if ($str =~ m|bin/perl|) {
        print "match!\n";
    }

- 正規表現は`/`で区切りますが, `/`だと不都合な場合も多いです(例えば, URLを表記する場合など. 全ての`/`をエスケープする必要がある).
- そこで, `m//`のように, 先頭に`m`を付けると, 任意の記号のペアを区切り記号として利用することができます.
- この場合, `|`を区切り記号にしています. よって, `/`をエスケープする必要はありません.

___
## 区切り記号の変更(2)
	my $str = '/usr/local/bin/perl';
	$str =~ s|/usr/local/bin/|/usr/bin/|;

- 置換の場合, このようにできます.

---
# 正規表現のオプション

___
## 繰り返してマッチ(g)
	my $str = 'Hello, hoge! Hello, fuga!';
	my @name = ($str =~ /Hello, (\w+?)!/g);
	# @name = ('hoge', 'fuga'); となる.

- `g`は, 正規表現のマッチングを繰り返し行います.
- また, 正規表現に`()`が含まれる場合, マッチした文字列のうち`()`の中に含まれる文字列をリストとして返します.

___
## 繰り返してマッチ(g)
	my $str = 'Hello, hoge! Hello, fuga!';
	my $str =~ s/Hello/Good morning/g;

- 置換の部分で説明したように, `s///g`とすると, 置換の処理を繰り返し行なってくれます.

___
## 大文字/小文字を区別しない(i)
	my $str = 'John and Beth';
    if ($str =~ /john/i) {
        print "match!\n";
    }

- `i`は, 正規表現中のアルファベットの大文字･小文字を区別せずにマッチングを行います.
- よって, `/john/i`は, `john`はもちろん, `John`や`JOHN`, `jOhN`などにもマッチします.

___
# 練習問題 (1/3)

    while (chomp(my $input = <STDIN>)) {
        ...
    }

- 上記のコードは, 標準入力から入力された文字列を, ひたすら`$input`に代入するコードである.
- このコードの`...`の部分を, 次の条件を満たすように書き換えてみよう.
- この問題のコードは, `while_input.pl`という名前で保存するようにしよう.

___
# 練習問題 (2/3)
- 文字列が`0`の場合, ループを抜ける(`last`を使って...).
- 文字列が`perl`ないし`Perl`を含む場合, ｢Find Perl!｣と表示する.
- 文字列に大文字小文字問わず, `python`の文字列が含まれる場合, ｢Find Python!｣と表示する.
- 文字列に`perl`ないし`ruby`ないし`python`が含まれる場合, ｢Love Programming!｣と表示する. 

___
# 練習問題 (3/3)
- 文字列の先頭に`papix`がある場合, ｢Find papix!｣と表示する.
- 文字列に`Hello`が含まれる場合, その後に続く単語`xxxx`を使って｢Hello! xxxx!｣と表示する.
    - 例えば, 文字列に｢Hello papix｣が含まれる場合, ｢Hello! papix!｣と表示すればOKです.

---
# 質問タイム

---
# お疲れさまでした