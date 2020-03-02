<template>
    <div class='list'>
        <div class='list-item' v-for='item in list' :key='item.id'>
            <input
            type='checkbox'
            class='list-item-checkbox'
            :checked='item.completed'
            @click='toggleStatus($event, item.id)' >
            <div class='list-item-content'>{{item.content}}</div>
            <button class='list-item-delete' @click='deleteItem(item.id)'>Delete</button>
        </div>
    </div>
</template>

<script>
export default {
  props: {
    list: Array
  },
  setup (props, context) {
    console.log('----', props.list)
    function toggleStatus (e, id) {
      context.emit('toggle', {
        isChecked: e.target.checked,
        id
      })
    }
    function deleteItem (id) {
      context.emit('delete', id)
    }
    return {
      toggleStatus,
      deleteItem
    }
  }
}
</script>

<style scoped>
    .list {
      padding-top: 10px;
    }
    .list-item {
        display: flex;
        justify-content: space-between;
        align-items: center;
        border-bottom: 1px solid #ccc;
        padding: 5px 0;
    }
    .list-item-checkbox {
        width: 30px;
        height: 30px;
        flex: 0 0 30px;
    }
    .list-item-content {
        flex: 1 1 auto;
        overflow: hidden;
        text-overflow: ellipsis;
        white-space: nowrap;
        padding: 0 10px;
    }
    .list-item-delete {
        background: rgb(250, 56, 56);
        flex: 0 0 60px;
        text-align: center;
        color: #fff;
        font-size: 12px;
        height: 30px;
        line-height: 30px;
        border: none;
    }
</style>
