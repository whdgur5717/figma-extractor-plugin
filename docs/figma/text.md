# Text Data

## FontName / TextCase / TextDecoration

- 공식 문서: `https://www.figma.com/plugin-docs/api/FontName/`

```ts
// plugin-api.d.ts
interface FontName {
	readonly family: string
	readonly style: string
}

type TextCase = "ORIGINAL" | "UPPER" | "LOWER" | "TITLE" | "SMALL_CAPS" | "SMALL_CAPS_FORCED"

type TextDecoration = "NONE" | "UNDERLINE" | "STRIKETHROUGH"
```

## LetterSpacing / LineHeight

- 공식 문서: `https://www.figma.com/plugin-docs/api/LetterSpacing/`
- 공식 문서: `https://www.figma.com/plugin-docs/api/LineHeight/`

```ts
// plugin-api.d.ts (발췌)
interface LetterSpacing {
	readonly value: number
	readonly unit: "PIXELS" | "PERCENT"
}

type LineHeight = { readonly value: number; readonly unit: "PIXELS" | "PERCENT" } | { readonly unit: "AUTO" }
```

## StyledTextSegment

- 공식 문서: `https://www.figma.com/plugin-docs/api/StyledTextSegment/`

```ts
// plugin-api.d.ts (발췌)
interface StyledTextSegment {
	characters: string
	start: number
	end: number
	fontName: FontName
	fontSize: number
	textDecoration: TextDecoration
	textCase: TextCase
	lineHeight: LineHeight
	letterSpacing: LetterSpacing
	fills: Paint[] | PluginAPI["mixed"]
	textStyleId: string
	listOptions: TextListOptions
}
```

## TextNode mixed 처리

- 공식 문서: `https://developers.figma.com/docs/plugins/working-with-text/`
- `figma.mixed`: `https://developers.figma.com/docs/plugins/api/properties/figma-mixed/`

**요점**

- 텍스트 속성은 `PluginAPI['mixed']`를 반환할 수 있음
- mixed일 때는 `getRange*` 또는 `getStyledTextSegments`로 범위 단위 접근

```ts
// plugin-api.d.ts (발췌)
interface BaseNonResizableTextMixin {
	fontName: FontName | PluginAPI["mixed"]
	textCase: TextCase | PluginAPI["mixed"]
	letterSpacing: LetterSpacing | PluginAPI["mixed"]
	getRangeFontName(start: number, end: number): FontName | PluginAPI["mixed"]
	setRangeFontName(start: number, end: number, value: FontName): void
}
```

### mixed 속성별 접근 방법 (텍스트)

**BaseNonResizableTextMixin / NonResizableTextMixin**

- `fontSize` → `getRangeFontSize`
- `fontName` → `getRangeFontName`
- `fontWeight` → `getRangeFontWeight`
- `textCase` → `getRangeTextCase`
- `letterSpacing` → `getRangeLetterSpacing`
- `openTypeFeatures` → `getRangeOpenTypeFeatures`
- `hyperlink` → `getRangeHyperlink`
- `fills` → `getRangeFills`
- `fillStyleId` → `getRangeFillStyleId`
- `textStyleId` → `getRangeTextStyleId`
- `boundVariables` → `getRangeBoundVariable`
- `textDecoration` → `getRangeTextDecoration`
- `textDecorationStyle` → `getRangeTextDecorationStyle`
- `textDecorationOffset` → `getRangeTextDecorationOffset`
- `textDecorationThickness` → `getRangeTextDecorationThickness`
- `textDecorationColor` → `getRangeTextDecorationColor`
- `textDecorationSkipInk` → `getRangeTextDecorationSkipInk`
- `lineHeight` → `getRangeLineHeight`
- `listOptions` → `getRangeListOptions`
- `listSpacing` → `getRangeListSpacing`
- `indentation` → `getRangeIndentation`
- `paragraphIndent` → `getRangeParagraphIndent`
- `paragraphSpacing` → `getRangeParagraphSpacing`
- `leadingTrim` → mixed 가능. 대응하는 range getter 없음 → mixed 분기 처리

**TextNode / TextPathNode**

- `textStyleId` (노드 속성) → mixed 가능. `getRangeTextStyleId`/`getStyledTextSegments`로 확인

**범위 일괄 접근**

- 여러 필드를 한 번에 읽으려면 `getStyledTextSegments` 사용

### Typings 주석 발췌

```ts
// plugin-api.d.ts (발췌)
// Text properties can return figma.mixed when ranges differ.
```

---

다음 문서: `data-variables.md`
