<template>
  <div id="app">
    <div class="container">
      <!--Render Component-->
      <Header
        @toggle-add-task="toggleAddTask"
        title="Task App Tracker"
        :showAddTask="showAddTask"
      />
      <div v-show="showAddTask">
        <AddTask @add-task="addTask" />
      </div>
      <!--assign the emitted function to a method--->
      <Tasks
        @toggle-reminder="toggleReminder"
        @delete-task="deleteTask"
        :tasks="tasks"
      />

      <!--Using Default Value-->
      <!-- <Header /> -->
    </div>
  </div>
</template>
 

<script>
//import components
import Header from "./components/Header";
import Tasks from "./components/Tasks";
import AddTask from "./components/AddTask";

//register components
export default {
  name: "App",
  components: {
    Header,
    Tasks,
    AddTask,
  },

  data() {
    return {
      tasks: [],
      showAddTask: false,
    };
  },

  methods: {
    toggleAddTask() {
      //show add task form to whatever that is not (opposite)
      this.showAddTask = !this.showAddTask;
    },

    addTask(task) {
      this.tasks = [...this.tasks, task];
    },

    deleteTask(id) {
      if (confirm("Are you sure you want to delete this data?")) {
        this.tasks = this.tasks.filter((task) => task.id !== id);
      }
    },

    toggleReminder(id) {
      this.tasks = this.tasks.map((task) =>
        //check if task.id is = to id if true then change the reminder to opposite of current task else if not match to id then not
        task.id === id ? { ...task, reminder: !task.reminder } : task
      );
    },
  },

  created() {
    this.tasks = [
      {
        id: 1,
        text: "Doctors Appointment",
        day: "March 1st at 2:30pm",
        reminder: true,
      },

      {
        id: 2,
        text: "Meeting at School",
        day: "March 3rd at 1:30pm",
        reminder: true,
      },

      {
        id: 3,
        text: "Food Shopping",
        day: "March 4th at 2:30pm",
        reminder: false,
      },
    ];
  },
};
</script>


<!--styles-->
<style>
@import url("https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap");
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: "Poppins", sans-serif;
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
