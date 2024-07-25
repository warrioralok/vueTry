<script setup>
 import { ref, onMounted } from "vue";
    const    name = ref('John Doe');
    const    status = ref("1");
    const    tasks = ref(['Task One', 'Tast Two', 'Task Three']);
    const    links =ref('http://google.com/');
    const    newTask = ref("");

    const togglestatus = () => {
           if(status.value === "1"){
            status.value = "2"
           }
           else if(status.value === "2"){
            status.value = "3"
           }
           else{
            status.value = "1"
           }
      
    }

    const addTask = () => {
       if(newTask.value.trim != ""){
          tasks.value.push(newTask.value)
          newTask.value = '';
       }
    }

    const deleteTask = (index) => {
      tasks.value.splice(index,1)
    }
    onMounted(async () => {
      try{
          const response = await fetch('https://jsonplaceholder.typicode.com/todos');
          const data = await response.json();
          tasks.value = data.map( (tasks) => tasks.title)
      }
      catch(error){
        console.log("Error Fetching Taks......")
      }
    })
</script>

<template>
  <h1>Vue Jobs {{ name }}</h1><br>
  <p v-if="status === '1'">visible</p>
  <p v-else-if="status === '2'">Semi visible</p>
  <p v-else>Not visible</p>
  <br>
  <form @submit.prevent="addTask">
    <label for="newTask">Add Task</label>
    <input type="text" id="newTask" name="newTask" v-model="newTask"/>
    <button type="submit">Submit</button>
  </form>
  <br>
  <ul>
    <li style="list-style: none;" v-for="(taks,index) in tasks" :key="taks">
       <span>{{ taks }}</span> <button @click="deleteTask(index)">X</button> 
    </li>
  </ul>
  <a :href="links">{{ links }}</a>
  <input type="text" v-model="links"/>
  <button @click="togglestatus">Click Me !!!</button>
</template>


