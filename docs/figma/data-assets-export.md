# Assets & Export

## Image / Video

- 공식 문서: `https://www.figma.com/plugin-docs/api/Image/`

```ts
// plugin-api.d.ts
interface Image {
	readonly hash: string
	getBytesAsync(): Promise<Uint8Array>
	getSizeAsync(): Promise<{ width: number; height: number }>
}

interface Video {
	readonly hash: string
}
```

## ExportSettings

- 공식 문서: `https://www.figma.com/plugin-docs/api/ExportSettings/`
- 가이드: `https://www.figma.com/plugin-docs/api/export/`

```ts
// plugin-api.d.ts (발췌)
interface ExportSettingsConstraints {
	readonly type: "SCALE" | "WIDTH" | "HEIGHT"
	readonly value: number
}

interface ExportSettingsImage {
	readonly format: "JPG" | "PNG"
	readonly contentsOnly?: boolean
	readonly useAbsoluteBounds?: boolean
	readonly suffix?: string
	readonly constraint?: ExportSettingsConstraints
	readonly colorProfile?: "DOCUMENT" | "SRGB" | "DISPLAY_P3_V4"
}

interface ExportSettingsSVG extends ExportSettingsSVGBase {
	readonly format: "SVG"
}

interface ExportSettingsPDF {
	readonly format: "PDF"
	readonly contentsOnly?: boolean
	readonly useAbsoluteBounds?: boolean
	readonly suffix?: string
	readonly colorProfile?: "DOCUMENT" | "SRGB" | "DISPLAY_P3_V4"
}
```

### Typings 주석 발췌

```ts
// plugin-api.d.ts (발췌)
// SVG export can render text as outlines or as <text> elements.
```

**사용 위치**

- `ExportMixin.exportSettings`
- `Node.exportAsync(settings)`

---

다음 문서: `data-plugin-data.md`
