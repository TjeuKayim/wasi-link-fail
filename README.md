# WASI link fail

Repo to reproduce a regression in `rustc` when linking with `wasi-sdk`.

Regression after `8a6d4342be6a6acbade8e7ef65e73d27ee8c9144` Jul 2
before `2bc4c03eb8180f2852f773054c75cfcfe42e9cc3` Sep 6


Half way `8ee57eed79ed4f7c9ce21b4a6dae6daad62193c1` doesn't have the file?

```sh
49b9a6486ab0814f4c7d57c22c75216fdc1ebf14 Jul 22 with patch OK
4b9675fb05a0da38d2c50785e2926ee34e3d312f Aug 17 with patch OK
git cherry-pick 2bc4c03eb8180f2852f773054c75cfcfe42e9cc3
python3 x.py build -i --target wasm32-wasi
cd ../wasi-link-fail
../rust/build/x86_64-unknown-linux-gnu/stage1/bin/rustc --target=wasm32-wasi -C linker=/opt/wasi-sdk/bin/clang src/main.rs
```
