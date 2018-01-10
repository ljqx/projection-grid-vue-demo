<template>
  <div class="demo">
    <div class="panel panel-primary">
      <div class="panel-heading">
        <h3>Projection Grid for VueJs</h3>
      </div>
      <div class="panel-body">
        <Form :classes.sync="classes" :icon.sync="icon" />
      </div>
      <ProjectionGrid :config="config" />
    </div>
  </div>
</template>

<script>
import ProjectionGrid from 'projection-grid-vue';
import _ from 'lodash';

import Form from './components/Form';
import IconedCell from './components/IconedCell';
import data from './data.json';

class DataSource {
  constructor({ data, callback }) {
    this.data = data;
    this.callback = callback;
  }
}

export default {
  components: { Form, ProjectionGrid },
  data() {
    return {
      sortBy: null,
      data: data.value,
      classes: [],
      icon: '',
    };
  },

  computed: {
    config() {
      return {
        classes: ['table'].concat(this.classes),
        data: this.data,
        caption: { content: 'Projection Grid Vue Demo' },
        cols: [{
          key: 'UserName',
          $td: {
            content: ({ isHeader, data }, content) => ({
              Component: IconedCell,
              props: { content, icon: this.icon },
            })
          },
          sorting: this.sortBy === 'UserName',
        },
        { key: 'FirstName' },
        { key: 'LastName' },
        {
          key: 'Emails',
          $td: {
            content({ isHeader, data }, { Component, props }) {
              if (isHeader) {
                return { Component, props };
              }
              return {
                Component,
                props: {
                  text: props.text.join(' & ')
                }
              };
            }
          }
        }],
        primaryKey: "UserName",
        projections: [],
        tfoot: {
          trs: [{
            content: 'foooooooooooooooooooot placeholder',
          }],
        },
        sorting: {
          $td: {
            styles: {
              background: 'pink',
            },
          },
          onSort: ({ key }) => {
            this.sortBy = key;
            this.data = _.sortBy(this.data, key);
          },
        },
      };
    },
  },

};

</script>
