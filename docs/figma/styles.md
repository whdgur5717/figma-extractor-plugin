# Styles

## PaintStyle

- **데이터 개념**: 페인트 목록을 재사용 가능한 스타일로 저장.
- **공식 설명 요약**: `type: 'PAINT'`와 `paints` 포함.
- **typings 구조**: `interface PaintStyle extends BaseStyleMixin`.
- **예제 데이터**

```json
{ "type": "PAINT", "paints": [{ "type": "SOLID", "color": { "r": 1, "g": 0, "b": 0 } }] }
```

## TextStyle

- **데이터 개념**: 텍스트 스타일 집합.
- **공식 설명 요약**: `type: 'TEXT'`와 텍스트 관련 속성 포함.
- **typings 구조**: `interface TextStyle extends BaseStyleMixin`.
- **예제 데이터**

```json
{
	"type": "TEXT",
	"fontSize": 16,
	"fontName": { "family": "Inter", "style": "Regular" },
	"textDecoration": "NONE",
	"letterSpacing": { "value": 0, "unit": "PIXELS" },
	"lineHeight": { "unit": "AUTO" },
	"leadingTrim": "NONE",
	"paragraphIndent": 0,
	"paragraphSpacing": 0,
	"listSpacing": 0,
	"hangingPunctuation": false,
	"hangingList": false,
	"textCase": "ORIGINAL"
}
```

## EffectStyle

- **데이터 개념**: 효과 목록을 재사용 가능한 스타일로 저장.
- **공식 설명 요약**: `type: 'EFFECT'`와 `effects` 포함.
- **typings 구조**: `interface EffectStyle extends BaseStyleMixin`.
- **예제 데이터**

```json
{
	"type": "EFFECT",
	"effects": [
		{
			"type": "DROP_SHADOW",
			"color": { "r": 0, "g": 0, "b": 0, "a": 0.25 },
			"offset": { "x": 0, "y": 4 },
			"radius": 8,
			"visible": true,
			"blendMode": "NORMAL"
		}
	]
}
```

## GridStyle

- **데이터 개념**: 레이아웃 그리드를 재사용 가능한 스타일로 저장.
- **공식 설명 요약**: `type: 'GRID'`와 `layoutGrids` 포함.
- **typings 구조**: `interface GridStyle extends BaseStyleMixin`.
- **예제 데이터**

```json
{
	"type": "GRID",
	"layoutGrids": [{ "pattern": "COLUMNS", "alignment": "MIN", "gutterSize": 16, "count": 12, "sectionSize": 48 }]
}
```

## 문서 링크

- https://developers.figma.com/docs/plugins/api/PaintStyle/
- https://developers.figma.com/docs/plugins/api/TextStyle/
- https://developers.figma.com/docs/plugins/api/EffectStyle/
- https://developers.figma.com/docs/plugins/api/GridStyle/
