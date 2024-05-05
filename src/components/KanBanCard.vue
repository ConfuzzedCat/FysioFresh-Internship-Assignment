<style>
  @import '../css/card.css';
</style>

<script setup>
const props = defineProps(['title', 'desc'])

console.log("Cards Props", props.title, props.desc)
</script>

<template>
    <div class="border-padding">
        <v-card                        
            :title="props.title"
            :text="props.desc"
        ></v-card>
    </div>
</template>