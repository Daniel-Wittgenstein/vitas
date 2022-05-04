<template>

<!--
    <maunzer-list ref="maunzer" heading-text=""></maunzer-list>
    <maunzer-list ref="maunzer" heading-text=""></maunzer-list>
    <maunzer-list ref="maunzer" heading-text=""></maunzer-list>
    <maunzer-list ref="maunzer" heading-text=""></maunzer-list>
    -->

    <div class="row items-stretch">
        <div class="col-6 q-pa-md">
            <p>Create</p>
            <div>
                <q-input outlined autogrow v-model="headerLeftText"
                @change="this.headerTextChanged"
                class="q-mb-md" label="Left-hand header text (multiple lines allowed)" />

                <q-input outlined autogrow v-model="headerRightText"
                @change="this.headerTextChanged"
                class="q-mb-md" label="Right-hand header text (multiple lines allowed)" />

                <maunzer-list
                    ref="sections"
                    :key="section.id" v-for="section in sections" :heading-text="section.title"
                    @change="subListChanged(section)"
                    >
                </maunzer-list>
            </div>
        </div>
        <div class="col-6 q-pa-md">
            <p>Preview</p>
            <div ref="cvparentdiv">


            </div>

        </div>

    </div>



<button @click="exportCv" >Export</button>



</template>



<script setup>

    let headerLeftText = ref("")

    let headerRightText = ref("")

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

    function subListChanged() {
        changeHappened()
    }

    function headerTextChanged() {
        changeHappened()
    }

    function changeHappened() {
        if (!getSubState || !mounted) {
            alert("App is not fully loaded yet. Please wait a moment.")
            return
        }
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

        console.log(subState, headerLeftText.value, headerRightText.value)
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