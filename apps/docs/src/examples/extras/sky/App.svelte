<script lang="ts">
  import { useTweakpane } from '$lib/useTweakpane'
  import { Canvas } from '@threlte/core'
  import { Sky } from '@threlte/extras'
  import { spring } from 'svelte/motion'
  import Scene from './Scene.svelte'

  const presets = {
    sunset: {
      turbidity: 10,
      rayleigh: 3,
      azimuth: 180,
      elevation: 0.5,
      mieCoefficient: 0.005,
      mieDirectionalG: 0.7,
      exposure: 0.37
    },
    noon: {
      turbidity: 0.65,
      rayleigh: 0.17,
      azimuth: 180,
      elevation: 85,
      mieCoefficient: 0.013,
      mieDirectionalG: 0.7,
      exposure: 1
    },
    afternoon: {
      turbidity: 4.78,
      rayleigh: 0.3,
      azimuth: 180,
      elevation: 30,
      mieCoefficient: 0.002,
      mieDirectionalG: 0.86,
      exposure: 0.65
    },
    night: {
      turbidity: 20,
      rayleigh: 0.57,
      azimuth: 180,
      elevation: -5,
      mieCoefficient: 0.038,
      mieDirectionalG: 0,
      exposure: 0.26
    }
  }

  const springValues = spring(presets.sunset, {
    damping: 0.95,
    precision: 0.0001,
    stiffness: 0.05
  })

  const { addInput, action, addButton } = useTweakpane({
    title: 'Sky',
    expanded: true
  })

  const setEnvironment = addInput({
    label: 'Set Environment',
    value: true
  })

  const turbidity = addInput({
    label: 'Turbidity',
    value: presets.sunset.turbidity,
    params: {
      min: 0,
      max: 20
    }
  })

  const rayleigh = addInput({
    label: 'Rayleigh',
    value: presets.sunset.rayleigh,
    params: {
      min: 0,
      max: 4
    }
  })

  const azimuth = addInput({
    label: 'Azimuth',
    value: presets.sunset.azimuth,
    params: {
      min: -180,
      max: 180
    }
  })

  const elevation = addInput({
    label: 'Elevation',
    value: presets.sunset.elevation,
    params: {
      min: -5,
      max: 90
    }
  })

  const mieCoefficient = addInput({
    label: 'Mie Coefficient',
    value: presets.sunset.mieCoefficient,
    params: {
      min: 0,
      max: 0.1
    }
  })

  const mieDirectionalG = addInput({
    label: 'Mie Directional G',
    value: presets.sunset.mieDirectionalG,
    params: {
      min: 0,
      max: 1
    }
  })

  const exposure = addInput({
    label: 'Exposure',
    value: presets.sunset.exposure,
    params: {
      min: 0,
      max: 2
    }
  })

  const applyPreset = (preset: keyof typeof presets) => {
    turbidity.set(presets[preset].turbidity)
    rayleigh.set(presets[preset].rayleigh)
    azimuth.set(presets[preset].azimuth)
    elevation.set(presets[preset].elevation)
    mieCoefficient.set(presets[preset].mieCoefficient)
    mieDirectionalG.set(presets[preset].mieDirectionalG)
    exposure.set(presets[preset].exposure)
  }

  addButton({
    title: 'Noon',
    label: 'Preset',
    onClick() {
      applyPreset('noon')
    }
  })

  addButton({
    title: 'Afternoon',
    label: 'Preset',
    onClick() {
      applyPreset('afternoon')
    }
  })

  addButton({
    title: 'Sunset',
    label: 'Preset',
    onClick() {
      applyPreset('sunset')
    }
  })

  addButton({
    title: 'Night',
    label: 'Preset',
    onClick() {
      applyPreset('night')
    }
  })

  $: {
    springValues.set({
      turbidity: $turbidity,
      rayleigh: $rayleigh,
      azimuth: $azimuth,
      elevation: $elevation,
      mieCoefficient: $mieCoefficient,
      mieDirectionalG: $mieDirectionalG,
      exposure: $exposure
    })
  }
</script>

<div use:action />

<Canvas>
  <Sky
    setEnvironment={$setEnvironment}
    turbidity={$springValues.turbidity}
    rayleigh={$springValues.rayleigh}
    azimuth={$springValues.azimuth}
    elevation={$springValues.elevation}
    mieCoefficient={$springValues.mieCoefficient}
    mieDirectionalG={$springValues.mieDirectionalG}
  />

  <Scene exposure={$springValues.exposure} />
</Canvas>
