# 홈 + Ubuntu에서 파이썬 개발환경 구성 (VSCode 포함)

---

## 파이썬 개발 환경 서버 설정

### 1. 개발 환경 선택지

* Python Interpreter: [https://www.python.org/](https://www.python.org/)
* Anaconda: Jupyter 포함, [https://www.anaconda.com/](https://www.anaconda.com/)
* VSCode: 확장 설치 필요, [https://code.visualstudio.com/](https://code.visualstudio.com/)
* PyCharm, Google Colab, Jupyter Lab 등

### 2. WSL(Windows Subsystem for Linux) 각설

* Windows에서 Linux 개발 환경 가능
* Microsoft Store에서 Ubuntu 및 기타 배포판 다운로드
* `wsl --install -d Ubuntu-22.04`
* 카드에서 Ubuntu 초기설정 (사용자 계정, 패스워드)

### 3. WSL 메뉴 활용 & Ubuntu 최신화

```bash
sudo apt update
sudo apt install python3 python3-pip -y
```

### 4. 파이썬 가상환경 설치 (venv)

```bash
sudo apt install python3.10-venv
python3 -m venv .venv
source .venv/bin/activate
```

### 5. VSCode 업트

* VSCode 설치: [https://code.visualstudio.com/](https://code.visualstudio.com/)
* "Remote - WSL" 확장 설치 (Ctrl + Shift + X)
* `code .` 명령 통해 VSCode에서 Linux 파일 열기

### 6. 주피터 노트북 확장

* Python, Jupyter 확장 설치
* New File → Jupyter Notebook → 코드 입력 후 실행 (Ctrl + Enter)

### 7. VSCode에서 파이썬 가상환경 활성화

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
# 제목
## 소제목
**굵게** *기울임*

[링크](https://example.com)

$E = mc^2$

```python
print("Hello from WSL!")
````

```

---

## 마무리

- WSL은 Windows의 편리함과 Linux의 자유로움을 모두 제공
- VSCode와 연계하면 WSL 내에서도 생산적인 Python 개발 환경 구축 가능
- Jupyter, venv, pip, 코드 실행 등 다양한 Python 워크플로우를 손쉽게 설정 가능

```
