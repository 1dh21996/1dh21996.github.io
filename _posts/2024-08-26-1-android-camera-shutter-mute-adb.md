---
relation:
  - "[[240826(월)]]"
title:
  - 갤럭시 카메라 셔터음 무음 설정
location: 
description:
  - ADB Tools 활용한, 갤럭시 카매라 셔터음 무음 설정
date:
  - 2024-08-26 23:40:00 +0900
categories:
  - KNOWLEDGE
  - android
tags:
  - 3-TASK/기록
  - 6-PUBLISH/블로그
pin: false
math: true
mermaid: true
---

## BACKGROUND

- [기사](https://weekly.chosun.com/news/articleView.html?idxno=30003) · [블로그](https://m.blog.naver.com/pauljcjang/222199155306)에 따르면, 한국정보통신기술협회는 카메라앱 셔터음을 60~68db 정하는 [휴대폰카메라촬영음표준안](https://www.tta.or.kr/tta/ttaSearchView.do?key=77&rep=1&searchStandardNo=TTAK.KO-06.0063/R1&searchCate=TTAS)을 2004년에 제정 · 유지하고 있습니다.
- 갤럭시 카매라 앱의 셔터음도 위 표준안이 적용된 것으로 보입니다만, 부정한 의도가 없는 촬영 시에 셔터음으로 주위의 주목받거나, 피사체가 달아나는 등 불편함이 있습니다.
- 무음카메라 앱을 썼었는데, 사진이 전송 될 것 같은 보안상의 찜찜함이 있어서, SetEdit 앱으로 무음 설정을 했었습니다.
- 어느날 SetEdit 앱이 갑자기 동작을 안하길래 찾아보니, 안드로이드 14 OneUI 6.0 이상 버전은 무음 설정이 불가하다고 합니다.
- 그래서 ADB Shell 앱으로 무음 설정을 했었는데, 2024년 08월 26일 업데이트 이후, 무슨 문제가 있는지 무음 설정이 안됐습니다.
- 그러다가 PC에서 무음 설정하는 방법을 찾았고 쉬우면서 적용도 편하길래, 경험을 나누고자 포스팅 하기로 했습니다.
- 변검, [갤럭시 카메라 무음 설정 One UI6.1 이후 adb 방법](https://blog.naver.com/ddihw/223449855441) 포스팅을 보며 진행했습니다.

<br>

## DETAIL

- 아래 순서로 진행했습니다.
	1. 개발자 옵션 & 디버깅 활성화
	2. 스마트폰 연결 & SDK 플랫폼 도구 준비
	3. 명령 프롬프트 열기
	4. 명령 실행

### 1. 개발자 옵션 & 디버깅 활성화

- '갤럭시 설정 앱' → '휴대전화 정보' → '소프트웨어 정보' → '빌드번호' 7번 터치 → '개발자 옵션' 활성화 됐다고 출력됩니다.
- '갤럭시 설정 앱' 다시 가보면, '개발자 옵션' 버튼이 생긴 것을 확인할 수 있습니다.
- '갤럭시 설정 앱' → '개발자 옵션' 이동 후, '사용 안 함' 옆 토글을 터치해서 '사용 중' 상태로 변경합니다.
- 하단에 있는 'USB 디버깅' 활성화 해주면 완료입니다.

### 2. 스마트폰 연결 & SDK 플랫폼 도구 준비

0. 폰과 PC를 케이블로 연결하고 패턴 · 지문 해제 후, '휴대전화 데이터 접근 허용' 알림 허용하면, 또 'USB 디버깅 허용' 알림 나오는데, 허용합니다.
1. [다운로드 링크](https://developer.android.com/tools/releases/platform-tools?hl=ko)에서 운영체제에 맞는 ZIP 파일을 다운 받고 압축을 해제합니다. [사용했던 zip파일 링크](https://raw.githubusercontent.com/1dh21996/1dh21996.github.io/main/assets/posts/1-0.zip) 첨부합니다.
2. 압축 해제하면 'platform-tools'폴더가 나오는데, 이름을 adb로 변경한 뒤, '복사'합니다.
3. C 드라이브에 '붙여넣기' 합니다.

![1-1.png](https://raw.githubusercontent.com/1dh21996/1dh21996.github.io/main/assets/posts/1-1.png)

### 3. 명령 프롬프트 열기

4. Windows 11 버전 기준, `windows` 키 입력하면 검색창 뜨는데, 바로 'cmd' 입력하면 '명령 프롬프트'가 뜹니다.
5. 우측 패널에서 '관리자 권한' 눌러 실행합니다.

![1-2.png](https://raw.githubusercontent.com/1dh21996/1dh21996.github.io/main/assets/posts/1-2.png)

### 4. 명령 실행

6. 현재 경로가 `C:\Windows\System32` 로 나오는데, `cd ../../adb`명령(상위 폴더, 상위 폴더, 하위 adb 폴더 이동)을 내려 adb 폴더로 이동합니다.
7. `adb devices` 명령으로 adb를 실행합니다.
8. `List of devices attached` 문구가 출력 되는지 확인합니다.
9. `adb shell settings put system csc_pref_camera_forced_shuttersound_key 0` 명령으로 셔터음을 무음으로 변경합니다.
10. `C:\adb` 문구 출력 되는지 확인합니다. 

![1-3.png](https://raw.githubusercontent.com/1dh21996/1dh21996.github.io/main/assets/posts/1-3.png)

<br>

## COMMENT

- 'USB 디버깅 허용' 알림 단계에서 허용을 안할 경우, 아래와 같이 에러가 발생합니다.
	```cmd
	Microsoft Windows [Version 10.0.22631.4037]
	(c) Microsoft Corporation. All rights reserved.
	
	C:\Windows\System32>cd ../../adb
	
	Rem `adb devices` 명령 시, 정상과 다른 unauthorized 출력이 발생합니다.
	C:\adb>adb devices
	* daemon not running; starting now at tcp:5037
	* daemon started successfully
	List of devices attached
	R3CW306MKDZ     unauthorized
	
	Rem `...shuttersound_key 0` 명령에서 device unauthorized. 출력 발생하면서 적용이 안됩니다.
	C:\adb>adb shell settings put system csc_pref_camera_forced_shuttersound_key 0
	adb.exe: device unauthorized.
	This adb server's $ADB_VENDOR_KEYS is not set
	Try 'adb kill-server' if that seems wrong.
	Otherwise check for a confirmation dialog on your device.
	```

## HISTORY

| DATE             | DETAIL      |
| ---------------- | ----------- |
| 240826(월) 23:40 | 포스팅 게시 | 