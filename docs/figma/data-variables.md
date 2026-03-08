# Variables (Design Tokens)

- 공식 문서: `https://www.figma.com/plugin-docs/api/Variable/`
- 공식 문서: `https://www.figma.com/plugin-docs/api/VariableCollection/`
- 공식 문서: `https://www.figma.com/plugin-docs/api/VariableAlias/`

```ts
// plugin-api.d.ts
interface VariableAlias {
	type: "VARIABLE_ALIAS"
	id: string
}

type VariableResolvedDataType = "BOOLEAN" | "COLOR" | "FLOAT" | "STRING"

type VariableValue = boolean | string | number | RGB | RGBA | VariableAlias

type VariableScope =
	| "ALL_SCOPES"
	| "TEXT_CONTENT"
	| "CORNER_RADIUS"
	| "WIDTH_HEIGHT"
	| "GAP"
	| "ALL_FILLS"
	| "FRAME_FILL"
	| "SHAPE_FILL"
	| "TEXT_FILL"
	| "STROKE_COLOR"
	| "STROKE_FLOAT"
	| "EFFECT_FLOAT"
	| "EFFECT_COLOR"
	| "OPACITY"
	| "FONT_FAMILY"
	| "FONT_STYLE"
	| "FONT_WEIGHT"
	| "FONT_SIZE"
	| "LINE_HEIGHT"
	| "LETTER_SPACING"
	| "PARAGRAPH_SPACING"
	| "PARAGRAPH_INDENT"
```

```ts
// plugin-api.d.ts (발췌)
interface Variable extends PluginDataMixin {
	readonly id: string
	name: string
	description: string
	hiddenFromPublishing: boolean
	getPublishStatusAsync(): Promise<PublishStatus>
	readonly remote: boolean
	readonly variableCollectionId: string
	readonly key: string
	readonly resolvedType: VariableResolvedDataType
	resolveForConsumer(consumer: SceneNode): { value: VariableValue; resolvedType: VariableResolvedDataType }
}
```

### Typings 주석 발췌

```ts
// plugin-api.d.ts (발췌)
// Resolved value depends on consumer node variable modes.
```

**사용 위치**

- `VariableValue` 안에 `VariableAlias` 포함
- `resolveForConsumer`는 `SceneNode`를 소비자로 받음

## VariableCollection (요약)

- 공식 문서: `https://www.figma.com/plugin-docs/api/VariableCollection/`

**요점**

- 컬렉션은 다중 모드(mode)를 가지며 변수는 모드별 값 보유

---

다음 문서: `data-assets-export.md`
