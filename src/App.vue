<template>
  <div class="container">
    <Header @toggle-add-task="toggleAddTask" title="Members" v-bind:showAddTask="showAddTask"/>
    <div v-if="showAddTask">
      <AddTask @add-task="addTask"/>
    </div>
    <div v-if="showEditTask">
      <EditTask @edit-task="editTask"/>
    </div>
    <Tasks @delete-task="deleteTask" @toggle-edit-task="toggleEditTask" :tasks="tasks"/>
  </div>
</template>

<script>
import Header from './components/Header.vue'
import Tasks from './components/Tasks.vue'
import AddTask from './components/AddTask.vue'
import EditTask from './components/EditTask.vue'

export default {
  name: 'App',
  components: {
    Header,
    Tasks,
    AddTask,
    EditTask
  },
  data(){
    return {
      tasks: [],
      showAddTask: false,
      showEditTask: false,
      editid: Number
    }
  },
  methods:{
    toggleAddTask(){
      this.showAddTask = !this.showAddTask
    },
    deleteTask(id){
      if(confirm('Are you sure?')){
         this.tasks = this.tasks.filter((task) => task.id !=id)
      }

    },
    addTask(task){
      this.tasks = [...this.tasks, task]
      this.showAddTask = !this.showAddTask
    },
    toggleEditTask(id){
      this.showEditTask = !this.showEditTask
      this.editid = id
    },
    editTask(task){
      for(let i=0;i<this.tasks.length;i++){
        if(this.tasks[i].id === this.editid){
          this.tasks[i].memberRole = task.memberRole;
          break;
        }
      }
      this.showEditTask = !this.showEditTask
    }
  },
  created(){
    this.tasks = [
        {
          id: 1,
          text: "Batman",
          memberRole: "Admin"
        },
        {
          id: 2,
          text: "Robin",
          memberRole: "Analyst"
        }
    ]
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap');
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: 'Poppins', sans-serif;
}
.container {
  max-width: 500px;
  margin: 30px auto;
  overflow: auto;
  min-height: 300px;
  border: 1px solid steelblue;
  padding: 30px;
  border-radius: 5px;
}
.btn {
  display: inline-block;
  background: #000;
  color: #fff;
  border: none;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 15px;
  font-family: inherit;
}
.btn:focus {
  outline: none;
}
.btn:active {
  transform: scale(0.98);
}
.btn-block {
  display: block;
  width: 100%;
}
</style>
