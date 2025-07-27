<template>
  <div id="app">
    <canvas id="wanko"></canvas>
  </div>
</template>

<script setup>
import * as PIXI from 'pixi.js'
import { Live2DModel } from 'pixi-live2d-display'
import { onMounted } from 'vue'

let app = null  // Pixi App reference

onMounted(async () => {
  const canvas = document.getElementById('wanko')

  // 如果已存在 app，先销毁
  if (app) {
    app.destroy(true, { children: true })
    app = null
  }

  app = new PIXI.Application({
    view: canvas,
    width: 300,
    height: 500,
    backgroundAlpha: 0,
    autoStart: true
  })

  const model = await Live2DModel.from('/wanko/runtime/wanko_touch.model3.json')
  app.stage.addChild(model)

  const scale = Math.min(300 / model.width, 500 / model.height)
  model.scale.set(scale)
  model.x = (app.renderer.width - model.width * scale) / 2
  model.y = app.renderer.height - model.height * scale

  model.interactive = true
  model.buttonMode = true

  // 滑鼠追踪
  canvas.addEventListener('mousemove', (e) => {
    const rect = canvas.getBoundingClientRect()
    const mx = e.clientX - rect.left
    const my = e.clientY - rect.top

    // 把滑鼠座標轉成 PIXI 設計的 0–1 對應
    model.focus(mx / app.renderer.width, my / app.renderer.height)
  })

  // 拖曳交互
  model.on('pointerdown', e => {
    model.dragging = true
    model._pointerX = e.data.global.x - model.x
    model._pointerY = e.data.global.y - model.y
  })
  model.on('pointermove', e => {
    if (model.dragging) {
      model.x = e.data.global.x - model._pointerX
      model.y = e.data.global.y - model._pointerY
    }
  })
  model.on('pointerup', () => (model.dragging = false))
  model.on('pointerupoutside', () => (model.dragging = false))

  // 点头/身体互动
  model.on('hit', areas => {
    if (areas.includes('head')) model.expression()
    if (areas.includes('body')) model.motion('tap_body')
  })

canvas.addEventListener('pointerdown', (e) => {
  model.dragging = true
  const rect = canvas.getBoundingClientRect()
  const mx = e.clientX - rect.left
  const my = e.clientY - rect.top

  model._pointerX = mx - model.x
  model._pointerY = my - model.y
})

canvas.addEventListener('pointermove', (e) => {
  if (!model.dragging) return
  const rect = canvas.getBoundingClientRect()
  const mx = e.clientX - rect.left
  const my = e.clientY - rect.top

  model.x = mx - model._pointerX
  model.y = my - model._pointerY
})

window.addEventListener('pointerup', () => {
  model.dragging = false
})
})
</script>

<style scoped>
#wanko {
  position: fixed;
  right: 0;
  bottom: 0;
  width: 100vw;
  height: 100vh;
  z-index: 9999;
  pointer-events: none; /* 這裡改成 none，讓滑鼠事件傳遞到 model 上 */
}
html, body, #app {
  margin: 0; padding: 0;
  width: 100%; height: 100%;
  overflow: hidden;
}
</style>
