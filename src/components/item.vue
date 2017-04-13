<template>
  <li @mouseenter="toggleColor(true)" @mouseleave="toggleColor(false)" :style="{background:color}">
    <label>
      <input type="checkbox" v-model="todo.checked"/>
      <span>{{todo.text}}</span>
    </label>
    <button class="btn btn-danger" v-show="isIn" @click="removeTodo">删除</button>
  </li>
</template>
<script>
    export default{
      data () {
        return {
            color: 'white',
            isIn: false
        }
      },
      props: {
        todo: Object
      },
      methods: {
        toggleColor (isEnter) {
          if(isEnter){
            this.color = '#eee'
            this.isIn = true
          }else{
            this.color = 'white'
            this.isIn = false
          }
        },
        removeTodo () {
          let text = this.todo.text
          if (window.confirm(`确定删除${text}评论吗？`)) {
            this.$dispatch('deleteTodo', this.todo)
          }

        }
      }
    }
</script>
<style>
  /*item*/
  li {
    list-style: none;
    height: 36px;
    line-height: 36px;
    padding: 0 5px;
    border-bottom: 1px solid #ddd;
  }

  li label {
    float: left;
    cursor: pointer;
  }

  li label li input {
    vertical-align: middle;
    margin-right: 6px;
    position: relative;
    top: -1px;
  }

  li button {
    float: right;
    display: none;
    margin-top: 3px;
  }

  li:before {
    content: initial;
  }

  li:last-child {
    border-bottom: none;
  }
</style>
