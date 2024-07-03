<script setup>
import {reactive, ref} from 'vue'
import Form from './components/Form.vue';
import Result from './components/Result.vue';

let showResult = ref(false)
let fieldsData = reactive({})

let onFormSubmitted = (fields) => {
  showResult.value = true
  fieldsData = fields
}
</script>

<template>
  <div id="app">
    <h1>Form</h1>
    <Form @form-submitted="onFormSubmitted"></Form>
    <Result :list="fieldsData"v-if="showResult"></Result>
    </div>
</template>