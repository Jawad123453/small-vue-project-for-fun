<script lang="ts">
import { ref } from "vue"
import JoblistVue from "./components/Joblist.vue";
import {type Job} from "@/Newtypes/Jobs"
import {type Ordertrem} from "@/Newtypes/Ordertrems"
import { defineComponent } from "vue"

export default defineComponent({
  components:{JoblistVue},
  setup(){
    const jobs=ref<Job[]>([
      {title:"Jawad",loaction:"lebanon",salary:32121,id:"1" },
      {title:"Husam",loaction:"London",salary:2344,id:"2" },
      {title:"Ali",loaction:"USA",salary:31245,id:"3" },
      {title:"Alx",loaction:"Urob",salary:54223,id:"4" },
      {title:"Nour",loaction:"asad",salary:123,id:"5" },
    ])

    let order=ref<Ordertrem>('title')

    const handleClick=(trems:Ordertrem)=>{
      order.value=trems
    }
    return {jobs , order ,handleClick }
  }
})
</script>

<template>
  <div>
    <header>
      <div class="order">
        <button @click="handleClick('title')">Order by title</button>
        <button @click="handleClick('salary')">Order by salary</button>
        <button @click="handleClick('loaction')">Order by location</button>
      </div>
    </header>
    <JoblistVue :jobs="jobs" :order="order"/>
  </div>
</template>

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