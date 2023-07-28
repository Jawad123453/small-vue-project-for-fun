<template>
  <div class="job-list">
    <p>Order by {{ order }}</p>
    <transition-group name="list" tag="ul">
      <li v-for="job in orderedJobs" :key="job.id">
        <h2>{{ job.title }} in {{ job.loaction }}</h2>
        <div class="salary">
          <p>{{ job.salary }} rupees</p>
        </div>
        <div class="description">
          <p>Lorem ipsum, dolor sit amet consectetur adipisicing elit. Saepe odio eum voluptas molestiae tenetur maiores minima officia pariatur magni nesciunt animi, beatae impedit doloribus a. Laudantium omnis perspiciatis non suscipit.</p>
        </div>
      </li>
    </transition-group>
  </div>
</template>

<script lang="ts">
import type { Job } from "../Newtypes/Jobs";
import type { Ordertrem } from "../Newtypes/Ordertrems";
import { computed, defineComponent, type PropType } from 'vue';

export default defineComponent({
  props:{
    jobs:{
      required:true,
      type:Array as PropType<Job[]>
    },
    order:{
      required:true,
      type:String as PropType<Ordertrem>
    }
  },
  setup(props) {
    const orderedJobs = computed(() => {
      return [...props.jobs].sort((a: Job, b: Job) => {
        return a[props.order] > b[props.order] ? -1 : 1
      })
    })
    return {orderedJobs}
  }
})
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

  .list-move{
    transition: all 1s;
  }
</style>