<template>
  <i :class="classes"></i>
</template>

<script lang="ts">
  import {Component, Prop, Vue} from "vue-property-decorator";
  @Component export default class Icon extends Vue {

    @Prop({ default: "fa" }) family!: string;
    @Prop({ default: false }) color!: string;
    @Prop({ default: 4 }) scale!: number;

    get classes() {

      let classes = ["icon", this.family, `fa-${this.icon}`];

      if(this.scale) classes.push(`font-size-${this.scale}`);
      if(this.color) classes.push(`color-${this.color}`);

      return classes.join(' ');
    }

    get icon() {

      let slots: any = this.$slots;

      return slots.default[0].text;
    }

  }
</script>

<style lang="scss">
  i {
    color: currentColor;
  }
</style>