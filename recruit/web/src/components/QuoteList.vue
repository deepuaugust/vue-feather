<template>
  <ul class="list-group" v-if="getUnique()>0">
    <editable-quote v-bind:authors="authors" v-bind:groups="groups" />
  </ul>
  <div class="panel-body" v-else>
    <p>No quotes found.</p>
  </div>
</template>

<script>
import EditableQuote from "./EditableQuote";

export default {
  components: { EditableQuote },
  data: {
    authors:[],
    groups: {},
  },
  props: {
    quotes: { type: Array, default: [] }
  },
  methods: {
    getUnique: function() {
      const groups = {};
      this.quotes.forEach(obj => {
        if (!groups.hasOwnProperty(obj.author)) {
          groups[obj.author] = [];
        }
        groups[obj.author].push(obj);
      });
      this.authors = Object.keys(groups);
      this.groups = groups;
      return this.authors.length;
    },
  }
};
</script>

<style lang="scss" scoped>
</style>
