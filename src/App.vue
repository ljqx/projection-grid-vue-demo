<template>
	<projection-grid :config="config" />
</template>

<script>
import ProjectionGrid from 'projection-grid-vue';
import _ from 'lodash';

import IconedCell from './components/iconed-cell.vue';
import data from './data.json';

class DataSource {
  constructor({ data, callback }) {
    this.data = data;
    this.callback = callback;
  }

  projection() {
    
  }
}

export default {
	components: { ProjectionGrid },
	data() {
		return {
			sortBy: null,
			data: data.value,
		};
	},

  computed: {
    config() {
      return {
        classes: ['mui-table', 'mui-table--bordered'],
        data: this.data,
        caption: { content: 'Projection Grid Vue Demo' },
        cols: [{
          key: 'UserName',
          $td: {
            content({ isHeader, data }, content) {
              return {
                Component: IconedCell,
                props: { content, icon: 'pencil' },
              };
            }
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
