<template>
  <div class="container">
    <div class="row">
      <div class="col-4">
        <user-form />
      </div>
      <div class="col-8">
        <user-list />
      </div>
    </div>
  </div>
</template>

<script>
import UserList from '@/components/UserList.vue'
import UserForm from '@/components/UserForm.vue'
export default {
  components: {
    UserList,
    UserForm
  }
}
</script>