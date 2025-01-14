# fints-institute-db

[![CI](https://github.com/svenstaro/fints-institute-db/workflows/CI/badge.svg)](https://github.com/svenstaro/fints-institute-db/actions)
[![codecov](https://codecov.io/gh/svenstaro/fints-institute-db/branch/master/graph/badge.svg)](https://codecov.io/gh/svenstaro/fints-institute-db)
[![Crates.io](https://img.shields.io/crates/v/fints-institute-db.svg)](https://crates.io/crates/fints-institute-db)
[![docs](https://docs.rs/fints-institute-db/badge.svg)](https://docs.rs/fints-institute-db)
[![license](http://img.shields.io/badge/license-MIT-blue.svg)](https://github.com/svenstaro/fints-institute-db/blob/master/LICENSE)
[![Lines of Code](https://tokei.rs/b1/github/svenstaro/fints-institute-db)](https://github.com/svenstaro/fints-institute-db)

This is a simple crate providing a convenient and safe interface to FinTS information of German banks.
During the build it will download a CSV file with all the banks which it will then put into the library itself so that no extra files have to be taken care of.

## Usage

Put this into your `Cargo.toml`:

```toml
[dependencies]
fints-institute-db = "1.0"
```

Then to use it:

```rust
use fints_institute_db::get_bank_by_bank_code;

if let Some(bank) = get_bank_by_bank_code("12070000") {
    println!("{:?}", bank.pin_tan_address);
}
```

Other use case, find bank by BIC:

```rust
use fints_institute_db::get_bank_by_bic;

if let Some(bank) = get_bank_by_bic("GENODEM1MEN") {
    println!("{:?}", bank.pin_tan_address);
}
```

## Command line utility

Additionally this crate includes a CLI tool for your convenience:

```plain
A library and CLI tool to access FinTS access information for many German banks

Usage: cli [OPTIONS]

Options:
      --iban <IBAN>                Look up bank by IBAN (format: DE02120300000000202051)
      --bankcode <BANK_CODE>       Look up bank by German bank code (format: 12030000)
      --bic <BIC>                  Look up bank by Bank Identifier Code (BIC) (format: GENODEM1MEN)
  -j, --json                       Change tool behavior to output all data for the record as JSON
      --print-completions <shell>  Generate completion file for a shell [possible values: bash, elvish, fish, powershell,
                                   zsh]
      --print-manpage              Generate man page
  -h, --help                       Print help information
  -V, --version                    Print version information
```

Example usages:

```sh
cargo run -- -b 12030000

cargo run -- -i DE02120300000000202051
```

This crate is inspired by https://github.com/jhermsmeier/fints-institute-db and https://github.com/dr-duplo/python-fints-url

## Releasing

This is mostly a note for me on how to release this thing:

- `cargo release`
- `cargo release --execute`
- Releases will automatically be deployed by GitHub Actions.
