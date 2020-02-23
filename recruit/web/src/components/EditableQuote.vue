<template>
  <ul>
    <li class="list-group-item" v-for="author in authors">
      {{author}}
      <ul>
        <li class="list-group-item" v-for="x in groups[author]">
          <span v-show="editable.indexOf(x._id)<0">{{x.text}}</span>
          <input v-show="editable.indexOf(x._id)!==-1" v-model="x.text" v-bind:id="x._id" />
          <button class="btn-del" type="button" @click="remove(x._id)">Delete</button>
          <button
            v-show="editable.indexOf(x._id)<0"
            v-bind:id="'btnedit_' + x._id"
            class="btn-del"
            type="button"
            @click="edit(x._id, author, x.text)"
          >Edit</button>
          <button
            v-show="editable.indexOf(x._id)!==-1"
            v-bind:id="'btnsave_' + x._id"
            class="btn-del"
            type="button"
            @click="save(x._id, author, x.text)"
          >Save</button>
        </li>
      </ul>
    </li>
  </ul>
</template>

<script>
export default {
  data() {
    return {
      editable: []
    };
  },
  props: {
    groups: { type: Object, required: true },
    authors: { type: Object, required: true }
  },
  methods: {
    remove(id) {
      this.$feathers
        .service("quotes")
        .remove(id)
        .then(() => this.$emit("remove"));
      this.$feathers.service("quotes").on("removed", val => {
        console.log("A quote has been removed", val);
      });
    },
    edit(id, auth, text) {
      this.editable.push(id);
    },
    save(id, auth, text) {
      this.$feathers
        .service("quotes")
        .update(id, {
          author: auth,
          text: text
        })
        .then(() => this.$emit("update"));
      this.$feathers.service("quotes").on("updated", val => {
        console.log("A quote has been updated", val);
      });
      const ind = this.editable.indexOf(id);
      this.editable.splice(ind, 1);
    }
  }
};
</script>

<style lang="scss" scoped>
.btn-del {
  float: right;
  margin-left: 10px;
}
</style>
