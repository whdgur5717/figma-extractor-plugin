# Figma Plugin API 데이터 타입 레퍼런스

이 문서는 **Figma Plugin API의 데이터 타입**을 대상으로 공식 문서 설명과 `@figma/plugin-typings`의 실제 타입 정의를 **타입 단위로 통합**해 정리한 레퍼런스입니다. 구현 코드나 기존 문서에 의존하지 않고, 공식 문서와 typings 정의만을 근거로 작성합니다.

## 소스

- 공식 문서: `https://www.figma.com/plugin-docs/` 및 `https://developers.figma.com/docs/plugins/`
- typings: `node_modules/@figma/plugin-typings/plugin-api.d.ts`

## 문서 구조

- `core-primitives.md`: 기본 수학/색상 타입 (Vector, Rect, Transform, RGB/RGBA 등)
- `nodes-and-mixins.md`: 노드 트리 + 믹스인 구조
- `styles-and-paints.md`: Style + Paint 계열
- `effects.md`: Effect 계열
- `layout-and-constraints.md`: 레이아웃/오토레이아웃/그리드/제약
- `text.md`: 텍스트 데이터 구조
- `data-variables.md`: 변수/토큰/바인딩
- `data-assets-export.md`: 이미지/비디오/익스포트
- `data-plugin-data.md`: plugin data (private/shared)
- `data-interactions.md`: 인터랙션 데이터 (Reaction/Action/Trigger/Transition)

## 작성 규칙

각 타입 섹션은 아래 포맷을 유지합니다.

- **공식 설명 요약**: 문서에 명시된 목적/의미
- **typings 구현 구조**: `plugin-api.d.ts` 실제 정의
- **실무 포인트**: nullable, 유니온 분기, mixed 처리, 값 범위
- **관련 타입/링크**: 연결되는 타입과 문서 링크

## figma.mixed (공식 설명 + typings)

- 공식 문서: `https://developers.figma.com/docs/plugins/api/properties/figma-mixed/`
- 텍스트 혼합 처리: `https://developers.figma.com/docs/plugins/working-with-text/`

```ts
// plugin-api.d.ts
// This a constant value that some node properties return when they are a mix of multiple values.
// ... Always compare against `figma.mixed`.
readonly mixed: unique symbol
```

**요점**

- `figma.mixed`는 **값 자체가 아니라 비교용 sentinel**입니다.
- mixed 처리는 **속성별 규칙**이 다릅니다. 각 문서의 mixed 섹션에 속성별 접근 방법을 정리했습니다.

---

다음 문서부터 각 데이터 타입을 도메인별로 상세히 정리합니다.
