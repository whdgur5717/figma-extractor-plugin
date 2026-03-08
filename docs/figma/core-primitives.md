# Core Primitives (Vector/Rect/Transform/Color)

공식 문서의 기본 데이터 구조와 typings 구현을 통합 정리합니다.

## Vector

- 공식 문서: `https://www.figma.com/plugin-docs/api/Vector/`

```ts
// plugin-api.d.ts
interface Vector {
	readonly x: number
	readonly y: number
}
```

**사용 위치**

- 좌표/오프셋/스케일 데이터에 공통 사용

## Rect

- 공식 문서: `https://www.figma.com/plugin-docs/api/Rect/`

```ts
// plugin-api.d.ts
interface Rect {
	readonly x: number
	readonly y: number
	readonly width: number
	readonly height: number
}
```

**사용 위치**

- `absoluteBoundingBox`/`absoluteRenderBounds` 등 bounds 계열에서 사용

## Transform

- 공식 문서: `https://www.figma.com/plugin-docs/api/Transform/`

```ts
// plugin-api.d.ts
type Transform = [[number, number, number], [number, number, number]]
```

**사용 위치**

- `relativeTransform`/`absoluteTransform` 및 `GradientPaint.gradientTransform` 등에서 사용

## RGB / RGBA

- 공식 문서: `https://www.figma.com/plugin-docs/api/Color/`

```ts
// plugin-api.d.ts
interface RGB {
	readonly r: number
	readonly g: number
	readonly b: number
}

interface RGBA {
	readonly r: number
	readonly g: number
	readonly b: number
	readonly a: number
}
```

**사용 위치**

- `SolidPaint.color` → `RGB`
- `Effect.color`, `LayoutGrid.color` 등 → `RGBA`

## mixed 반환 여부

- 이 문서의 기본 타입(Vector/Rect/Transform/RGB/RGBA) 자체에는 `PluginAPI['mixed']`가 없습니다.
- mixed는 **노드 속성**에서 발생하며, 해당 속성 문서에서 처리 규칙을 확인합니다.

## VectorPath / VectorNetwork (개요)

- 공식 문서: `https://www.figma.com/plugin-docs/api/VectorPath/`
- 공식 문서: `https://www.figma.com/plugin-docs/api/VectorNetwork/`

**요약**

- 벡터 노드의 path/네트워크 데이터 구조
- 실제 타입은 `plugin-api.d.ts`에 분산 정의되어 있으므로 노드/geometry 섹션과 함께 확인

---

다음 문서: `nodes-and-mixins.md`
