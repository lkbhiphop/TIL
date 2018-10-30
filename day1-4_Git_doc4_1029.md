# Git

git - 분산버전관리시스템

1. ##### git init  = 로컬에 git파일의 저장소를 만든다

2. ##### git add  = commit할 파일들을 임시저장한다(장바구니에 넣는다)

​       가. 임시저장한다(staging단계)

​       나. git add .을 사용해서 현재 폴더 및 하위 모든 항목을 추가

​       다. git add text.txt를 사용해서 원하는 파일 하나씩 추가도 가능

3. ##### git commit = 새로운 버젼을 만들어서 로컬에 저장한다

   가. 새로운 버젼을 만든다.

​       나. git commit -m "여기다 뭐 수정했는지 적어!"   

​       다. git log --> commit 이력을 확인한다.

4. ##### remote  = 원격 저장소 설정한다.

​       가. git remote add origin <url주소>

​       ** 꼭 오리진이 아니여도 상관없지만, origin사용

5. ##### git push = 원격저장소에 코드 올리기

​       가. 내가 원하는 원격 저장소에 코드를 올리겠다. 

​       나. `git push origin master` master라는 origin을 올리겠다. 저 위에 remote                 

​             주소로 master라는 코드를 올릴 것이다.





#####    자주사용하는 명령어

      1. `git status` 파일이나 폴더 수정되었는지 확인

   


   2. `git diff `   수정된 내용 확인



      3. `git log`    지금까지 작성한 commit목록을 보여준다. 
      4.  `git remote` 내가 갖고 있는 origin목록을 알려준다.



#####    git 쓸때 유용한 사이트

- [git입문](https://backlog.com/git-tutorial/kr/)

- [git본판](https://git-scm.com/docs)



##### 로컬 저장소를 복제(clone)하려면 아래 명령어

```bash
git clone /로컬/저장소/경로
```

##### 원격 저장소를 복제(clone)하려면 아래 명령어

```bash
git clone 사용자명@호스트:/원격/저장소/경로
```

