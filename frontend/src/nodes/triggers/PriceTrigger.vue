<template>
  <div class="p-4 border">
    {{ data.metadata.asset }}
    <Handle type="source" :position="Position.Right" />
  </div>
</template>

<script lang="ts" setup>
import { Handle, Position } from '@vue-flow/core'

export type PriceTriggerMetaData = {
  asset: string
  price: number
  decimals: number
}

defineProps<{
  data: {
    metadata: PriceTriggerMetaData
  }
  isConnectable: boolean
}>()
</script>
