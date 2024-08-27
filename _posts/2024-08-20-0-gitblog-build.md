---
relation:
  - "[[240809(금)]]"
title:
  - 블로그 만들기
location: 
description:
  - GitHub Gitpage 기능과 Chirpy 테마로 '블로그' 만들기
date:
  - 2024-08-20 14:10:00 +0900
categories:
  - PROJECT
  - 블로그
tags:
  - 3-TASK/기록
  - 6-PUBLISH/블로그
pin: false
math: true
mermaid: true
---

## BACKGROUND

### 블로그 구축-필요

- 기억에 도움 되는 포스팅
	- 경험한 것을 옵시디언으로 정리했었는데, 이 과정을 겪으면 기억이 더 오래가는 것을 느꼈습니다.
	- 경험을 글로 정리하는 과정이 내재화에 긍정적이라는 것을 알게 되었습니다.
- 보탬이 되기 위한 경험 공유
	- 프로젝트 수행할 때, 타인이 남긴 경험이 문제 해결에 큰 도움이 됐었습니다.
	- 정리한 경험이 누군가에게 도움이 될 수 있다고 느껴, 보답 받은 만큼, 보탬이 되고 싶었습니다.

### 블로그 구축-결심

- 블로그 중단 이유
	- 개발 지식 부족으로, 포털 사이트의 블로그만 할 수 있었는데, 콘텐츠를 보관하기에 불편했습니다.
	- 블로그 정책은 계속 변화하나, 콘텐츠 백업 · 마이그레이션은 개선이 안됐습니다. '콘텐츠 주도권이 포털에 있다' 라는 생각에 의욕이 나지 않았습니다.
- 블로그 결심 이유
	- 직무 변환으로 학습량이 많아졌는데, 기억을 더 잘 하고자 블로그를 운영을 결심했습니다.
	- 콘텐츠 주도권이 온전하면서, 테마가 심플한 [Jay's Blog](https://otzslayer.github.io/pandas/2021/10/30/exploding-nested-list.html)를 봤고, 가진 개발 지식 수준으로 블로그 생성 · 운영이 가능할 것 같았습니다.

### 블로그 구축-탐색

- 깃페이지로 구축한 배경
	- 깃허브의 깃페이지가 유일한 '글로벌한 무료 배포 서비스'로 알고 있습니다.
	- Git을 익히면서 git · GitHub 활용이 많이 편해진 이유도 있습니다.
- Chirpy 테마 선택 배경
	- FastAPI로 구축 시도하다가, 어려움이 많아 일정이 계속 밀렸고, 테마를 활용하는 것으로 방향을 잡았습니다.
	- [카일 블로그](https://zzsza.github.io/)에서 '심플한 정보 공유 블로그' 구상을 했었고, 구상과 일치하는 [Jay's Blog](https://otzslayer.github.io/pandas/2021/10/30/exploding-nested-list.html)를 발견했습니다. 그리고 그 테마가 Chirpy였습니다.

### 블로그 구축-목표

1. 깃블로그 구축
	- Git · Git Hub의 Git Page 기능을 활용해서 블로그를 생성 · 배포한다.
		- 이유 1. Git · Git Hub가 편리함
		- 이유 2. 로컬에서 구동할 수 있는 방식
			- 인터넷 없이도 동작 가능
			- 콘텐츠 주도권이 온전한 로컬 파일 배포 방식
2. 옵시디언과 연동되는 시스템 구축
	- 간편한 포스팅을 위해, 옵시디언과 유기적 연결 필요
	- 손쉽게 포스팅 할 수 있도록 연동 시스템 구현

<br>

## DETAIL

### 깃블로그-생성

- GitHub는 계정 내 저장소 1개에 대한 호스팅을 지원하는데, 이것을 Git Page 서비스라고 합니다.
- 저장소 이름을 `<깃허브 아이디>.github.io` 로 저장하고 Public으로 설정하면 자동으로 호스팅이 진행됩니다.
- 2024-08-14T20:24:00+09:00 기준, [Chirpy 시작 가이드 문서](https://chirpy.cotes.page/posts/getting-started/#option-2-github-fork) 보면, 2가지 옵션으로 만들 수 있습니다.
	1. git template: 1번째 옵션이며, 폴더 트리가 달라서, 다른 코드 참고에 어려움이 있었습니다.
	2. git fork: 2번째 옵션이며, 다른건 원활 했는데 'utterance' 활용한 댓글 기능 구현이 안됐고, 'Giscus' [활용](https://jihwan98.github.io/posts/giscus-%EC%84%A4%EC%A0%95/)으로 해결했습니다.
	3. [다른 생성](https://wlqmffl0102.github.io/posts/Making-Git-blogs-for-beginners-2/): 터미널로 생성하고 덮어쓰는 방식이며, 코드 파악이 어려워 힘들었습니다.
	- 💬 시행착오를 겪어보니 2번째 Git Fork 방식이 좋았습니다. <sub>가이드 문서 내용 외, 여러 방법이 있겠지만, 3가지만 해봤습니다</sub> 

#### 생성-git template 방식

- chirpy-Start 레포지토리를 자신의 Github 레포지토리로 복사해 오는 방식입니다.
- 업데이트 편리한 방식이라고 하나, 타 블로그와 파일 구성이 달라, 참고하면서 기능을 추가하거나 커스텀하기 어려웠습니다.
- 진행 프로세스는 아래와 같습니다.
	1. 레포지토리 생성
		1. [chirpy-Start, 복제하는 페이지](https://github.com/cotes2020/chirpy-starter)로 이동
		2. 우상단의 초록색 `Use this template` 버튼 클릭
		3. `Create a new repository` 선택
		4. `Repository name *`에 `<자신의 깃허브 아이디>.github.io` 입력
		5. 초록색 `Create repositry` 버튼 클릭 <sub>(Private 체크하면 배포가 안됩니다.)</sub>
	2. 레포지토리 다운로드
		1. 생성된 후, 초록색 `Code` 버튼 클릭 <sub>(`git clone` 알면, clone 진행)</sub>
		2. `Download ZIP` 버튼 클릭
		3. 원하는 경로에 압축 풀기
	3. 로컬 실행 테스트
		1. 터미널로 해당 경로로 이동하고 `jekyll serve` 진행

#### 생성-git fork 방식

- jekyll-theme-chirpy 레포지토리를 자신의 Github 레포지토리로 복사해오는 방식입니다.
- 업데이트 불편한 방식이라고 하나, 레퍼런스 코드가 많아, 기능 추가 등의 따라하기 편했습니다.
- 진행 프로세스는 아래와 같습니다.
	1. 레포지토리 생성
		1. [jekyll-theme-chirpy, git fork 하는 페이지](https://github.com/cotes2020/jekyll-theme-chirpy/fork)로 이동
		2. 초록색 `Create fork` 클릭
	2. 레포지토리 다운로드
		1. 생성된 후, 초록색 `Code` 버튼 클릭 (git clone 알면, clone 진행)
		2. `Download ZIP` 버튼 클릭
		3. 원하는 경로에 압축 풀어주기
	3. 초기화 진행 (불필요한 데이터 삭제)
		1. [Note.js 설치](https://nodejs.org/en)
		2. 터미널 열고 다운로드한 레포지토리로 이동
		3. `bash tools/init.sh` 명령어 입력
		4. `Initialization successful!` 메시지 나와야함
	4. 로컬 실행 테스트
		1. 터미널로 해당 경로로 이동하고 `jekyll serve` 진행

<br>

### 깃블로그-커스텀

- [레포지토리](https://github.com/1dh21996/1dh21996.github.io) 깃 태그 0.0.0 ~ 1.0.0 사이의 커밋 내용 일부를 다뤘습니다.
- 개인적으로 변화를 크게 느꼈던 부분만 다뤘습니다.

#### 커스텀-사이드바

1. 프로필 이미지 변경
	1. `_config.yml` avatar 부분에 프로필 이미지 파일의 경로를 넣어줍니다.

		```yml
		# the avatar on sidebar, support local or CORS resources  
		avatar:
		avatar: /assets/avatar.png
		```

2. 프로필 타이틀 변경
	1. `_config.yml` titile과 tagline 다른 문구로 변경합니다.

		```yml
		# jekyll-seo-tag settings › https://github.com/jekyll/jekyll-seo-tag/blob/master/docs/usage.md  
		# ↓ --------------------------  
	  
		title: Chirpy # the main title  
		title: <메인 타이틀 문구> # the main title
		
		tagline: A text-focused Jekyll theme # it will display as the sub-title  
		tagline: <서브 타이틀 문구> # it will display as the sub-title
		```

3. 하단 버튼 링크 변경
	1. \_data/contact.yml에서 버튼 순서와, 노출 여부<sub>(주석처리)</sub>를 설정할 수 있습니다.

		```yml
		- type: github  
		  icon: 'fab fa-github'  
		  
		# - type: twitter  
		#   icon: "fa-brands fa-x-twitter"  
		  
		- type: email  
		  icon: "fas fa-envelope"  
		  noblank: true # open link in current tab  
	
		- type: <버튼 이름>
		  icon: <버튼 아이콘>
		  url:  <버튼 링크>
		  
		- type: linkedin  
		  icon: 'fab fa-linkedin'   # icons powered by <https://fontawesome.com/>  
		  url:  'https://www.linkedin.com/in/donghyeon-han-6518a5263/' # Fill with your Linkedin homepage  
		```

	2. `_config.yml` github, email, link 부분에 각각 맞는 링크를 걸어줄수 있습니다. 

		```yml
		github:  
		  username: github_username # change to your github username  
		  
		twitter:  
		  username: twitter_username # change to your twitter username  
		  # Change to your full name.  
		  # It will be displayed as the default author of the posts and the copyright owner in the Footer  
		  name: your_full_name  
		  email: example@domain.com # change to your email address  
		  links:  
		    # The first element serves as the copyright owner's link  
		    - https://twitter.com/username # change to your twitter homepage  
		    - https://github.com/username # change to your github homepage  
		    # Uncomment below to add more social links  
		    # - https://www.facebook.com/username  
		    # - https://www.linkedin.com/in/username  
		```

#### 커스텀-푸터

1. 푸터 이름 변경
	1. `_config.yml`name 부분에 자신의 이름을 기재하면, 'your_full_name' 부분이 기재한 이름으로 바뀝니다.

		```yml
		social:  
		  # Change to your full name.  
		  # It will be displayed as the default author of the posts and the copyright owner in the Footer  
		  name: your_full_name  
		```

2. 푸터 테마 출처 수정
	1. `_includes/footer.html` 30~49 line을 주석처리하면, 'Using the Chirpy theme for jekyll' 문구가 사라집니다.

#### 커스텀-게시글

1. 게시글 링크 버튼 수정
	1. `_data/share.html` 블로그 주 사용자로 예상되는 제가 텔레그램만 써서, 나머지는 주석처리했습니다.


		```html
		platforms:  
		  # - type: Twitter  
		  #   icon: "fa-brands fa-square-x-twitter"  
		  #   link: "https://twitter.com/intent/tweet?text=TITLE&url=URL"  
		  
		  # - type: Facebook  
		  #   icon: "fab fa-facebook-square"  
		  #   link: "https://www.facebook.com/sharer/sharer.php?title=TITLE&u=URL"  
		  
		  - type: Telegram  
		    icon: "fab fa-telegram"		
		```

### 깃블로그-기능추가

#### 기능추가-댓글

- [참고 링크](https://jihwan98.github.io/posts/giscus-%EC%84%A4%EC%A0%95/)

## COMMENT

### 느낀점

- 레퍼런스 중요성
	- 공식 문서를 참고해서 생성했는데, 로컬 구동 · 배포 실패 등 문제가 있었고, 다른 Chirpy 블로그 코드, 포스트를 보면서 완성했습니다.
	- 교육과정 프로젝트에서 느꼈던, 멘토님의 강조했던, '레퍼런스 중요성'을 다시 한번 절실히 느꼈고, <span style="background:#2A4F52">레퍼런스를 탐색하는 습관</span>을 붙여볼까 합니다. 
- 버전 관리 중요성
	- 여러 옵션으로 빌드하다보니, 배포가 꼬이면서 에러가 발생하는 등 난리가 났었습니다.
	- 버전 관리 안할 경우, 에러 파악 · 문제 분석이 어렵다는 것과, 에너지 낭비가 심하다는 것을 느껴, <span style="background:#2A4F52">버전관리에 대한 고민</span>을 해보게 됐습니다.

### 평가

#### 평가-좋은점

- 내 소유의 블로그
	- 콘텐츠를 가지고 있다는 것이 좋았고, 더 이상 포털 사이트의 정책에 휘둘릴 필요가 없어졌습니다.
	- 깃페이지 정책 변경이 변수라고 생각하는데, <span style="background:#2A4F52">서버 지식 · 장비에 대한 구상</span>을 하고 있습니다.
- 옵시디언과 연동성
	- 옵시디언에서 포스팅 작성 · 게시가 가능해서 좋았습니다. 
	- 글을 작성 후, Linter 돌리고 Templater 로 프론트메타 만들고 & Git 플러그인으로 게시하는 방식으로 연동했습니다.

#### 평가-문제점

- 블로그 개선 문제
	- 포스팅 같은 기본적인 요소에 문제는 없지만, 작동하는 플로우를 모르니, 앞으로 개선이 막막한 부분이 있습니다.
	- 향후에 <span style="background:#2A4F52">언어 · 구조에 대해 배우고 이해하거나, 다른 언어로 재구성</span> 하는 것이 필요하다고 느꼈습니다.

## HISTORY

| DATE             | DETAIL      |
| ---------------- | ----------- |
| 240820(화) 14:35 | 포스트 게시 | 
