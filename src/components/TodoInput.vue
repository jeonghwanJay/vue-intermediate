<template>
  <div class="inputBox shadow">
    <input type="text" v-model="newTodoItem" v-on:keyup.enter="addTodo">
    <span v-on:click="addTodo" class="addContainer">
      <i class="addBtn fa-solid fa-plus"></i>
    </span>

    <Alert-Modal v-if="showModal" @close="showModal = false">
        <!--
      you can use custom content here to overwrite
      default content
    -->
        <h3 slot="header">Warning!
          <i class="fa-solid fa-circle-xmark" v-on:click="closeModalBtn"></i>
        </h3>
        <h3 slot="body"> 텍스트를 입력하세요.</h3>
      </Alert-Modal>
  </div>
</template>

<script>
import AlertModal from './common/AlertModal.vue'
export default {
  data: function() {
    return {
      newTodoItem: '',
      showModal: false,
    }
  },
  methods: {
    addTodo: function() {
      if(this.newTodoItem !== '') {
        this.$emit('addTodoItem', this.newTodoItem)
        this.newTodoItem = '';
      } else {
        this.showModal = !this.showModal
      }
    },
    closeModalBtn: function() {
      this.showModal = false
    }
  },
  components: {
    AlertModal,
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
  width: 3rem;
  border-radius: 0 5px 5px 0;
}
.addBtn {
  color: white;
  vertical-align: middle;
  justify-content: center;
}
</style>