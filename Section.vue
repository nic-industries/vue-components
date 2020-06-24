<template>
  <section class="section">
    <div class="section-content">
      <slot></slot>
    </div>
  </section>
</template>


<script lang="ts">
  import {Component, Prop, Vue} from "vue-property-decorator";
  @Component export default class Section extends Vue {}
</script>


<style lang="scss">
  .section {
    @include Convert\Pixel-Rem(margin-top, 60px);
    flex-direction: column;
    display: flex;
    width: 100%;
    &:not(:last-child) {
      @include Convert\Pixel-Rem(margin-bottom, -16px);
    }
    &-content {
      flex-direction: column;
      display: flex;
      width: 100%;
    }
  }
</style>