<!--
# Attributes
-->
# アトリビュート

<!--
An attribute is metadata applied to some module, crate or item. This metadata
can be used to/for:
-->
アトリビュートはモジュール、クレート、要素に対するメタデータです。以下がその使用目的です。



<!--
* [conditional compilation of code][cfg]
* [set crate name, version and type (binary or library)][crate]
* disable [lints][lint] (warnings)
* enable compiler features (macros, glob imports, etc.)
* link to a foreign library
* mark functions as unit tests
* mark functions that will be part of a benchmark
* [attribute like macros][macros]
-->
* [コンパイル時の条件分岐][cfg]
* [クレート名、バージョン、種類（バイナリか、ライブラリか）の設定][crate]
* [リント][lint]の無効化
* コンパイラ付属の機能（マクロ、グロブ、インポートなど）の使用
* 外部ライブラリへのリンク
* ユニットテスト用の関数を明示
* ベンチマーク用の関数を明示

<!--
When attributes apply to a whole crate, their syntax is `#![crate_attribute]`,
and when they apply to a module or item, the syntax is `#[item_attribute]`
(notice the missing bang `!`).
-->
アトリビュートがクレート全体に適用される場合、`#![crate_attribute]`という書き方になります。モジュールないしは要素に適用される場合は`#[item_attribute]`になります。（`!`がないことに注目）

<!--
Attributes can take arguments with different syntaxes:
-->
アトリビュートは以下の様な書き方で引数を取ることができます。

* `#[attribute = "value"]`
* `#[attribute(key = "value")]`
* `#[attribute(value)]`

Attributes can have multiple values and can be separated over multiple lines, too:

```rust,ignore
#[attribute(value, value2)]


#[attribute(value, value2, value3,
            value4, value5)]
```

[cfg]: attribute/cfg.md
[crate]: attribute/crate.md
[lint]: https://en.wikipedia.org/wiki/Lint_%28software%29
[macros]: https://doc.rust-lang.org/book/ch19-06-macros.html#attribute-like-macros
