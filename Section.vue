<template>
  <section class="section">
    <div class="section-content">
      <div v-if="title" class="section-title flex flex-row justify-space-between items-flex-end mb-4">
        <h2 class="mb-0">{{title}}</h2>
        <a v-if="link" :href="link">{{linkText}}</a>
      </div>
      <slot></slot>
    </div>
  </section>
</template>


<script lang="ts">

  import {Component, Prop, Vue} from "vue-property-decorator";

  @Component export default class Section extends Vue {

    @Prop() title!: string;
    @Prop() link!: string;
    @Prop() linkText!: string;

  }
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
    &-title {
      > h2, > .h2 {
        line-height: 1;
      }
      > a {
        @include Convert\Pixel-Rem(margin-left, 25px);
        @include Convert\Pixel-Rem(font-size, 14px);
        font-weight: 600;
      }
    }
    &-content {
      flex-direction: column;
      display: flex;
      width: 100%;
    }
  }
</style>