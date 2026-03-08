# Interactions (Reaction / Action / Trigger / Transition)

- 공식 문서: `https://www.figma.com/plugin-docs/api/Reaction/`
- 공식 문서: `https://www.figma.com/plugin-docs/api/Action/`
- 공식 문서: `https://www.figma.com/plugin-docs/api/Trigger/`
- 공식 문서: `https://www.figma.com/plugin-docs/api/Transition/`

## Reaction

```ts
// plugin-api.d.ts
type Reaction = {
	/** @deprecated Use actions */
	action?: Action
	actions?: Action[]
	trigger: Trigger | null
}
```

## Action

```ts
// plugin-api.d.ts (발췌)
type Action =
	| { readonly type: "BACK" | "CLOSE" }
	| { readonly type: "URL"; url: string; openInNewTab?: boolean }
	| {
			readonly type: "UPDATE_MEDIA_RUNTIME"
			readonly destinationId: string | null
			readonly mediaAction: "PLAY" | "PAUSE" | "TOGGLE_PLAY_PAUSE" | "MUTE" | "UNMUTE" | "TOGGLE_MUTE_UNMUTE"
	  }
	| {
			readonly type: "UPDATE_MEDIA_RUNTIME"
			readonly destinationId?: string | null
			readonly mediaAction: "SKIP_FORWARD" | "SKIP_BACKWARD"
			readonly amountToSkip: number
	  }
	| {
			readonly type: "UPDATE_MEDIA_RUNTIME"
			readonly destinationId?: string | null
			readonly mediaAction: "SKIP_TO"
			readonly newTimestamp: number
	  }
	| { readonly type: "SET_VARIABLE"; readonly variableId: string | null; readonly variableValue?: VariableData }
	| {
			readonly type: "SET_VARIABLE_MODE"
			readonly variableCollectionId: string | null
			readonly variableModeId: string | null
	  }
	| { readonly type: "CONDITIONAL"; readonly conditionalBlocks: ConditionalBlock[] }
	| {
			readonly type: "NODE"
			readonly destinationId: string | null
			readonly navigation: Navigation
			readonly transition: Transition | null
			readonly preserveScrollPosition?: boolean
			readonly overlayRelativePosition?: Vector
			readonly resetVideoPosition?: boolean
			readonly resetScrollPosition?: boolean
			readonly resetInteractiveComponents?: boolean
	  }
```

## Trigger

```ts
// plugin-api.d.ts
type Trigger =
	| { readonly type: "ON_CLICK" | "ON_HOVER" | "ON_PRESS" | "ON_DRAG" }
	| { readonly type: "AFTER_TIMEOUT"; readonly timeout: number }
	| { readonly type: "MOUSE_UP" | "MOUSE_DOWN"; readonly delay: number }
	| { readonly type: "MOUSE_ENTER" | "MOUSE_LEAVE"; readonly delay: number; readonly deprecatedVersion: boolean }
	| {
			readonly type: "ON_KEY_DOWN"
			readonly device: "KEYBOARD" | "XBOX_ONE" | "PS4" | "SWITCH_PRO" | "UNKNOWN_CONTROLLER"
			readonly keyCodes: ReadonlyArray<number>
	  }
	| { readonly type: "ON_MEDIA_HIT"; readonly mediaHitTime: number }
	| { readonly type: "ON_MEDIA_END" }
```

## Transition

```ts
// plugin-api.d.ts
interface SimpleTransition {
	readonly type: "DISSOLVE" | "SMART_ANIMATE" | "SCROLL_ANIMATE"
	readonly easing: Easing
	readonly duration: number
}

interface DirectionalTransition {
	readonly type: "MOVE_IN" | "MOVE_OUT" | "PUSH" | "SLIDE_IN" | "SLIDE_OUT"
	readonly direction: "LEFT" | "RIGHT" | "TOP" | "BOTTOM"
	readonly matchLayers: boolean
	readonly easing: Easing
	readonly duration: number
}

type Transition = SimpleTransition | DirectionalTransition
```

### Typings 주석 발췌

```ts
// plugin-api.d.ts (발췌)
// Reaction.action is deprecated; use actions.
```

**사용 위치**

- `Reaction` 내 `actions`/`trigger`
- `ReactionMixin.reactions`

---

다음 문서: `index.md`
