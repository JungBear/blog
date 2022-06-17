---
title: 06/17날 강의내용
---
## Blog 만들기
hexo를 이용한 Blog 만들기
### 1. github에서 blog repositories 만들기
``` bash
$ hexo init blog
```

### 2. github에서 ID.github.io 폴더만들기

### 3. blog 폴더를 파이참으로 실행

``` bash
$ cd blog
$ npm install
$ npm install hexo-server --save
$ npm install hexo-deployer-git --save
```

### 4. _config.yml파일 더블클릭
파일중간에 있는 
``` bash 
$ url: @@@
```
을
``` bash
$ url: https://ID.github.io
```
로 수정

### 5. 테스트 및 배포

``` bash
$ hexo server  #테스트
$ hexo generate
$ hexo deploy  #배포
```
