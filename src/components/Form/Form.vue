<template>
  <form @submit="onSubmitForm">
    <slot></slot>
  </form>
</template>

<!-- eslint-disable @typescript-eslint/no-explicit-any -->
<script lang="ts" setup>
import { ref, provide } from 'vue'

import { useForm } from 'vee-validate'

const { onSubmit, initialValues, clearOnSubmit } = defineProps<{
  onSubmit: (values: Record<string, any>) => void
  initialValues: Record<string, any>
  clearOnSubmit?: boolean
}>()

const { handleSubmit, defineField, resetForm } = useForm({
  initialValues,
})

const data = ref<{
  values: Record<string, [any, Record<string, any>]>
}>({
  values: Object.entries(initialValues).reduce(
    (prev, [name]) => ({ ...prev, [name]: defineField(name) }),
    {},
  ),
})

const getField = (name: string) => {
  return { value: data.value.values[name][0], attributes: data.value.values[name][1] }
}

provide('form', {
  ...data,
  getField,
})

const onSubmitForm = handleSubmit((values) => {
  onSubmit(values)
  if (clearOnSubmit) {
    resetForm()
  }
})
</script>
