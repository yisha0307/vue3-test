<template>
    <div class='input-section'>
        <h2>TODO LIST</h2>
        <input type='text' v-model="todoContent" @keyup.enter="submit">
    </div>
</template>

<script>
import {reactive, toRefs} from '@vue/composition-api'
export default {
  setup (props, context) {
    const data = reactive({
      todoContent: ''
    })
    function submit () {
      context.emit('submit', data.todoContent)
      data.todoContent = ''
    }
    return {
      ...toRefs(data),
      submit
    }
  }
}
</script>
