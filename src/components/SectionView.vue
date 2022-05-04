<template>


    <q-card class="my-card bg-primary text-white maunzer-entry">
        <q-card-section>
            <div class="row inline items-center">

                <q-input
                    ref = "title-input"
                    bottom-slots v-model="title"
                    @change="$emit('update:title', section, title); finishEditingHeading();"
                    
                    label="Title for this section:" counter maxlength="200"
                    class = "force-white force-white2"
                    v-if="headingIsBeingEdited"
                    >

                    <template v-slot:before>
                    <q-icon name="work" />
                    </template>

                </q-input>

                <q-btn round flat icon="check"
                v-if = "headingIsBeingEdited"
                @click="finishEditingHeading"></q-btn>

                <div class="q-mr-md list-heading"
                v-if = "!headingIsBeingEdited"
                >{{section.title}}</div>
            
                <q-btn round flat icon="edit"
                v-if = "!headingIsBeingEdited"
                @click="editHeading(this)"></q-btn>


                <q-btn round flat icon="add_circle_outline"
                v-if = "!headingIsBeingEdited"
                @click="addItem"></q-btn>

            </div>

        </q-card-section>
    </q-card>






<!-- ############################ -->





    <draggable 
        v-model="myArray"
        group="people"
        @start="drag=true" 
        @end="drag=false"
        item-key="id">
        <template #item="{element}">

            <q-card class="my-card bg-secondary text-white maunzer-entry">
                <q-card-section>
                    

                    <p color="secondary" text-color="white"
                        class=""
                        v-if="!element.isBeingEdited && element.dateOrRange.value === 'range'">
                        from {{element.model.text}} {{element.model2}}
                        to {{element.model3.text}} {{element.model4}}:
                        {{element.jobDescription}}
                    </p>


                    <p color="secondary" text-color="white"
                        class=""
                        v-if="!element.isBeingEdited && element.dateOrRange.value === 'date'">
                        {{element.model.text}} {{element.model2}}:
                        {{element.jobDescription}}
                    </p>



                    <div class=" row inline items-center" v-if="element.isBeingEdited">


                        <q-select class="select-picker force-white q-mr-md" v-if="element.isBeingEdited"
                        outlined 
                            v-model="element.dateOrRange" :options="element.dateOrRangeOptions" 
                            option-label="text"
                            option-value="value"
                            dense>
                            <template v-slot:append>
                            
                            </template>
                        </q-select>


                        <q-badge color="secondary" text-color="white"
                        class="q-ml-lg"
                        v-if="element.dateOrRange.value === 'range'"
                        >
                        from
                        </q-badge>

                        <q-select class="select-picker q-mr-md force-white" v-if="element.isBeingEdited"
                        outlined
                            v-model="element.model" :options="element.options" 
                            option-label="text"
                            option-value="value"
                            dense>
                            <template v-slot:append>
                            <q-icon name="event" color="white" />
                            </template>
                        </q-select>

                        <q-select class="select-picker force-white" v-if="element.isBeingEdited"
                        outlined 
                            v-model="element.model2" :options="element.options2" 
                            dense>
                            <template v-slot:append>
                            <q-icon name="event" color="white" />
                            </template>
                        </q-select>



                        <q-badge color="secondary" text-color="white"
                        class="q-ml-lg"
                        v-if="element.dateOrRange.value === 'range'"
                        >
                        to
                        </q-badge>




                        <q-select class="select-picker q-mr-md force-white"
                            v-if="element.isBeingEdited && element.dateOrRange.value === 'range'"
                        outlined 
                            v-model="element.model3" :options="element.options3"
                            option-label="text"
                            option-value="value"
                            dense>
                            <template v-slot:append>
                            <q-icon name="event" color="white" />
                            </template>
                        </q-select>

                        <q-select class="select-picker force-white"
                            v-if="element.isBeingEdited && element.dateOrRange.value === 'range'"
                        outlined 

                            v-model="element.model4" :options="element.options4" 
                            dense>
                            <template v-slot:append>
                            <q-icon name="event" color="white" />
                            </template>
                        </q-select>

                            
                    </div>

                        

                    <q-input bottom-slots v-model="element.jobDescription"
                        label="Job description:" counter maxlength="200"
                        class = "force-white force-white2 q-mt-lg"
                        v-if="element.isBeingEdited"
                        >

                        <template v-slot:before>
                        <q-icon name="work" />
                        </template>

    <!--  
                        <template v-slot:append>

    <q-icon v-if="element.jobDescription !== ''"
                            name="close" @click="element.jobDescription = ''"
                            class="cursor-pointer" />
                        </template>

                        <template v-slot:hint>
                        Job ...
                        </template>-->
                    </q-input>



                    <q-btn v-if="!element.isBeingEdited" class="q-ml-sm"
                        round flat icon="edit" @click="editItem(element)" />

                    <q-btn v-if="!element.isBeingEdited"
                        round flat icon="delete" @click="deleteItem(element)" />
                    
                    <q-btn v-if="element.isBeingEdited" class="q-ml-sm"
                        round flat icon="check" @click="finishedEditing(element)" />
                    

                </q-card-section>
            </q-card>



    </template>
    </draggable>




</template>



<script setup>


import {ref, getCurrentInstance } from 'vue'

const app = getCurrentInstance()

import draggable from 'vuedraggable'

const props = defineProps({
    section: Object,
})

let drag = false

let myArray = ref([]) 

let title = ref(props.section.title)

const emit = defineEmits(['update:title', 'update:contents'])


let headingIsBeingEdited = ref(false)



function finishEditingHeading() {
    headingIsBeingEdited.value = false
}

function editHeading(that) {
    //myArray.forEach(n => n.isBeingEdited = false)
    headingIsBeingEdited.value = true
    setTimeout(() => {
        let input = that.$refs["title-input"]
        input.focus()
    }, 200);
}




//##################################################


function changeHappened() {
    console.log("change happened", app)
    emit('update:contents', props.section.id, myArray.value)
}

function editItem(element) {
    //console.log(myArray.value, element)
    myArray.value.forEach(n => n.isBeingEdited = false)
    element.isBeingEdited = true
}

function deleteItem(element) {
    myArray.value = myArray.value.filter(n => n !== element)
    changeHappened()

}

function finishedEditing(element) {
    element.isBeingEdited = false
    console.log(element, element.model)
    changeHappened()
}

function addItem() {
    let years = []

    let months = [
        {text: "January", value: "1"},
        {text: "February", value: "2"},
        {text: "March", value: "3"},
        {text: "April", value: "4"},
        {text: "May", value: "5"},
        {text: "June", value: "6"},
        {text: "July", value: "7"},
        {text: "August", value: "8"},
        {text: "September", value: "9"},
        {text: "October", value: "10"},
        {text: "November", value: "11"},
        {text: "December", value: "12"},
    ]
    for (let i = 2030; i > 1948; i--) {
            years.push(i + "")
    }
    let drOpts = [
        {
            text: "single date",
            value: "date",
        },

        {
            text: "from ... to ...",
            value: "range",
        }
    ]
    let id = crypto.randomUUID()
    myArray.value.push({
            name: "new entry " + id,
            id: id,
            model: {text: "January", value: "1"},
            options: months,                 
            model2: "2015",
            options2: years,
            model3: {text: "March", value: "3"},
            options3: months,                 
            model4: "2022",
            options4: years,
            dateOrRangeOptions: drOpts,
            dateOrRange: drOpts[1],
            jobDescription: "Customer Care at Dogs Inc.",
    
    })
    changeHappened()
}




</script>