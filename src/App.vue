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
    columnCards: []
  }
)
columns.push(
  {
    columnTitle:"In Progress",
    columnCards: []
  }
)
columns.push(
  {
    columnTitle:"Done",
    columnCards: []
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
