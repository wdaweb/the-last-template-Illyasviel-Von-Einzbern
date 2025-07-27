<template>
  <canvas id="wanko" style="width: 100%; height: 500px;"></canvas>
</template>

<script setup>
import { onMounted } from 'vue'
import * as PIXI from 'pixi.js'
import { Live2DModel } from 'pixi-live2d-display'

onMounted(async () => {
  const app = new PIXI.Application({
    view: document.getElementById('wanko'),
    autoStart: true,
    backgroundColor: 0xffffff,
    resizeTo: window,
  });

  const model = await Live2DModel.from("/wanko/runtime/wanko_touch.model3.json");

  model.scale.set(0.3);
  model.x = 100;
  model.y = 100;

  app.stage.addChild(model);
});
</script>
