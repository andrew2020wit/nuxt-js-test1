<template>
  <div class="container">
    <h2>Update User</h2>
    <form @submit.prevent="onSubmit">
      <input
        v-model.trim="name"
        name="name"
        placeholder="name"
        minlength="3"
        maxlength="128"
        required
      />
      <input
        v-model.number="age"
        name="age"
        type="number"
        placeholder="age"
        min="10"
        max="100"
        required
      />
      <input type="submit" value="Update" />
    </form>
  </div>
</template>

<script>
import { apiUrl } from '@/const'
export default {
  async asyncData({ $axios, params, env }) {
    const point = apiUrl + '/main/crud-rest/0/user/' + params.id
    const usersExt = await $axios.$get(point)
    const user = usersExt.payload
    return { name: user.name, age: +user.age }
  },
  data() {
    return {
      name: '',
      age: 0,
    }
  },
  methods: {
    async onSubmit() {
      console.log('name', this.name, this.age)
      const point = apiUrl + '/main/crud-rest/0/user/' + this.$route.params.id
      await this.$axios
        .$put(point, {
          id: this.$route.params.id,
          name: this.name,
          age: this.age,
        })
        .then((response) => {
          console.log(response)
          this.$router.go()
        })
    },
  },
}
</script>
