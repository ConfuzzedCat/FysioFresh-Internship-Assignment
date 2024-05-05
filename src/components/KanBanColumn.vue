<script setup>
import KanBanCard from './KanBanCard.vue';
const props = defineProps(['title', 'cards'])
</script>


<template>
    <v-col cols="auto" md="auto">
        <p>{{ props.title }}</p>
        <div v-for="card in props.cards">
            <KanBanCard 
                :title="card.title"
                :desc="card.desc"
            />
        </div>
    </v-col>
</template>

<script>

</script>