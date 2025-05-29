# 파이썬 개발환경 설정 가이드 (VSCode 사용)

---

## 프로그래밍 개발 환경 선택지

### 파이썬 인터프리터 설치

* [Python 공신 웹사이트](https://www.python.org/)
* Windows 복통 설치: Microsoft Store에서 "Python 3.13" 설치

### 개발 환경 포함 기술

| 환경           | 특징                 |
| ------------ | ------------------ |
| Anaconda     | 파이썬 + Jupyter 포함   |
| VSCode       | 확장을 통해 가변성 가지면서 간편 |
| PyCharm      | 유료 버전은 가장 바로운 IDE  |
| Jupyter Lab  | 설치 후 여러 파일 가능      |
| Google Colab | 웹 기본, 설치 필요 없음     |

---

## VSCode 설치 및 설정

### 설치

* 웹사이트: [https://code.visualstudio.com/](https://code.visualstudio.com/)
* 기본 값대로 설치 진행

### 필수 익스텐션

| 확장               | 기능                     |
| ---------------- | ---------------------- |
| Python           | 코드 실행, 디버그, 가상환경 관리    |
| Pylance          | 자동완전, 타입검사             |
| Jupyter          | 과\uud559과 시각화 연동       |
| GitLens          | Git 관리법 강화             |
| FastAPI Snippets | FastAPI 자동완전           |
| REST Client      | .http 파일로 HTTP 요청 시트   |
| Docker           | Dockerfile, compose 지원 |

---

## 파이썬 파일

* `.py`: 표준 파이썬 파일
* `.ipynb`: Jupyter 노트북 파일

---

## 가상환경 (Virtual Environment)

### 만들기

```bash
python -m venv .venv
```

### 활성화

```bash
# Windows CMD
.venv\Scripts\activate

# Windows PowerShell
.venv\Scripts\Activate.ps1

# macOS/Linux
source .venv/bin/activate
```

> 활성화 성공시 터미널에 (.venv)가 표시됨

### 패키지 관리

```bash
# 목록을 requirements.txt에 저장
pip freeze > requirements.txt

# requirements 기반 설치
pip install -r requirements.txt

# 오프랜인 보관용 파일 다운로드
pip download -r requirements.txt -d packages/

# 오프랜 설치
pip install --no-index --find-links=packages/ -r requirements.txt
```

---

## 주피터 노트북에서 가상환경 추가

1. `.ipynb` 파일 생성
2. 커널 선택 → `Python Environments...`
3. `+ Create Python Environment` 선택
4. `.venv` 추가 후 선택

---

## 터미널 열기 (VSCode)

```bash
# 단\u축키: Ctrl + Shift + `
```

* (.venv) 표시에서 가상환경 활성화 확인
* 보이지 않으면 수동 활성화

---

## 파이썬 실행

* 우측 상단 Run Python File 클릭 또는

```bash
python filename.py
```

---

## Markdown 셀 과 Code 셀 (Jupyter)

### Markdown 셀

* 문서 작성, 코드 설명용
* 포맷: `#` 제목, `*` 기울임, `**` 굵게 등
* 수식: `$E = mc^2$`, `$$a^2 + b^2 = c^2$$`
* 이미지: `![설명](url)`
* 링크: `[이름](https://example.com)`

### Code 셀

* Python 코드 실행, 분석, 시각화 등

---

## 마무리

이 문서는 VSCode 기반 파이썬 개발 환경을 빠르게 설정하기 위한 실용 가이드입니다. 가상환경 활용, 확장 프로그램, 노트북 환경까지 Python 개발 입문자에게 필수적인 핵심 내용을 정리했습니다.
