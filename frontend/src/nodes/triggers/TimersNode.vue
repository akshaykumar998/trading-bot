<template>
  <div class="p-4 border">
    {{ data.metadata.time / 3600 }}
    <Handle type="source" :position="Position.Right" />
  </div>
</template>

<script lang="ts" setup>
import { Handle, Position } from '@vue-flow/core'

export type TimerNodeMetaData = {
  time: number
}

defineProps<{
  data: {
    metadata: TimerNodeMetaData
  }
  isConnectable: boolean
}>()
</script>
