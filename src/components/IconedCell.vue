<template>
  <div>
    <span>
      <component :is="content.Component" v-bind="content.props" />
    </span>
    <span :class="classes" v-if="icon" />
  </div>
</template>

<script>
import 'bootstrap/dist/css/bootstrap.min.css';

export default {
  props: ['content', 'icon'],
  computed: {
    classes() {
      return ['glyphicon', `glyphicon-${this.icon}`].join(' ');
    }
  }
}
</script>

<style>

</style>
