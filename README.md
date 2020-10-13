# WASI link fail

Repo to reproduce a regression in `rustc` when linking with `wasi-sdk`.

Regression after `8a6d4342be6a6acbade8e7ef65e73d27ee8c9144` Jul 2
before `2bc4c03eb8180f2852f773054c75cfcfe42e9cc3` Sep 6


Half way `8ee57eed79ed4f7c9ce21b4a6dae6daad62193c1` doesn't have the file?

```sh
49b9a6486ab0814f4c7d57c22c75216fdc1ebf14 Jul 22 with patch OK
4b9675fb05a0da38d2c50785e2926ee34e3d312f Aug 17 with patch OK
4f66117945df3b21e46ee9013e1c8a88f4b27842 Sep 03 with patch OK
0d0f6b113047b2cf9afbde990cee30fd5b866469 Sep 03 commit before patch FAIL
2bc4c03eb8180f2852f773054c75cfcfe42e9cc3 Sep 03 patch OK

2020-09-06, rust version 1.48.0-nightly (cdc8f0606 2020-09-05) FAIL unknown argument: --eh-frame-hdr
cdc8f0606d0f3c4f3866643382c8a5776d1bdaed Sep 05 with patch OK
94b8eb80abf68d7505aca3562a625ec00fa394a1 Sep 6 01:58:35 Merge patch OK
aa81d32165dc9f0952bc520f223503aedd755b31 Sep 06 OK

5d74e880061c250936105125a2ffa901f315aaaa Sun Sep 6 18:26:33
2020-09-07, rust version 1.48.0-nightly (73dc675b9 2020-09-06) FAIL Bad relocation type

git cherry-pick 2bc4c03eb8180f2852f773054c75cfcfe42e9cc3
python3 x.py build -i --target wasm32-wasi
cd ../wasi-link-fail
../rust/build/x86_64-unknown-linux-gnu/stage1/bin/rustc --target=wasm32-wasi -C linker=/opt/wasi-sdk/bin/clang src/main.rs
```
