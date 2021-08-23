<template>
  <div class="job-list">
    <p>Ordered by {{ order }}</p>
    <transition-group name="list" tag="ul">
      <li v-for="job in orderedJobs" :key="job.id">
        <h2>{{ job.title }} in {{ job.location }}</h2>
        <div class="salary">
          <img src="../assets/rupee.svg" alt="rupee icon" />
          <p>{{ job.salary }} rupees</p>
        </div>
        <div class="description">
          <p>
            Lorem ipsum dolor sit amet consectetur adipisicing elit. Numquam
            excepturi tenetur delectus alias libero, eius ex deleniti illum
            recusandae corporis obcaecati, atque ullam dicta eveniet at enim
            voluptas iste? Alias.
          </p>
        </div>
      </li>
    </transition-group>
  </div>
</template>
<script lang="ts">
import { computed, defineComponent, PropType } from 'vue'
import Job from '@/types/Job'
import OrderTerm from '@/types/OrderTerm'

export default defineComponent({
  props: {
    jobs: {
      required: true,
      type: Array as PropType<Job[]>
    },
    order: {
      required: true,
      type: String as PropType<OrderTerm>
    }
  },
  setup(props) {
    const orderedJobs = computed(() => {
      return [...props.jobs].sort((a: Job, b: Job) => {
        return a[props.order] > b[props.order] ? 1 : -1
      })
    })
    return { orderedJobs }
  }
})
</script>
<style scoped>
.job-list {
  max-width: 960px;
  margin: 2.5rem auto;
}
.job-list ul {
  padding: 0;
}
.job-list li {
  list-style-type: none;
  background-color: white;
  box-shadow: 0 4px 8px -4px #0002, 0 2px 4px -2px #0003;
  padding: 1rem;
  margin: 1rem 0;
  border-radius: 0.5rem;
}
.job-list h2 {
  margin-block-end: 0.625rem;
  text-transform: capitalize;
}
.salary {
  display: flex;
}
.salary img {
  width: 1.875rem;
}
.salary p {
  color: #17bf66;
  font-weight: bold;
  margin: 0.625rem 0.25rem;
}
.list-move {
  transition: all 500ms ease-in-out;
}
</style>
