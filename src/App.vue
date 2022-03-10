<template>
  <div class="app">
    <header>
      <div class="order">
        <h4>Ordered by</h4>
        <button @click="handleClick('title')">Title</button>
        <button @click="handleClick('salary')">Salary</button>
        <button @click="handleClick('location')">Location</button>
  
      </div>
    </header>
    <JobAdd @addjob="handleAddJob"/>
    <JobsList :jobs="jobs" :order="order" @handleDelete="handleTheDelete"/>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from "vue";
import Job from "@/types/Job";
import JobsList from "./components/JobsList.vue";
import JobAdd from "./components/JobAdd.vue"
import OrderBy from "@/types/orderby";

export default defineComponent({
  name: "App",
  components: {
    JobsList,
    JobAdd
  },
  setup() {
    const jobs = ref<Job[]>([
      {
        title: "farm worker",
        location: "lon lon ranch",
        salary: 30000,
        id: "1",
      },
      {
        title: "quarryman",
        location: "death mountain",
        salary: 40000,
        id: "2",
      },
      {
        title: "flute player",
        location: "the lost woods",
        salary: 35000,
        id: "3",
      },
      { title: "fisherman", location: "lake hylia", salary: 21000, id: "4" },
      {
        title: "prison guard",
        location: "gerudo valley",
        salary: 32000,
        id: "5",
      },
    ]);

    const order = ref<OrderBy>("title");
    const handleClick = (term: OrderBy) => {
      order.value = term;

    };
  
    const handleTheDelete = (jobid:string):void =>{
      
        const newJobs = jobs.value.filter((job)=>{
          return job.id !== jobid
        })
        if(newJobs.length){
          jobs.value = newJobs
        }
    }

    const handleAddJob = (newjob:Job):void =>{
     
      const check = jobs.value.find((job)=>{
        return job.id === newjob.id
      })
      if(!check){
      jobs.value.push(newjob)
      }
     
    }

    

    return { jobs, handleClick, order, handleTheDelete,handleAddJob};
  },
});
</script>

<style>
header {
  text-align: center;
}
header .order {
  margin-top: 20px;
}
button {
  margin: 0 10px;
  color: #1195c9;
  border: 3px solid #1195c9;
  background: #d5f0ff;
  padding: 8px 16px;
  border-radius: 4px;
  cursor: pointer;
  font-weight: bold;
}
</style>
