<template>
  <div id="todolist">

    <input v-model="newTodo" v-on:keyup.enter="addTodo" />

    <ul class="lists">
      <li v-for="(item, index) in todolist"
          :key="index"
          @click="removeItem(index)"
          transition="item"
      >{{item.content}}</li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTodo: "",
      todolist: [
        {content: 'first todo'}
      ]
    }
  },
  methods: {
    addTodo() {
      let content = this.newTodo.trim();
      if(content.length > 0) {
        this.todolist.push({content: content});
        this.newTodo = "";
      }
    },
    removeItem(index) {
      this.todolist.splice(index, 1);
    },
  }
}
</script>


<style>

#todolist {
  border-top: 1px solid #000;
  text-align: left;
  padding: 8px;
}
#todolist input {
  width: 200px;
  padding: 4px;
  border-radius: 15px;
  border: 1px solid lightblue;
}
ul.lists {
  width: 80%;
  max-width: 200px;
  text-align: left;
}

ul.lists li {
  cursor: pointer;
}
ul.lists li:hover {
  color: lightcoral;
  text-decoration: line-through;
}

.fade-enter-active  { animation: go 2s }

@keyframes go {
  from { background: #fff; }
  to { background: #999; }
}

</style>
