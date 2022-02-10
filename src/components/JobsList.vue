<template>
    <div class="job-list">
        <ul>
            <li v-for="job in jobs" :key="job.id">{{job.title}}</li>
        </ul>
    </div>
</template>

<script lang="ts">
import { defineComponent,PropType } from 'vue'
import Job from '@/types/Job'
export default defineComponent({
    props:{
        jobs:{
            required:true,
            type:Array as PropType<Job[]>
        }
    },
    setup(props) {
        console.log(props)
    },
})
</script>

<style scoped>

</style>