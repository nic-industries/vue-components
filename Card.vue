<template>
  <div :class="`card ${!padding ? 'no-padding' : ''}`" @focusin="focusin" @click="click">
    <slot></slot>
  </div>
</template>

<script lang="ts">
  import {Component, Emit, Prop, Vue} from "vue-property-decorator";

  @Component export default class Card extends Vue {

    @Prop({ default: true }) padding!: boolean;

    @Emit() focusin($event: any) { return $event; }
    @Emit() click($event: any) { return $event; }

  }

</script>

<style lang="scss">
  .card {
    @include Convert\Pixel-Rem(margin-bottom, 16px);
    @include Convert\Pixel-Rem(border-radius, 3px);
    @include Convert\Pixel-Rem(padding, 24px);
    box-shadow: 0 3px 6px -3px rgba($Color\Default\Black, 0.3);
    background-color: $Color\Default\White;
    flex-direction: column;
    position: relative;
    overflow: hidden;
    display: flex;
    height: auto;
    width: 100%;
    flex: 1;
    &[for] {
      cursor: pointer;
    }
    &.no-padding {
      padding: 0;
    }
    &-no-radius {
      border-radius: 0;
    }
    &-no-shadow {
      box-shadow: none;
    }
    &-title {
      @include Convert\Pixel-Rem(border-top-right-radius, 4px);
      @include Convert\Pixel-Rem(border-top-left-radius, 4px);
      @include Convert\Pixel-Rem(margin-right, -24px);
      @include Convert\Pixel-Rem(margin-left, -24px);
      @include Convert\Pixel-Rem(margin-top, -24px);
      @include Convert\Pixel-Rem(font-size, 16px);
      @include Convert\Pixel-Rem(padding, 12px);
      background-color: $Color\Cerakote\Gray;
      color: $Color\Default\White;
      text-align: center;
      margin-bottom: 0;
    }
    &-image {
      @include Convert\Pixel-Rem(border-top-right-radius, 4px);
      @include Convert\Pixel-Rem(border-top-left-radius, 4px);
      @include Convert\Pixel-Rem(margin-bottom, 16px);
      @include Convert\Pixel-Rem(margin-right, -24px);
      @include Convert\Pixel-Rem(margin-left, -24px);
      @include Convert\Pixel-Rem(margin-top, -24px);
      max-width: calc(100% + 48px);
      min-width: calc(100% + 48px);
      width: calc(100% + 48px);
      > img {
        width: 100%;
      }
    }
  }
</style>