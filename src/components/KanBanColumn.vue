<style>
  @import '../css/card.css';
</style>

<!-- <script setup>
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

</script> -->

<script>
import draggable from "vuedraggable";
import KanBanCard from './KanBanCard.vue';
let tempTitle = "";
let tempDesc = "No description";
let id = 0;
export default {
    name: "kanbancolumn",
    components: {
        draggable,
        KanBanCard
    },
    props:['title', 'cards'],
    data() {
        return {
            isAddingCard: false,
            toggleDelete: false,
            list: this.cards
        };
    },
    methods: {

        updateTitleCard: function (s){
            tempTitle = s
        },

        updateDescCard: function (s){
            tempDesc = s
        },

        addCard: function (){
            this.list.push({
                id: id++,
                title: tempTitle, 
                desc: tempDesc
            })
            tempTitle = ""
            tempDesc = "No description"
        },
        removeCard: function (element){
            const index = this.list.indexOf(element); 
            if (index > -1) { 
                this.list.splice(index, 1);
            }
        }
    }
};
</script>


<template>
    <div>
        <v-col cols="auto" md="auto" style="min-width: 10em">
            <v-card >
                <v-card-item> 
                    <v-card-title>{{ this.title }}</v-card-title>
                </v-card-item>
                <draggable :list="this.list" group="columns">                    
                    <template #item="{element}">
                        <div class="border-margin">
                            <KanBanCard
                            :title="element.title"
                            :desc="element.desc"
                            @mouseover="toggleDelete = !toggleDelete"
                            />
                            <v-icon
                                icon="mdi-delete-circle"
                                @click="removeCard(element)"
                                v-show="toggleDelete"
                            >
                            </v-icon>
                        </div>
                    </template>
                </draggable>
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