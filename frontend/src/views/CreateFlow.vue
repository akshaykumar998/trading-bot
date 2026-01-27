<template>
  <div style="height: 100vh">
    <TriggerSheet @trigger-selected="handleTriggerSelected"></TriggerSheet>
    <VueFlow
      v-model:nodes="nodes"
      v-model:edges="edges"
      fit-view-on-init
      class="vue-flow-basic-example"
      :default-zoom="1.5"
      :min-zoom="0.2"
      :max-zoom="4"
    >
    </VueFlow>
  </div>
</template>

<script lang="ts" setup>
import { ref } from 'vue'
import { VueFlow, useVueFlow, type Node, type Edge } from '@vue-flow/core'
import TriggerSheet from '@/components/TriggerSheet.vue'

const { onConnect, addEdges, addNodes } = useVueFlow()

const nodes = ref<Node[]>([])

const edges = ref<Edge[]>([])

onConnect((params) => {
  addEdges([params])
})

const handleTriggerSelected = (trigger: { id: string; title: string }) => {
  const newNode: Node = {
    id: trigger.id,
    label: trigger.title,
    position: { x: 250, y: 25 },
    type: 'custom',
  }
  addNodes([newNode])
}
</script>

<style>
@media (min-width: 1024px) {
  .about {
    min-height: 100vh;
    display: flex;
    align-items: center;
  }
}
</style>
