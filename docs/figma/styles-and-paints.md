# Styles & Paints

## Paint (fills/strokes/backgrounds)

- 공식 문서: `https://www.figma.com/plugin-docs/api/Paint/`

```ts
// plugin-api.d.ts
type Paint = SolidPaint | GradientPaint | ImagePaint | VideoPaint | PatternPaint
```

### Typings 주석 발췌

```ts
// plugin-api.d.ts (발췌)
// SolidPaint.color does not have alpha; use opacity instead.
// ImagePaint.scaleMode controls which fields are applicable.
```

### SolidPaint

```ts
interface SolidPaint {
	readonly type: "SOLID"
	readonly color: RGB
	readonly visible?: boolean
	readonly opacity?: number
	readonly blendMode?: BlendMode
	readonly boundVariables?: { [field in VariableBindablePaintField]?: VariableAlias }
}
```

### GradientPaint

```ts
interface GradientPaint {
	readonly type: "GRADIENT_LINEAR" | "GRADIENT_RADIAL" | "GRADIENT_ANGULAR" | "GRADIENT_DIAMOND"
	readonly gradientTransform: Transform
	readonly gradientStops: ReadonlyArray<ColorStop>
	readonly visible?: boolean
	readonly opacity?: number
	readonly blendMode?: BlendMode
}
```

### ImagePaint

```ts
interface ImagePaint {
	readonly type: "IMAGE"
	readonly scaleMode: "FILL" | "FIT" | "CROP" | "TILE"
	readonly imageHash: string | null
	readonly imageTransform?: Transform
	readonly scalingFactor?: number
	readonly rotation?: number
	readonly filters?: ImageFilters
	readonly visible?: boolean
	readonly opacity?: number
	readonly blendMode?: BlendMode
}
```

### VideoPaint

```ts
interface VideoPaint {
	readonly type: "VIDEO"
	readonly scaleMode: "FILL" | "FIT" | "CROP" | "TILE"
	readonly videoHash: string | null
	readonly videoTransform?: Transform
	readonly scalingFactor?: number
	readonly rotation?: number
	readonly filters?: ImageFilters
	readonly visible?: boolean
	readonly opacity?: number
	readonly blendMode?: BlendMode
}
```

### PatternPaint

```ts
interface PatternPaint {
	readonly type: "PATTERN"
	readonly sourceNodeId: string
	readonly tileType: "RECTANGULAR" | "HORIZONTAL_HEXAGONAL" | "VERTICAL_HEXAGONAL"
	readonly scalingFactor: number
	readonly spacing: Vector
	readonly horizontalAlignment: "START" | "CENTER" | "END"
	readonly visible?: boolean
	readonly opacity?: number
	readonly blendMode?: BlendMode
}
```

**사용 위치**

- `Paint` → `MinimalFillsMixin.fills`, `MinimalStrokesMixin.strokes`, `PaintStyle.paints`
- `ImagePaint/VideoPaint`는 `scaleMode`에 따라 `imageTransform`/`scalingFactor`가 함께 사용됨

## mixed 반환 여부

- `Paint` 타입 자체는 mixed가 없음
- mixed는 **노드의 `fills`/`fillStyleId`**에서 발생 (`MinimalFillsMixin`), 특히 텍스트에서 범위별 색상이 다르면 mixed 반환

## Style (BaseStyle / PaintStyle / TextStyle / EffectStyle / GridStyle)

- 공식 문서: `https://www.figma.com/plugin-docs/api/Style/`
- 공식 문서: `https://www.figma.com/plugin-docs/api/TextStyle/`
- 공식 문서: `https://www.figma.com/plugin-docs/api/PaintStyle/`
- 공식 문서: `https://www.figma.com/plugin-docs/api/EffectStyle/`
- 공식 문서: `https://www.figma.com/plugin-docs/api/GridStyle/`

```ts
// plugin-api.d.ts (발췌)
type StyleType = "PAINT" | "TEXT" | "EFFECT" | "GRID"

type BaseStyle = PaintStyle | TextStyle | EffectStyle | GridStyle
```

```ts
interface PaintStyle extends BaseStyleMixin {
	type: "PAINT"
	paints: ReadonlyArray<Paint>
	readonly boundVariables?: {
		readonly [field in VariableBindablePaintStyleField]?: VariableAlias[]
	}
}
```

```ts
interface TextStyle extends BaseStyleMixin {
	type: "TEXT"
	fontSize: number
	textDecoration: TextDecoration
	fontName: FontName
	letterSpacing: LetterSpacing
	lineHeight: LineHeight
	leadingTrim: LeadingTrim
	paragraphIndent: number
	paragraphSpacing: number
	listSpacing: number
	hangingPunctuation: boolean
	hangingList: boolean
	textCase: TextCase
	boundVariables?: { [field in VariableBindableTextField]?: VariableAlias }
}
```

```ts
interface EffectStyle extends BaseStyleMixin {
	type: "EFFECT"
	effects: ReadonlyArray<Effect>
	readonly boundVariables?: {
		readonly [field in VariableBindableEffectStyleField]?: VariableAlias[]
	}
}
```

```ts
interface GridStyle extends BaseStyleMixin {
	type: "GRID"
	layoutGrids: ReadonlyArray<LayoutGrid>
	readonly boundVariables?: {
		readonly [field in VariableBindableGridStyleField]?: VariableAlias[]
	}
}
```

**실무 포인트**

- 스타일은 노드의 styleId와 매칭됨 (`setFillStyleIdAsync` 등)
- `boundVariables`는 스타일 단위로 바인딩된 변수 목록

---

다음 문서: `effects.md`
