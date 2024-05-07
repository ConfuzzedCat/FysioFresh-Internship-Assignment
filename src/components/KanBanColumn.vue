<style>
  @import '../css/card.css';
</style>

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
    props:['title', 'cards', 'color', 'cardColor'],
    data() {
        return {
            isAddingCard: false,
            isHovering: false,
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
            if(tempTitle.length > 0){
                this.list.push({
                    id: id++,
                    title: tempTitle, 
                    desc: tempDesc,
                    color: this.cardColor
                })
                tempTitle = ""
                tempDesc = "No description"
            }
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
    <div class="columns">
        <v-col cols="auto" md="auto">
            <v-card
            :color="this.color"
            @mouseover="isHovering = true" 
            @mouseleave="isHovering = false">
                <v-card-item> 
                    <v-card-title>{{ this.title }}</v-card-title>
                </v-card-item>
                <draggable :list="this.list" group="columns" :key="this.title">                    
                    <template #item="{element}">
                        <div class="border-margin">
                            <KanBanCard
                            :title="element.title"
                            :desc="element.desc"
                            :color="this.cardColor"
                            @delete="removeCard(element)"
                            />
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
                    <Transition>
                        <div v-if="isHovering">
                            <v-btn v-if="isAddingCard" icon="mdi-check-circle" @click="[isAddingCard = !isAddingCard, addCard()]"></v-btn>
                            <v-btn icon="mdi-plus" variant="tonal" @click="isAddingCard = !isAddingCard"></v-btn>
                        </div>
                    </Transition>
                </v-card-actions>                
            </v-card>
        </v-col>
    </div>
</template>