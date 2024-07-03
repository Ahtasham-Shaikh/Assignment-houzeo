<template>
    <div class="flex">
        <input style="width: 180px;" @change="handleFileChange" :v-model="props.fileModel" type="file" multiple accept=".jpeg, .pdf" />
        <img class="del-btn" height="24px" src="/delete.svg" />
    </div>
</template>

<script setup>

    let props = defineProps({
        fileModel: Array
    })

    let handleFileChange = (event) => {
        console.log(props.fileModel)
    }
</script>