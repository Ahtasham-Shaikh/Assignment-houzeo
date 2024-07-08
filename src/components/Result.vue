<template>
    <h3>Your answer</h3>
    <!-- {{ props.list2 }} -->
    <table>
        <tr>
            <th>Field</th>
            <th>Your answer</th>
        </tr>
        <div v-for="(obj, i) in props.list2">
            <Answer v-for="field in obj.fields" :key="field" :field="field.fieldName" :answer="field.value">
        </Answer>
        </div>
        <Answer v-for="field in props.list" :key="field.fieldName" :field="field.fieldName" :answer="field.value"></Answer>
    </table>
</template>

<script setup>
    import Answer from './Answer.vue';

    const props = defineProps({
        list: Object, 
        list2: Object,
    })
</script>