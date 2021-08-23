<template>
  <div class="app">
    <header>
      <div class="title">
        <img src="./assets/heart.svg" alt="site logo" />
        <h1>Hyrule Jobs</h1>
      </div>
      <div class="order">
        <button @click="handleClick('title')">order by title</button>
        <button @click="handleClick('salary')">order by salary</button>
        <button @click="handleClick('location')">order by location</button>
      </div>
    </header>
    <JobList :jobs="jobs" :order="order" />
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue'
import Job from './types/Job'
import OrderTerm from './types/OrderTerm'
import JobList from './components/JobList.vue'

export default defineComponent({
  name: 'App',
  components: {
    JobList
  },
  setup() {
    const jobs = ref<Job[]>([
      {
        title: 'farm worker',
        location: 'lon lon ranch',
        salary: 30000,
        id: '1'
      },
      {
        title: 'quarryman',
        location: 'death mountain',
        salary: 40000,
        id: '2'
      },
      {
        title: 'flute player',
        location: 'the lost woods',
        salary: 35000,
        id: '3'
      },
      {
        title: 'fisherman',
        location: 'lake hylia',
        salary: 21000,
        id: '4'
      },
      {
        title: 'prison guard',
        location: 'gerudo valley',
        salary: 32000,
        id: '5'
      }
    ])
    const order = ref<OrderTerm>('title')
    const handleClick = (term: OrderTerm) => {
      order.value = term
    }
    return { jobs, handleClick, order }
  },
  methods: {}
})
</script>
<style>
header {
  text-align: center;
}
header .order {
  margin-top: 1.25rem;
}
header .title {
  display: flex;
  justify-content: center;
}
header img {
  width: 3.75rem;
  margin-inline-end: 1.25rem;
}
header h1 {
  font-size: 3rem;
}
button {
  user-select: none;
  margin: 0 0.625rem;
  color: #1195c9;
  border: 0.1875rem solid #1195c9;
  background-color: #d5f0ff;
  padding: 0.5rem 1rem;
  border-radius: 0.5rem;
  cursor: pointer;
  font-weight: bold;
  box-shadow: 0 4px 8px -4px #0002, 0 2px 4px -2px #0003;
  transition: transform 150ms ease-out, box-shadow 150ms ease-out;
}
button:hover,
button:focus-visible {
  transform: translateY(-1px);
  box-shadow: 0 6px 12px -6px #0002, 0 3px 6px -3px #0003;
}
button:active {
  transition: transform 150ms ease-out, box-shadow 150ms ease-out;
  transform: translateY(1px);
  box-shadow: 0 1px 2px -1px #0002, 0 0 1px 0 #0003;
}
</style>
