---
title: "STS3 이클립스 GitHub 설정"
output:
  html_document:
    keep_md: true
disqusIdentifier: fdsF34ff34
categories: Java
metaAlignment: center
date: '2022-10-16 22:10:20'
---

### STS와 GitHub를 연동해보자.
<!-- excerpt -->

- 계정 → Settings → 맨 밑에 Developer Settings → Personal access tokens → Generate new tokens → Expiration(제한기간) No Expiration 으로 변경 → 모든 권한 체크 후 이름적고 만들기 → **무슨 코드 나오는데 이 코드 꼭!! 기억해놓기**
    
    ![Untitled](/images/STS3_Github/Untitled.png)
    
    ![Untitled](/images/STS3_Github/Untitled%201.png)
    
    ![Untitled](/images/STS3_Github/Untitled%202.png)
    
    ![Untitled](/images/STS3_Github/Untitled%203.png)
    
    ![Untitled](/images/STS3_Github/Untitled%204.png)
    
    ![Untitled](/images/STS3_Github/Untitled%205.png)
    
- 새 리포지터리 만들기 → Add .gitignore : 무시할 파일 즉, GitHub에 올라가면 안되는 것들 여기서는 JAVA 설정. → Choose License : 공짜로 라이센스를 쓸 경우 출처를 나타내야 하는데 이때 쓰는 것 → 만들기
    
    ![Untitled](/images/STS3_Github/Untitled%206.png)
    
    ![Untitled](/images/STS3_Github/Untitled%207.png)
    
    ![Untitled](/images/STS3_Github/Untitled%208.png)
    

- 새 레포지토리 주소 복사 → SourceTree 앱 실행 → 새 탭에서 Clone → 맨 위의 탐색 옆에 주소붙여넣고 탐색 누르기 → 두 번째 탐색으로 저장할 경로 지정 → 연습용 폴더 만들고 폴더 선택 하고 클론
    
    ![Untitled](/images/STS3_Github/Untitled%209.png)
    
    ![Untitled](/images/STS3_Github/Untitled%2010.png)
    
    ![Untitled](/images/STS3_Github/Untitled%2011.png)
    
    ![Untitled](/images/STS3_Github/Untitled%2012.png)
    
- 새 파일 아무거나 하나 만들고 커밋(밑에 “origin/main에 바뀐 내용 즉시 푸시” 를 체크하면 푸시까지 자동으로 됨) → 커밋만 했을 경우 푸시도 하라고 Push알림에 1이 떠있음
    
    ![Untitled](/images/STS3_Github/Untitled%2013.png)
    
    ![Untitled](/images/STS3_Github/Untitled%2014.png)
    
    ![Untitled](/images/STS3_Github/Untitled%2015.png)
    
    ![Untitled](/images/STS3_Github/Untitled%2016.png)
    
    ![Untitled](/images/STS3_Github/Untitled%2017.png)
    
    ![Untitled](/images/STS3_Github/Untitled%2018.png)
    
    ![Untitled](/images/STS3_Github/Untitled%2019.png)
    
- 이렇게 경로가 나뉘었을때 Push 하려고 하면 에러가 나온다.
    - 왜? → 현재는 ‘첫번째 커밋’ 이 올라가있는데 ‘체크 풀고 커밋’ 을 등록하려고 하면 충돌이 생기기 때문에
- ‘체크 풀고 커밋’ 에 체크아웃(해당시점으로 이동) 한 후에 병합을 진행하면 다음처럼 병합된다.
    
    ![Untitled](/images/STS3_Github/Untitled%2020.png)
    
    ![Untitled](/images/STS3_Github/Untitled%2021.png)
    
- 우리는 Clone 을 했기 때문에 자동으로 Push 에 링크가 들어가있다. → 만약 다른 사람꺼 받은 상태에서 Push 하려면 Push 탭 가서 링크 복붙
    
    ![Untitled](/images/STS3_Github/Untitled%2022.png)
    

- Public : GitHub 주소만 알면 누구나 소스를 볼 수 있다.
    - 누구나 Clone 은 할 수 있지만
    - 누구나 Push할 수 있는 권한이 있는 건 아니다.
    - 만든사람이 해당 레포짓의 Settings / Collaborators 에서 Add People 누르고 GitHub 계정을 추가하면 된다.
        
        ![Untitled](/images/STS3_Github/Untitled%2023.png)
        
    

---

## STS 에서 바로 깃헙으로 올리기

- STS 에서 Git의 관점으로 보기 위해서 Window → Perspective → Open Perspective → Other 에서 Git 클릭
    
    ![Untitled](/images/STS3_Github/Untitled%2024.png)
    
    ![Untitled](/images/STS3_Github/Untitled%2025.png)
    
- … 3개표시(더보기) 클릭 → Create Repository → 내가 올릴 폴더로 선택 → Branch name 바꿔서 Create 클릭
    
    ![Untitled](/images/STS3_Github/Untitled%2026.png)
    
    ![Untitled](/images/STS3_Github/Untitled%2027.png)
    

- 우리가 만든 레포는 로컬에만 있고 Java에는 연동이 안 되어 있기 때문에 우클릭 → Import로 Java와 연동을 시켜준다
    
    ![Untitled](/images/STS3_Github/Untitled%2028.png)
    
    ![Untitled](/images/STS3_Github/Untitled%2029.png)
    
- 다시 오른쪽위에 JAVA 관점으로 돌아와서 → 내가 올리려고 했던 폴더에 우클릭
    
    ![Untitled](/images/STS3_Github/Untitled%2030.png)
    

- Team → Add to Index
    
    ![Untitled](/images/STS3_Github/Untitled%2031.png)
    

- 다시 Team → Comit 을 누르면 오른쪽에 Commit Message 작성
    
    ![Untitled](/images/STS3_Github/Untitled%2032.png)
    
- Commit and Push 클릭
    
    ![Untitled](/images/STS3_Github/Untitled%2033.png)
    

- URI 에 내가 올릴 GitHub Repository 주소 복붙
    
    ![Untitled](/images/STS3_Github/Untitled%2034.png)
    

- Authentication 에는 User 에 아이디 적고
    
    Password 에는 아까 맨위에서 중요하다고 한 token 코드를 복붙 
    
    ![Untitled](/images/STS3_Github/Untitled%2035.png)
    

- 다음 → Push → 하면GitHub에 내가 만든 패키지 올라감
    
    ![Untitled](/images/STS3_Github/Untitled%2036.png)
    
    ![Untitled](/images/STS3_Github/Untitled%2037.png)
    
- 이렇게 하면 “First_Remote_Practice” 폴더의 내용이 “Practice1” GitHub 레포에 올라가게 된다. 즉, 폴더의 이름과 깃허브 레포의 이름이 달라도 상관없다
    
    

---

### 겪은 에러

- 만약 Push 과정에서 ‘Rejected non fast forward’ 에러가 뜬다면
    
    공통분모가 없어서 아예 관련이 없는 두 저장소를 병합한다는 뜻이므로
    
    Pull 로 기존의 레포와 합친 후 수정해서 Push 하면 해결된다.