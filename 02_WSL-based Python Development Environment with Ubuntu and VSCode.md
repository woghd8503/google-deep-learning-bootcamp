# 홈 + Ubuntu에서 파이썬 개발환경 구성 (VSCode 포함)

---

## 파이썬 개발 환경 서버 설정

### 1. 개발 환경 선택지

* Python Interpreter: [https://www.python.org/](https://www.python.org/)
* Anaconda: Jupyter 포함, [https://www.anaconda.com/](https://www.anaconda.com/)
* VSCode: 확장 설치 필요, [https://code.visualstudio.com/](https://code.visualstudio.com/)
* PyCharm, Google Colab, Jupyter Lab 등

### 2. 윈도우 WSL + Ubuntu에 VSCode를 이용한 파이썬 개발환경 구성하기

Windows의 WSL(Windows Subsystem for Linux)에 Ubuntu를 설치하고 VSCode를 활용한 Python 개발 환경과  
Windows에 바로 VSCode를 설치하여 Python 개발 환경을 구성하는 것에는 몇 가지 주요 차이가 있습니다.  
각각의 접근 방식은 개발 목표와 환경에 따라 장단점이 있습니다.

| 항목               | WSL + Ubuntu                                                                 | Windows에 직접 설치                                                  |
|--------------------|------------------------------------------------------------------------------|------------------------------------------------------------------------|
| **운영체제 기반**   | Linux 기반 개발 환경 제공.                                                  | Windows 기반 개발 환경 제공.                                         |
| **패키지 관리**     | apt와 같은 Linux 패키지 매니저 사용.                                        | Windows 환경에서 pip, conda 등으로 관리.                             |
| **파일 시스템**     | Linux 파일 시스템 사용, Windows와 공유 가능하나 속도 느림.                   | Windows 파일 시스템에서 직접 작업, 속도 빠름.                        |
| **성능**           | Linux 네이티브 성능 제공, 서버 환경과 유사.                                 | Windows 네이티브 성능, GUI 앱과 연동 쉬움.                           |
| **개발 환경 유연성**| 여러 Linux 배포판 설치 가능, Docker 등과 호환성 뛰어남.                      | Windows 전용 도구 및 소프트웨어와 통합이 간단.                       |
| **VSCode 통합**     | WSL 확장을 통해 Linux 환경에서도 VSCode 사용 가능.                          | VSCode 설치만으로 바로 사용 가능, 추가 설정 없음.                   |
| **복잡도**         | WSL, Ubuntu 설정 및 VSCode 확장 설치 필요 → 다소 복잡.                       | 설치 및 설정이 간단하여 빠르게 구성 가능.                            |
| **적합한 경우**     | Linux 개발 환경, 서버 배포, Docker 사용 등 기술 활용 시 유리.               | 간단한 Python 개발, Windows 앱 개발, 초기 학습 부담 줄이고 싶을 때. |


### 3. WSL 메뉴 활용 & Ubuntu 최신화

```bash
sudo apt update
sudo apt install python3 python3-pip -y
```

### 4. WSL 명령어

> 윈도우 WSL + Ubuntu에 VSCode를 이용한 파이썬 개발환경 구성하기

| 구분                 | 명령어                                         | 설명                                                              | 예시                                 |
|----------------------|-----------------------------------------------|-------------------------------------------------------------------|--------------------------------------|
| **WSL 버전 정보**     | `wsl --list` 또는 `wsl -l`                    | 설치된 WSL 배포판 목록 출력                                        | `wsl --list`                         |
|                      | `wsl --list --verbose` 또는 `wsl -l -v`       | 설치된 배포판의 상세 정보 출력(버전, 상태 등)                     | `wsl --list --verbose` 또는 `wsl -l -v` |
|                      | `wsl --status`                                | WSL 설치 상태 및 기본 설정 확인                                   | `wsl --status`                       |
| **WSL 버전 관리**     | `wsl --set-version <배포판 이름> <버전>`     | 특정 배포판의 WSL 버전 변경 (1 또는 2)                            | `wsl --set-version Ubuntu-22.04 2`   |
|                      | `wsl --set-default-version <버전>`           | 새로 설치되는 배포판의 기본 WSL 버전 설정                         | `wsl --set-default-version 2`       |
| **배포판 설치 및 제거**| `wsl --install`                               | WSL과 기본 Linux 배포판(기본: Ubuntu) 설치                        | `wsl --install`                      |
|                      | `wsl --install -d <배포판 이름>`             | 특정 Linux 배포판 설치                                            | `wsl --install -d Ubuntu-20.04`     |
|                      | `wsl --unregister <배포판 이름>`             | 특정 WSL 배포판 제거 (데이터 포함)                                | `wsl --unregister Ubuntu-20.04`     |
| **배포판 시작 및 설정**| `wsl`                                         | 기본 배포판 실행                                                  | `wsl`                                |
|                      | `wsl -d <배포판 이름>`                        | 특정 배포판 실행                                                  | `wsl -d Ubuntu-22.04`                |
|                      | `wsl --set-default <배포판 이름>`            | 기본 배포판 설정                                                  | `wsl --set-default Ubuntu-22.04`    |
| **파일 시스템 및 경로**| `wsl --mount <디스크 경로>`                   | 물리 디스크를 WSL에 마운트 (WSL 2 전용)                           | `wsl --mount \\.\PHYSICALDRIVE1` |
|                      | `wsl --unmount <디스크 경로>`                | 마운트된 디스크 해제                                              | `wsl --unmount \\.\PHYSICALDRIVE1` |
|                      | `/mnt/<드라이브 문자>`                        | WSL에서 Windows 파일 시스템 접근                                  | `/mnt/c/Users/username/Desktop`     |
|                      | `explorer.exe .`                              | 현재 디렉토리를 Windows 탐색기로 열기                             | `explorer.exe .`                     |
| **네트워크 및 프로세스**| `wsl --shutdown`                              | 모든 WSL 배포판 종료 및 백그라운드 프로세스 정리                  | `wsl --shutdown`                     |
|                      | `wsl --terminate <배포판 이름>`              | 특정 배포판 종료                                                  | `wsl --terminate Ubuntu-22.04`      |
| **도움말 및 기타**     | `wsl --help`                                  | WSL 명령어 도움말 보기                                             | `wsl --help`                         |
|                      | `wsl -u <사용자 이름>`                        | 특정 사용자로 WSL 실행                                             | `wsl -u root`                        |
|                      | `wsl --update`                                | WSL 커널 업데이트                                                 | `wsl --update`                       |
| **wsl --rollback**   | `wsl --rollback`                              | 이전 WSL 커널 버전으로 롤백                                       | `wsl --rollback`                     |


### 5. 파이썬 가상환경 설치 (venv)

```bash
sudo apt install python3.10-venv
python3 -m venv .venv
source .venv/bin/activate
```

### 6. VSCode 업데이이트

* VSCode 설치: [https://code.visualstudio.com/](https://code.visualstudio.com/)
* "Remote - WSL" 확장 설치 (Ctrl + Shift + X)
* `code .` 명령 통해 VSCode에서 Linux 파일 열기

### 7. 주피터 노트북 확장

* Python, Jupyter 확장 설치
* New File → Jupyter Notebook → 코드 입력 후 실행 (Ctrl + Enter)

### 8. VSCode에서 파이썬 가상환경 활성화

```bash
pip freeze > requirements.txt
pip install -r requirements.txt
pip download -r requirements.txt -d packages/
pip install --no-index --find-links=packages/ -r requirements.txt
```

---

## 필요 명령을 기준으로 한 WSL 명령어

```bash
# 배포판 목록 조회
wsl -l -v

# 배포판 복잡
wsl --set-default Ubuntu-22.04

# 배포판 작도에서 WSL 로 진입
wsl -d Ubuntu-22.04

# 배포판 종료
wsl --terminate Ubuntu-22.04

# 배포판 제거 (주의)
wsl --unregister Ubuntu-22.04
```

---

## 추가 설정

### Markdown 셀 / Code 셀 사용

* Markdown: 설명, 수식, 이미지, 링크 등 텍스트 기반 셀
* Code: Python 코드 실행용 셀

### Markdown 예제

````markdown
✅ 제목 만들기

- `#`, `##`, `###` 등을 사용해 제목의 크기를 조절할 수 있음.

```markdown
# Heading 1  
## Heading 2  
### Heading 3
```

---

✅ 강조 (굵게 / 기울임)

- 굵게: `**텍스트**` 또는 `__텍스트__`  
- 기울임: `*텍스트*` 또는 `_텍스트_`  
- 굵게+기울임: `***텍스트***`

---

✅ 리스트

- 순서 없는 리스트: `-`, `*`, `+`  
- 순서 있는 리스트: 숫자 뒤에 점(`.`)을 사용

```markdown
- 항목 1
- 항목 2

1. 첫 번째 항목  
2. 두 번째 항목
```

---

✅ 코드 블록

- 인라인 코드: \`코드\`  
- 여러 줄 코드 블록: 백틱(\`\`\`) 3개 사용

```python
print("Hello, Markdown!")
```

---

✅ 수평선

- `---` 또는 `***` 사용

```markdown
---
***
```

---

✅ 링크 삽입

- `[텍스트](URL)` 형식 사용

```markdown
[Google](https://www.google.com)
```

---

✅ 이미지 삽입

- `![이미지 설명](이미지 URL 또는 경로)` 형식 사용

```markdown
![Example Image](https://via.placeholder.com/150)
```

---

✅ HTML 태그 사용

- Markdown 셀에서는 HTML도 지원합니다.

```html
<b>굵은 텍스트</b>
```

---

✅ 표 만들기

- `|` 와 `-`를 사용

```markdown
| 항목 | 설명             |
|------|------------------|
| 제목 | Markdown 사용법  |
| 작성자 | 여러분         |
```

---

✅ 수식 작성 (LaTeX 지원)

- 인라인 수식: `$수식$`  
  예: `$E = mc^2$`

- 블록 수식: `$$수식$$`
````


## 마무리

- WSL은 Windows의 편리함과 Linux의 자유로움을 모두 제공
- VSCode와 연계하면 WSL 내에서도 생산적인 Python 개발 환경 구축 가능
- Jupyter, venv, pip, 코드 실행 등 다양한 Python 워크플로우를 손쉽게 설정 가능


