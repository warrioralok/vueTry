<script>
  export default{
    data(){
      return{
        name: 'John Doe',
        status: "1",
        tasks: ['Task One', 'Tast Two', 'Task Three'],
        links:'http://google.com/',
      }
    },
      methods:{
        togglestatus(){
           if(this.status === "1"){
                this.status = "2"
           }
           else if(this.status === "2"){
              this.status = "3"
           }
           else{
              this.status = "1"
           }
           console.log(this.status);
      }
    }
  }
</script>

<template>
  <h1>Vue Jobs {{ name }}</h1><br>
  <p v-if="status === '1'">visible</p>
  <p v-else-if="status === '2'">Semi visible</p>
  <p v-else>Not visible</p>
  <br>
  <br>
  <ul>
    <li style="list-style: none;" v-for="taks in tasks" :key="taks">{{ taks }}</li>
  </ul>
  <a :href="links">{{ links }}</a>
  <button @click="togglestatus">Click Me !!!</button>
</template>


