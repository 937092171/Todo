<template>
  <div>
    <h1>任务清单</h1>
  </div>

  <hr>
  <todo-input @add="onAddNewTask"></todo-input>
  <todo-list :list="tasklist" class="mt-2"></todo-list>
  <todo-button v-model:active="activeBtnIndex"></todo-button>
</template>

<script>
import TodoList from './components/todo-list/TodoList.vue'
import TodoInput from './components/todo-list/TodoInput.vue'
import TodoButton from './components/todo-button/TodoButton.vue'

export default {
  name: 'MyApp',
  components: {
    TodoList,
    TodoInput,
    TodoButton
  },
  data() {
    return {
      // 任务列表的数据
      todolist: [
        { id: 1, task: '周一早晨9点开会', done: false },
        { id: 2, task: '周一晚上8点聚餐', done: false },
        { id: 3, task: '准备周三上午的演讲稿', done: true }
      ],
      // 下一个可用的id值
      nextId: 4,
      // 激活的按钮的索引
      activeBtnIndex: 0
    }
  },
  methods: {
    // TodoInput 组件 add 事件的处理函数
    onAddNewTask(taskname) {
      // 向任务列表中新增任务信息
      this.todolist.push({
        id:this.nextId,
        task:taskname,
        done:false, // 默认状态为 false
      })
      // 让 nextId 自增+1
      this.nextId++
    }
  },
  computed: {
    // 根据激活按钮的索引值，动态计算要展示的列表数据
    tasklist() {
      // 对“源数据”进行 switch...case 的匹配，并返回“计算之后的结果”
      switch(this.activeBtnIndex) {
        case 0 :
          return this.todolist
        case 1:
          return this.todolist.filter( x => x.done )
        case 2:
          return this.todolist.filter( x => !x.done)
      }
    }
  }
}
</script>

<style lang="less" scoped>
</style>