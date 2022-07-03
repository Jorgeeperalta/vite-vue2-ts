<template>
  <v-card>
    <h1>Soy un componente</h1>
    <v-text-field v-model="nombre" />
    {{ nombre }}
  </v-card>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import Teleport from 'vue2-teleport';

@Component({ components: { Teleport } })
export default class About extends Vue {
  nombre: string = '';
}
</script>
