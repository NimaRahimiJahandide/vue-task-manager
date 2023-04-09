<template>
  <div class="container">
      <Header @toggle-add-task="toggleAddTask" title="Task Tracker" :showAddTask="showAddTask"/>
      <div v-if="showAddTask">
        <AddTask @add-task="addTask"/>
      </div>
      <Task @toggle-reminder="toggleReminder" @delete-task="deleteTask" :tasks="tasks"/>
    </div>
</template>

<script>
import Header from './components/Header.vue';
import Task from './components/Tasks.vue';
import AddTask from './components/AddTask.vue';

export default{
  name: 'App',
  components: {
    Header,
    Task,
    AddTask
  },
  data(){
    return {
      tasks: [],
      showAddTask: false
    }
  },
  created(){
    this. tasks =[
      {
        id: 1,
        text: 'Doctor Appointment',
        day: 'March 1st at 2:30pm',
        reminder: true
      },
      {
        id: 2,
        text: 'Meeting at School',
        day: 'March 3rd at 1:30pm',
        reminder: true
      },
      {
        id: 3,
        text: 'Food Shopping',
        day: 'March 3rd at 11:00pm',
        reminder: false
      },
    ]
  },
  methods:{
    deleteTask(id){
      if (confirm('Are you sure?')) {
        this.tasks = this.tasks.filter((task) => task.id !== id)
      }
    },
    toggleReminder(id){
      this.tasks = this.tasks.map((task)=>task.id === id ? {...task, reminder: !task.reminder} : task)
    },
    addTask(task){
      this.tasks = [...this.tasks, task]
    },
    toggleAddTask(){
      this.showAddTask = !this.showAddTask
    }
  }
}


</script>


<style>
body {
  font-family: sans-serif;
}
.container {
  max-width: 500px;
  margin: 30px auto;
  overflow: auto;
  min-height: 300px;
  border: 1px solid steelblue;
  padding: 30px;
  border-radius: 5px
}
.btn{
  display: inline-block;
  background-color: #000;
  color: #fff;
  border: none;
  padding: 10px 20px ;
  margin: 5px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 15px;
  font-family: inherit;
}


</style>
