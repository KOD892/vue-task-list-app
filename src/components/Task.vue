<template>
      <li :id="task.done ? 'done' : ''" @dblclick="$emit('TaskDone',task.id)" class="collection-item">{{ task.task }}<a href="#" @click.prevent="$emit('deleteTask',task.id)" class="secondary-content"><i class="fa-solid fa-trash"></i> </a> </li>
</template>



<script>
export default {
    name:'Task-file',
    props:{
        task: Object
    }
    }
</script>
<style scoped>
#done {
    text-decoration: line-through !important;
    background: #ddd;
}
/* .fa-solid {
   color: red !important;
} */
</style>