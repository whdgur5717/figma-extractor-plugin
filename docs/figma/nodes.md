# Nodes (Scene Graph)

## Node Types (overview)

- **데이터 개념**: Figma 문서의 모든 레이어는 Node이며, Node는 `type`으로 구분된다.
- **공식 설명 요약**: 노드 타입 목록과 타입별 상세는 Node Types 인덱스에 정리되어 있다.
- **typings 구조**: `BaseNode = DocumentNode | PageNode | SceneNode`, `NodeType` 리터럴 유니온.
- **예제 데이터**

```json
{ "type": "FRAME" }
```

## 문서 링크

- https://developers.figma.com/docs/plugins/api/nodes/
