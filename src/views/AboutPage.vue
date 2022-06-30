<template>
  <v-container class="about">
    <h1>This is an aboutdfsa page</h1>
    <v-btn @click="contador(10)">suma</v-btn>
    {{count}} 
  </v-container>
</template>

<script lang="ts">



/** Home */
export default  {
    data() {
    return {
      count: 0 as number, 
    }
  },
  methods: {
    contador(numero : number){
  
     return numero ++
     
    }
  }
}


</script>
