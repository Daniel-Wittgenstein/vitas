

<template>

    <div>

                


<div class="section-title">
            {{section.title}}
        </div>
        
        <div
            :key="i" v-for="(entry, i) in props.section.entries"
        >
            - {{entry.jobDescription}}
        </div>

    </div>

</template>



<script setup>


const props = defineProps({
    section: Object,
})

console.log(props,props.section, 3023982398329832, props.section.entries)

</script>