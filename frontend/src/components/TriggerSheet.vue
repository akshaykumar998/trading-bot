<template>
  <Sheet defaultOpen>
    <SheetContent>
      <SheetHeader>
        <SheetTitle>Select Trigger</SheetTitle>
        <SheetDescription> Select the type of trigger that you need </SheetDescription>
        <Select v-model="selectedTrigger" @update="handleSelect">
          <SelectTrigger class="w-[180px]">
            <SelectValue placeholder="Select a Trigger" />
          </SelectTrigger>
          <SelectContent>
            <SelectGroup>
              <SelectItem
                v-for="trigger in SUPPORTED_TRIGGERS"
                :key="trigger.id"
                :value="trigger.id"
              >
                {{ trigger.title }}
              </SelectItem>
            </SelectGroup>
          </SelectContent>
        </Select>
        <div v-if="selectedTrigger === 'timer'">
          <Label for="timer">Timer</Label>
          <Input id="timer" type="text" v-model.number="metadata.time"></Input>
        </div>
        <div v-if="selectedTrigger === 'price-trigger'">
          <Label for="price">Price</Label>
          <Input id="price" type="text" v-model.number="metadata.price"></Input>
          <Label for="metadata.asset">Assets</Label>
          <Select v-model="metadata.asset">
            <SelectTrigger class="w-[180px]">
              <SelectValue placeholder="Select a Asset" />
            </SelectTrigger>
            <SelectContent>
              <SelectGroup>
                <SelectLabel></SelectLabel>
                <SelectItem v-for="asset in SUPPORTED_ASSETS" :key="asset" :value="asset">
                  {{ asset }}
                </SelectItem>
              </SelectGroup>
            </SelectContent>
          </Select>
        </div>
      </SheetHeader>
      <SheetFooter>
        <Button type="submit" @click="createFlow"> Create Flow </Button>
      </SheetFooter>
    </SheetContent>
  </Sheet>
</template>

<script setup lang="ts">
import { Button } from '@/components/ui/button'
import { ref } from 'vue'
import type { PriceTriggerMetaData } from '@/nodes/triggers/PriceTrigger.vue'
import type { TimerNodeMetaData } from '@/nodes/triggers/TimersNode.vue'
import {
  Sheet,
  SheetContent,
  SheetDescription,
  SheetFooter,
  SheetHeader,
  SheetTitle,
} from '@/components/ui/sheet'
import {
  Select,
  SelectContent,
  SelectGroup,
  SelectItem,
  SelectTrigger,
  SelectValue,
} from '@/components/ui/select'
import Input from './ui/input/Input.vue'
import Label from './ui/label/Label.vue'
import SelectLabel from './ui/select/SelectLabel.vue'

const SUPPORTED_TRIGGERS = ref([
  {
    id: 'timer',
    title: 'Timer',
    description: 'Run this trigger every x seconds/minutes',
  },
  {
    id: 'price-trigger',
    title: 'Price Trigger',
    description: 'Runs whenever the price goes above or below a certain number',
  },
])

const selectedTrigger = ref<string>('')

const handleSelect = (value: string | null) => {
  if (value) {
    selectedTrigger.value = value
  }
}

const emit = defineEmits<{
  'trigger-selected': [trigger: { id: string; title: string }]
}>()

const SUPPORTED_ASSETS = ref(['SOL', 'BTC', 'ETH'])

const metadata = ref<PriceTriggerMetaData | TimerNodeMetaData>({
  asset: '',
  price: 0,
  decimals: 0,
})

const createFlow = () => {
  const trigger = SUPPORTED_TRIGGERS.value.find((t) => t.id === selectedTrigger.value)
  if (trigger) {
    emit('trigger-selected', { id: trigger.id, title: trigger.title })
  }
}
</script>
