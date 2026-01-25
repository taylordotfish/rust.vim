taylor.fish fork of rust.vim
============================

This is a fork of [rust.vim][upstream] with an updated syntax highlighting file
([syntax/rust.vim][syntax]).

For the original README, see [README.orig.md][orig].

[upstream]: https://github.com/rust-lang/rust.vim
[syntax]: syntax/rust.vim
[orig]: README.orig.md

Installation
------------

Copy `syntax/rust.vim` to `~/.vim/syntax/`:

```sh
git clone https://codeberg.org/taylordotfish/rust.vim
mkdir -p ~/.vim/syntax
cp rust.vim/syntax/rust.vim ~/.vim/syntax/
```

Changes
-------

* Added ability to customize which edition is used for highlighting.
  Set `g:rust_edition` before the syntax file is loaded; e.g.,
  `let g:rust_edition = 2021` or `let g:rust_edition = "latest"`.
* Enum variants that happen to have the same name as a prelude item are no
  longer highlighted; e.g., `enum Shape { Box, Sphere }` or
  `let s = Shape::Box`. (Note that this also applies to associated types in
  paths, as in `let x: <T as Trait>::String`.)
* Added support for `safe fn`.
* Added support for `&raw const` and `&raw mut`.
* Added support for the `gen` keyword. (Fixes [#521].)
* Added support for items added to the prelude in the 2021 and 2024 editions,
  like `TryFrom` and `Future`.
* Updated list of derive macros.
* Keywords in positions where an item name is expected are now highlighted
  (e.g., `fn do() {}` or `mod priv;`). (Fixes [#406].)
* Added support for non-ASCII characters in identifiers (`Café::new()`).
* Added support for `?` as a macro repetition operator (`$()?`).
  (Fixes [#498].)
* Added support for raw identifiers in paths and function calls (`r#foo()`).
* `as` is now highlighted as a keyword rather than an operator. (Fixes [#493].)
* Improved highlighting of `async`, `await`, `try`, and `dyn`.
* Improved highlighting of `impl ... for ...` using proper parsing.
* Improved detection of turbofish function calls (`f::<T>()`).
* Improved parsing of attributes (fixes cases like `#[[]]`).
* Fixed highlighting of successive reference-of operators (`&&x`).
* Fixed parsing of `/* */*` (previously parsed as a comment containing an
  unclosed nested comment).
* Improved detection of which Markdown code blocks should be highlighted as
  Rust code in doc comments.
* Fixed parsing of multiline attributes and macro repetition expressions
  (`$(x)*`) inside code blocks in doc comments.
* Fixed parsing of non-Rust code blocks in block doc comments (`/** */`).
* Fixed parsing of doc comments containing an unclosed code block.
* Leading `# ` characters in doc comment code blocks (to hide lines in
  rustdoc’s output) are now highlighted.
* Added option not to highlight code in doc comments:
  `let g:rust_highlight_doc_code = 0` before the syntax file is loaded.
  (Fixes [#407].)
* Reduced stale highlighting when syntactic constructs span multiple
  lines by setting `syn sync linebreaks` to 1.
* Added a distinct syntax group for prelude structs instead of including
  them in `rustTrait`.
* Reduced false positives in highlighting of assert and panic macros
  (`assertiveness!()`, `paniculate!()`).
* Removed obsolete syntax.

[#521]: https://github.com/rust-lang/rust.vim/pull/521
[#406]: https://github.com/rust-lang/rust.vim/issues/406
[#498]: https://github.com/rust-lang/rust.vim/pull/498
[#493]: https://github.com/rust-lang/rust.vim/issues/493
[#407]: https://github.com/rust-lang/rust.vim/issues/407

License
-------

The changes in this repository are licensed under the same license as the
original: your choice of either the [MIT license](LICENSE-MIT) or version 2 of
the [Apache License](LICENSE-APACHE). For more information, see
[README.orig.md][orig].
