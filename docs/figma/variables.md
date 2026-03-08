# Variables & Tokens

## Variable

- **데이터 개념**: 모드별 값을 가진 단일 디자인 토큰.
- **공식 설명 요약**: `VariableCollection`에 속하며 `valuesByMode`, `resolvedType`를 가진다.
- **typings 구조**: `interface Variable`.
- **예제 데이터**

```json
{
	"id": "VariableID:1:7",
	"name": "color-primary",
	"description": "Primary color",
	"remote": false,
	"variableCollectionId": "VariableCollectionId:1:3",
	"key": "key123",
	"resolvedType": "COLOR",
	"valuesByMode": {
		"VariableCollectionId:1:3/0:1": { "r": 1, "g": 0, "b": 0, "a": 1 }
	}
}
```

## VariableCollection

- **데이터 개념**: 동일 모드 집합을 공유하는 변수 묶음.
- **공식 설명 요약**: `modes`, `variableIds`, `defaultModeId` 제공.
- **typings 구조**: `interface VariableCollection`.
- **예제 데이터**

```json
{
	"id": "VariableCollectionId:1:3",
	"name": "Semantic Colors",
	"remote": false,
	"isExtension": false,
	"modes": [{ "modeId": "VariableCollectionId:1:3/0:1", "name": "Light" }],
	"variableIds": ["VariableID:1:7"],
	"defaultModeId": "VariableCollectionId:1:3/0:1",
	"key": "collectionKey"
}
```

## VariableAlias

- **데이터 개념**: 변수 바인딩을 위한 참조.
- **공식 설명 요약**: `{ type: 'VARIABLE_ALIAS', id }` 구조.
- **typings 구조**: `type VariableAlias`.
- **예제 데이터**

```json
{ "type": "VARIABLE_ALIAS", "id": "VariableID:1:7" }
```

## VariableResolvedDataType

- **데이터 개념**: 변수가 최종적으로 해석되는 값의 타입.
- **공식 설명 요약**: `BOOLEAN | COLOR | FLOAT | STRING`.
- **typings 구조**: `type VariableResolvedDataType = ...`
- **예제 데이터**

```json
{ "resolvedType": "COLOR" }
```

## VariableValue

- **데이터 개념**: 변수의 실제 값 유니온.
- **공식 설명 요약**: `string | number | boolean | RGB | RGBA | VariableAlias`.
- **typings 구조**: `type VariableValue = ...`
- **예제 데이터 (유니온 전체)**

```json
{ "value": "primary" }
```

```json
{ "value": 12 }
```

```json
{ "value": true }
```

```json
{ "value": { "r": 1, "g": 0.2, "b": 0 } }
```

```json
{ "value": { "r": 1, "g": 0.2, "b": 0, "a": 0.8 } }
```

```json
{ "value": { "type": "VARIABLE_ALIAS", "id": "VariableID:1:7" } }
```

## VariableScope

- **데이터 개념**: 변수 선택기에서 노출되는 범위.
- **공식 설명 요약**: 다양한 스코프 문자열 유니온.
- **typings 구조**: `type VariableScope = ...`
- **예제 데이터**

```json
{ "scopes": ["ALL_FILLS", "TEXT_FILL"] }
```

## Bindable Fields

- **데이터 개념**: 변수 바인딩 가능한 필드 집합.
- **공식 설명 요약**: Node/Text/Paint/Effect/LayoutGrid/Style/ColorStop별 필드 정의.
- **typings 구조**:
  - `VariableBindableNodeField`
  - `VariableBindableTextField`
  - `VariableBindablePaintField = 'color'`
  - `VariableBindableEffectField`
  - `VariableBindableLayoutGridField`
  - `VariableBindablePaintStyleField = 'color'`
  - `VariableBindableEffectStyleField = 'effects'`
  - `VariableBindableGridStyleField = 'layoutGrids'`
  - `VariableBindableColorStopField = 'color'`
- **예제 데이터**

```json
{ "nodeField": "opacity", "textField": "fontSize", "paintField": "color" }
```

```json
{ "effectField": "radius", "layoutGridField": "gutterSize" }
```

```json
{ "paintStyleField": "color", "effectStyleField": "effects", "gridStyleField": "layoutGrids" }
```

```json
{ "colorStopField": "color" }
```

## 문서 링크

- https://developers.figma.com/docs/plugins/api/Variable/
- https://developers.figma.com/docs/plugins/api/VariableCollection/
- https://developers.figma.com/docs/plugins/api/VariableAlias/
- https://developers.figma.com/docs/plugins/api/VariableResolvedDataType/
- https://developers.figma.com/docs/plugins/api/VariableScope/
- https://developers.figma.com/docs/plugins/api/VariableValue/
- https://developers.figma.com/docs/plugins/api/VariableBindableNodeField/
- https://developers.figma.com/docs/plugins/api/VariableBindableTextField/
- https://developers.figma.com/docs/plugins/api/VariableBindablePaintField/
- https://developers.figma.com/docs/plugins/api/VariableBindableEffectField/
- https://developers.figma.com/docs/plugins/api/VariableBindableLayoutGridField/
- https://developers.figma.com/docs/plugins/api/VariableBindablePaintStyleField/
- https://developers.figma.com/docs/plugins/api/VariableBindableEffectStyleField/
- https://developers.figma.com/docs/plugins/api/VariableBindableGridStyleField/
- https://developers.figma.com/docs/plugins/api/VariableBindableColorStopField/
