<template>
  <form class="flex-column" @submit="submit">
    <slot></slot>
  </form>
</template>

<script lang="ts">
  import {Component, Emit, Prop, Vue} from "vue-property-decorator";
  @Component export default class Form extends Vue {
    @Emit() submit($event: any) {
      return $event;
    }
  }
</script>