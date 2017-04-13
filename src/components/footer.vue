<template>
  <div class="todo-footer">
    <label>
      <input type="checkbox" v-model="allChecked"/>
    </label>
    <span>
          <span>已完成{{checkedLength}}</span> / 全部{{todos.length}}
        </span>
    <button class="btn btn-danger" @click="removeItem">清除已完成任务</button>
  </div>
</template>
<script>
    export default{
      methods: {
        removeItem () {
            this.todos.filter(obj => {
              return obj.checked
            }).forEach(newTodo => this.remove(newTodo))
        }
      },
      props: {
        todos: Array,
        update: Function,
        remove: Function
      },
      computed: {
        checkedLength: function () {
          return this.todos.filter((obj) => {
            return obj.checked
          }).length
        },
        allChecked: {
          set: function (value) {
            this.update(value)
          },
          get: function () {
            return this.todos.filter(obj => !obj.checked).length === 0 && this.todos.length > 0
          }
        }
      }
    }
</script>
<style>
  /*footer*/
  .todo-footer {
    height: 40px;
    line-height: 40px;
    padding-left: 6px;
    margin-top: 5px;
  }

  .todo-footer label {
    display: inline-block;
    margin-right: 20px;
    cursor: pointer;
  }

  .todo-footer label input {
    position: relative;
    top: -1px;
    vertical-align: middle;
    margin-right: 5px;
  }

  .todo-footer button {
    float: right;
    margin-top: 5px;
  }
</style>
