<!--
# Variable Bindings
-->
# 変数束縛

<!--
Rust provides type safety via static typing. Variable bindings can be type
annotated when declared. However, in most cases, the compiler will be able
to infer the type of the variable from the context, heavily reducing the
annotation burden.
-->
Rustは静的(`static`)な型付けゆえに型安全です。変数束縛は宣言時に型を指定できます。とはいえたいていの場合は、コンパイラは変数の型をコンテキストから推測することができますので、型指定の負担を大幅に軽減できます。

<!--
Values (like literals) can be bound to variables, using the `let` binding.
-->
値（リテラルなど）は`let`を用いて変数に束縛することができます。

```rust,editable
fn main() {
    let an_integer = 1u32;
    let a_boolean = true;
    let unit = ();

    // copy `an_integer` into `copied_integer`
    // `an_integer`を`copied_integer`へとコピー
    let copied_integer = an_integer;

    println!("An integer: {:?}", copied_integer);
    println!("A boolean: {:?}", a_boolean);
    println!("Meet the unit value: {:?}", unit);

    // The compiler warns about unused variable bindings; these warnings can
    // be silenced by prefixing the variable name with an underscore
    // 使用されていない変数があると、コンパイラは警告を出します。
    // 変数名の頭に`_`（アンダーバー）を付けると警告を消すことができます。
    let _unused_variable = 3u32;

    let noisy_unused_variable = 2u32;
    // FIXME ^ Prefix with an underscore to suppress the warning
    // FIXME ^ 頭にアンダーバーを付けて、警告を抑えましょう。
}
```
