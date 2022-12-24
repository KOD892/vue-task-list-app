<template>
    <div class="container">
        <div class="row">
            <div class="col s12">
                <div id="main" class="card">
                    <Header @addTask="onAddTask" />
                    <Tasks @taskDone="done" @clearTasks="clear" @deleteTask="deleteTask" :tasks="tasks" />

                </div>

            </div>
        </div>
    </div>

</template>

<script>
import Header from './components/Header-file.vue'
import Tasks from './components/Tasks.vue'

export default {
  name: 'App',
  components: {
    Header,
    Tasks
    
  },
  data(){
    return {
      tasks:[]
    }
  },
  methods:{ 
    async getTasks(){
      const res = await fetch('http://localhost:5000/tasks');
        return await res.json()
    },
    async getTask(id){
      const res = await fetch(`http://localhost:5000/tasks/${id}`);
      return await res.json()
    },
    async onAddTask(task){
      const res = await fetch('http://localhost:5000/tasks',{
        method:'POST',
        headers:{
          'Content-type':'application/json'
        },
        body: JSON.stringify(task)
      })
      const data = await res.json()
      this.tasks.push(data)
    },
    clear(){
      if(confirm('Clear Tasks')){
        this.tasks = []
      }
    },
    async deleteTask(id){
      const res = await fetch(`http://localhost:5000/tasks/${id}`,{
        method:'DELETE'});
        
      res.status == 200 ?  this.tasks = this.tasks.filter((task)=> task.id !== id ) : alert('Error deleting task') 
    },
    async done(id){
      const tsk = await this.getTask(id);
      const updtask = {...tsk, 'done': !tsk.done}
      
      const res = await fetch(`http://localhost:5000/tasks/${id}`,{
          method:'PUT',
          headers:{
            'Content-type':'application/json'
          },
          body: JSON.stringify(updtask),
        })
        const data = await res.json();

        this.tasks = this.tasks.map((t)=> t.id==id ? {...t, done: data.done} : t );
    }

  },
  async created(){
     this.tasks = await this.getTasks()
  }
}
</script>

<style>


</style>
