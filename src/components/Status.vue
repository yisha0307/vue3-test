<template>
    <div class='status-section'>
        <label for='all'>
            All
            <input type='radio' name='status' id='all' value='all' v-model='status'>
        </label>
        <br />
        <label for='completed'>
            Completed
            <input type='radio' name='status' id='completed' value='completed' v-model='status'>
        </label>
        <br />
        <label for='uncompleted'>
            Uncompleted
            <input type='radio' name='status' id='uncompleted' value='uncompleted' v-model='status'>
        </label>
        <br />
    </div>
</template>

<script>
import {reactive, toRefs, watch} from '@vue/composition-api'
export default {
  setup () {
    const data = reactive({
      status: 'all'
    })
    function watchFunc (val) {
      this && this.$emit('change', val)
    }
    watch(() => data.status, watchFunc)
    return {
      ...toRefs(data),
      watchFunc
    }
  }
}
</script>
