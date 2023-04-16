# 스크립트 보안 오류 PSSecurity Exception

날짜: 2023년 4월 16일
생성 일시: 2023년 4월 16일 오후 8:57
생성자: oduckProgrammer 
최종 편집 일시: 2023년 4월 16일 오후 10:18
최종 편집자: oduckProgrammer 
태그: Powershell, 보안

## 오늘 공부한 내용 ✏

노트북을 새로 사서 환경설정을 다시 하던 도중…😂  vscode 터미널에서 nest를 설치하려니…

![Untitled](%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%B8%E1%84%90%E1%85%B3%20%E1%84%87%E1%85%A9%E1%84%8B%E1%85%A1%E1%86%AB%20%E1%84%8B%E1%85%A9%E1%84%85%E1%85%B2%20PSSecurity%20Exception%2009fa5922b89c4c6787358433a17b14df/Untitled.png)

PSSecurityException 에러 발생..!

생각 해보니.. 처음 npm으로 라이브러리를 설치할 떄 발생했던 이슈였다. ~~(사실 해결방법 찾고 기억남)~~ 이번에는 기억하기 위해서 조금 더 근본적인 원인을 찾아보니.. 

Windows에서 PowerShell을 악성 스크립트의 실행을 방지하기 위해 기본적으로 ****Restricted****
정책으로 설정 되어 있다고 한다.

그래서 저번처럼 정책을 변경해야지..라고 1차원적으로 생각 하던 중, 조금 더 알아보니 PowerShell에서만 발생하는 에러이고 VScode에서 다른 CLI를 쓰면 실행이 된다고 한다..! (VScode 터미널은 기본적으로 PowerShell이며 변경 가능)  

이런 단순한 방법이…🤣  이래서 메타정보가 중요한 건가..?! ~~mac 사고 싶다 휴..~~

![Untitled](%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%B8%E1%84%90%E1%85%B3%20%E1%84%87%E1%85%A9%E1%84%8B%E1%85%A1%E1%86%AB%20%E1%84%8B%E1%85%A9%E1%84%85%E1%85%B2%20PSSecurity%20Exception%2009fa5922b89c4c6787358433a17b14df/Untitled%201.png)

위에 그림처럼 VScode 내에서 다른 터미널로 접속 가능하며 난 git bash를 사용해서 해결했다.

![Untitled](%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%B8%E1%84%90%E1%85%B3%20%E1%84%87%E1%85%A9%E1%84%8B%E1%85%A1%E1%86%AB%20%E1%84%8B%E1%85%A9%E1%84%85%E1%85%B2%20PSSecurity%20Exception%2009fa5922b89c4c6787358433a17b14df/Untitled%202.png)

~~큭큭.. 간단하구만…~~ 

PowerShell 실행 정책은 공식문서에 아주 잘 나와있지만 혹시 모를 미래를 위해 가볍게 정리해보고자 한다.

### ****AllSigned****

- 모든 스크립트와 구성파일에 신뢰할 수 있는 제공자의 서명이 있으면 모두 실행 가능
- 서명이 되더라도 악의적인 스크립트를 실행할 가능성이 있다고 함.

### ****Bypass****

- 그냥 통과~ 😅

### ****Default****

- 기본 실행 정책이며 Windows에서는 **Restricted**

### ****RemoteSigned****

- Windows 서버 컴퓨터에 대한 기본 실행 정책이며, 인터넷에서 다운로드한 스크립트 및 구성 파일이 서명이 되어있다면 실행 가능
- 로컬에서는 따로 서명이 필요하지 않음

### ****Restricted****

- Windows 클라이언트 컴퓨터에 대한 기본 실행 정책이며, 모든 Script 파일 실행 방지

### ****Undefined****

- 해당 범위에 실행 정책이 설정되어 있지 않음
- 모든 범위가 **Undefined**이면  **Restricted**로 적용 된다

### ****Unrestricted****

- Windows OS가 아닌 컴퓨터에 대한 기본 실행 정책이며 변경할 수 없다.
- 모든 스크립트가 실행 가능하며, 실행하기 전 사용자에게 경고한다.

<aside>
💡 유효한 실행 정책을 확인하는 명령어: Get-ExecutionPolicy

</aside>

<aside>
💡 실행 정책을 변경하는 명령어: Set-ExecutionPolicy -ExecutionPolicy <PolicyName>

</aside>

실행 정책을 변경해도 되지만, 일단 보안상으로는 그대로 두는 것이 더 안전하다고 생각했다.

MS에서 ****Restricted****를 기본 설정으로 둔 이유가 있겠지…ㅎ

~~언젠간 써먹을 일이 있길 바라며 .. 제발~~~

-끝-

## 어려웠던 내용 ⚔

## 궁금한내용 / 부족한 내용 🛡

## 느낀점 🎯

확실히 공식문서를 확인하니 깊이있게 알 수 있는것 같다..!

## 오늘 참고한 자료 📚

[실행 정책 정보 - PowerShell](https://learn.microsoft.com/ko-kr/powershell/module/microsoft.powershell.core/about/about_execution_policies?view=powershell-7.3)
