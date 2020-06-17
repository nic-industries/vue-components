<template>
  <div class="container">
    <slot></slot>
  </div>
</template>

<script lang="ts">
  import {Component, Vue} from "vue-property-decorator";
  @Component export default class Container extends Vue {}
</script>

<style lang="scss">
  .container {
    max-width: $Container\Width;
    margin-right: auto;
    margin-left: auto;
    width: 100%;
  }
</style>