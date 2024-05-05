<style>
  @import '../css/card.css';
</style>

<script setup>
import { ref } from "vue"
import KanBanCard from './KanBanCard.vue';
let props = defineProps(['title', 'cards'])
const isAddingCard = ref(false)

let tempTitle = ""
let tempDesc = "No description"

function updateTitleCard(s){
    tempTitle = s
}

function updateDescCard(s){
    tempDesc = s
}

function addCard(){
    let tprops = props

    tprops.cards.push({
        title: tempTitle, 
        desc: tempDesc
    })
    props = tprops
    tempTitle = ""
    tempDesc = "No description"
}

</script>


<template>
    <div>
        <v-col cols="auto" md="auto" style="min-width: 10em">
            <v-card >
                <v-card-item> 
                    <v-card-title>{{ props.title }}</v-card-title>
                </v-card-item>
                <div v-for="card in props.cards">
                    <div class="border-margin">
                        <KanBanCard
                            :title="card.title"
                            :desc="card.desc"
                        />
                    </div>
                </div>
                <div v-if="isAddingCard">
                    <v-text-field 
                        @update:model-value="updateTitleCard"  
                        label="Title">
                    </v-text-field>
                    <v-text-field 
                        @update:model-value="updateDescCard"  
                        label="Description">
                    </v-text-field>
                </div>                
                <v-card-actions class="justify-center">
                    <v-btn v-if="isAddingCard" icon="mdi-check-circle" @click="[isAddingCard = !isAddingCard, addCard()]"></v-btn>
                    <v-btn icon="mdi-plus" variant="tonal" @click="isAddingCard = !isAddingCard"></v-btn>
                </v-card-actions>                
            </v-card>
        </v-col>
    </div>
</template>