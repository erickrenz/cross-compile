# Rust - cross compiling with Cargo

## Usage

This is an example of cross-compiling from x86 (`x86_64`) to ARM (`aarch64`).

1. Install the GCC cross-compilation toolchain with your default package manager (apt-get, dnf, pacman, brew, ...)

```bash
$ sudo apt-get install gcc-aarch64-linux-gnu
```

2. Install the target platform with rustup

```bash
$ rustup target add aarch64-unknown-linux-gnu
```

3. Within your project, create cargo `config.toml` file

```bash
$ mkdir .cargo
$ touch config.toml
```

4. Update `config.toml` with cross compilation details

```toml
[build]
target = "aarch64-unknown-linux-gnu"

[target.aarch64-unknown-linux-gnu]
linker = "gcc-aarch64-linux-gnu"
```

5. Build and test your excecutable on the target system

```bash
# build normally on host
$ cargo build

# copy to target
$ scp target/aarch64-unknown-linux-gnu/debug/cross-compile user@arm:~

# run on target
$ ssh user@arm:~ ./cross-compile
Rust cross compiled from x86_64 -> aarch64
```

## Alternatives

You can choose to manually select your compiler of choice each build of the project.

```bash
# Test locally on x86
cargo build --target=x86_64-unknown-linux-gnu

# Test remotely on ARM
cargo build  --target=aarch64-unknown-linux-gnu
```

If you find yourself doing a lot of local testing, you can comment out the targets in the `config.toml` file. Then you can test locally as you normally would:

```bash
# Test locally on x86 - after commenting out config.toml
cargo build
```

## Resources

- Cross-compilation: [rustup book](https://rust-lang.github.io/rustup/cross-compilation.html)
- Platform Support: [rustc book](https://doc.rust-lang.org/nightly/rustc/platform-support.html)
- More example code: [japaric/rust-cross](https://github.com/japaric/rust-cross)

## License

This repository is distributed under the terms of the [MIT license](https://opensource.org/licenses/MIT). See terms and conditions [here](./LICENSE-MIT).