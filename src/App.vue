<template>
  <v-app>
    <v-main>
      <v-row class="global-padding">        
        <div v-for="(col, i) in columns" :key="i" >
          <KanBanColumn
              :title="col.columnTitle"
              :cards="col.columnCards"
              :color="col.columnColor"
              :cardColor="col.cardColor"
          />
        </div>
      </v-row>
    </v-main>
    <!-- <v-footer app>
      <v-text-field
      label="Add a column"
      @update:model-value="updateTempName"
      >
    </v-text-field>
    </v-footer> -->
  </v-app>
</template>

<script setup>
import KanBanColumn from './components/KanBanColumn.vue';

let columns = []
let tempColumnName = ""

// Add example columns
columns.push(
  {
    columnTitle:"To Do",
    columnCards: [],
    columnColor: "#ff0000",
    cardColor: "#990000"
  }
)
columns.push(
  {
    columnTitle:"In Progress",
    columnCards: [],
    columnColor: "#00ff00",
    cardColor: "#009900"
  }
)
columns.push(
  {
    columnTitle:"Done",
    columnCards: [],
    columnColor: "#0000ff",
    cardColor: "#000099"
  }
)

function addColumn(){
  console.log(tempColumnName)
  if(tempColumnName.length > 0){
    columns.push(
      {
        columnTitle:tempColumnName,
        columnCards: []
      }
    )
    console.log(columns)
    tempColumnName = ""
  }
}

function updateTempName(s){
  tempColumnName = s
  console.log(tempColumnName)
}

</script>
