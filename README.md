# 📸 인생네컷 (Life 4 Cuts)

브라우저에서 카메라로 인생네컷을 찍고 이미지로 저장하는 웹앱.

## 🚀 GitHub Pages로 배포하는 방법

### 1단계: GitHub 저장소 만들기
1. github.com 접속 → 우측 상단 `+` → `New repository`
2. Repository name: 원하는 이름 (예: `life4cuts`)
3. **Public** 으로 설정 (Pages는 Private이면 유료)
4. `Create repository`

### 2단계: 파일 업로드
저장소 페이지에서 `uploading an existing file` 또는 `Add file → Upload files` 클릭 후, 이 폴더의 모든 파일/폴더를 통째로 드래그하세요. 즉:

```
저장소 루트/
├── index.html           ← 메인 파일 (반드시 이 이름이어야 함)
└── frames/
    ├── frame_4cut_classic.png
    ├── frame_4cut_pink_heart.png
    └── frame_4cut_film.png
```

`Commit changes` 클릭.

### 3단계: GitHub Pages 켜기
1. 저장소 → `Settings` 탭
2. 왼쪽 메뉴 `Pages`
3. Source: `Deploy from a branch`
4. Branch: `main` 선택, 폴더: `/ (root)` 선택, `Save`
5. 1~2분 기다리면 상단에 URL 표시됨:
   `https://본인아이디.github.io/저장소이름/`

### 4단계: 모바일에서 접속
- 위 URL을 폰에서 열기
- 카메라 권한 요청 시 **허용** → 이후 같은 URL은 자동으로 권한 유지
- iOS 홈 화면에 추가하면 앱처럼 사용 가능

---

## 🎨 새 프레임 추가하는 방법

### 1) 프레임 PNG 만들기

투명 배경 PNG로 사진 자리는 비워두고 테두리/장식만 그립니다.

**캔버스 사이즈 (정확히 지켜야 합니다):**
| 컷 수 | 사이즈 (W × H) |
|------|---------------|
| 2컷  | 600 × 1218 px |
| 4컷  | 600 × 2328 px |
| 6컷  | 600 × 3438 px |

**사진 영역 좌표:**
- 좌측 마진 30px, 우측 마진 30px
- 사진 한 칸: 540 × 540 px (정사각형)
- 위쪽 시작: y=30
- 사진 사이 간격: 16px

**4컷 기준 사진 영역 좌표:**
- 1번 사진: (30, 30) ~ (570, 570)
- 2번 사진: (30, 586) ~ (570, 1126)
- 3번 사진: (30, 1142) ~ (570, 1682)
- 4번 사진: (30, 1698) ~ (570, 2238)
- 하단 텍스트 영역: y=2238 ~ 2328 (90px)

**제작 도구:**
- Photoshop, Figma, Procreate, GIMP 등
- 이 영역들을 투명하게 비우고, 그 외에 테두리/배경/장식 그리기
- PNG로 저장 (투명 배경 보존)

### 2) 파일 업로드

`frames/` 폴더에 PNG 업로드:
```
frames/frame_4cut_내프레임이름.png
frames/frame_2cut_내프레임이름.png   (2컷용도 만들었다면)
frames/frame_6cut_내프레임이름.png   (6컷용도 만들었다면)
```

### 3) `index.html` 의 FRAMES 배열에 등록

`index.html` 을 열고 `const FRAMES = [` 부분 찾기 (대략 250번째 줄). 다음과 같이 추가:

```javascript
const FRAMES = [
  // ... 기존 프레임들 ...
  {
    id: 'my_frame',                    // 영문 고유 ID
    name: '내 프레임',                  // 화면에 보일 이름
    files: {
      4: 'frames/frame_4cut_my_frame.png'
      // 2컷도 만들었다면: 2: 'frames/frame_2cut_my_frame.png',
      // 6컷도 만들었다면: 6: 'frames/frame_6cut_my_frame.png'
    }
  }
];
```

### 4) GitHub에 다시 업로드 → 1~2분 후 반영됨

---

## 🐛 문제 해결

**"카메라 권한이 거부됐어요" 오류:**
- 주소창의 자물쇠 🔒 아이콘 클릭 → 사이트 설정 → 카메라 → 허용으로 변경

**모바일에서 카메라가 안 열림:**
- `https://`로 접속 중인지 확인 (HTTPS 필수)
- 다른 앱이 카메라 사용 중이면 종료 후 재시도

**프레임이 안 보임:**
- 파일 경로/이름이 정확한지 확인
- 컷 수 선택과 프레임이 매칭되는지 확인 (회색으로 보이면 그 컷 수 미지원)

**iOS 사진첩에 저장 안 됨:**
- "이미지 저장하기" 누르면 새 창이 열림 → 이미지를 **길게 눌러** "이미지 저장" 선택

---

## 📋 기능 요약

- 2컷 / 4컷 / 6컷 선택
- 외부 PNG 프레임 (오버레이 방식)
- 5종 필터 (원본, 흑백, 빈티지, 밝게, 부드럽게)
- 전·후면 카메라 전환
- 3초 카운트다운 자동 촬영
- 설정 자동 저장 (localStorage)
- 모바일 호환 (iOS Safari, Android Chrome)
