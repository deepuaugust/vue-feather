<template>
  <div class="container">
    <div class="row">
      <div class="col-md-6 col-md-offset-3">
        <!-- <div class="well">
          <quote-form @create="fetchQuotes"/>
        </div>-->
        <button type="button" class="btn-add" @click="showModal">Add Quote</button>
        <modal v-show="isModalVisible" @close="closeModal" />
        <loopy-button />
        <search />
      </div>
    </div>
  </div>
</template>

<script>
import Modal from "./components/Modal";
import LoopyButton from "./components/LoopyButton";
import Search from "./components/Search";

export default {
  data() {
    return {
      quotes: [],
      isModalVisible: false
    };
  },
  components: { Modal, LoopyButton, Search },
  methods: {
    showModal() {
      this.isModalVisible = true;
    },
    closeModal() {
      this.isModalVisible = false;
    },
  }
};
</script>

<style lang="scss" scoped>
.container {
  margin-top: 2em;
}
.btn-add {
  float: right;
}
</style>
