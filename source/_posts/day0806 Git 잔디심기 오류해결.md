---
title: "Git 잔디심기 오류해결"
output:
  html_document:
    keep_md: true
disqusIdentifier: fdsF34ff34
categories: blog
clearReading: true
thumbnailImage: Github.png
thumbnailImagePosition: left
autoThumbnailImage: yes
metaAlignment: center
date: '2022-08-07 08:30:23'
---



- 가끔씩 commit 를 했는데 잔디가 안 심어져서 해결법 찾아봄
<!-- excerpt -->

- 분명 1 commit를 했는데 commit이 등록이 안돼서 잔디가 안 심어지는 경우가 발생했다.
    
    구글링 해본 결과!
    

## GitHub에 등록된 이메일과 닉네임이 내 로컬 이메일과 닉네임하고 달라서 생긴 문제..

- GitHub에 등록된 이메일은 [gmail](http://gmail.com) 이었고 내 로컬 컴퓨터에서 쓴 이메일은 [naver](http://naver.com) 이었다…

---

## 해결법

- 다음 코드를 입력해서 설정을 바꿔주면 해결된다. dhtpdud2009@naver.com 을 발견했다.
    
    (q 누르면 나가짐)
    
    ![Untitled](Git%20%E1%84%8C%E1%85%A1%E1%86%AB%E1%84%83%E1%85%B5%E1%84%89%E1%85%B5%E1%86%B7%E1%84%80%E1%85%B5%20%E1%84%8B%E1%85%A9%E1%84%85%E1%85%B2%E1%84%92%E1%85%A2%E1%84%80%E1%85%A7%E1%86%AF%200564ac301686433180a69e7f5e53bd6e/Untitled.png)
    
    ![Untitled](Git%20%E1%84%8C%E1%85%A1%E1%86%AB%E1%84%83%E1%85%B5%E1%84%89%E1%85%B5%E1%86%B7%E1%84%80%E1%85%B5%20%E1%84%8B%E1%85%A9%E1%84%85%E1%85%B2%E1%84%92%E1%85%A2%E1%84%80%E1%85%A7%E1%86%AF%200564ac301686433180a69e7f5e53bd6e/Untitled%201.png)
    

```
git config --list
```

- GitHub에 등록된 이메일을 확인하자
    
    ![Untitled](Git%20%E1%84%8C%E1%85%A1%E1%86%AB%E1%84%83%E1%85%B5%E1%84%89%E1%85%B5%E1%86%B7%E1%84%80%E1%85%B5%20%E1%84%8B%E1%85%A9%E1%84%85%E1%85%B2%E1%84%92%E1%85%A2%E1%84%80%E1%85%A7%E1%86%AF%200564ac301686433180a69e7f5e53bd6e/Untitled%202.png)
    
    ![Untitled](Git%20%E1%84%8C%E1%85%A1%E1%86%AB%E1%84%83%E1%85%B5%E1%84%89%E1%85%B5%E1%86%B7%E1%84%80%E1%85%B5%20%E1%84%8B%E1%85%A9%E1%84%85%E1%85%B2%E1%84%92%E1%85%A2%E1%84%80%E1%85%A7%E1%86%AF%200564ac301686433180a69e7f5e53bd6e/Untitled%203.png)
    
- 둘이 다른 것을 확인했다.

- 다음 코드로 로컬 config 이메일과 Global config 이메일을 통일 시킨다
    
    ![Untitled](Git%20%E1%84%8C%E1%85%A1%E1%86%AB%E1%84%83%E1%85%B5%E1%84%89%E1%85%B5%E1%86%B7%E1%84%80%E1%85%B5%20%E1%84%8B%E1%85%A9%E1%84%85%E1%85%B2%E1%84%92%E1%85%A2%E1%84%80%E1%85%A7%E1%86%AF%200564ac301686433180a69e7f5e53bd6e/Untitled%204.png)
    

```
git config user.name "이름"    --> 이름이 다른 경우
git config user.email "이메일" --> 이메일이 다른 경우

git config --global user.name "이름"     --> 글로벌도
git config --global user.email "이메일"  --> 동일하게
```

- 이 후 commit 을 하면 정상적으로 1 commit 씩 GitHub 에 등록된다!