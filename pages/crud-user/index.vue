<template lang="pug">
  div.container
    h1 Users list
    CreateUser
    h2 List
    ol
      li(v-for="item in users" :key="item.id")
        NuxtLink(:to="baseUrl+item.id") {{item.name}}, age: {{item.age}}
</template>

<script>
import { apiUrl } from '@/const'
export default {
  async asyncData({ $axios, env }) {
    const point = apiUrl + '/main/crud-rest/0/user'
    const usersExt = await $axios.$get(point)
    const users = usersExt.payload
    return { users }
  },
  data() {
    return {
      baseUrl: '/crud-user/',
    }
  },
}
</script>
