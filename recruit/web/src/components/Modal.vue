<template>
  <transition name="modal-fade">
    <div class="modal-backdrop">
      <div
        class="modal"
        role="dialog"
        aria-labelledby="modalTitle"
        aria-describedby="modalDescription"
      >
        <header class="modal-header" id="modalTitle">
          <slot name="header">ADD QUOTE</slot>
        </header>
        <section class="modal-body" id="modalDescription">
          <form @submit.prevent="onSubmit">
            <div class="form-group">
              <label for="exampleInputName">Author name</label>
              <input
                type="text"
                class="form-control"
                id="exampleInputName"
                placeholder="Name"
                v-model="name"
              />
            </div>
            <div class="form-group">
              <label for="exampleInputQuote">Quote</label>
              <input
                type="text"
                class="form-control"
                id="exampleInputQuote"
                placeholder="Quote"
                v-model="quote"
              />
            </div>
            <button type="submit" class="btn btn-default">Save quote</button>
          </form>
        </section>
        <footer class="modal-footer">
          <slot name="footer">
            <button type="button" class="btn-green" @click="close" aria-label="Close modal">Close</button>
          </slot>
        </footer>
      </div>
    </div>
  </transition>
</template>
<script>
export default {
  name: "modal",
  methods: {
    close() {
      this.$emit("close");
    },
    onSubmit() {
      this.$feathers
        .service("quotes")
        .create({
          author: this.name,
          text: this.quote
        })
        .then(() => this.$emit("create"));
      this.$feathers.service("quotes").on("created", val => {
        console.log("A new quote has been created", val);
      });
      this.close();
    }
  }
};
</script>
<style>
.modal-backdrop {
  position: fixed;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  background-color: rgba(0, 0, 0, 0.3);
  display: flex;
  justify-content: center;
  align-items: center;
}

.modal {
  position: relative;
  background: #ffffff;
  box-shadow: 2px 2px 20px 1px;
  overflow-x: auto;
  display: flex;
  flex-direction: column;
  flex-basis: 35%;
}

.modal-header,
.modal-footer {
  padding: 15px;
  display: flex;
}

.modal-header {
  border-bottom: 1px solid #eeeeee;
  color: #4aae9b;
  justify-content: space-between;
}

.modal-footer {
  border-top: 1px solid #eeeeee;
  justify-content: flex-end;
}

.modal-body {
  position: relative;
  padding: 20px 10px;
}

.btn-close {
  border: none;
  font-size: 20px;
  padding: 20px;
  cursor: pointer;
  font-weight: bold;
  color: #4aae9b;
  background: transparent;
}

.btn-green {
  color: white;
  background: #4aae9b;
  border: 1px solid #4aae9b;
  border-radius: 2px;
}
</style>