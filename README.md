# figma-extractor-plugin

Figma 디자인 노드를 구조화된 React 호환 포맷으로 추출하는 Figma 플러그인. 선택한 노드의 스타일, 레이아웃, 디자인 토큰, 컴포넌트 참조를 정규화하여 LLM 기반 코드 생성에 적합한 데이터를 만든다.

## 주요 기능

- **노드 트리 추출** — 선택한 Figma 노드와 하위 노드를 재귀적으로 순회하여 완전한 트리 구조로 변환
- **디자인 토큰 보존** — Figma Variables(디자인 토큰)를 추적하고, 토큰 이름/컬렉션/모드 정보를 fallback 값과 함께 유지
- **컴포넌트 인스턴스 처리** — Instance → Component 참조, variant 정보를 보존하여 프레임워크 컴포넌트 매핑 가능
- **CSS 호환성 검사** — CSS로 표현 불가능한 효과(angular gradient, noise, glass 등)를 감지하고 SVG fallback으로 자동 전환
- **에셋 참조 수집** — 이미지, 벡터, 마스크 등의 에셋 참조를 별도로 추출

## 파이프라인 구조

```
Figma Selection
    ↓
Extract  — Figma API에서 raw 속성 수집 (fills, stroke, effects, layout, text, corner)
    ↓
Normalize — 일관된 스키마로 정규화 (TokenizedValue, NormalizedValue)
    ↓
Compatibility Check — CSS 렌더링 가능 여부 판단, 불가 시 SVG export
    ↓
Enrich — boundVariables → TokenRef 해석, 토큰 매핑 적용
    ↓
Output — ReactNode 트리 (JSON)
```

## 출력 형식

```jsonc
{
  "type": "FRAME",
  "props": {
    "id": "123:456",
    "name": "Card",
    "style": { /* 정규화된 스타일 */ },
    "boundVariables": { /* 토큰 바인딩 */ }
  },
  "children": [ /* 재귀적 자식 노드 */ ],
  "instanceRef": { "componentId": "...", "componentName": "Button", "variantInfo": { "size": "md" } },
  "tokensRef": [ /* 디자인 토큰 매핑 */ ],
  "assets": [ /* 이미지/벡터 에셋 참조 */ ],
  "svgFallback": "..."  // CSS 비호환 시
}
```

## 지원 노드 타입

`FRAME` · `INSTANCE` · `TEXT` · `RECTANGLE` · `GROUP`

## 개발

```bash
pnpm install
pnpm dev        # Figma 플러그인 개발 서버
pnpm build      # 프로덕션 빌드
pnpm lint       # ESLint
pnpm type-check # TypeScript 검사
```

`pnpm dev` 실행 후 Figma → Plugins → Development → Import plugin from manifest 에서 `manifest.json`을 선택하여 로드한다.

## 프로젝트 구조

```
src/
├── main/                    # Figma 메인 스레드 (Plugin API 접근)
│   ├── main.ts              # 진입점 — selection 이벤트 → buildNodeTree → UI 전송
│   ├── node/                # 노드 트리 빌더 & 타입 정의
│   └── pipeline/
│       ├── extract/         # Raw 데이터 추출 (fills, stroke, effects, layout, text, corner)
│       ├── normalize/       # 스키마 정규화 (TokenizedValue, NormalizedValue)
│       ├── compatibility/   # CSS 호환성 검사
│       ├── export/          # SVG fallback export
│       ├── variables/       # VariableRegistry — 토큰 해석 & 캐싱
│       └── shared/          # Zod 스키마
└── ui/                      # UI 스레드 (React iframe)
    ├── App.tsx              # 추출 결과 JSON 표시 + 클립보드 복사
    └── components/          # Button, Icon, Input
```
