# Plugin Data (Private / Shared)

- 공식 문서: `https://www.figma.com/plugin-docs/api/BaseNodeMixin/#getplugin-data`
- 공식 문서: `https://www.figma.com/plugin-docs/api/BaseNodeMixin/#setplugin-data`
- 공식 문서: `https://www.figma.com/plugin-docs/api/BaseNodeMixin/#getsharedplugin-data`
- 공식 문서: `https://www.figma.com/plugin-docs/api/BaseNodeMixin/#setsharedplugin-data`

```ts
// plugin-api.d.ts (발췌)
interface PluginDataMixin {
	getPluginData(key: string): string
	setPluginData(key: string, value: string): void
	getPluginDataKeys(): string[]
	getSharedPluginData(namespace: string, key: string): string
	setSharedPluginData(namespace: string, key: string, value: string): void
	getSharedPluginDataKeys(namespace: string): string[]
}
```

### Typings 주석 발췌

```ts
// plugin-api.d.ts (발췌)
// Data is private for stability, not security.
// Total entry size cannot exceed 100 kB.
```

**사용 위치**

- `BaseNodeMixin`과 `BaseStyleMixin`에서 `PluginDataMixin`을 통해 제공

---

다음 문서: `data-interactions.md`
