<template>
  <hr :class="classes" />
</template>

<script lang="ts">

  import {Component, Emit, Prop, Vue} from "vue-property-decorator";


  /**
   * @class Spacer
   * @description Vue component for displaying a vertical spacer element.
   * @property height The size multiplier that determines the height of the spacer.
   * @example <VerticalSpacer height="4" />
   */

  @Component export default class VerticalSpacer extends Vue {

    @Prop({ default: 4 }) height!: number;

    get classes() {

      let classes = ['vertical-spacer', 'display-flex', 'mt-0', `mb-${this.height}`];
      return classes.join(" ");

    }

  }

</script>


<style lang="scss">
  .vertical-spacer {
    background: none;
    border: none;
  }
</style>