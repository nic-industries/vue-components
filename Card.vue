<template>
  <div :class="classes" @focusin="focusin" @click="click">
    <slot></slot>
  </div>
</template>

<script lang="ts">

  import {Component, Emit, Prop, Vue} from "vue-property-decorator";

  /**
   * @class Card
   * @description Vue component for displaying a card element.
   * @property padding <boolean> Flag for adding padding to the card.
   * @property rounded <boolean> Flag for adding rounded corners to the card.
   * @example <Card></Card>
   */

  @Component export default class Card extends Vue {

    @Prop({ default: true }) padding!: boolean;
    @Prop({ default: true }) rounded!: boolean;

    @Emit() focusin($event: any) { return $event; }
    @Emit() click($event: any) { return $event; }


    /**
     * @method classes
     * @description Generates a string of all applicable component classes.
     * @returns string
     */

    get classes() {

      let classes = ['card'];

      if(!this.padding) classes.push("no-padding");
      if(!this.rounded) classes.push("no-radius");

      return classes.join(" ");
    }

  }

</script>

<style lang="scss">
  .card {
    @include Convert\Pixel-Rem(margin-bottom, 16px);
    @include Convert\Pixel-Rem(border-radius, 3px);
    @include Convert\Pixel-Rem(padding, 24px);
    box-shadow: 0 3px 6px -3px rgba(black, 0.3);
    background-color: white;
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
    &.no-radius {
      border-radius: 0;
    }
    &.no-shadow {
      box-shadow: none;
    }
  }
</style>