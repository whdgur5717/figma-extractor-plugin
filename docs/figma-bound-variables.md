# Figma Plugin API - boundVariables 읽기 가이드

이 문서는 Figma Plugin API에서 Variable 바인딩 정보를 읽는 방법을 정리한 레퍼런스입니다.

## 목차

1. [개요](#개요)
2. [VariableAlias 타입](#variablealias-타입)
3. [바인딩 가능한 속성 목록](#바인딩-가능한-속성-목록)
4. [boundVariables 읽기](#boundvariables-읽기)
5. [코드 예시](#코드-예시)

---

## 개요

Figma에서 Variable을 노드 속성에 적용하면, 해당 바인딩 정보가 노드의 `boundVariables` 프로퍼티에 `VariableAlias` 형태로 저장됩니다.

```
Variable (디자인 토큰)
    ↓ 바인딩
Node.boundVariables (VariableAlias 객체)
```

---

## VariableAlias 타입

Variable 바인딩을 나타내는 기본 타입입니다.

```typescript
interface VariableAlias {
	type: "VARIABLE_ALIAS"
	id: string // Variable ID (예: "VariableID:1:7")
}
```

| 속성   | 타입               | 설명                                |
| ------ | ------------------ | ----------------------------------- |
| `type` | `'VARIABLE_ALIAS'` | 리터럴 상수, Variable 참조임을 식별 |
| `id`   | `string`           | 바인딩된 Variable의 고유 ID         |

### Variable ID로 실제 Variable 조회

```typescript
const variable = await figma.variables.getVariableByIdAsync(alias.id)
// variable.name, variable.resolvedType 등 접근 가능
```

---

## 바인딩 가능한 속성 목록

### 1. VariableBindableNodeField (노드 속성)

노드에 직접 바인딩 가능한 속성들입니다.

#### 크기 (Dimensions)

| 속성        | 타입    | 설명      |
| ----------- | ------- | --------- |
| `width`     | `FLOAT` | 노드 너비 |
| `height`    | `FLOAT` | 노드 높이 |
| `minWidth`  | `FLOAT` | 최소 너비 |
| `maxWidth`  | `FLOAT` | 최대 너비 |
| `minHeight` | `FLOAT` | 최소 높이 |
| `maxHeight` | `FLOAT` | 최대 높이 |

#### Auto Layout (레이아웃)

| 속성                 | 타입    | 설명                    |
| -------------------- | ------- | ----------------------- |
| `itemSpacing`        | `FLOAT` | 아이템 간격 (gap)       |
| `counterAxisSpacing` | `FLOAT` | 교차축 간격 (wrap 모드) |
| `paddingLeft`        | `FLOAT` | 왼쪽 패딩               |
| `paddingRight`       | `FLOAT` | 오른쪽 패딩             |
| `paddingTop`         | `FLOAT` | 위쪽 패딩               |
| `paddingBottom`      | `FLOAT` | 아래쪽 패딩             |

#### Corner Radius (모서리)

| 속성                | 타입    | 설명               |
| ------------------- | ------- | ------------------ |
| `topLeftRadius`     | `FLOAT` | 좌상단 모서리 반경 |
| `topRightRadius`    | `FLOAT` | 우상단 모서리 반경 |
| `bottomLeftRadius`  | `FLOAT` | 좌하단 모서리 반경 |
| `bottomRightRadius` | `FLOAT` | 우하단 모서리 반경 |

#### Stroke (선)

| 속성                 | 타입    | 설명           |
| -------------------- | ------- | -------------- |
| `strokeWeight`       | `FLOAT` | 전체 선 두께   |
| `strokeTopWeight`    | `FLOAT` | 위쪽 선 두께   |
| `strokeRightWeight`  | `FLOAT` | 오른쪽 선 두께 |
| `strokeBottomWeight` | `FLOAT` | 아래쪽 선 두께 |
| `strokeLeftWeight`   | `FLOAT` | 왼쪽 선 두께   |

#### Grid (그리드 레이아웃)

| 속성            | 타입    | 설명           |
| --------------- | ------- | -------------- |
| `gridRowGap`    | `FLOAT` | 그리드 행 간격 |
| `gridColumnGap` | `FLOAT` | 그리드 열 간격 |

#### 기타

| 속성         | 타입      | 설명                   |
| ------------ | --------- | ---------------------- |
| `visible`    | `BOOLEAN` | 표시 여부              |
| `opacity`    | `FLOAT`   | 불투명도 (0-1)         |
| `characters` | `STRING`  | 텍스트 내용 (TextNode) |

### 2. VariableBindableTextField (텍스트 속성)

텍스트 노드의 범위별 스타일에 바인딩 가능한 속성들입니다.

| 속성               | 타입     | 설명                           |
| ------------------ | -------- | ------------------------------ |
| `fontFamily`       | `STRING` | 폰트 패밀리                    |
| `fontStyle`        | `STRING` | 폰트 스타일 (Regular, Bold 등) |
| `fontWeight`       | `FLOAT`  | 폰트 굵기 (400, 700 등)        |
| `fontSize`         | `FLOAT`  | 폰트 크기                      |
| `letterSpacing`    | `FLOAT`  | 자간                           |
| `lineHeight`       | `FLOAT`  | 행간                           |
| `paragraphSpacing` | `FLOAT`  | 문단 간격                      |
| `paragraphIndent`  | `FLOAT`  | 문단 들여쓰기                  |

### 3. Paint 속성 (Fills, Strokes)

Paint 객체 내부에서 바인딩 가능한 속성입니다.

| 속성    | 타입    | 설명 | 적용 대상                |
| ------- | ------- | ---- | ------------------------ |
| `color` | `COLOR` | 색상 | SolidPaint, GradientStop |

### 4. Effect 속성

Effect 객체 내부에서 바인딩 가능한 속성입니다.

| 속성      | 타입    | 설명        | 적용 대상                                          |
| --------- | ------- | ----------- | -------------------------------------------------- |
| `color`   | `COLOR` | 그림자 색상 | DropShadow, InnerShadow                            |
| `offsetX` | `FLOAT` | X축 오프셋  | DropShadow, InnerShadow                            |
| `offsetY` | `FLOAT` | Y축 오프셋  | DropShadow, InnerShadow                            |
| `radius`  | `FLOAT` | 블러 반경   | DropShadow, InnerShadow, LayerBlur, BackgroundBlur |
| `spread`  | `FLOAT` | 확산        | DropShadow, InnerShadow                            |

### 5. LayoutGrid 속성

LayoutGrid 객체에서 바인딩 가능한 속성입니다. pattern/alignment 조합에 따라 허용 필드가 다릅니다.

| 속성          | 타입    | 설명        |
| ------------- | ------- | ----------- |
| `sectionSize` | `FLOAT` | 섹션 크기   |
| `count`       | `FLOAT` | 행/열 개수  |
| `offset`      | `FLOAT` | 시작 오프셋 |
| `gutterSize`  | `FLOAT` | 거터 크기   |

### 6. Style boundVariables

스타일에서도 boundVariables를 제공합니다.

| 스타일 타입   | 바인딩 가능한 필드 |
| ------------- | ------------------ |
| `PaintStyle`  | `color`            |
| `EffectStyle` | `effects`          |
| `GridStyle`   | `layoutGrids`      |

### 7. ComponentProperties (Instance)

InstanceNode의 componentProperties는 value에 변수 바인딩을 가질 수 있습니다.

- `instance.componentProperties[<propKey>].boundVariables?.value`

---

## boundVariables 읽기

### boundVariables 값 형태

boundVariables는 다음 형태로 나타날 수 있습니다.

```typescript
type BoundVariableValue = VariableAlias | VariableAlias[] | { [key: string]: BoundVariableValue }
```

예시: `size: { x, y }`, `individualStrokeWeights: { top, right, bottom, left }`

### 노드에서 직접 읽기

```typescript
const node = await figma.getNodeByIdAsync("1:4");
const boundVars = node.boundVariables;

// 결과 예시
{
  "width": { "type": "VARIABLE_ALIAS", "id": "VariableID:1:5" },
  "paddingLeft": { "type": "VARIABLE_ALIAS", "id": "VariableID:1:10" },
  "fills": [
    { "type": "VARIABLE_ALIAS", "id": "VariableID:1:7" }
  ],
  "strokes": [
    { "type": "VARIABLE_ALIAS", "id": "VariableID:1:8" }
  ]
}
```

### 배열 속성 (fills, strokes, effects)

fills, strokes, effects는 배열이므로 인덱스별로 접근합니다.

```typescript
// fills의 첫 번째 Paint에 바인딩된 color
const fillAlias = node.boundVariables?.fills?.[0]

// 또는 Paint 객체에서 직접 접근
const paint = node.fills[0]
if ("boundVariables" in paint) {
	const colorAlias = paint.boundVariables?.color
}
```

### Gradient Stops

그라디언트의 각 stop에도 개별 바인딩이 가능합니다.

```typescript
const gradientPaint = node.fills[0] as GradientPaint
gradientPaint.gradientStops.forEach((stop, index) => {
	const colorAlias = stop.boundVariables?.color
	// { type: 'VARIABLE_ALIAS', id: 'VariableID:...' }
})
```

### LayoutGrid

```typescript
if ("layoutGrids" in node && Array.isArray(node.layoutGrids)) {
	node.layoutGrids.forEach((grid) => {
		const gridAlias = grid.boundVariables
	})
}
```

### ComponentProperties (Instance)

```typescript
if ("componentProperties" in node && node.componentProperties) {
	Object.values(node.componentProperties).forEach((prop) => {
		const valueAlias = prop.boundVariables?.value
	})
}
```

### 텍스트 범위별 읽기

```typescript
// 특정 범위의 특정 속성
const fontWeightAlias = textNode.getRangeBoundVariable(0, 5, "fontWeight")

// 모든 세그먼트의 boundVariables
const segments = textNode.getStyledTextSegments(["boundVariables"])
segments.forEach((segment) => {
	console.log(segment.start, segment.end, segment.boundVariables)
})
```

---

## 코드 예시

### boundVariables 전체 수집 (Extract 패턴)

```typescript
type BoundVariableValue = VariableAlias | VariableAlias[] | { [key: string]: BoundVariableValue }

const isVariableAlias = (value: unknown): value is VariableAlias => {
	return (
		!!value &&
		typeof value === "object" &&
		"type" in value &&
		"id" in value &&
		(value as { type?: unknown }).type === "VARIABLE_ALIAS" &&
		typeof (value as { id?: unknown }).id === "string"
	)
}

const collectAliases = (value: BoundVariableValue | undefined, ids: Set<string>): void => {
	if (!value) return
	if (Array.isArray(value)) {
		value.forEach((entry) => collectAliases(entry as BoundVariableValue, ids))
		return
	}
	if (isVariableAlias(value)) {
		ids.add(value.id)
		return
	}
	if (typeof value === "object") {
		Object.values(value as Record<string, BoundVariableValue>).forEach((entry) => {
			collectAliases(entry, ids)
		})
	}
}

const collectBoundVariableIds = (node: SceneNode): string[] => {
	const ids = new Set<string>()

	// 1. 노드 레벨 boundVariables
	collectAliases(node.boundVariables as BoundVariableValue | undefined, ids)

	// 2. Paint (fills, strokes) + gradient stops
	const collectFromPaints = (paints: readonly Paint[] | typeof figma.mixed) => {
		if (paints === figma.mixed || !Array.isArray(paints)) return
		paints.forEach((paint) => {
			if ("boundVariables" in paint) {
				collectAliases(paint.boundVariables as BoundVariableValue | undefined, ids)
			}
			if ("gradientStops" in paint) {
				paint.gradientStops.forEach((stop) => {
					collectAliases(stop.boundVariables as BoundVariableValue | undefined, ids)
				})
			}
		})
	}

	if ("fills" in node) collectFromPaints(node.fills)
	if ("strokes" in node) collectFromPaints(node.strokes)

	// 3. Effects
	if ("effects" in node && Array.isArray(node.effects)) {
		node.effects.forEach((effect) => {
			if ("boundVariables" in effect) {
				collectAliases(effect.boundVariables as BoundVariableValue | undefined, ids)
			}
		})
	}

	// 4. Layout grids
	if ("layoutGrids" in node && Array.isArray(node.layoutGrids)) {
		node.layoutGrids.forEach((grid) => {
			if ("boundVariables" in grid) {
				collectAliases(grid.boundVariables as BoundVariableValue | undefined, ids)
			}
		})
	}

	// 5. Component properties (Instance)
	if ("componentProperties" in node && node.componentProperties) {
		Object.values(node.componentProperties).forEach((prop) => {
			collectAliases(prop.boundVariables?.value as BoundVariableValue | undefined, ids)
		})
	}

	// 6. Text segments
	if (node.type === "TEXT") {
		const segments = node.getStyledTextSegments(["boundVariables"])
		segments.forEach((segment) => {
			collectAliases(segment.boundVariables as BoundVariableValue | undefined, ids)
		})
	}

	return Array.from(ids)
}

const collectStyleBoundVariableIds = (style: PaintStyle | EffectStyle | GridStyle): string[] => {
	const ids = new Set<string>()
	collectAliases(style.boundVariables as BoundVariableValue | undefined, ids)
	return Array.from(ids)
}
```

### TokenizedValue 패턴 (Normalize용)

```typescript
type TokenRef = {
	id: string
	name?: string
	collectionId?: string
	collectionName?: string
}

type TokenizedValue<T> = T | { tokenRef: TokenRef; fallback: T }

const toTokenizedValue = <T>(value: T, alias: VariableAlias | null | undefined): TokenizedValue<T> => {
	return alias ? { tokenRef: { id: alias.id }, fallback: value } : value
}

// 사용 예시
const normalizedColor = toTokenizedValue({ hex: "#FF0000", rgb: "rgb(255,0,0)" }, paint.boundVariables?.color)
```

---

## 참고 자료

- [Working with Variables | Figma Developer Docs](https://developers.figma.com/docs/plugins/working-with-variables/)
- [VariableBindableNodeField | Figma Plugin API](https://developers.figma.com/docs/plugins/api/VariableBindableNodeField/)
- [VariableBindableTextField | Figma Plugin API](https://developers.figma.com/docs/plugins/api/VariableBindableTextField/)
- [VariableBindablePaintField | Figma Plugin API](https://developers.figma.com/docs/plugins/api/VariableBindablePaintField/)
- [VariableBindableEffectField | Figma Plugin API](https://developers.figma.com/docs/plugins/api/VariableBindableEffectField/)
- [VariableBindableLayoutGridField | Figma Plugin API](https://developers.figma.com/docs/plugins/api/VariableBindableLayoutGridField/)
- [VariableBindablePaintStyleField | Figma Plugin API](https://developers.figma.com/docs/plugins/api/VariableBindablePaintStyleField/)
- [VariableBindableEffectStyleField | Figma Plugin API](https://developers.figma.com/docs/plugins/api/VariableBindableEffectStyleField/)
- [VariableBindableGridStyleField | Figma Plugin API](https://developers.figma.com/docs/plugins/api/VariableBindableGridStyleField/)
- [PaintStyle | Figma Plugin API](https://developers.figma.com/docs/plugins/api/PaintStyle/)
- [EffectStyle | Figma Plugin API](https://developers.figma.com/docs/plugins/api/EffectStyle/)
- [GridStyle | Figma Plugin API](https://developers.figma.com/docs/plugins/api/GridStyle/)
- [VariableAlias | Figma Plugin API](https://developers.figma.com/docs/plugins/api/VariableAlias/)
- [figma.variables | Figma Plugin API](https://developers.figma.com/docs/plugins/api/figma-variables/)
