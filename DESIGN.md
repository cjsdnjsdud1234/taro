# 타로카드 서비스 디자인 가이드 (DESIGN.md)
> Apple의 정제된 화이트 갤러리 미학(White Gallery Aesthetic)과 모던 신비주의 타로의 만남.  
> 절제된 타이포그래피, 군더더기 없는 레이아웃, 직관적인 인터랙션 위에 나만의 타로 카드를 예술품처럼 조명합니다.

---

## 1. 디자인 철학 및 비주얼 아이덴티티

### 1.1 컨셉: Clean Modern Gallery Tarot (모던 갤러리 타로)
- **화이트 갤러리 캔버스**: 어둡고 조잡한 기존 운세 서비스의 그래픽을 탈피하고, Apple 특유의 순백 갤러리 공간(`Gallery White`)과 미세한 그레이 밴드(`Studio Mist`)를 배경으로 채택합니다.
- **주인공은 타로 카드**: 복잡한 장식을 배제하고, 중앙의 타로 카드 일러스트와 사용자 맞춤 3줄 해석이 온전히 돋보이도록 모든 컨트롤과 여백을 조용하고 정갈하게 배치합니다.
- **신뢰와 투명성**: 개인정보를 저장하지 않는 원칙을 투명하고 견고한 UI(안심 잠금 뱃지, 단정한 라인)로 시각화하여 사용자가 안심하고 즐길 수 있는 신뢰감을 제공합니다.
- **모바일 퍼스트 (Mobile-First)**: 모바일 웹(스마트폰 뷰포트 390px~430px 기준)에 최적화된 편안한 터치 타깃과 부드러운 전환 효과를 제공합니다.

---

## 2. 디자인 토큰 (Design Tokens)

### 2.1 색상 팔레트 (Tokens — Colors)

| 역할 | 이름 | Hex 코드 | CSS 변수 | 용도 |
|---|---|---|---|---|
| **Base Surface** | Gallery White | `#ffffff` | `--color-gallery-white` | 메인 페이지 배경, 카드 앞/뒷면 캔버스, 결과 캡처 배경 |
| **Sub Surface** | Studio Mist | `#f5f5f7` | `--color-studio-mist` | 폼 입력 컨테이너 배경, 개인정보 안내 박스, 토글 칩 기본 배경 |
| **Elevated Surface** | Paper Frost | `#fafafc` | `--color-paper-frost` | 모달/다이얼로그 서피스, 팝오버 배경 |
| **Border / Divider** | Hairline Silver | `#e5e5ea` | `--color-hairline-silver` | 1px 미세 구분선, 입력창 및 카드 테두리 |
| **Active Border** | Steel Silver | `#86868b` | `--color-steel-silver` | 포커스되지 않은 인풋 테두리, 보조 칩 아웃라인 |
| **Primary Text** | Deep Ink | `#1d1d1f` | `--color-ink` | 제목, 본문 핵심 카피, 강조 레이블, 버튼 텍스트 |
| **Secondary Text** | Slate Muted | `#6e6e73` | `--color-slate` | 부가 설명, 안내 문구, 비활성 라벨, 날짜 보조 텍스트 |
| **Tertiary Text** | Light Slate | `#86868b` | `--color-light-slate` | 플레이스홀더, 오락용 안내 푸터 |
| **Point Accent** | Apple Blue | `#0071e3` | `--color-primary-blue` | 주요 전환 버튼(CTA), 활성 링크, 별자리 강조 |
| **Mystic Accent** | Celestial Indigo | `#4f46e5` | `--color-mystic-indigo` | 타로 카드 테두리 및 신비로운 비주얼 하이라이트 |
| **Zodiac Accent** | Warm Amber | `#b45309` | `--color-zodiac-amber` | 별자리 및 생년월일 계산 문구 포인트 컬러 |

### 2.2 shadcn/ui 시맨틱 테마 변수 매핑 (Light Theme Default)

```css
:root {
  /* shadcn/ui Semantic Colors */
  --background: 0 0% 100%;             /* #ffffff (Gallery White) */
  --foreground: 240 10% 12%;           /* #1d1d1f (Deep Ink) */

  --card: 0 0% 100%;                   /* #ffffff */
  --card-foreground: 240 10% 12%;

  --popover: 240 20% 99%;              /* #fafafc */
  --popover-foreground: 240 10% 12%;

  --primary: 211 100% 45%;             /* #0071e3 (Pricing/Apple Blue) */
  --primary-foreground: 0 0% 100%;     /* #ffffff */

  --secondary: 240 5% 96%;             /* #f5f5f7 (Studio Mist) */
  --secondary-foreground: 240 10% 12%; /* #1d1d1f */

  --muted: 240 5% 96%;                 /* #f5f5f7 */
  --muted-foreground: 240 4% 44%;      /* #6e6e73 */

  --accent: 240 5% 96%;                /* #f5f5f7 */
  --accent-foreground: 211 100% 45%;   /* #0071e3 */

  --destructive: 0 84% 60%;            /* #ef4444 */
  --destructive-foreground: 0 0% 100%;

  --border: 240 6% 91%;                /* #e5e5ea (Hairline Silver) */
  --input: 240 6% 91%;                 /* #e5e5ea */
  --ring: 211 100% 45%;                /* #0071e3 (Focus Ring) */

  /* Radii */
  --radius: 1.75rem;                   /* 28px - Apple 둥근 모서리 */
  --radius-card: 28px;
  --radius-pill: 9999px;
  --radius-input: 16px;
}
```

---

## 3. 타이포그래피 (Typography)

### 3.1 폰트 패밀리
- **한글/영문 기본**: `Pretendard`, `SF Pro Display`, `SF Pro Text`, -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif
- **특징**: 일관된 자간(Letter-spacing -0.02em ~ -0.01em)을 적용하여 밀도감 있고 단단한 타이포그래피 인상을 형성합니다.

### 3.2 타입 스케일 (Type Scale)

| 역할 | 폰트 크기 | 행간(Line-Height) | 자간(Tracking) | 두께(Weight) | Tailwind 매핑 예시 |
|---|---|---|---|---|---|
| **Hero Display** | 32px | 1.15 (37px) | -0.025em | Semibold (600) | `text-3xl font-semibold tracking-tight` |
| **Section Title** | 24px | 1.25 (30px) | -0.02em | Semibold (600) | `text-2xl font-semibold tracking-tight` |
| **Card Heading** | 20px | 1.3 (26px) | -0.015em | Semibold (600) | `text-xl font-semibold` |
| **Body Large** | 17px | 1.45 (25px) | -0.015em | Regular (400) / Med (500) | `text-[17px] leading-relaxed` |
| **Body Medium** | 15px | 1.5 (22.5px) | -0.01em | Regular (400) | `text-[15px] leading-normal` |
| **Caption / Label** | 13px | 1.4 (18px) | -0.005em | Regular (400) / Med (500) | `text-[13px] text-muted-foreground` |
| **Micro / Footnote** | 11px | 1.3 (14px) | 0 | Regular (400) | `text-[11px] text-slate-500` |

---

## 4. 간격 및 레이아웃 (Spacing & Shapes)

- **기본 그리드 유닛**: `4px`
- **모바일 뷰포트 레이아웃**:
  - 최대 너비(Max-Width): `430px` (아이폰 Pro Max 규격 완벽 대응, 데스크톱에서는 중앙 정렬 카드형 레이아웃)
  - 좌우 패딩: `20px` (`px-5`)
  - 섹션 간 수직 마진: `28px` ~ `36px` (`gap-7` ~ `gap-9`)
- **컴포넌트 곡률(Border Radius)**:
  - **Feature Card & Canvas**: `28px` (`rounded-[28px]`)
  - **Button / Chip (Pill)**: `9999px` (`rounded-full`)
  - **Form Input Field**: `16px` (`rounded-2xl`)
  - **Info Box (Privacy Callout)**: `20px` (`rounded-[20px]`)
- **그림자(Shadows)**:
  - Apple Do & Don't 원칙에 따라 둔탁한 드롭 섀도우를 배제합니다.
  - 경계는 `1px solid var(--border)` (`#e5e5ea`) 단선으로만 마감하여 군더더기 없는 플랫 갤러리 룩을 완성합니다.

---

## 5. 컴포넌트 상세 가이드 (shadcn/ui 스타일)

### 5.1 버튼 (Button)
- **Primary CTA ([타로 시작], [카드 한 장 뽑기])**:
  - 형태: `h-14 w-full rounded-full bg-[#1d1d1f] text-white font-medium text-[17px]` (또는 Accent Blue `#0071e3`)
  - 인터랙션: 활성화 시 호버 `bg-black/90`, 클릭 시 살짝 작아지는 스케일 효과 `active:scale-[0.98] transition-all`
  - 비활성 상태(Disabled): `bg-[#e5e5ea] text-[#86868b] cursor-not-allowed`
- **Secondary Action ([이미지 저장], [결과 공유])**:
  - 형태: `h-12 rounded-full bg-[#f5f5f7] text-[#1d1d1f] font-medium text-[15px] hover:bg-[#e5e5ea]`
- **Ghost Utility ([다시 뽑기], [처음으로])**:
  - 형태: `h-10 text-[14px] text-[#6e6e73] hover:text-[#1d1d1f] underline-offset-4 hover:underline`

### 5.2 주제 선택 칩 (Topic Toggle Chips - F-2)
- 6개 주제: 💼 커리어 · 💰 재물 · 💕 연애 · 🌿 건강 · 📚 학업 · ✨ 종합
- 3열 × 2행 그리드 배치 (`grid grid-cols-3 gap-2.5`)
- **미선택 상태**: `bg-[#f5f5f7] text-[#1d1d1f] border border-transparent rounded-full py-2.5 px-3 text-[14px] font-medium`
- **선택 상태**: `bg-[#1d1d1f] text-white border border-[#1d1d1f] shadow-sm` (또는 Primary Blue `#0071e3`)

### 5.3 텍스트 인풋 (Input - F-2)
- 이름(최대 10자), 생년월일(YYYY.MM.DD), 전공(선택)
- 형태:
  - `h-13 w-full bg-[#f5f5f7] border border-transparent focus:border-[#0071e3] focus:bg-white rounded-2xl px-4 text-[16px] text-[#1d1d1f] transition-all outline-none`
- 레이블 & 서포트 텍스트:
  - 필드 상단에 간결한 SF Pro Text 13px 레이블 배치
  - 필수/선택 여부를 직관적으로 표기

### 5.4 개인정보 안심 콜아웃 (Privacy Callout Box)
- 개인정보는 서버로 전송하지 않는다는 원칙(원칙 1)을 고지하는 신뢰성 컴포넌트
- 스타일:
  ```html
  <div class="flex items-start gap-3 p-4 bg-[#f5f5f7] rounded-[20px] border border-[#e5e5ea]/60 text-[13px] text-[#6e6e73] leading-relaxed">
    <span class="text-[16px] mt-0.5">🔒</span>
    <div>입력한 이름·생년월일·전공은 해석을 만드는 데만 쓰고 저장하지 않아요. 창을 닫거나 [처음으로]를 누르면 바로 지워져요.</div>
  </div>
  ```

### 5.5 타로 카드 뽑기 인터랙션 & 뒤집기 (F-3 Card Flip)
- **카드 규격**: 모바일 화면 기준 가로 180px × 세로 300px (비율 약 1:1.66), `rounded-[20px]`
- **앞/뒷면 연출**:
  - **뒷면**: 깊은 밤하늘/기하학 패턴의 미니멀 아트
  - **앞면**: 22장 메이저 아르카나 모던 라인 아트 일러스트
- **Flip 애니메이션 (CSS 3D Transform)**:
  - `transition-transform duration-700 ease-out [transform-style:preserve-3d]`
  - 뽑기 버튼 클릭 시 0.8초 동안 Y축 180도 회전하며 부드럽게 앞면 공개

### 5.6 결과 카드 및 다운로드 이미지 (1080×1350 Canvas - F-4, F-5)
- 인스타그램 피드/스토리 및 메신저 공유에 최적화된 **4:5 비율(1080 × 1350 px)** 캔버스
- **카드 내부 구성 (상단 → 하단)**:
  1. **헤더 캡션**: `{이름}님의 타로 · {주제}` (`text-[15px] font-medium text-[#6e6e73]`)
  2. **카드 비주얼**: 라운드 프레임 속 카드 그림 (`rounded-2xl border border-[#e5e5ea]`)
  3. **카드 정보**: `XIX 태양 · ♌ 사자자리` (`text-[19px] font-semibold text-[#1d1d1f] mt-3`)
  4. **3줄 맞춤 해석 (90자 이내)**:
     - 1줄: 카드 × 주제 기본 문장
     - 2줄: 생년월일 별자리 문장
     - 3줄: 전공 계열 맞춤 문장
     - 폰트: `text-[16px] leading-[1.6] text-[#1d1d1f]`
  5. **하단 푸터**:
     - `※ 오락용 타로 해석입니다` (`text-[12px] text-[#86868b]`)
     - 서비스 로고/타이틀: `오늘의 타로 (Today Tarot)`

### 5.7 알림 토스트 (Feedback Toast)
- 상태별 안내 문구(TARO_02 기준)를 화면 상단/하단에 플로팅 캡슐 형태로 2초간 표시:
  - 이미지 저장: `"이미지를 저장했어요"`
  - 인앱 브라우저 다운로드 불가: `"이미지를 길게 눌러 저장해 주세요"`
  - 자동 복사 성공: `"결과를 복사했어요. 원하는 앱에 붙여 넣어 주세요"`
  - 스타일: `bg-[#1d1d1f]/90 text-white backdrop-blur-md px-5 py-3 rounded-full text-[14px]`

---

## 6. 화면별 와이어프레임 구현 가이드 (Screen Mapping)

```
┌───────────────────────────────────────┐
│ S-01 시작 화면                         │
├───────────────────────────────────────┤
│ • 헤더: 🔮 오늘의 타로                   │
│ • 카드 비주얼: 중앙 카드 뒷면 그래픽        │
│ • 카피: 내 정보를 넣고 카드 한 장으로      │
│         나만의 해석을 받아 봐요         │
│ • [타로 시작] Primary 버튼              │
│ • 푸터: ※ 오락용 타로 · 정보는 저장 안 해요│
└───────────────────────────────────────┘
                   ↓ (타로 시작)
┌───────────────────────────────────────┐
│ S-02 내 정보 & 주제 선택 화면           │
├───────────────────────────────────────┤
│ • 상단: ← 나에 대해 알려 주세요          │
│ • [이름 입력] (최대 10자)                │
│ • [생년월일 입력] (YYYY.MM.DD)           │
│ • [전공 입력] (선택)                     │
│ • [어떤 주제가 궁금한가요?] 6개 칩       │
│ • 🔒 개인정보 안심 안내 박스            │
│ • [카드 한 장 뽑기] (모두 입력 시 활성화) │
└───────────────────────────────────────┘
                   ↓ (카드 뽑기 & 플립 0.8s)
┌───────────────────────────────────────┐
│ S-03 맞춤 해석 결과 화면                │
├───────────────────────────────────────┤
│ ┌───────────────────────────────────┐ │
│ │ 1080×1350 카드 캔버스 영역         │ │
│ │ • {이름}님의 타로 · {주제}          │ │
│ │ • 카드 앞면 그림                   │ │
│ │ • 카드 번호/이름 · 별자리          │ │
│ │ • 맞춤 3줄 해석                    │ │
│ │ • ※ 오락용 타로 해석입니다          │ │
│ └───────────────────────────────────┘ │
│ • [이미지 저장]  [결과 공유]           │
│ • [다시 뽑기]    [처음으로]            │
│ • 🔒 정보 폐기 안내 문구               │
└───────────────────────────────────────┘
```

---

## 7. Tailwind CSS v4 `@theme` 설정 스니펫

```css
@theme {
  /* Colors */
  --color-gallery-white: #ffffff;
  --color-studio-mist: #f5f5f7;
  --color-paper-frost: #fafafc;
  --color-hairline-silver: #e5e5ea;
  --color-steel-silver: #86868b;
  --color-ink: #1d1d1f;
  --color-slate: #6e6e73;
  --color-primary-blue: #0071e3;
  --color-mystic-indigo: #4f46e5;
  --color-zodiac-amber: #b45309;

  /* Font Families */
  --font-pretendard: 'Pretendard', -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif;
  --font-display: 'SF Pro Display', 'Pretendard', sans-serif;
  --font-body: 'SF Pro Text', 'Pretendard', sans-serif;

  /* Radii */
  --radius-card: 28px;
  --radius-box: 20px;
  --radius-input: 16px;
  --radius-pill: 9999px;

  /* Animation */
  --keyframes-flip: {
    '0%': { transform: 'rotateY(0deg)' },
    '100%': { transform: 'rotateY(180deg)' }
  };
  --animation-flip: flip 0.8s cubic-bezier(0.16, 1, 0.3, 1) forwards;
}
```
