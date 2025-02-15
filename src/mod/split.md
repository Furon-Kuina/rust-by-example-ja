<!--
# File hierarchy
-->
# ファイルの階層構造

<!--
Modules can be mapped to a file/directory hierarchy. Let's break down the
[visibility example][visibility] in files:
-->
モジュールはファイル・ディレクトリ間の階層構造と対応関係にあります。モジュールに[お互いがどのように見えているか][visibility]、以下の様なファイルを例に詳しく見ていきましょう。

```shell
$ tree .
.
├── my
│   ├── inaccessible.rs
│   └── nested.rs
├── my.rs
└── split.rs
```

In `split.rs`:

```rust,ignore
// This declaration will look for a file named `my.rs` and will
// insert its contents inside a module named `my` under this scope
// このように宣言すると、`my.rs`という名のファイルを探し、
// その内容をこのファイル中で`my`という名から使用することができるようにします。
mod my;

fn function() {
    println!("called `function()`");
}

fn main() {
    my::function();

    function();

    my::indirect_access();

    my::nested::function();
}

```

In `my.rs`:

```rust,ignore
// Similarly `mod inaccessible` and `mod nested` will locate the `nested.rs`
// and `inaccessible.rs` files and insert them here under their respective
// modules
// 同様に`mod inaccessible`、`mod nested`によって、`nested.rs`、`inaccessible.rs`の内容をこの中で使用することができるようになる。
// 訳注: `pub`をつけないかぎり、この中でしか使用できない。
mod inaccessible;
pub mod nested;

pub fn function() {
    println!("called `my::function()`");
}

fn private_function() {
    println!("called `my::private_function()`");
}

pub fn indirect_access() {
    print!("called `my::indirect_access()`, that\n> ");

    private_function();
}
```

In `my/nested.rs`:

```rust,ignore
pub fn function() {
    println!("called `my::nested::function()`");
}

#[allow(dead_code)]
fn private_function() {
    println!("called `my::nested::private_function()`");
}
```

In `my/inaccessible.rs`:

```rust,ignore
#[allow(dead_code)]
pub fn public_function() {
    println!("called `my::inaccessible::public_function()`");
}
```

<!--
Let's check that things still work as before:
-->
では、以前と同じように実行できるか確認しましょう。

```shell
$ rustc split.rs && ./split
called `my::function()`
called `function()`
called `my::indirect_access()`, that
> called `my::private_function()`
called `my::nested::function()`
```

[visibility]: visibility.md
