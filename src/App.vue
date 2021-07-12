<template>
  <div id="app">
    <input v-model="todo.label" type="text" name="" id="">
    <button @click="save">Save</button>
    <ul v-if="lists.length > 0">
      <li v-for="(item, index) in lists" :key="item.todo">
        <span :style="{ 'background-color': item.isCompleted ? 'green' : '#fff' }">{{ item.label }}</span>
        <input v-model="item.isCompleted" type="checkbox" name="" id="">
        <button @click="edit(item, index)">Edit</button>
        <button @click="remove(index)">Delete</button>
      </li>
    </ul>
    <p></p>
  </div>
</template>

<script>

export default {
  name: 'App',
  data () {
    return {
      todo: {},
      lists: [],
    }
  },
  methods: {
    save() {
      if(this.todo.id) {
        this.lists.forEach((item, index) => {
          if(index === this.todo.id) {
            this.lists[index].label = this.todo.label
          }
        })
        this.todo = {}
       return
      }
      this.lists.push({...this.todo, isCompleted: false})
      this.todo = {}

    },
    edit(item, index) {
      this.todo = {...item, id: index}
    },
    remove(idx) {
      this.lists = this.lists.filter((item, index) => index !== idx)
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
