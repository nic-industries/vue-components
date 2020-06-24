<template>

  <router-link v-if="link" v-slot="{href, navigate}" :to="link">
    <a :class="classes" :style="styles" :href="href" @click="navigate">
      <Icon v-if="icon">{{icon}}</Icon>
      <slot></slot>
    </a>
  </router-link>

  <button v-else :class="classes" :style="styles" @click="click">
    <Icon v-if="icon">{{icon}}</Icon>
    <slot></slot>
  </button>

</template>

<script lang="ts">
  import {Component, Prop, Emit, Vue} from "vue-property-decorator";
  @Component({
    components: {
      Icon: () => import("@nic-industries/vue-components/Icon.vue")
    }
  }) export default class Button extends Vue {

    @Prop({ default: "primary" }) color!: string;
    @Prop( { default: "default" }) size!: "default"|"medium"|"small"|"mini";

    @Prop({ default: false }) disabled!: boolean;
    @Prop({ default: false }) loading!: boolean;
    @Prop({ default: false }) rounded!: boolean;
    @Prop({ default: false }) borders!: boolean;
    @Prop({ default: false }) link!: string;
    @Prop({ default: false }) icon!: string;

    get classes() {

      let classes = ["btn", "text-500", "text-uppercase", "display-inline-flex", "justify-center", "items-center"];

      if(this.color && !this.borders) classes.push(`bg-${this.color}`);
      if(this.color && this.borders) classes.push(`border-${this.color}`);

      if(this.size) classes.push(`btn-${this.size}`);
      if(this.rounded) classes.push("btn-rounded");

      return classes.join(" ");

    }

    get styles() {

      let styles = [];

      if(this.color) styles.push(`--button-color: var(--color-${this.color});`);
      if(this.color) styles.push(`--button-color-hover: var(--color-${this.color}-90);`);

      return styles.join(" ");

    }

    @Emit() blur($event:  any) { return $event; }
    @Emit() focus($event: any) { return $event; }
    @Emit() click($event: any) { return $event; }

  }
</script>

<style lang="scss">
  .btn {
    @include Transition((background-color, border-color, color));
    @include Convert\Pixel-Rem(padding-right, 20px);
    @include Convert\Pixel-Rem(padding-left, 20px);
    @include Convert\Pixel-Rem(font-size, 13px);
    @include Convert\Pixel-Rem(height, 46px);
    -webkit-appearance: button;
    -moz-appearance: button;
    touch-action: manipulation;
    white-space: nowrap;
    width: max-content;
    user-select: none;
    cursor: pointer;
    border-width: 0;
    z-index: 1;
    &:hover,
    &:focus-within {
      background-color: var(--button-color-hover);
    }
    &-medium {
      @include Convert\Pixel-Rem(padding-right, 16px);
      @include Convert\Pixel-Rem(padding-left, 16px);
      @include Convert\Pixel-Rem(font-size, 13px);
      @include Convert\Pixel-Rem(height, 40px);
    }
    &-small {
      @include Convert\Pixel-Rem(padding-right, 12px);
      @include Convert\Pixel-Rem(padding-left, 12px);
      @include Convert\Pixel-Rem(font-size, 12px);
      @include Convert\Pixel-Rem(height, 34px);
    }
    &-mini {
      @include Convert\Pixel-Rem(padding-right, 8px);
      @include Convert\Pixel-Rem(padding-left, 8px);
      @include Convert\Pixel-Rem(font-size, 11px);
      @include Convert\Pixel-Rem(height, 28px);
    }
    &-rounded {
      @include Convert\Pixel-Rem(border-radius, 3px);
    }
    &[class*=border-] {
      background-color: transparent;
      border-style: solid;
      border-width: 2px;
      &:hover,
      &:focus-within {
        border-color: var(--button-color-hover);
      }
    }
    .icon {
      @include Convert\Pixel-Rem(margin-right, 5px);
    }
  }
</style>