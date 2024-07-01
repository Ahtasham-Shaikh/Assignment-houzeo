<template>
    <tr>
        <td>{{ props.field }}</td>
        <td>{{ props.answer }}</td>
    </tr>
</template>

<script setup>
    const props = defineProps({
        field: String,
        answer: String,
    })
</script>