<template>
  <form class="form-inline">
    <div class="checkbox">
      <label>
        <input type="checkbox" v-model="isBordered"/>
        <span>Is bordered?</span>
      </label>
    </div>
    <div class="checkbox">
      <label>
        <input type="checkbox" v-model="isStriped"/>
        <span>Is striped?</span>
      </label>
    </div>
    <div class="checkbox">
      <label>
        <input type="checkbox" v-model="isHover"/>
        <span>Is hover?</span>
      </label>
    </div>
    <div class="form-group">
      <label>Cell Icon:</label>
      <select class="form-control" v-bind:value="icon" v-on:change="onIconChange">
        <option value="">None</option>
        <option value="ok">OK</option>
        <option value="pencil">Pencil</option>
        <option value="heart">Heart</option>
        <option value="heart-empty">Empty Heart</option>
      </select>
    </div>
  </form>
</template>

<script>
import _ from 'lodash'; // eslint-disable-line

function toggleClass(classes, className) {
  if (_.includes(classes, className)) {
    return _.without(classes, className);
  } else {
    return classes.concat(className);
  }
}

const classes = {
  bordered: 'table-bordered',
  striped: 'table-striped',
  hover: 'table-hover'
};

export default {
  props: ['icon', 'classes'],
  data() {
    return {
      sortKey: '',
      options: ['a', 'b'],
    };
  },
  computed: {
    isBordered: {
      get() {
        return this.classes.includes(classes.bordered);
      },
      set() {
        this.$emit('update:classes', toggleClass(this.classes, classes.bordered));
      }
    },
    isStriped: {
      get() {
        return this.classes.includes(classes.striped);
      },
      set() {
        this.$emit('update:classes', toggleClass(this.classes, classes.striped));
      }
    },
    isHover: {
      get() {
        return this.classes.includes(classes.hover);
      },
      set() {
        this.$emit('update:classes', toggleClass(this.classes, classes.hover));
      }
    },
  },
  methods: {
    onIconChange(e) {
      this.$emit('update:icon', e.target.value);
    }
  }
};
</script>

<style>

</style>
