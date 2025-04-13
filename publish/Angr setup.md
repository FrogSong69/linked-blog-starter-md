
cd angr-env/
source bin/activate


use `cross build --release --target x86_64-unknown-linux-musl` for rust projects

cd ~/math_check_rust
docker run --rm -v "$PWD":/home/rust/src -w /home/rust/src -it messense/rust-musl-cross:x86_64-musl /bin/bash
`cargo build --release --target x86_64-unknown-linux-musl`
exit
cp target/x86_64-unknown-linux-musl/release/math_check_rust ~/angr-scripts/
cd  ~/angr-scripts
 source ~/angr-env/bin/activate
 