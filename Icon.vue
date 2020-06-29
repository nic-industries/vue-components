<template>
  <i :class="classes"></i>
</template>

<script lang="ts">

  import {Component, Prop, Vue} from "vue-property-decorator";

  /**
   * @class Icon
   * @description Vue component for displaying an icon.
   * @property family The family of icons to use
   * @property color The color of the icon
   * @example <Icon>home</Icon>
   */

  @Component export default class Icon extends Vue {


    @Prop({ default: "fa" }) family!: "fa"|"fas"|"far"|"fal"|"fab";
    @Prop({ default: false }) color!: string;
    @Prop({ default: 4 }) scale!: number;


    /**
     * @method icon
     * @description Gets the icon name from the template slot.
     * @reference https://fontawesome.com/icons?d=listing&m=free
     * @example <Icon>icon-name-here</Icon>
     * @returns string
     */

    get icon() {

      return this.$slots['default'][0].text;

    }


    /**
     * @method classes
     * @description Generates a string of all applicable component classes.
     * @returns string
     */

    get classes() {

      let classes = ["icon", this.family, `fa-${this.icon}`];

      if(this.scale) classes.push(`font-size-${this.scale}`);
      if(this.color) classes.push(`color-${this.color}`);

      return classes.join(' ');
    }

  }
</script>

<style lang="scss">
  i {
    color: currentColor;
  }
</style>