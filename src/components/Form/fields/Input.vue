<template>
  <input type="text" v-model="value" v-bind="attributes" />
</template>

<script setup lang="ts">
import { inject } from 'vue'

const { name } = defineProps<{
  name: string
}>()

// eslint-disable-next-line @typescript-eslint/no-explicit-any
const data: any = inject('form')

const { value, attributes } = data.getField(name)
</script>
