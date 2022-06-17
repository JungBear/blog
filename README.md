# blog making
- 필요 명령어

```bash
hexo init blog
cd blog
npm install
npm install hexo-server --save
npm install hexo-deployer-git --save
hexo server   #테스트용 코드
hexo generate #배포할때 먼저 쓰기
hexo deploy   #배포할때 두번째로 쓰기
```
config에 있는 수정할 수 있는 것들은 블로그 전체 타이틀
source에 있는 파일들은 포스트에 관한 것