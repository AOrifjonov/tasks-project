<template>
  <div class="container">
    <Header @toggle-add-task="toggleAddTask" title="Заметка" :showAddTask="showAddTask" />
    <div v-if="showAddTask">
        <AddTask @add-task="addTask" />
    </div>
    <Tasks @toggler-reminder="togglerReminder" @delete-task="deleteTask" :tasks="tasks" />
  </div>
</template>


<script>
import Header from "./components/Header.vue";
import AddTask from "./components/AddTask.vue";
import Tasks from "./components/Tasks.vue";
export default {
  components: {
    Header,
    Tasks,
    AddTask
  },

  data() {
    return {
      tasks: [],
      showAddTask: false,
    };
  },

  created() {
    this.tasks = [
      {
        id: 1,
        text: "Manchester City was created",
        day: "january 16th 2022 at 8:14pm",
        reminder: true,
      },
      {
        id: 2,
        text: "Barcelona was created",
        day: "january 16th 2022 at 8:15pm",
        reminder: true,
      },
      {
        id: 3,
        text: "Atletiko Madrid was created",
        day: "january 16th 2022 at 8:16pm",
        reminder: true,
      },
    ];
  },
  methods: {
    toggleAddTask(){
        this.showAddTask = !this.showAddTask;
    },

    deleteTask(id) {
      if (confirm(`Ushbu content o'chirilishiga rozimisiz?`)) {
        this.tasks = this.tasks.filter((task) => task.id !== id);
      }
    },
    togglerReminder(id){
        this.tasks = this.tasks.map((task) => task.id === id ? {...task, reminder: !task.reminder} : 
        task);
    },
    addTask(newTask){
        this.tasks = [...this.tasks, newTask]
    }
  },
};
</script>

<style>
/* @import url('https://fonts.googleapis.com/css2?family=Poppins:ital,wght@0,600;0,700;1,400;1,500;&display=swap'); */
* {
  box-sizing: border-box;
  padding: 0;
  margin: 0;
}

body {
  font-family: "poppins", sans-serif;
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
