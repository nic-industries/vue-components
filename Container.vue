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
    @include Viewport\Min($Viewport\SM) {
      @include Convert\Pixel-Rem(padding-right, $Container\Padding);
      @include Convert\Pixel-Rem(padding-left, $Container\Padding);
    }
  }
</style>