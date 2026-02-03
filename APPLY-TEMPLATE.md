# PDF-to-PPTX 프로젝트에 템플릿 적용하기

**날짜**: 2026-02-03
**템플릿 버전**: 3.0.0

---

## 📋 적용 전 확인사항

### 현재 프로젝트 상태
- 프로젝트 경로: `C:\Users\admin\Project\Extension\pdf-to-pptx`
- .claude 폴더: ❌ 없음 (새로 생성)
- Git 저장소: ✅ 초기화됨

### 가상환경 사용
- **Conda 환경 사용 중**
- `.venv` 폴더 불필요
- Conda 환경 이름 문서화 필요

---

## 🔧 적용 단계

### 1단계: 템플릿 복사

```bash
# PowerShell (권장)
Copy-Item -Path "C:\Users\admin\Project\Templates\project-template\.claude" -Destination "C:\Users\admin\Project\Extension\pdf-to-pptx\.claude" -Recurse -Force

# 또는 CMD
xcopy "C:\Users\admin\Project\Templates\project-template\.claude" "C:\Users\admin\Project\Extension\pdf-to-pptx\.claude" /E /I /Y
```

**실행 후 확인**:
```bash
cd C:\Users\admin\Project\Extension\pdf-to-pptx
ls -la .claude/
```

**예상 출력**:
```
.claude/
├── CLAUDE.md
├── CLAUDE.ko.md
├── CONTEXT.md
├── SISYPHUS.md
├── SISYPHUS.ko.md
├── notes/
├── plans/
└── rules/
```

---

### 2단계: CONTEXT.md 커스터마이징

**파일**: `.claude/CONTEXT.md`

다음 섹션을 수정하세요:

```markdown
## 🎯 프로젝트 정보

**프로젝트명**: PDF to PPTX Converter
**생성일**: 2026-02-03

### 기술 스택
- Python 3.11
- PyMuPDF (PDF 처리)
- python-pptx (PowerPoint 생성)
- Pillow (이미지 처리)
- Conda (가상환경)

### 프로젝트 규칙
- PDF 파일을 PowerPoint로 변환
- 각 PDF 페이지를 이미지로 변환 후 슬라이드 삽입
- 고품질 이미지 유지 (DPI 300 권장)
```

---

### 3단계: CLAUDE.md 프로젝트 가이드 작성

**파일**: `.claude/CLAUDE.md`

```markdown
# 프로젝트 개발 가이드

> PDF to PPTX Converter 프로젝트 가이드

---

## 개발 환경

- Python 버전: 3.11
- 패키지 매니저: pip (Conda 환경 내)
- 주요 라이브러리:
  - PyMuPDF: PDF 처리
  - python-pptx: PowerPoint 생성
  - Pillow: 이미지 처리

**Conda 환경**:
```bash
conda activate pdf-to-pptx  # 또는 사용 중인 환경 이름
```

---

## 프로젝트 구조

```
pdf-to-pptx/
├── src/                    # 소스 코드
│   ├── converter.py        # PDF to PPTX 변환 로직
│   └── utils.py            # 유틸리티 함수
├── tests/                  # 테스트 코드
├── examples/               # 예제 PDF 파일
├── .claude/                # Claude 설정
└── requirements.txt        # 의존성
```

---

## 개발 워크플로우

1. 기능 개발 전 `.claude/plans/`에서 계획 확인
2. 브랜치 생성: `feature/기능명`
3. 개발 진행
4. 테스트 실행: `pytest`
5. PR 생성

---

## 코딩 컨벤션

- PEP 8 준수
- Black 포맷터 사용
- Type hints 작성
- Docstring 필수 (Google 스타일)

---

## 테스트 전략

- 단위 테스트: 각 함수별 테스트
- 통합 테스트: 전체 변환 프로세스 테스트
- 샘플 PDF 파일로 검증

---

**문서 버전**: 1.0.0
```

---

### 4단계: 개발 계획 작성

**파일**: `.claude/plans/main-development-plan.md`

PDF to PPTX 변환기의 메인 개발 계획을 작성하세요.

**예시 구조**:
```markdown
# PDF to PPTX Converter 개발 계획

## 목표
PDF 파일을 고품질 PowerPoint 파일로 변환하는 도구 개발

## 주요 기능
1. [ ] PDF 파일 읽기 및 페이지 추출
2. [ ] 각 페이지를 고해상도 이미지로 변환
3. [ ] PowerPoint 파일 생성 및 이미지 삽입
4. [ ] 배치 변환 지원
5. [ ] CLI 인터페이스 제공

## 작업 순서
...
```

---

### 5단계: .gitignore 업데이트

**파일**: `.gitignore`

Conda 환경용으로 설정:

```gitignore
# Python
__pycache__/
*.py[cod]
*$py.class
*.so

# 환경 변수
.env
.env.local

# Conda (환경은 외부에 있으므로 추가 불필요)
# .venv 관련 항목 제거 가능

# IDE
.vscode/
.idea/
*.swp
*.swo

# 테스트
.pytest_cache/
.coverage
htmlcov/

# 빌드
dist/
build/
*.egg-info/

# 프로젝트 특수
examples/*.pptx  # 생성된 PowerPoint 파일 제외
temp/
```

---

### 6단계: Conda 환경 문서화

**environment.yml 생성** (선택, 팀 공유용):

```bash
conda env export > environment.yml
```

**또는 requirements.txt 유지**:
```bash
pip list --format=freeze > requirements.txt
```

---

### 7단계: README.md 업데이트

프로젝트 README에 다음 정보 추가:

```markdown
# PDF to PPTX Converter

PDF 파일을 PowerPoint(PPTX) 파일로 변환하는 Python 도구

## 설치

### Conda 환경 설정
```bash
# 환경 생성
conda create -n pdf-to-pptx python=3.11
conda activate pdf-to-pptx

# 의존성 설치
pip install -r requirements.txt
```

## 사용법

```bash
python src/converter.py input.pdf output.pptx
```

## 개발

`.claude/` 폴더의 개발 가이드 참고:
- `.claude/CONTEXT.md` - 프로젝트 컨텍스트
- `.claude/CLAUDE.md` - 개발 가이드
- `.claude/plans/` - 개발 계획
```

---

### 8단계: Git 커밋

```bash
cd C:\Users\admin\Project\Extension\pdf-to-pptx

# 상태 확인
git status

# 템플릿 추가
git add .claude/

# 커밋
git commit -m "feat: Add Claude template structure

- Add .claude/ folder with CONTEXT.md, CLAUDE.md, SISYPHUS.md
- Configure project documentation structure
- Add plans/, notes/, rules/ folders
- Template version: 3.0.0

Co-Authored-By: Claude Sonnet 4.5 <noreply@anthropic.com>"

# 상태 확인
git log --oneline -3
```

---

## ✅ 적용 완료 체크리스트

### 파일 구조
- [ ] `.claude/` 폴더 생성됨
- [ ] `.claude/CONTEXT.md` 커스터마이징 완료
- [ ] `.claude/CLAUDE.md` 프로젝트 가이드 작성
- [ ] `.claude/plans/` 폴더에 개발 계획 작성
- [ ] `.gitignore` 업데이트 (Conda 환경용)

### 문서화
- [ ] README.md 업데이트
- [ ] Conda 환경 이름 문서화
- [ ] 프로젝트 구조 설명 추가

### Git
- [ ] 템플릿 파일 커밋
- [ ] 커밋 메시지 작성

### 검증
- [ ] Claude CLI 세션 시작 테스트
- [ ] CONTEXT.md 자동 읽기 확인
- [ ] 개발 계획 확인

---

## 🚀 다음 단계

1. **Claude CLI 세션 시작**:
   ```bash
   cd C:\Users\admin\Project\Extension\pdf-to-pptx
   claude
   ```

2. **자동 확인사항**:
   - `.claude/CONTEXT.md` 자동 읽기
   - 프로젝트 컨텍스트 파악
   - `.claude/plans/` 계획 확인

3. **Sisyphus 모드 활성화** (필요시):
   ```
   /sisyphus
   ```

4. **개발 시작**!

---

## 💡 템플릿 사용 팁

### 플랜 자동 저장
- 플랜 모드로 작업 후 완료하면
- 자동으로 `.claude/notes/` 폴더에 저장됨
- 플랜 제목이 파일명이 됨

### 폴더 구분
- **plans/**: 메인 개발 계획 (AI가 실행)
- **notes/**: 완료된 플랜 기록 (참고용)
- **rules/**: 코딩 규칙

### MCP 서버
- 전역: `C:\Users\admin\.claude.json` (이미 설정됨)
- 프로젝트별: `.mcp.json` (필요시 추가)

---

**작성일**: 2026-02-03
**템플릿 버전**: 3.0.0
