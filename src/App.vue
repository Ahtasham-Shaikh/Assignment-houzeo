<script setup>
import {reactive, ref} from 'vue'
import Form from './components/Form.vue';
import Result from './components/Result.vue';

let showResult = ref(false)
let fieldsData = reactive({})
let groupFieldsData = reactive({})

let onFormSubmitted = (fields, groupFields) => {
  showResult.value = true
  Object.assign(fieldsData, fields);
  groupFieldsData = groupFields
  console.log(groupFieldsData)
}
</script>

<template>
  <div id="app">
    <h1>Form</h1>
    <Form @form-submitted="onFormSubmitted"></Form>
    <Result :list2="groupFieldsData" :list="fieldsData"v-if="showResult"></Result>
    </div>
</template>