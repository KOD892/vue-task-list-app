<template>
    <div class="card-content">
        <span class="card-title">{{ title }}</span>
        <div class="row">
                <form @submit.prevent="onSubmit">
                    <div class="input-field col s12">
                        <input v-model="task" type="text" name="task" id="task">
                        <label for="task">New Task</label>
                    </div>
                    <div id="btn">
                        <input type="submit" value="Add Task" class="btn">
                    </div>
                </form>
        </div>
    </div>
</template>

<script>
export default {
    name:'Header-file',
    data(){
        return {
           title:'Task List',
           task:'',
        }
    },
    methods:{
        onSubmit(){
             if(this.task !== ''){
             const newTask = {id:Math.floor(Math.random()*10000), task:this.task, done:false}
             this.task = ''
             this.$emit('addTask', newTask);
             }
             else{
                alert('Task cannot be empty ')
             }
            
        }
    }

}
</script>

<style scoped>
#btn{
    padding-left: 1.4% !important;
}
</style>