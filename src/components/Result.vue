<template>
    <h3>Your answer</h3>

    <table>
        <tr>
            <th>Field</th>
            <th>Your answer</th>
        </tr>
        <Answer v-for="field in props.list" :key="field.fieldName" :field="field.fieldName" :answer="field.value"></Answer>
    </table>
</template>

<script setup>
    import Answer from './Answer.vue';

    const props = defineProps({
        list: Array
    })
</script>