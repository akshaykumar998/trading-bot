<template>
  <Select v-model="model">
    <SelectTrigger class="w-[180px]">
      <SelectValue />
    </SelectTrigger>
    <SelectContent>
      <SelectGroup>
        <SelectItem v-for="asset in SUPPORTED_ASSETS" :key="asset" :value="asset">
          {{ asset }}
        </SelectItem>
      </SelectGroup>
    </SelectContent>
  </Select>
</template>

<script lang="ts" setup>
import {
  Select,
  SelectContent,
  SelectGroup,
  SelectItem,
  SelectTrigger,
  SelectValue,
} from '@/components/ui/select'
const SUPPORTED_ASSETS = ['SOL', 'BTC', 'ETH'] as const
export type SupportedAsset = (typeof SUPPORTED_ASSETS)[number]
const model = defineModel<SupportedAsset | undefined>()
</script>
