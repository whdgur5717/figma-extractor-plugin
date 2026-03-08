# Shared Node Properties (Mixins)

## Mixins 개요

- **데이터 개념**: 여러 노드가 공통으로 가지는 속성과 메서드를 Mixins로 정의한다.
- **공식 설명 요약**: 각 속성별 지원 노드 목록과 설명이 Node Properties 인덱스에 정리되어 있다.
- **typings 구조**: `ChildrenMixin`, `LayoutMixin`, `GeometryMixin`, `MinimalFillsMixin`, `MinimalStrokesMixin`, `MinimalBlendMixin`, `ConstraintMixin`, `AutoLayoutMixin`, `TextMixin` 등.
- **예제 데이터**

```json
{ "absoluteBoundingBox": { "x": 0, "y": 0, "width": 100, "height": 80 } }
```

## Mixed 값 (PluginAPI['mixed'])

- **데이터 개념**: 동일 노드 내에서 범위/세그먼트별 값이 다르면 `figma.mixed`가 반환된다.
- **typings 구조 예시**:
  - `fills: ReadonlyArray<Paint> | PluginAPI['mixed']`
  - `fillStyleId: string | PluginAPI['mixed']`
  - `strokes: ReadonlyArray<Paint> | PluginAPI['mixed']`
  - `strokeWeight: number | PluginAPI['mixed']`
  - `strokeCap: StrokeCap | PluginAPI['mixed']`
  - `strokeJoin: StrokeJoin | PluginAPI['mixed']`
  - `cornerRadius: number | PluginAPI['mixed']`
  - `handleMirroring: HandleMirroring | PluginAPI['mixed']`
  - `fontSize: number | PluginAPI['mixed']`
  - `fontName: FontName | PluginAPI['mixed']`
  - `fontWeight: number | PluginAPI['mixed']`
  - `textCase: TextCase | PluginAPI['mixed']`
  - `letterSpacing: LetterSpacing | PluginAPI['mixed']`
  - `lineHeight: LineHeight | PluginAPI['mixed']`
  - `textDecoration*`: `TextDecoration* | PluginAPI['mixed'] | null`
- **예제 데이터 (mixed)**

```json
{ "fills": "figma.mixed" }
```

```json
{ "strokeWeight": "figma.mixed", "strokeCap": "figma.mixed" }
```

```json
{ "fontSize": "figma.mixed", "textDecoration": "figma.mixed" }
```

## 문서 링크

- https://developers.figma.com/docs/plugins/api/node-properties/
