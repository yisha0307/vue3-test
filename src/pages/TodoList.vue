<template>
    <div class='todo-list'>
        <InputSection @submit = 'submit'/>
        <Status @change = 'onStatusChanged'/>
        <TodoList
            :list='onShowList'
            @toggle='toggleStatus'
            @delete = 'onItemDelete'
        />
    </div>
</template>

<script>
import InputSection from '../components/Input'
import Status from '../components/status'
import TodoList from '../components/TodoList-section'
import {reactive, computed, toRefs} from '@vue/composition-api'
export default {
  components: {
    Status,
    TodoList,
    InputSection
  },
  setup () {
    const data = reactive({
    // 类似于vue2里的data()
      todoList: [],
      showingStatus: 'all',
      onShowList: computed(() => {
        if (data.showingStatus === 'all') {
          return data.todoList
        } else if (data.showingStatus === 'completed') {
          return data.todoList.filter(({completed}) => completed)
        } else if (data.showingStatus === 'uncompleted') {
          return data.todoList.filter(({completed}) => !completed)
        }
      })
    })
    function submit (content) {
      data.todoList.push({
        completed: false,
        content,
        id: parseInt(Math.random(0, 1) * 100000)
      })
      console.log(data.todoList)
    }
    function onStatusChanged (status) {
      console.log(status)
      data.showingStatus = status
    }
    function toggleStatus ({ isChecked, id }) {
      data.todoList.forEach(item => {
        if (item.id === id) {
          item.completed = isChecked
        }
      })
    }
    function onItemDelete (id) {
      let index = 0
      data.todoList.forEach((item, i) => {
        if (item.id === id) {
          index = i
        }
      })
      data.todoList.splice(index, 1)
    }
    return {
      ...toRefs(data),
      submit,
      onStatusChanged,
      onItemDelete,
      toggleStatus
    }
  }
}
</script>
