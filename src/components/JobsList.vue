<template>
  <div class="job-list">
    <p>Ordered by : {{ order }}</p>
    <transition-group name="list" tag="ul">
      <li v-for="job in orderedJobs" :key="job.id">
        <div class="card">
          <div class="header">
            <h4>{{ job.title }}</h4>
            <div class="delete" @click="$emit('handleDelete', job.id)">X</div>
          </div>

          <div class="salary">
            <p>{{ job.salary }} rupees</p>
          </div>
          <div class="description">
            <p>
              Lorem ipsum dolor sit amet consectetur, adipisicing elit. Rem
              omnis voluptatum eius doloremque optio iusto sequi dignissimos.
              Pariatur earum assumenda dolores possimus quidem quam,
              reprehenderit aliquid consequuntur amet non facere.
            </p>
          </div>
        </div>
      </li>
    </transition-group>
  </div>
</template>

<script lang="ts">
import { computed, defineComponent, PropType } from "vue";
import Job from "@/types/Job";
import OrderBy from "@/types/orderby";

export default defineComponent({
  props: {
    jobs: {
      required: true,
      type: Array as PropType<Job[]>,
    },
    order: {
      required: true,
      type: String as PropType<OrderBy>,
    },
  },
  setup(props) {
    const orderedJobs = computed(() => {
      return [...props.jobs].sort((a: Job, b: Job) => {
        return a[props.order] > b[props.order] ? 1 : -1;
      });
    });
    return { orderedJobs };
  },
});
</script>

<style scoped>
.job-list {
  max-width: 960px;
  margin: 40px auto;
}
.job-list ul {
  padding: 0;
}
.job-list li {
  list-style-type: none;
  background: white;
  padding: 16px;
  margin: 16px 0;
  border-radius: 4px;
}
.header {
  display: flex;
  align-items: center;
}
.header h4 {
  flex: 2;
}
.delete {
  color: red;
  cursor: pointer;
}
.job-list h2 {
  margin: 0 0 10px;
  text-transform: capitalize;
}
.salary {
  display: flex;
}
.salary img {
  width: 30px;
}
.salary p {
  color: #17bf66;
  font-weight: bold;
  margin: 10px 4px;
}
.list-move {
  transition: all 1s;
}
</style>
