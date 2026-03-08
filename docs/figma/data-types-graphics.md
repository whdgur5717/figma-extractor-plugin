# Data Types — Graphics (Paint, Effect, Style)

## RGB / RGBA

- **데이터 개념**: 색상 값을 0~1 범위 float로 표현.
- **공식 설명 요약**: RGB는 알파 없이, RGBA는 알파 포함.
- **typings 구조**: `interface RGB { r; g; b }`, `interface RGBA { r; g; b; a }`
- **예제 데이터**

```json
{ "r": 1, "g": 0.5, "b": 0 }
```

```json
{ "r": 0.2, "g": 0.3, "b": 0.4, "a": 0.8 }
```

## Paint

- **데이터 개념**: 채움/테두리를 구성하는 페인트.
- **공식 설명 요약**: Solid/Gradient/Image/Video/Pattern 다섯 타입 유니온.
- **typings 구조**: `type Paint = SolidPaint | GradientPaint | ImagePaint | VideoPaint | PatternPaint`
- **예제 데이터 (유니온 전체)**

```json
{ "type": "SOLID", "color": { "r": 1, "g": 0, "b": 0 }, "opacity": 0.8, "visible": true }
```

```json
{
	"type": "GRADIENT_LINEAR",
	"gradientTransform": [
		[1, 0, 0],
		[0, 1, 0]
	],
	"gradientStops": [
		{ "position": 0, "color": { "r": 1, "g": 0, "b": 0, "a": 1 } },
		{ "position": 1, "color": { "r": 0, "g": 0, "b": 1, "a": 1 } }
	]
}
```

```json
{
	"type": "IMAGE",
	"scaleMode": "CROP",
	"imageHash": "abcd1234",
	"imageTransform": [
		[1, 0, 0],
		[0, 1, 0]
	]
}
```

```json
{
	"type": "VIDEO",
	"scaleMode": "FIT",
	"videoHash": "vid1234",
	"filters": { "exposure": 0.2, "contrast": 0.1 }
}
```

```json
{
	"type": "PATTERN",
	"sourceNodeId": "1:2",
	"tileType": "RECTANGULAR",
	"scalingFactor": 1,
	"spacing": { "x": 8, "y": 8 },
	"horizontalAlignment": "CENTER"
}
```

## Effect

- **데이터 개념**: 그림자/블러/노이즈/텍스처/글래스 등 시각 효과.
- **공식 설명 요약**: DropShadow, InnerShadow, Blur, Noise, Texture, Glass 유니온.
- **typings 구조**: `type Effect = DropShadowEffect | InnerShadowEffect | BlurEffect | NoiseEffect | TextureEffect | GlassEffect`
- **예제 데이터 (유니온 전체)**

```json
{
	"type": "DROP_SHADOW",
	"color": { "r": 0, "g": 0, "b": 0, "a": 0.25 },
	"offset": { "x": 0, "y": 4 },
	"radius": 8,
	"blendMode": "NORMAL",
	"visible": true
}
```

```json
{
	"type": "INNER_SHADOW",
	"color": { "r": 0, "g": 0, "b": 0, "a": 0.2 },
	"offset": { "x": 0, "y": 2 },
	"radius": 4,
	"blendMode": "NORMAL",
	"visible": true
}
```

```json
{ "type": "LAYER_BLUR", "blurType": "NORMAL", "radius": 12, "visible": true }
```

```json
{
	"type": "BACKGROUND_BLUR",
	"blurType": "PROGRESSIVE",
	"radius": 20,
	"startRadius": 4,
	"startOffset": { "x": 0, "y": 0 },
	"endOffset": { "x": 1, "y": 1 },
	"visible": true
}
```

```json
{
	"type": "NOISE",
	"noiseType": "MONOTONE",
	"color": { "r": 0, "g": 0, "b": 0, "a": 1 },
	"noiseSize": 2,
	"density": 0.4,
	"blendMode": "NORMAL",
	"visible": true
}
```

```json
{
	"type": "NOISE",
	"noiseType": "DUOTONE",
	"color": { "r": 0, "g": 0, "b": 0, "a": 1 },
	"secondaryColor": { "r": 1, "g": 1, "b": 1, "a": 1 },
	"noiseSize": 2,
	"density": 0.4,
	"blendMode": "NORMAL",
	"visible": true
}
```

```json
{
	"type": "NOISE",
	"noiseType": "MULTITONE",
	"color": { "r": 0, "g": 0, "b": 0, "a": 1 },
	"opacity": 0.6,
	"noiseSize": 2,
	"density": 0.4,
	"blendMode": "NORMAL",
	"visible": true
}
```

```json
{ "type": "TEXTURE", "noiseSize": 3, "radius": 6, "clipToShape": true, "visible": true }
```

```json
{
	"type": "GLASS",
	"lightIntensity": 0.6,
	"lightAngle": 30,
	"refraction": 0.4,
	"depth": 2,
	"dispersion": 0.2,
	"radius": 8,
	"visible": true
}
```

## BlendMode

- **데이터 개념**: 레이어/페인트의 블렌딩 모드.
- **공식 설명 요약**: PASS_THROUGH, NORMAL, MULTIPLY 등 표준 모드 집합.
- **typings 구조**: `type BlendMode = 'PASS_THROUGH' | 'NORMAL' | ...`
- **예제 데이터**

```json
{ "blendMode": "MULTIPLY" }
```

## MaskType

- **데이터 개념**: 마스크 적용 방식.
- **공식 설명 요약**: `ALPHA` / `VECTOR` / `LUMINANCE`.
- **typings 구조**: `type MaskType = 'ALPHA' | 'VECTOR' | 'LUMINANCE'`
- **예제 데이터**

```json
{ "maskType": "ALPHA" }
```

## StrokeCap / StrokeJoin

- **데이터 개념**: 스트로크 끝/조인 모양.
- **공식 설명 요약**: 캡과 조인 타입을 리터럴로 정의.
- **typings 구조**: `StrokeCap = 'NONE' | 'ROUND' | 'SQUARE' | ...`, `StrokeJoin = 'MITER' | 'BEVEL' | 'ROUND'`
- **예제 데이터**

```json
{ "strokeCap": "ROUND", "strokeJoin": "MITER" }
```

## Image

- **데이터 개념**: 이미지 파일 핸들.
- **공식 설명 요약**: `ImagePaint`에서 해시로 참조하며, `getBytesAsync`, `getSizeAsync` 제공.
- **typings 구조**: `interface Image { hash; getBytesAsync(); getSizeAsync(); }`
- **예제 데이터**

```json
{ "hash": "abcd1234" }
```

## ExportSettings

- **데이터 개념**: 노드 export 설정.
- **공식 설명 요약**: Image/SVG/PDF/REST(JSON) 포맷을 지원.
- **typings 구조**: `ExportSettings = ExportSettingsImage | ExportSettingsSVG | ExportSettingsPDF` (REST는 문서에만 있음)
- **예제 데이터 (유니온 + REST)**

```json
{ "format": "PNG", "constraint": { "type": "SCALE", "value": 2 } }
```

```json
{ "format": "SVG", "svgOutlineText": true, "svgSimplifyStroke": true }
```

```json
{ "format": "SVG_STRING", "svgIdAttribute": true }
```

```json
{ "format": "PDF", "useAbsoluteBounds": true }
```

```json
{ "format": "JSON_REST_V1" }
```

## 문서 링크

- https://developers.figma.com/docs/plugins/api/Paint/
- https://developers.figma.com/docs/plugins/api/Effect/
- https://developers.figma.com/docs/plugins/api/RGB/
- https://developers.figma.com/docs/plugins/api/MaskType/
- https://developers.figma.com/docs/plugins/api/BlendMode/
- https://developers.figma.com/docs/plugins/api/StrokeCap/
- https://developers.figma.com/docs/plugins/api/StrokeJoin/
- https://developers.figma.com/docs/plugins/api/Image/
- https://developers.figma.com/docs/plugins/api/ExportSettings/
