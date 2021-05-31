<template>
  <table class="table">
  <thead>
    <tr>
      <th scope="col">Name</th>
      <th scope="col">Twitter</th>
      <th scope="col">Rocket</th>
    </tr>
  </thead>
  <tbody>
    <tr v-for="user in users" :key="user.id" :style="{ opacity: user.id === -1 ? '0.5' : 'initial' }">
      <th scope="row">👤 {{ user.name }}</th>
      <template>
        <td  v-if="user.twitter" class="twitter">
          🐦<a :href="`https://twitter.com/${user.twitter}`" target="_blank">@{{ user.twitter }}</a>
        </td>
        <td  v-else>
          <p class="noItem">No twitter account</p>
        </td>
      </template>
      
      <template>
        <td v-if="user.rocket" class="rocket">🚀 {{ user.rocket }}</td>
        <td  v-else>
          <p class="noItem">No rocket</p>
        </td>
      </template>
    </tr>
  </tbody>
</table>
</template>

<script>
import { GET_USERS } from '../queries'
export default {
  apollo: {
    users: {
      query: GET_USERS
    }
  }
}
</script>
<style scoped>
.user {
  display: flex;
  flex-direction: row;
  justify-content: center;
}
.name {
  font-size: 18px;
  font-weight: bold;
  margin-right: 10px;
}
.twitter {
  font-weight: bold;
  margin-right: 20px;
}
.twitter a {
  text-decoration: none;
}
.twitter a:hover {
  text-decoration: underline;
}
.rocket {
  font-weight: bold;
}
.noItem {
  color: red;
  font-weight: bold;
}
</style>