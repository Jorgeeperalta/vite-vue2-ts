/* eslint-disable require-jsdoc */
<template>
  <v-container class="about">
    <h1>This is an aboutdfsa page</h1>
    <v-btn @click="contador(10)">suma</v-btn>
    {{ count }}
  </v-container>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';

import Teleport from 'vue2-teleport';

@Component({ components: { Teleport } })
/** Home */
export default class About extends Vue {
  count: number = 0;


  contador(numero: number): number {
    this.count += numero;
    return this.count;
  }
}
</script>
