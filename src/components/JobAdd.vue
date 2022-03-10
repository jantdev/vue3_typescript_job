<template>
  <div class="addjob">
      <form @submit.prevent="handleSubmit">
          <fieldset>
              <legend>Add Job</legend>
              <label for="title">Title:</label>
              <input type="text" name="title" v-model="newJob.title">
              <label for="location">location</label>
              <input type="text" name="location" v-model="newJob.location">
              <label for="salary">salary</label>
              <input type="text" name="salary" v-model="newJob.salary">
              <input type="submit" value="Submit" @click.once="handleSubmit">
          </fieldset>
      </form>  
  </div>
</template>

<script lang="ts">
import {defineComponent, reactive} from "vue"
import Job from "@/types/Job";
export default defineComponent({


setup(_,{emit}){



const newJob = reactive({
    title:"",
    location:"",
    salary:0,
    id:""
} as Job)

const handleSubmit = () =>{
    if(newJob.title !=="" && newJob.location!=="" && newJob.salary!==0){
        const deReact = {...newJob};
        deReact.id = Math.random()*100+""
        emit("addjob",deReact)
    }
    clearForm()
}

const clearForm = ()=>{
    newJob.title = ""
    newJob.location = ""
    newJob.salary = 0
}



return{newJob,handleSubmit}

}

})
</script>

<style>

</style>