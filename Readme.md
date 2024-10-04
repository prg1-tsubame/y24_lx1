# `lx01` プロジェクト

`sbt` は `*.sbt` ファイルがあるディレクトリで起動します。

なんで `lx01` なの？ → `sbt` を実行するとき、`*.sbt` という形式の `sbt` プロジェクトの定義ファイルを探します。このプロジェクトの場合は `lx01.sbt` が該当します。配布されたファイルのなかで `lx01.sbt` が存在するのは `lx01` ディレクトリです。ですので、`sbt` を起動するまに、そのディレクトリに移動してから実行なければいけません。


# [`hello1.scala`](src/hello1.scala)

Scala の最小構成のプログラムの例。

実行文は `@main` 修飾を与えられた `def main` 宣言のなかに記述します。`@main` 宣言された宣言のなかの記述は Scala のプログラムで最初に呼び出されます。

    `def main` で定義されている `main` という名前は任意です。ほかの名前（たとえば `hello1` とか）に変えても、構いません。変更して `sbt run` して、このことを確認してみましょう。

`println` は Scala から文字列を標準出力に送るための関数。


# [`hello2.scala`](src/hello3.scala)

複数の文を順次実行する例。特に難しいこともなく、期待する順序で文を並べればその順に実行されます。


# [`hello3.scala`](src/hello4.scala)

定数定義は `val 定数名 = 定数の値` の形式を取ります。定数のスコープ内であれば、どこからも定数の値を定数名で参照できます。

- この例の `val` 宣言は `def main` 宣言の内側で宣言されています。`def main` 宣言の内側で宣言された定数は、`main` 手続きの `{` と `}` で挟まれた範囲で有効になります。このような有効範囲のことを**宣言のスコープ**と呼びます。

- `val` 宣言は、ほかの宣言の内側がだけでない場所に移動することもできます。ほかの宣言に含まれないスコープのことを**大域的なスコープ**と呼びます。大域的なスコープ（あるいは**大域スコープ**）で宣言された値は、プログラム中のどこからも参照されます。


# [`hello4.scala`](src/hello4.scala)

`def main` 宣言の内側では自分が定義した関数を呼び出すことができます。この例では役割 (`role`) と氏名 (`professor`) を与えられると、その人物の紹介文を出力する `hello` 関数を使っています。

Scala における普通の関数定義の方法は以下の通りです。

```
def 関数名(引数名1: 型1, ...): 返り値の型 = {
  関数の本体
}
```

特に関数の本体がひとつの式だけで構成されている場合は：

```
def 関数名(引数名1: 型1, ...): 返り値の型 = 返り値の式
```

関数が値を返さない場合、返り値の型として `Unit` を宣言します：

```
def 関数名(引数名1: 型1, ...): Unit = {
  関数の本体
}
```

`hello5.scala` で定義された `hello` 関数は値を返さないため最後の形式で定義してあります。


# [`hello5.scala`](src/hello5.scala): おまけの便利機能（文字列補完）

2つの文字列型の変数 `role` と `professor` があって、これらを使った文を構成することを考えます。このとき `+` 演算子を使って、`role + "担当は" + professor + "です。"`と書くことができます。でも、この書き方では引用符や演算子が邪魔をして、何が出力するのか理解しにくい場合もあります。Scalaは文字列定数の前に`s`と書いておけば、文字列のなかに変数の値を埋め込むことができます。

    s"${role}担当は${professor}です。"

この例で、`role = 講義`、`professor = 脇田 建`の場合、"講義担当は脇田 建です" という文字列が構成されます。

このように、文字列のなかに Scala の変数を埋め込んで、変数の値で文字列の内容を拡張する仕組みのことを*文字列補完*と呼びます。

さらに面白い文字列補完の機能として任意の Scala の式の値を埋め込むこともできます。

たとえば、`s"${role}担当は${instructors(instr)}です。"`の場合、`List`型の変数`instructors`の`instr`番目の要素を埋め込んでいます。

ここで `instr` という名前の変数を用いています。Scala の変数については、授業のなかでまだ学んでない内容ですが、変数の概念は Python や C と似ているのでなんとなくわかるでしょう。ここでは、`instr` の値は 0 で初期化され、`hello` 関数が呼び出されるごとに1ずつ大きくなります。

# `hello.{scala,c}`

プログラミング言語の実行方式（たとえば、インタプリタ、コンパイラなどの例として作った）