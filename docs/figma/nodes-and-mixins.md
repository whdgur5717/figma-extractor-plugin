# Nodes & Mixins

이 문서는 **SceneNode 트리 구조**와 **Mixin 기반 데이터 모델**을 정리합니다.

## 노드 타입 (SceneNode)

- 공식 문서: `https://www.figma.com/plugin-docs/api/nodes/`
- 공식 문서: `https://developers.figma.com/docs/plugins/api/node-types`

```ts
// plugin-api.d.ts
type SceneNode =
	| SliceNode
	| FrameNode
	| GroupNode
	| ComponentSetNode
	| ComponentNode
	| InstanceNode
	| BooleanOperationNode
	| VectorNode
	| StarNode
	| LineNode
	| EllipseNode
	| PolygonNode
	| RectangleNode
	| TextNode
	| TextPathNode
	| TransformGroupNode
	| StickyNode
	| ConnectorNode
	| ShapeWithTextNode
	| CodeBlockNode
	| StampNode
	| WidgetNode
	| EmbedNode
	| LinkUnfurlNode
	| MediaNode
	| SectionNode
	| HighlightNode
	| WashiTapeNode
	| TableNode
	| SlideNode
	| SlideRowNode
	| SlideGridNode
	| InteractiveSlideElementNode
```

**요점**

- `SceneNode`는 문서에서 조작 가능한 모든 레이어 타입의 합집합입니다.
- 실제 속성은 노드가 포함하는 Mixin 조합으로 결정됩니다.

## BaseNode / NodeType

- 공식 문서: `https://www.figma.com/plugin-docs/api/node-types/`

```ts
// plugin-api.d.ts
type BaseNode = DocumentNode | PageNode | SceneNode
type NodeType = BaseNode["type"]
```

## BaseNodeMixin (핵심 공통 데이터)

- 공식 문서: `https://www.figma.com/plugin-docs/api/BaseNodeMixin/`

```ts
// plugin-api.d.ts (발췌)
interface BaseNodeMixin extends PluginDataMixin, DevResourcesMixin {
	readonly id: string
	readonly parent: (BaseNode & ChildrenMixin) | null
	name: string
	readonly removed: boolean
	toString(): string
	remove(): void
	setRelaunchData(data: { [command: string]: string }): void
	getRelaunchData(): { [command: string]: string }
	readonly isAsset: boolean
	getCSSAsync(): Promise<{ [key: string]: string }>
	getTopLevelFrame(): FrameNode | undefined
}
```

### Typings 주석 발췌

```ts
// plugin-api.d.ts (발췌)
// The node id can be used with methods such as figma.getNodeByIdAsync.
// In URLs the node id uses hyphens; for API you must use colons.
// ...
// Sets state on the node to show a button and description when the node is selected.
```

**실무 포인트**

- `id`는 직렬화/역직렬화에 사용 (URL에서 `-` → `:` 변환 필요)
- `removed`는 장시간 실행 플러그인에서 필수 방어 체크

## 주요 Mixin 카테고리 (데이터 관점)

### 기본/트리

- `ChildrenMixin`, `ContainerMixin`, `SceneNodeMixin`

### 시각/스타일

- `BlendMixin`, `OpacityMixin`, `MinimalBlendMixin`, `MinimalFillsMixin`, `MinimalStrokesMixin`, `StrokeMixin`, `GeometryMixin`

### 레이아웃

- `LayoutMixin`, `AutoLayoutMixin`, `AutoLayoutChildrenMixin`, `GridLayoutMixin`, `GridChildrenMixin`, `ConstraintMixin`, `DimensionAndPositionMixin`

### 텍스트

- `BaseNonResizableTextMixin`, `NonResizableTextMixin`, `TextMixin`

### 기타

- `ExportMixin`, `DevResourcesMixin`, `AnnotationsMixin`, `AspectRatioLockMixin`

**요점**

- 데이터 구조는 **노드 타입이 아니라 믹스인 합성**에 의해 결정됩니다.
- 특정 속성은 mixin을 만족하는 노드에서만 존재합니다.

## mixed 반환 속성 (노드/믹스인)

```ts
// plugin-api.d.ts (발췌)
interface MinimalStrokesMixin {
	strokeWeight: number | PluginAPI["mixed"]
	strokeJoin: StrokeJoin | PluginAPI["mixed"]
}
interface GeometryMixin {
	strokeCap: StrokeCap | PluginAPI["mixed"]
}
interface MinimalFillsMixin {
	fills: ReadonlyArray<Paint> | PluginAPI["mixed"]
	fillStyleId: string | PluginAPI["mixed"]
}
interface CornerMixin {
	cornerRadius: number | PluginAPI["mixed"]
}
interface VectorLikeMixin {
	handleMirroring: HandleMirroring | PluginAPI["mixed"]
}
interface LabelSublayerNode {
	fills: Paint[] | PluginAPI["mixed"]
}
```

### 속성별 mixed 접근 방법

- `strokeWeight` → `IndividualStrokesMixin`의 `strokeTopWeight`/`strokeRightWeight`/`strokeBottomWeight`/`strokeLeftWeight` 사용.
- `strokeJoin` → 정점별 값 혼재 가능. 벡터 네트워크(`vectorNetwork`) 기반 데이터로 처리하거나 mixed 분기.
- `strokeCap` → 정점별 값 혼재 가능. 벡터 네트워크(`vectorNetwork`) 기반 데이터로 처리하거나 mixed 분기.
- `fills` (MinimalFillsMixin) → 텍스트 범위별 fills가 섞인 경우 mixed. 텍스트인 경우 `getRangeFills`/`getStyledTextSegments` 사용, 그 외는 mixed 분기.
- `fillStyleId` (MinimalFillsMixin) → 텍스트 범위별 스타일이 섞인 경우 mixed. 텍스트인 경우 `getRangeFillStyleId`/`getStyledTextSegments` 사용, 그 외는 mixed 분기.
- `cornerRadius` → `RectangleCornerMixin`의 `topLeftRadius`/`topRightRadius`/`bottomLeftRadius`/`bottomRightRadius` 사용. (벡터 노드는 정점별 값 혼재 가능)
- `handleMirroring` → 벡터 네트워크(`vectorNetwork`)에서 정점별 값 혼재 가능. 필요 시 네트워크 데이터로 처리하거나 mixed 분기.
- `LabelSublayerNode.fills` → range API 없음. mixed 여부만 판별 후 분기 처리.

## DocumentNode / PageNode

- 공식 문서: `https://www.figma.com/plugin-docs/api/DocumentNode/`
- 공식 문서: `https://www.figma.com/plugin-docs/api/PageNode/`

**요점**

- `DocumentNode`는 루트 (`figma.root`), `PageNode`는 캔버스 페이지
- 데이터 트리의 최상위 구조

---

다음 문서: `styles-and-paints.md`
