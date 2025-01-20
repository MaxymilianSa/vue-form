<template>
  <h1>Form</h1>
  <Form v-bind="form">
    <Input name="name" />
  </Form>
</template>

<!-- eslint-disable @typescript-eslint/no-explicit-any -->
<script lang="ts" setup>
import Form from './components/Form/Form.vue'

import Input from './components/Form/fields/Input.vue'

const form = {
  initialValues: {
    name: '',
  },
  onSubmit: (values: Record<string, any>) => {
    console.log(values)
  },
}
</script>
