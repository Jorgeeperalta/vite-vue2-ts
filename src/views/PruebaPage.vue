<template>
  <v-container class="about">
    <h1>This is Prueba page</h1>
    <v-btn @click="contador(10)">suma</v-btn>
    {{ count }}
    <Componente/>
  </v-container>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import Componente from '@/components/ComponentePrueba.vue';


import Teleport from 'vue2-teleport';

@Component({ components: {  Teleport, Componente } })
/** Home */
export default class Home extends Vue {
  // eslint-disable-next-line prettier/prettier
  count: number = 0;
  // eslint-disable-next-line prettier/prettier

  contador(numero: number): number {
    this.count += numero;
    return this.count;
  }
}
</script>
