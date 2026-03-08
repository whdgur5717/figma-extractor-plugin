# Vector Data

## Vector

- **데이터 개념**: 2D 좌표/오프셋 단위.
- **공식 설명 요약**: `x`, `y`로 구성.
- **typings 구조**: `interface Vector { x; y }`
- **예제 데이터**

```json
{ "x": 12, "y": -4 }
```

## VectorPath

- **데이터 개념**: SVG path 문자열 기반 경로.
- **공식 설명 요약**: `windingRule`과 `data`로 구성.
- **typings 구조**: `interface VectorPath { windingRule: WindingRule | 'NONE'; data: string }`
- **예제 데이터 (유니온 전체)**

```json
{ "windingRule": "NONZERO", "data": "M 0 100 L 100 100 L 50 0 Z" }
```

```json
{ "windingRule": "EVENODD", "data": "M 0 0 L 100 0 L 100 100 L 0 100 Z" }
```

```json
{ "windingRule": "NONE", "data": "M 0 0 L 100 0" }
```

## VectorNetwork

- **데이터 개념**: 그래프 기반 벡터 구조(Vertices/Segments/Regions).
- **공식 설명 요약**: `vertices`, `segments`, `regions`로 구성.
- **typings 구조**: `interface VectorNetwork`.
- **예제 데이터**

```json
{
	"vertices": [
		{ "x": 0, "y": 100 },
		{ "x": 100, "y": 100 },
		{ "x": 50, "y": 0 }
	],
	"segments": [
		{ "start": 0, "end": 1 },
		{ "start": 1, "end": 2 },
		{ "start": 2, "end": 0 }
	],
	"regions": [{ "windingRule": "NONZERO", "loops": [[0, 1, 2]] }]
}
```

## HandleMirroring

- **데이터 개념**: 벡터 핸들의 대칭 동작.
- **공식 설명 요약**: NONE/ANGLE/ANGLE_AND_LENGTH.
- **typings 구조**: `type HandleMirroring = 'NONE' | 'ANGLE' | 'ANGLE_AND_LENGTH'`
- **예제 데이터**

```json
{ "handleMirroring": "ANGLE" }
```

## 문서 링크

- https://developers.figma.com/docs/plugins/api/Vector/
- https://developers.figma.com/docs/plugins/api/VectorPath/
- https://developers.figma.com/docs/plugins/api/VectorNetwork/
- https://developers.figma.com/docs/plugins/api/HandleMirroring/
