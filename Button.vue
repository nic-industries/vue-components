<template>

  <router-link v-if="link" v-slot="{href, navigate}" :to="link">
    <a :class="classes" :style="styles" :href="href" :disabled="disabled || loading" @click="navigate">
      <Icon v-if="loading" family="fas">spinner fa-spin</Icon>
      <Icon v-if="icon">{{icon}}</Icon>
      {{text}}
    </a>
  </router-link>

  <button v-else :class="classes" :style="styles" :type="type" :disabled="disabled || loading" @click="click">
    <Icon v-if="loading" family="fas">spinner fa-spin</Icon>
    <Icon v-if="icon">{{icon}}</Icon>
    {{text}}
  </button>

</template>

<script lang="ts">

  import Styles from "@nic-industries/ts-mixins/Styles";
  import Color from "@nic-industries/ts-mixins/Color";

  import {Component, Prop, Emit, Vue} from "vue-property-decorator";

  @Component({
    components: {
      Icon: () => import("@nic-industries/vue-components/Icon.vue")
    }
  })

  /**
   * @class Button
   * @description Vue component for displaying a button element.
   * @property icon The name of the {@link Icon} to display.
   * @example <Button>Click Me</Button>
   */

  export default class Button extends Vue {

    // Value component properties.
    @Prop({ default: "primary" }) color!:   string;
    @Prop({ default: "default" }) size!:   "default"|"medium"|"small"|"mini";
    @Prop({ default: "button" })  type!:   "button"|"submit"|"reset";
    @Prop({ default: "none "})    design!: "none"|"solid"|"outline"|"link";

    // Flag component properties.
    @Prop({ default: false }) loadingText!: string;
    @Prop({ default: false }) fullWidth!: boolean;
    @Prop({ default: false }) disabled!: boolean;
    @Prop({ default: false }) loading!:  boolean;
    @Prop({ default: false }) rounded!:  boolean;
    @Prop({ default: false }) borders!:  boolean;
    @Prop({ default: false }) link!:     string;
    @Prop({ default: false }) icon!:     string;


    @Emit() blur($event:  any) { return $event; }
    @Emit() focus($event: any) { return $event; }
    @Emit() click($event: any) { return $event; }


    get text() {

      let slots: any = this.$slots;
      return this.loadingText && this.loading ? this.loadingText : ('default' in slots ? slots['default'][0].text : "");

    }


    /**
     * @method classes
     * @description Generates a string of all applicable component classes.
     * @returns string
     */

    get classes() {

      let classes = ["btn", "text-600", "text-uppercase", "display-inline-flex", "justify-center", "items-center"];

      if(this.fullWidth) classes.push('w-full');
      if(this.design) classes.push(`btn-style-${this.design}`);
      if(this.size) classes.push(`btn-size-${this.size}`);
      if(this.rounded) classes.push("btn-rounded");

      return classes.join(" ");

    }


    /**
     * @method styles
     * @description Generates a string of all applicable component styles.
     * @returns string
     */

    get styles() {

      let styles = [];

      let color = Styles.RootVar(`--color-${this.color}`);

      styles.push(`--button-text-color: var(--color-${Color.Brightness(color) ? 'white' : 'black'});`);
      styles.push(`--button-color-light: rgba(${Color.Convert(color, "rgba", 0.05)});`);
      styles.push(`--button-hover-color: var(--color-${this.color}-800);`);
      styles.push(`--button-color: var(--color-${this.color});`);

      return styles.join(" ");

    }

  }
</script>

<style lang="scss">
  .btn {
    @include Transition((background-color, border-color, color));
    @include Convert\Pixel-Rem(letter-spacing, .5px);
    touch-action: manipulation;
    -webkit-appearance: button;
    -moz-appearance: button;
    white-space: nowrap;
    width: max-content;
    user-select: none;
    background: none;
    border-width: 0;
    cursor: pointer;
    z-index: 1;
    padding: 0;

    &:hover,
    &:focus-within {
      color: var(--button-color);
    }

    &-size-default {
      @include Convert\Pixel-Rem(padding-right, 20px);
      @include Convert\Pixel-Rem(padding-left, 20px);
      @include Convert\Pixel-Rem(font-size, 13px);
      @include Convert\Pixel-Rem(height, 46px);
    }

    &-size-medium {
      @include Convert\Pixel-Rem(padding-right, 16px);
      @include Convert\Pixel-Rem(padding-left, 16px);
      @include Convert\Pixel-Rem(font-size, 13px);
      @include Convert\Pixel-Rem(height, 40px);
    }

    &-size-small {
      @include Convert\Pixel-Rem(padding-right, 12px);
      @include Convert\Pixel-Rem(padding-left, 12px);
      @include Convert\Pixel-Rem(font-size, 12px);
      @include Convert\Pixel-Rem(height, 34px);
    }

    &-size-mini {
      @include Convert\Pixel-Rem(padding-right, 8px);
      @include Convert\Pixel-Rem(padding-left, 8px);
      @include Convert\Pixel-Rem(font-size, 11px);
      @include Convert\Pixel-Rem(height, 28px);
    }

    &-rounded {
      @include Convert\Pixel-Rem(border-radius, 3px);
    }

    &-style-solid {
      background-color: var(--button-color);
      color: var(--button-text-color);

      &:hover,
      &:focus-within {
        background-color: var(--button-hover-color);
        color: var(--button-text-color);
      }

    }

    &-style-outline {
      border: 2px solid var(--button-color);
      background-color: transparent;
      color: var(--button-color);

      &:hover,
      &:focus-within {
        background-color: var(--button-color);
        color: var(--button-text-color);
      }

    }

    &-style-link {
      color: currentColor;
      padding-right: 0;
      padding-left: 0;

      &:hover,
      &:focus-within {
        color: var(--button-color);
      }

    }

    .icon {
      @include Convert\Pixel-Rem(margin-right, 5px);
    }

  }
</style>