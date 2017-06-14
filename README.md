[![Build Status](https://travis-ci.org/lpenz/rust-sourcebundler.svg?branch=master)](https://travis-ci.org/lpenz/rust-sourcebundler)

# rust-sourcebundler

Bundle the source code of a rust cargo crate in a single source file.

Very useful for sending the source code to a competitive programming site that
accept only a single file ([codingame](https://codingame.com), I'm looking at
you) and still keeping the cargo structure locally.


## Usage

Add the following snippet to your *Cargo.toml*:

```
[package]
(...)
build = "build.rs"

[build-dependencies]
rustsourcebundler = { git = "https://github.com/lpenz/rust-sourcebundler" }
```

And create the file *build.rs* with the following:

```
/*! Bundle mybin.rs and the crate libraries into singlefile.rs */

use std::path::Path;
extern crate rustsourcebundler;
use rustsourcebundler::Bundler;

fn main() {
    let mut bundler: Bundler = Bundler::new(Path::new("src/bin/csbk.rs"),
                                            Path::new("src/bin/singlefile.rs"));
    bundler.run();
}
```