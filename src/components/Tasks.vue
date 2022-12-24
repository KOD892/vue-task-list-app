<template>
    <div class="card-action">
            <h5 class="card-title">Tasks</h5>
            <ul class="collection" v-for="task in tasks" :key="task.id" >
            <!-- tasks -->
             
                <Task @taskDone="$emit('taskDone',task.id)" @deleteTask="$emit('deleteTask',task.id)"  :task="task" />  
              
            </ul>
            <!-- problem -->
            <Button text="Clear Tasks"  @btnClick="$emit('clearTasks')" />
             
    </div>
</template>
<script>
import Button from './Button.vue';
import Task from './Task.vue'

export default {
    name:'Tasks-file',
    props:{
       tasks:Array
    },
    emits:['clearTask','deleteTask','taskDone'],
    components:{
        Button,
        Task
    }
}
</script>
