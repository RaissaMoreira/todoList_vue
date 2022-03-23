<template>
  <div class="todo-list">
    <h3>Todo List</h3>
    <input
      type="text"
      class="input-new-item"
      v-on:keyup.enter="addNewItemToList"
    />

    <ul>
      <ListItem
        v-for="(item, index) in list"
        :key="index"
        :item="item"
        :index="index"
        @delete-item="deleteItem"
      />
    </ul>
  </div>
</template>

<script>
import ListItem from './ListItem'

export default {
  name: 'TodoList',

  components: {
    ListItem
  },

  data() {
    return {
      list: []
    }
  },

  created() {
    // converte JSON p/ objeto
    const itensInLocalStorage = JSON.parse(localStorage.getItem('list'))
    //necessary check to see if it is the first time.
    this.list = itensInLocalStorage ? itensInLocalStorage : []
  },

  methods: {
    addNewItemToList(event) {
      const newItem = event.target.value

      // unshift: adiciona item no início da lista
      this.list.unshift({
        label: newItem,
        checked: false
      })

      // limpar o campo
      event.target.value = ''
    },

    deleteItem(index) {
      this.list.splice(index, 1)
    },

    updateLocalStorage() {
      // add in localStorage
      // tranformando objeto em JSON p/ salvar no localStorage
      localStorage.setItem('list', JSON.stringify(this.list))
    }
  },

  watch: {
    // observar a list
    list() {
      this.updateLocalStorage()
    }
  }
}
</script>

<style scoped>
.todo-list {
  width: 500px;
  margin: auto;
}

.input-new-item {
  width: 80%;
  height: 30px;
}

ul {
  list-style: none;
  padding: 0;
  width: 80%;
  margin: 20px auto;
  text-align: left;
}
</style>
