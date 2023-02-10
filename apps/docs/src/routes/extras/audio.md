---
title: Audio
---

!!!module_summary title=Audio|sourcePath=audio/Audio.svelte|name=Audio|from=extras|type=component|relatedDocs={[{name:"three.js Audio reference",url:"https://threejs.org/docs/#api/en/audio/Audio"}]}

Create a non-positional (global) audio object.
This uses the [Web Audio API](https://developer.mozilla.org/en-US/Web/API/Web_Audio_API).

:::admonition type="tip"
You need to have an `<AudioListener>` component in your scene in order to use `<Audio>`and `<PositionalAudio>`components.
:::
!!!

### Example

```svelte
<script>
  import { T, Canvas, AudioListener, Audio } from '@threlte/core'
</script>

<Canvas>
  <T.PerspectiveCamera makeDefault position={[3, 3, 3]} lookAt={[0, 0, 0]}>
    <AudioListener />
  </T.PerspectiveCamera>

  <Audio source={'/audio/track.mp3'} />
</Canvas>
```

### Properties

```ts
// optional
viewportAware: boolean = false
position: Position | undefined = undefined
scale: Scale | undefined = undefined
rotation: Rotation | undefined = undefined
lookAt: LookAt | undefined = undefined
castShadow: boolean | undefined = undefined
receiveShadow: boolean | undefined = undefined
frustumCulled: boolean | undefined = undefined
renderOrder: number | undefined = undefined
visible: boolean | undefined = undefined
dispose: boolean | undefined = undefined
userData: Record<string, any> | undefined = undefined
autoplay: boolean | undefined = undefined
detune: number | undefined = undefined
source: string | AudioBuffer | HTMLMediaElement | AudioBufferSourceNode | MediaStream | undefined = undefined
volume: number | undefined = undefined
loop: boolean | undefined = undefined
filters: BiquadFilterNode[] | BiquadFilterNode | undefined = undefined
playbackRate: number | undefined = undefined
id: string | undefined = undefined
```

### Bindings

```ts
audio: THREE.Audio
inViewport: boolean
play: (delay?: number) => Promise<THREE.Audio>
pause: () => THREE.Audio
stop: () => THREE.Audio
```

### Events

```ts
viewportenter: undefined
viewportleave: undefined
load: AudioBuffer
progress: ProgressEvent<EventTarget>
error: ErrorEvent
```