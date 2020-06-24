<template>
  <figure :class="classes" :style="styles"></figure>
</template>

<script lang="ts">
  import {Component, Prop, Vue} from "vue-property-decorator";
  @Component export default class Avatar extends Vue {

    @Prop({ default: "primary" }) color!: string;
    @Prop({ default: true }) rounded!: boolean;

    @Prop() image!: string;
    @Prop() text!: string;

    @Prop({default: 36}) size!: number;

    get classes() {

      let classes = ["avatar", "display-flex", "justify-center", "items-center"];

      if(this.rounded) classes.push("rounded");
      if(this.color) classes.push(`bg-${this.color}`);

      return classes.join(' ');
    }

    get styles() {

      let styles = [];

      // Set the background image of the avatar.
      if(this.image) styles.push(`--avatar-image: url(${this.image});`);

      // Set the text of the avatar.
      if(this.text) styles.push(`--avatar-text: '${this.text}';`);

      // Set the width and height of the avatar.
      if(this.size) styles.push(`--avatar-size: ${this.size}px;`);

      return styles.join(' ');
    }

  }
</script>

<style lang="scss">
  .avatar {
    background-image: var(--avatar-image, none);
    background-position: center center;
    background-repeat: no-repeat;
    background-size: cover;
    line-height: var(--avatar-size, 36px);
    height: var(--avatar-size, 36px);
    width: var(--avatar-size, 36px);
    text-align: center;
    overflow: hidden;
    &::before {
      @include Convert\Pixel-Rem(letter-spacing, 1px);
      @include Convert\Pixel-Rem(padding-left, 2px);
      font-size: calc(var(--avatar-size, 36px) / 2);
      content: var(--avatar-text, '');
      line-height: 1;
      color: white;
    }
    &.rounded {
      border-radius: 100%;
    }
  }
</style>