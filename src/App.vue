<template>
  <v-app>
    <v-main>
      <v-row>        
        <div v-for="col in columns">
          <KanBanColumn
            :title="col.columnTitle"
            :cards="col.columnCards"
          />
        </div>
      </v-row>
    </v-main>
  </v-app>
</template>

<script setup>
import KanBanColumn from './components/KanBanColumn.vue';

var columns = []
var cards = []
var testDesc = "This is a test Description."

// Add example cards
for(let i = 0; i < 5; i++){
  cards.push({
    title: `test${i}`, 
    desc: testDesc
  })
}

// Add example columns
columns.push(
  {
    columnTitle:"To Do",
    columnCards: cards
  }
)
columns.push(
  {
    columnTitle:"In Progress",
    columnCards: cards
  }
)
</script>
