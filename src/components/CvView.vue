<template>

<!--
    <maunzer-list ref="maunzer" heading-text=""></maunzer-list>
    <maunzer-list ref="maunzer" heading-text=""></maunzer-list>
    <maunzer-list ref="maunzer" heading-text=""></maunzer-list>
    <maunzer-list ref="maunzer" heading-text=""></maunzer-list>
    -->
    
    

<div ref="cvparentdiv">
    <maunzer-list
        ref="sections"
        :key="section.id" v-for="section in sections" :heading-text="section.title">
    </maunzer-list>
</div>


<button @click="exportCv" >Export</button>


</template>



<script setup>

    import { getCurrentInstance, onMounted, ref } from 'vue'
    let app = getCurrentInstance()

    import MaunzerList from 'components/MaunzerList.vue';

    import html2pdf from 'html2pdf.js'

    const cvparentdiv = ref(null)

    let mounted = false

    let tid = 0
    let sections = [
        { title: "Career / Education", id: tid++, },
        { title: "Awards", id: tid++, },
        { title: "Skills", id: tid++, },
        { title: "Languages", id: tid++, },
    ]
    
    let getSubState

    function test() {

    }




    function exportCv() {

        if (!getSubState || !mounted) {
            alert("App is not fully loaded yet. Please wait a moment.")
            return
        }


        let el = cvparentdiv.value
        html2pdf(el)

        return


        let subState = getSubState()
        for (let item of subState) {
            let state = item.state
            let heading = state.heading
            //console.log(1234, state, state.entries)
            if (state.entries && state.entries.length) {
                for (let x of state.entries) {
                    //console.log(5678, x)
                    console.log(x.dateOrRange.value, x.jobDescription,
                        x.model.text, x.model2, x.model3.text, x.model4,
                    )
                }
            }
        }
        console.log("maunzer lists have state:", subState)
        
    }



    onMounted(() => {
        //console.log(12345233, app, "app.refs" , getCurrentInstance().refs, "sections:", app.refs.sections)
        
        getSubState = () => {
            let subState = []
            for (let section of app.refs.sections) {
                let res = section.getState()
                subState.push({
                    state: res,
                })
            }
            return subState
        }


        mounted = true

    })




//https://stackoverflow.com/questions/68958446/how-to-access-this-keyword-in-script-setup-vue-sfc


    
    //var markdowns = this.$refs.markdowndetails.items wtf how to access this?


</script>