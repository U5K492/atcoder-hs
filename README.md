# AtCoder Environment in Haskell with Devcontainer
---

## Getting Started
---
1. Reopen in container
2. install tools
```
  # acc
  npm i -g atcoder-cli

  # oj
  pip3 install online-judge-tools
```
3. link acc and oj
```
  acc check-oj
```
4. login AtCoder
```
  acc login
  # type AtCoder Username and Password

  oj login https://atcoder.jp/
```
5. change sample case dir will create by acc as test from tests
```
  acc config default-test-dirname-format test
```
6. Download all tasks by default when acc new
```
  acc config default-task-choice all
```

## Challenge Contest
```
  ex) ABC288

  cd src
  acc new abc288

  cd abc288/a
  touch Main.hs
```
##### run test
```
  oj t -c "runghc main.hs"
```
##### submit
```
  acc submit main.hs
```