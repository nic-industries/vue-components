<template>
  <div :class="classes">
    <slot></slot>
  </div>
</template>

<script lang="ts">
  import {Component, Prop, Vue} from "vue-property-decorator";

  @Component export default class Column extends Vue {

    @Prop() sizes!: any;
    @Prop({ default: true  }) padding!: boolean;
    @Prop({ default: false }) auto!: boolean;
    @Prop({ default: false }) grow!: boolean;

    get classes() {

      let classes = ['col'];

      if(this.sizes) Object.keys(this.sizes).map(size => classes.push(`${size}:col-${this.sizes[size]}`));

      if(!this.padding) classes.push('no-padding');
      if(this.auto) classes.push('col-auto');
      if(this.grow) classes.push('col-grow');


      return classes.join(' ');
    }

  }
</script>

<style lang="scss">

  .col {
    flex-direction: column;
    display: inline-flex;
    flex: 0 1 auto;
    &:not(.no-padding) {
      @include Convert\Pixel-Rem(padding-right, 8px);
      @include Convert\Pixel-Rem(padding-left, 8px);
    }
  }

  @mixin Columns($prefix: '') {

    .#{$prefix}col-auto {
      flex: 1 0 auto;
      width: auto;
    }

    .#{$prefix}col-grow {
      flex: 1;
    }

    .#{$prefix}col-1\/1,
    .#{$prefix}col-full {
      flex: 0 1 100%;
      width: 100%;
    }

    @for $i from 1 through $Grid\MaxColumns {

      @for $j from 1 through $Grid\MaxColumns {

        @if $j > $i {

          .#{$prefix}col-#{$i}\/#{$j} {
            flex: 0 1 #{($i / $j) * 100%};
            width: #{($i / $j) * 100%};
          }

        }

      }

    }

  }

  @include Columns();

  @each $prefix, $breakpoint in $prefixes {
    @include Viewport\Min($breakpoint) { @include Columns($prefix); }
  }

</style>