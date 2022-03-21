<template>
  <div class="todo-list">
    <h3>Todo List</h3>
    <input type="text" v-on:keyup.enter="addNewItemToList">

    <ul>
      <li v-for="(item, index) in list" :key="index">
        <input type="checkbox" v-model="item.checked">
        {{ item.label }}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'TodoList',

  data() {
    return {
      list: []
    }
  },

  created() {
    // converte JSON p/ objeto
    // fazer a lista receber o que tem no localStorage
    const itensInLocalStorage = JSON.parse(localStorage.getItem('list'));
    this.list = itensInLocalStorage ? itensInLocalStorage : [];
  },

  methods: {
    addNewItemToList(event) {
      const newItem = event.target.value;

      // unshift: adiciona item no início da lista
      this.list.unshift({
        label: newItem, checked: false
      })

      // add in localStorage

      // tranformando objeto em JSON p/ salvar no localStorage
      localStorage.setItem('list', JSON.stringify(this.list));

      // limpar o campo
      event.target.value = '';
    }
  }
}
</script>

<style scoped>
ul {
  list-style: none;
  padding: 0;
}
</style>
