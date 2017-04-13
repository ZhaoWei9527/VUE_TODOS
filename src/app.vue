<template>
  <div class="todo-container">
    <div class="todo-wrap">
      <todo-header :add-item="addItem"></todo-header>
      <todo-main :todos="todos"></todo-main>
      <todo-footer :todos="todos"
                    :update="updateItem"
                   :remove="removeItem"
      ></todo-footer>
    </div>
  </div>
</template>
<script>
    import Header from './components/header'
    import Main from './components/main'
    import Footer from './components/footer'

    export default{
      data () {
        return {
          todos: [
            {id: 1, checked: false, text: '吃饭'},
            {id: 2, checked: true, text: '睡觉'},
            {id: 3, checked: false, text: '打豆豆'}
          ]
        }
      },
      methods: {
        addItem (todo) {
          this.todos.unshift(todo)
        },
        removeItem (todo) {
          this.todos.$remove(todo)
        },
        updateItem (value) {
            this.todos.forEach((todo) => {
              todo.checked = value
            })
        }
      },
      events: {
        'deleteTodo': function (todo) {
          this.removeItem(todo)
        }
      },
      components: {
        'todo-header': Header,
        'todo-main': Main,
        'todo-footer': Footer
      }
    }
</script>
<style>
  /*app*/
  .todo-container {
    width: 600px;
    margin: 0 auto;
  }
  .todo-container .todo-wrap {
    padding: 10px;
    border: 1px solid #ddd;
    border-radius: 5px;
  }
</style>
