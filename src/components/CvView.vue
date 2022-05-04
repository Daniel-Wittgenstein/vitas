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
            <q-input outlined autogrow v-model="cvData.topText.left.text"
           
            class="q-mb-md" label="Left-hand header text (multiple lines allowed)" />

            <q-input outlined autogrow v-model="cvData.topText.right.text"
          
            class="q-mb-md" label="Right-hand header text (multiple lines allowed)" />

            <section-view
                v-on:update:title = "updateTitle"
                v-on:update:contents = "updateContents"
                ref="sections"
                :key="section.id" v-for="section in cvData.sections" :section="section"
                
                >
            </section-view>


        </div>
    </div>
    <div class="col-6 q-pa-md">
        <p>Preview</p>
        <div ref="cvparentdiv">

            <print-preview
                :key="304404309320489943" :cv-data="cvData"
                >
            </print-preview>

        </div>

    </div>

</div>



<button @click="exportCv" >Export</button>


</template>



<script setup>

function updateContents(sectionId, newData) {
    let cloned = JSON.parse(JSON.stringify(newData))
    //console.log(13,13, sectionId, newData, cloned)

    let foundSection = false
    for (let xsection of cvData.value.sections) {
        if (xsection.id === sectionId) foundSection = xsection
    }

    if (!foundSection) throw `Fatal error: cannot update contents of section`

    foundSection.entries = cloned
}

function updateTitle(section, title) {
    section.title = title
}

let addSection = (function() {
    let id = 0
    return (title = "No title", icon = false) => {
        id ++
        return {
            title: title,
            id: id,
            entries: [],
            icon: icon,
        }
    }
})()


let cvData = ref({
    
    picture: {
        image: "",
    },

    topText: {
        left: {
            text: ``,
        },
        right: {
            text: ``,
        },
    },

    footer: {
        text: ``,
    },

    sections: [
        addSection("Career / Education"),
        addSection("Awards"),
        addSection("Skills"),
        addSection("Languages"),
    ],

})



import { getCurrentInstance, onMounted, ref } from 'vue'
let app = getCurrentInstance()

import SectionView from 'components/SectionView.vue';

import PrintPreview from 'components/PrintPreview.vue';


import html2pdf from 'html2pdf.js'

const cvparentdiv = ref(null)





</script>