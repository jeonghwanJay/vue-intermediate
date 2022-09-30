<template>
  <section>
    <transition-group name="list" tag="ul">
      <li v-for="(todoItem, index) in todoItems" class="shadow" v-bind:key="todoItem">
        <i class="checkBtn fa-solid fa-check" v-on:click="toggleComplete"></i>
          <span>{{todoItem}}</span> 
          <span class="removeBtn">
            <i class="removeBtn fa-solid fa-trash" v-on:click="removeTodo(todoItem,index)"></i>
          </span>
            
      </li>
    </transition-group> 
  </section>
</template>

<script>
export default {
data: function() {
  return {
    todoItems: [],
  }
},
  created: function() {
    if(localStorage.length > 0) {
      for (var i = 0; i < localStorage.length; i++) {
        this.todoItems.push(localStorage.key(i))
      } 
    }
  },
  methods: {
    removeTodo: function(todoItem, index) {
      localStorage.removeItem(todoItem)
      this.todoItems.splice(index,1)
    },
    toggleComplete: function() {
      console.log('ddd');
    }
  }
}
</script>

<style scoped>
ul {
  list-style-type: none;
  padding-left: 0px;
  margin-top: 0;
  text-align: left;
}
li {
  display: flex;
  min-height: 50px;
  height: 50px;
  line-height: 50px;
  margin: 0.5rem 0;
  padding: 0 0.9rem;
  background: white;
  border-radius: 5px;
}
.checkBtn {
  line-height: 45px;
  color: #62acde;
  margin-right: 5px;
}
.checkBtnCompleted {
  color: #b3adad;
}
.textCompleted {
  text-decoration: line-through;
  color: #b3adad;
}
.removeBtn {
  margin-left: auto;
  color: #de4343;
}
</style>