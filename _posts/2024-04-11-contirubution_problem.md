---
title: [github] fork 해온 repository 잔디 안심김(?) 오류 해결
---
# 😿 잔디가 안심어져요...
jekyll-chrisp를 fork해서 블로그를 만들고 몇일동안 글을 commit했는데 contribution에 뜨지 않았다.

https://docs.github.com/en/account-and-profile/setting-up-and-managing-your-github-profile/managing-contribution-settings-on-your-profile/why-are-my-contributions-not-showing-up-on-my-profile

깃허브 공식 문서에서는 4가지 이유를 말해준다.

## 1. 커밋이 24시간 이내에 이루어졌을 경우
contribution이 계산되기 위한 요구사항을 충족하는 까지 최대 24시간을 기다려야 할 수 있다.

## 2. 로컬 git commit 이메일이 계정에 연결되어있지 않는 경우
처음에 나는 이 문제 때문에 오류가 생긴 줄 알았지만 확인해보니 이메일이 제대로 등록되어있었다. 


### 2-1. commit 이메일 주소 설정하는 방법 (윈도우 ver)

https://docs.github.com/en/account-and-profile/setting-up-and-managing-your-personal-account-on-github/managing-email-preferences/setting-your-commit-email-address#about-commit-email-addresses

위 문서를 참고하면 이메일 주소를 설정할 수 있다.
윈도우 버전만 설명하자면

#### 2-1-1. GitHub에서 커밋 이메일 주소 설정
* 깃허브 페이지 오른쪽 상단에서 프로필 사진을 클릭한 다음 설정(settings)을 선택한다.

![git](https://docs.github.com/assets/cb-45016/mw-1440/images/help/settings/userbar-account-settings-global-nav-update.webp)

* 사이드바의 Access 섹션에서 Emails를 클릭한다.
  
![git](/assets/img/favicons/git1.png)

* Add email addres 에 이메일을 추하하고 Add 버튼을 누른다.
  
![git2](/assets/img/favicons/git2.png)

* 이메일 주소를 확인한다.
  * 이메일 주소 아래에서 확인 이메일 다시 보내기
  (Resend verification email)를 클릭한다.
  ![git](https://docs.github.com/assets/cb-35730/mw-1440/images/help/settings/email-verify-button.webp)

  * GitHub에서 링크가 포함된 이메일을 보내준다. 해당 링크를 클릭하면 GitHub 대시보드로 이동하고 확인 배너가 표시된다.

* Primary email address 에서 웹 기반  Git 작업과 연결할 이메일 주소를 선택한다.
![git](https://docs.github.com/assets/cb-119951/mw-1440/images/help/settings/email-primary.webp)


#### 2-2-2. Git에서 커밋 이메일 주소 설정
* Git Bash를 연다.
* Git에서 이메일 주소를 설정한다.
```
git config --global user.email "YOUR_EMAIL"
```

* Git에서 이메일 주소를 올바르게 설정했는지 확인한다
```
$ git config --global user.email
email@example.com
```

---