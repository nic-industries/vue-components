<template>
  <div :class="classes" :style="styles">
    <div class="modal-content">
      <slot name="actions"></slot>
      <slot name="title"></slot>
      <slot name="content"></slot>
    </div>
    <div class="modal-shadow" @click.prevent="$store.dispatch('CloseModal')"></div>
  </div>
</template>

<script lang="ts">
  import {Component, Prop, Vue} from "vue-property-decorator";
  @Component export default class Avatar extends Vue {

    @Prop({ default: 800 }) width!: number;

    get classes() {

      let classes = ["modal"];

      return classes.join(' ');
    }

    get styles() {

      let styles = [];


      return styles.join(' ');
    }

  }
</script>

<style lang="scss"></style>