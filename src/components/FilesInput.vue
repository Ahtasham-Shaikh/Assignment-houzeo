<template>
    <div class="flex">
        <input @change="handleFileChange" :v-model="props.fileModel" type="file" multiple accept=".jpeg, .pdf" />
    </div>
</template>

<script setup>
    let emit = defineEmits('file-change', )
    let fileName;

    let handleFileChange = (event) => {
        fileName = event.target.files[0].name
        emit('file-change', fileName)
    }
</script>