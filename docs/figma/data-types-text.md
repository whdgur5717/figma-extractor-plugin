# Data Types — Text

## StyledTextSegment

- **데이터 개념**: 동일 스타일 범위의 텍스트 세그먼트.
- **공식 설명 요약**: 범위(start/end)와 해당 스타일 속성을 포함.
- **typings 구조**: `StyledTextSegment` 인터페이스.
- **예제 데이터**

```json
{
	"characters": "Hello",
	"start": 0,
	"end": 5,
	"fontSize": 16,
	"fontName": { "family": "Inter", "style": "Regular" },
	"fontWeight": 400,
	"fontStyle": "REGULAR",
	"textDecoration": "UNDERLINE",
	"textDecorationStyle": "SOLID",
	"textDecorationOffset": { "value": 2, "unit": "PIXELS" },
	"textDecorationThickness": { "value": 1, "unit": "PIXELS" },
	"textDecorationColor": { "value": { "type": "SOLID", "color": { "r": 0, "g": 0, "b": 0 } } },
	"textDecorationSkipInk": true,
	"textCase": "ORIGINAL",
	"lineHeight": { "unit": "AUTO" },
	"letterSpacing": { "value": 0, "unit": "PIXELS" },
	"fills": [{ "type": "SOLID", "color": { "r": 0, "g": 0, "b": 0 } }],
	"textStyleId": "S:1",
	"fillStyleId": "S:2",
	"listOptions": { "type": "NONE" },
	"listSpacing": 0,
	"indentation": 0,
	"paragraphIndent": 0,
	"paragraphSpacing": 0,
	"hyperlink": { "type": "URL", "value": "https://figma.com" },
	"openTypeFeatures": { "LIGA": true, "KERN": false },
	"textStyleOverrides": []
}
```

## FontName / FontStyle

- **데이터 개념**: 폰트 패밀리/스타일 조합과 기울임 여부.
- **공식 설명 요약**: `FontName`은 `{ family, style }`, `FontStyle`은 `REGULAR | ITALIC`.
- **typings 구조**: `interface FontName`, `type FontStyle`.
- **예제 데이터**

```json
{ "fontName": { "family": "Inter", "style": "Bold" }, "fontStyle": "ITALIC" }
```

## TextCase

- **데이터 개념**: 텍스트 케이스 변환 방식.
- **공식 설명 요약**: ORIGINAL/UPPER/LOWER/TITLE/SMALL_CAPS/SMALL_CAPS_FORCED.
- **typings 구조**: `type TextCase = ...`
- **예제 데이터**

```json
{ "textCase": "TITLE" }
```

## LetterSpacing

- **데이터 개념**: 글자 간격.
- **공식 설명 요약**: `{ value, unit: PIXELS | PERCENT }`.
- **typings 구조**: `interface LetterSpacing`.
- **예제 데이터**

```json
{ "letterSpacing": { "value": 2, "unit": "PIXELS" } }
```

## LineHeight

- **데이터 개념**: 줄 간격.
- **공식 설명 요약**: `{ value, unit }` 또는 `{ unit: AUTO }`.
- **typings 구조**: `type LineHeight`.
- **예제 데이터 (유니온 전체)**

```json
{ "lineHeight": { "value": 20, "unit": "PIXELS" } }
```

```json
{ "lineHeight": { "unit": "AUTO" } }
```

## LeadingTrim

- **데이터 개념**: 텍스트 glyph 상하 여백 제거 방식.
- **공식 설명 요약**: `CAP_HEIGHT | NONE`.
- **typings 구조**: `type LeadingTrim`.
- **예제 데이터**

```json
{ "leadingTrim": "CAP_HEIGHT" }
```

## TextDecoration (및 하위 타입)

- **데이터 개념**: 텍스트 장식(밑줄/취소선) 및 스타일/두께/색.
- **공식 설명 요약**: `TextDecoration`과 `TextDecorationStyle`, `TextDecorationOffset`, `TextDecorationThickness`, `TextDecorationColor`로 구성.
- **typings 구조**:
  - `TextDecoration = 'NONE' | 'UNDERLINE' | 'STRIKETHROUGH'`
  - `TextDecorationStyle = 'SOLID' | 'WAVY' | 'DOTTED'`
  - `TextDecorationOffset`/`Thickness`: `{ value, unit } | { unit: 'AUTO' }`
  - `TextDecorationColor`: `{ value: SolidPaint } | { value: 'AUTO' }`
- **예제 데이터 (유니온 전체)**

```json
{ "textDecoration": "UNDERLINE", "textDecorationStyle": "WAVY" }
```

```json
{ "textDecorationOffset": { "value": 2, "unit": "PIXELS" } }
```

```json
{ "textDecorationOffset": { "unit": "AUTO" } }
```

```json
{ "textDecorationThickness": { "value": 1, "unit": "PIXELS" } }
```

```json
{ "textDecorationThickness": { "unit": "AUTO" } }
```

```json
{ "textDecorationColor": { "value": { "type": "SOLID", "color": { "r": 0, "g": 0, "b": 0 } } } }
```

```json
{ "textDecorationColor": { "value": "AUTO" } }
```

## TextListOptions

- **데이터 개념**: 텍스트 리스트 타입.
- **공식 설명 요약**: ORDERED/UNORDERED/NONE.
- **typings 구조**: `type TextListOptions = { type: 'ORDERED' | 'UNORDERED' | 'NONE' }`
- **예제 데이터**

```json
{ "listOptions": { "type": "ORDERED" } }
```

## HyperlinkTarget

- **데이터 개념**: 하이퍼링크 대상.
- **공식 설명 요약**: `URL` 또는 `NODE`.
- **typings 구조**: `type HyperlinkTarget = { type: 'URL' | 'NODE'; value: string }`
- **예제 데이터 (유니온 전체)**

```json
{ "hyperlink": { "type": "URL", "value": "https://figma.com" } }
```

```json
{ "hyperlink": { "type": "NODE", "value": "1:23" } }
```

## 문서 링크

- https://developers.figma.com/docs/plugins/api/StyledTextSegment/
- https://developers.figma.com/docs/plugins/api/FontName/
- https://developers.figma.com/docs/plugins/api/FontStyle/
- https://developers.figma.com/docs/plugins/api/TextCase/
- https://developers.figma.com/docs/plugins/api/LetterSpacing/
- https://developers.figma.com/docs/plugins/api/LineHeight/
- https://developers.figma.com/docs/plugins/api/LeadingTrim/
- https://developers.figma.com/docs/plugins/api/TextDecoration/
- https://developers.figma.com/docs/plugins/api/TextDecorationStyle/
- https://developers.figma.com/docs/plugins/api/TextDecorationOffset/
- https://developers.figma.com/docs/plugins/api/TextDecorationThickness/
- https://developers.figma.com/docs/plugins/api/TextDecorationColor/
- https://developers.figma.com/docs/plugins/api/TextListOptions/
- https://developers.figma.com/docs/plugins/api/HyperlinkTarget/
