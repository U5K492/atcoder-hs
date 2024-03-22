# AtCoder Environment in Haskell with Devcontainer
---

## Getting Started
---
1. Reopen in container
2. link acc and oj
```
  acc check-oj
```
3. login AtCoder
```
  acc login
  # type AtCoder Username and Password

  oj login https://atcoder.jp/
```
4. change sample case dir will create by acc as test from tests
```
  acc config default-test-dirname-format test
```
5. Download all tasks by default when acc new
```
  acc config default-task-choice all
```

## Challenge Contest
```
  ex) ABC288

  acc new abc288

  cd abc288/a
  touch main.hs
```
##### run test
```
  oj t -c "runghc main.hs"
```
##### submit
```
  acc submit main.hs
```