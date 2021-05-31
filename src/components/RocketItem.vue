<template>
   <div>
    <div v-if="rocket">
        <h2>{{rocket.name}}</h2>
        <h2>{{rocket.description}}</h2>
        <h2>{{rocket.costPerLaunch}}</h2>
    </div>
   </div>
</template>

<script>
import { GET_ROCKET } from '../queries'
export default {
  apollo: {
    rocket: {
      query: GET_ROCKET,
      variables() {
        return { id: this.$route.params.id }
      }
    }
  }
}
</script>

<style lang="scss" scoped>

</style>