<template lang="pug">
  div.container
    h1 User details
    p <strong> Name: </strong> {{user.name}}
    p <strong>Age:</strong> {{user.age}}
</template>

<script>
import { apiUrl } from '@/const'
export default {
  async asyncData({ $axios, params, env }) {
    const point = apiUrl + '/main/crud-rest/0/user/' + params.id
    console.log('point', point)
    const usersExt = await $axios.$get(point)
    const user = usersExt.payload
    return { user }
  },
}
</script>
