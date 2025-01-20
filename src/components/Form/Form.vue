<template>
  <form @submit="onSubmitForm">
    <slot></slot>
  </form>
</template>

<!-- eslint-disable @typescript-eslint/no-explicit-any -->
<script lang="ts" setup>
import { ref, provide } from 'vue'

import { useForm } from 'vee-validate'

const { onSubmit, initialValues } = defineProps<{
  onSubmit: (values: Record<string, any>) => void
  initialValues: Record<string, any>
}>()

const { handleSubmit, defineField } = useForm({
  initialValues,
})

const data = ref({
  values: Object.entries(initialValues).reduce(
    (prev, [name]) => ({ ...prev, [name]: defineField(name) }),
    {},
  ),
})
provide('form', data)

const onSubmitForm = handleSubmit((values) => {
  onSubmit(values)
})
</script>
