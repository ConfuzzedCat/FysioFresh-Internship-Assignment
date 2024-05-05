<style>
  @import '../css/card.css';
</style>

<script setup>
import { ref } from "vue"
let props = defineProps(['title', 'desc'])
const isTitleEditing = ref(false)
const isDescEditing = ref(false)

console.log("Card props:", props.title, props.desc)

function updateTitle(s){
    let tprops = props
    if(s.length > 0){
        props = {
            title: s,
            desc: tprops.desc
        }
    }
    console.log(props)
}

function updateDesc(s){
    let tprops = props
    props = {
        title: tprops.title,
        desc: s
    }
    console.log(props)
}
</script>

<template>
    <div class="border-spacing">
        <v-card>
        <v-card-item> 
            <v-card-title >
                <v-text-field 
                    @update:model-value="updateTitle" 
                    @click:append="isTitleEditing = !isTitleEditing" 
                    :label="props.title" 
                    append-icon="mdi-check-circle" 
                    v-if="isTitleEditing"></v-text-field>
                <p v-else 
                    @click="isTitleEditing = !isTitleEditing"
                >{{ props.title }}</p>
            </v-card-title>
        </v-card-item>
        <v-card-text>
            <v-text-field 
                    @update:model-value="updateDesc" 
                    @click:append="isDescEditing = !isDescEditing" 
                    :label="props.desc" 
                    append-icon="mdi-check-circle" 
                    v-if="isDescEditing"></v-text-field>
                <p v-else 
                    @click="isDescEditing = !isDescEditing"
                >{{ props.desc }}</p>
        </v-card-text>
      </v-card>
    </div>
</template>