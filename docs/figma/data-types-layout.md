# Data Types — Layout & Geometry

## Rect

- **데이터 개념**: 좌표 및 크기 사각형 데이터.
- **공식 설명 요약**: `x`, `y`, `width`, `height`로 구성.
- **typings 구조**: `interface Rect { x; y; width; height }`
- **예제 데이터**

```json
{ "x": 0, "y": 0, "width": 120, "height": 40 }
```

## Transform

- **데이터 개념**: 2x3 affine 변환 행렬.
- **공식 설명 요약**: `[[a, c, e], [b, d, f]]` 구조.
- **typings 구조**: `type Transform = [[number, number, number], [number, number, number]]`
- **예제 데이터**

```json
[
	[1, 0, 20],
	[0, 1, 10]
]
```

## Constraints

- **데이터 개념**: 부모 리사이즈 시 자식 고정/스케일 방식.
- **공식 설명 요약**: `horizontal`/`vertical` 각각 `ConstraintType`.
- **typings 구조**: `interface Constraints { horizontal; vertical }`, `type ConstraintType = 'MIN' | 'CENTER' | 'MAX' | 'STRETCH' | 'SCALE'`
- **예제 데이터 (모든 타입 예시)**

```json
{ "horizontal": "MIN", "vertical": "MIN" }
```

```json
{ "horizontal": "CENTER", "vertical": "CENTER" }
```

```json
{ "horizontal": "MAX", "vertical": "MAX" }
```

```json
{ "horizontal": "STRETCH", "vertical": "STRETCH" }
```

```json
{ "horizontal": "SCALE", "vertical": "SCALE" }
```

## LayoutGrid

- **데이터 개념**: 프레임의 컬럼/로우/그리드 구성.
- **공식 설명 요약**: `RowsColsLayoutGrid | GridLayoutGrid` 유니온.
- **typings 구조**: `type LayoutGrid = RowsColsLayoutGrid | GridLayoutGrid`
- **예제 데이터 (유니온 전체)**

```json
{ "pattern": "COLUMNS", "alignment": "MIN", "gutterSize": 16, "count": 12, "sectionSize": 48, "offset": 0 }
```

```json
{ "pattern": "ROWS", "alignment": "CENTER", "gutterSize": 8, "count": 6, "sectionSize": 40 }
```

```json
{ "pattern": "GRID", "sectionSize": 8 }
```

## OverflowDirection

- **데이터 개념**: 프레임 스크롤 방향.
- **공식 설명 요약**: `NONE`, `HORIZONTAL`, `VERTICAL`, `BOTH`.
- **typings 구조**: `type OverflowDirection = 'NONE' | 'HORIZONTAL' | 'VERTICAL' | 'BOTH'`
- **예제 데이터 (모든 타입 예시)**

```json
{ "overflowDirection": "NONE" }
```

```json
{ "overflowDirection": "HORIZONTAL" }
```

```json
{ "overflowDirection": "VERTICAL" }
```

```json
{ "overflowDirection": "BOTH" }
```

## 문서 링크

- https://developers.figma.com/docs/plugins/api/Rect/
- https://developers.figma.com/docs/plugins/api/Transform/
- https://developers.figma.com/docs/plugins/api/Constraints/
- https://developers.figma.com/docs/plugins/api/LayoutGrid/
- https://developers.figma.com/docs/plugins/api/OverflowDirection/
