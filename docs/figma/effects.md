# Effects

- 공식 문서: `https://www.figma.com/plugin-docs/api/Effect/`
- Shadow: `https://www.figma.com/plugin-docs/api/ShadowEffect/`
- Blur: `https://www.figma.com/plugin-docs/api/BlurEffect/`

```ts
// plugin-api.d.ts
type Effect = DropShadowEffect | InnerShadowEffect | BlurEffect | NoiseEffect | TextureEffect | GlassEffect
```

### Typings 주석 발췌

```ts
// plugin-api.d.ts (발췌)
// Texture effects currently do not support binding variables.
// Glass effects currently do not support binding variables.
```

## Shadow Effects

```ts
interface DropShadowEffect {
	readonly type: "DROP_SHADOW"
	readonly color: RGBA
	readonly offset: Vector
	readonly radius: number
	readonly spread?: number
	readonly visible: boolean
	readonly blendMode: BlendMode
	readonly boundVariables?: { [field in VariableBindableEffectField]?: VariableAlias }
}

interface InnerShadowEffect {
	readonly type: "INNER_SHADOW"
	readonly color: RGBA
	readonly offset: Vector
	readonly radius: number
	readonly spread?: number
	readonly visible: boolean
	readonly blendMode: BlendMode
	readonly boundVariables?: { [field in VariableBindableEffectField]?: VariableAlias }
}
```

## Blur Effects

```ts
interface BlurEffect {
	readonly type: "LAYER_BLUR" | "BACKGROUND_BLUR"
	readonly radius: number
	readonly visible: boolean
	readonly boundVariables?: { [field in VariableBindableEffectField]?: VariableAlias }
}
```

## Noise / Texture / Glass

```ts
type NoiseEffect = NoiseEffectMonotone | NoiseEffectDuotone | NoiseEffectMultitone

interface TextureEffect {
	readonly type: "TEXTURE"
	readonly visible: boolean
	readonly noiseSize: number
	readonly radius: number
	readonly clipToShape: boolean
	readonly boundVariables?: {}
}

interface GlassEffect {
	readonly type: "GLASS"
	readonly visible: boolean
	readonly lightIntensity: number
	readonly lightAngle: number
	readonly refraction: number
	readonly depth: number
	readonly dispersion: number
	readonly radius: number
	readonly boundVariables?: {}
}
```

**사용 위치**

- `BlendMixin.effects`
- `EffectStyle.effects`

---

다음 문서: `layout-and-constraints.md`
