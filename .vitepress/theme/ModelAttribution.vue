<script setup lang="ts">
import { computed } from 'vue'
import { useData, withBase } from 'vitepress'
const { lang, page } = useData()
const zh = computed(() => lang.value === 'zh-CN')
const visible = computed(() => page.value.relativePath === 'architecture.md' || page.value.relativePath === 'zh/architecture.md')
</script>
<template><aside v-if="visible" id="model-attribution" class="nightlab-model-attribution" :aria-label="zh ? '模型来源' : 'Model attribution'">
<strong>{{ zh ? '模型与灯号' : 'Model & LED notes' }}</strong>
<p>{{ zh ? '首页以蓝色点亮 blink(1) 字标面上的 LED 1，以红色点亮 ThingM 面上的 LED 2，模拟两颗 PCB 灯透过扩散罩的混光。两个颜色是固定的屏幕演示值。' : 'The home preview drives LED 1 blue on the blink(1) face and LED 2 red on the ThingM face. The model simulates how light from the PCB mixes in the diffuser using these fixed demo colors.' }}</p>
<p><a href="https://github.com/b1ug/blink1-models">blink(1) Models</a> · ThingM / todbot · <a href="https://github.com/todbot/blink1/tree/101abe3599c661c4dd4d1204b4d50fb592293143/hardware/enclosure">{{ zh ? '外壳 CAD' : 'Enclosure CAD' }}</a> (<a :href="withBase('/nightlab/model-assets/LICENSE.txt')">CC BY-SA 4.0</a>) · <a href="https://github.com/todbot/blink1/blob/101abe3599c661c4dd4d1204b4d50fb592293143/hardware/schematic/blink1mk2_v2c6.brd">{{ zh ? 'PCB 布局' : 'PCB layout' }}</a> (<a :href="withBase('/nightlab/model-assets/PCB-LICENSE.txt')">CC BY-SA 3.0</a>)</p>
<p><a :href="withBase('/nightlab/source-receipt.json')">{{ zh ? '模型来源与变更记录' : 'Model sources & changes' }}</a> · <a :href="withBase('/nightlab/model-assets/source.json')">{{ zh ? 'CAD 资源记录' : 'CAD asset record' }}</a> · <a :href="withBase('/nightlab/vendor/three/LICENSE.txt')">Three.js MIT</a></p>
</aside></template>
