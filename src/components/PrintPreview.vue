
<template>

    <print-preview-section
        :key="section.id" v-for="section in cvData.sections" :section="section"
        >
    </print-preview-section>

</template>




<script setup>

import PrintPreviewSection from 'components/PrintPreviewSection.vue'

const props = defineProps({
    cvData: Object,
})

console.log("cv data", props.cvData)

</script>
