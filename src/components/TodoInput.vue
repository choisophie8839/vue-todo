<template>
    <div class="inputBox shadow">
      <input type="text" v-model="newTodoItem" @keyup.enter="addTodo">
      <span class="addContainer" @click="addTodo">
        <i class="fas fa-plus addBtn"></i>
      </span>
      <!-- use the modal component, pass in the prop -->
      <Modal v-if="showModal" @close="showModal = false">
        <!--
          you can use custom content here to overwrite
          default content
        -->
        <h3 slot="header">
          ALERT
          <i class="closeModalBtn fas fa-times" @click="showModal = false"></i>
        </h3>
        <div slot="body">Ooops, you didn't write anything</div>
        <div slot="footer"></div>
      </Modal>
    </div>
</template>

<script>
import Modal from "./common/Modal";
export default {
  name: "TodoInput",
  components: {
    Modal
  },
  data () {
      return {
        newTodoItem: "",
        showModal: false
      }
  },
  methods: {
    addTodo () {
      if (this.newTodoItem != '') {
        const text = this.newTodoItem.trim()
        this.$store.commit('addOneItem', text)
        this.clearInput()
      } else {
        this.showModal = !this.showModal
      }
    },
    clearInput () {
      this.newTodoItem = ''
    }
  }
}
</script>

<style scoped>
  input:focus {
    outline: none;
  }
  .inputBox {
    background: white;
    height: 50px;
    line-height: 50px;
    border-radius: 5px;
  }
  .inputBox input {
    border-style: none;
    font-size: 0.9rem;
  }
  .addContainer {
    float: right;
    background: linear-gradient(to right, #6478FB, #8763FB);
    display: block;
    border-radius: 0 5px 5px 0;
    width: 50px;
  }
  .addBtn {
    color: white;
    vertical-align: middle;
  }
  .closeModalBtn {
    color: #42b983;
  }
</style>
