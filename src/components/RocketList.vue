<template>
  <ul>
    <li v-for="rocket in rockets" :key="rocket.id">
      <div class="card">
        <div class="card-header">
          <router-link :to="{ name: 'Rocket', params: { id: rocket.id } }">
            🚀 {{ rocket.name }}
          </router-link>
        </div>
        <div class="card-body">
          <blockquote class="blockquote mb-0">
            <p>{{ rocket.description.substring(1, 25).concat('....') }}</p>
          </blockquote>
        </div>
      </div>
    </li>
  </ul>
</template>

<script>
import { GET_ROCKETS } from '../queries'
export default {
  apollo: {
    rockets: {
      query: GET_ROCKETS
    }
  },
}
</script>
<style lang="scss" scoped>
li {
  margin: 10px 0;
}
</style>