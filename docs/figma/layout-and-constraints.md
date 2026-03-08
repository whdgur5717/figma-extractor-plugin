# Layout & Constraints

## Constraints

- 공식 문서: `https://www.figma.com/plugin-docs/api/Constraint/`

```ts
// plugin-api.d.ts
type ConstraintType = "MIN" | "CENTER" | "MAX" | "STRETCH" | "SCALE"
interface Constraints {
	readonly horizontal: ConstraintType
	readonly vertical: ConstraintType
}
```

## LayoutGrid

- 공식 문서: `https://www.figma.com/plugin-docs/api/LayoutGrid/`

```ts
interface RowsColsLayoutGrid {
	readonly pattern: "ROWS" | "COLUMNS"
	readonly alignment: "MIN" | "MAX" | "STRETCH" | "CENTER"
	readonly gutterSize: number
	readonly count: number
	readonly sectionSize?: number
	readonly offset?: number
	readonly visible?: boolean
	readonly color?: RGBA
	readonly boundVariables?: { [field in VariableBindableLayoutGridField]?: VariableAlias }
}

interface GridLayoutGrid {
	readonly pattern: "GRID"
	readonly sectionSize: number
	readonly visible?: boolean
	readonly color?: RGBA
	readonly boundVariables?: { ["sectionSize"]?: VariableAlias }
}

type LayoutGrid = RowsColsLayoutGrid | GridLayoutGrid
```

### Typings 주석 발췌

```ts
// plugin-api.d.ts (발췌)
// count can be set to Infinity (UI: Auto)
// sectionSize is ignored when alignment == 'STRETCH'
```

**사용 위치**

- `ConstraintMixin.constraints`
- `BaseFrameMixin.layoutGrids`
- `GridStyle.layoutGrids`

## Auto Layout 데이터

- 공식 문서: `https://www.figma.com/plugin-docs/api/AutoLayoutMixin/`
- 관련 속성 문서: `https://developers.figma.com/docs/plugins/api/properties/nodes-layoutmode/`

**핵심 요점**

- `layoutMode`가 `'HORIZONTAL' | 'VERTICAL'`일 때만 오토레이아웃 속성 유효
- `primaryAxisSizingMode`, `counterAxisSizingMode`, `itemSpacing`, `padding*`, `layoutWrap` 등은 AutoLayoutMixin에 속함

**실무 포인트**

- Auto layout 속성은 **Mixin 조건부**이므로 노드 타입만 보고 접근하지 말 것
- `layoutWrap`이 `'WRAP'`일 때만 `counterAxisSpacing`/`counterAxisAlignContent`가 의미 있음

---

다음 문서: `text.md`
