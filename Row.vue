<template>
  <div :class="classes">
    <slot></slot>
  </div>
</template>

<script lang="ts">
  import {Component, Prop, Vue} from "vue-property-decorator";

  @Component export default class Row extends Vue {

    @Prop({ default: "flex-start" }) justify!: string;
    @Prop({ default: "initial" }) align!: string;

    get classes() {

      let classes = ["row"];

      if(this.justify) classes.push(`justify-${this.justify}`);
      if(this.align) classes.push(`align-${this.align}`);

      return classes.join(" ");

    }

  }

</script>

<style lang="scss">
  .row {
    justify-content: flex-start;
    flex-direction: row;
    flex-wrap: wrap;
    display: flex;
    @each $justify in (flex-start, flex-end, center, space-between, space-around, space-evenly, initial) {
      &.justify-#{$justify} {
        justify-content: $justify;
      }
    }
    @each $align in (flex-start, flex-end, center, initial) {
      &.align-#{$align} {
        align-items: $align;
      }
    }
    &:not(.no-margins) {
      @include Convert\Pixel-Rem(margin-right, -8px);
      @include Convert\Pixel-Rem(margin-left, -8px);
      min-width: calc(100% + 16px);
    }
  }
</style>