

<template>

    <div class="section">

                


        <div class="section-title">
            {{section.title}}
        </div>
        
        <div
            class = "entry"
            :key="i" v-for="(element, i) in props.section.entries"
        >

            <table>
                <tr>
                    <td>
                        <span
                            v-if="element.dateOrRange.value === 'range'"
                        >
                            {{element.model.text}} {{element.model2}}
                            –<br>{{element.model3.text}} {{element.model4}}
                        </span>


                        <span
                            v-if="element.dateOrRange.value === 'date'"
                        >
                            {{element.model.text}} {{element.model2}}
                        </span>




                    </td>
                    <td>
                        <span>{{element.jobDescription}}</span>
                    </td>
                </tr>
            </table>


        </div>




    </div>

</template>



<script setup>


const props = defineProps({
    section: Object,
})

//console.log(props,props.section, 3023982398329832, props.section.entries)

</script>



<style scoped>

    table {
        table-layout: fixed;
        border: 0px solid #ddd;
        width: 100%;
    }

    td {
        width: 50%;
        padding: 1rem;
        vertical-align: top;
    }

    .section {
        margin-bottom: 1.6rem;
    }

    .section-title {
        background: #038cfc;
        color: white;
        font-size: 1rem;
        padding: 1rem;
        margin-bottom: 0.8rem;
        border-radius: 2px 2px 2px 2px;
    }

    .entry {

    }

</style>