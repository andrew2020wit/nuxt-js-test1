<template lang="pug">
  div.container
    h1 Users list
    // pre {{users}}
    ol
      li(v-for="item in users" :key="item.id") {{item.name}}
</template>

<script>
export default {
  async asyncData({ $axios }) {
    const usersExt = await $axios.$get(
      `http://localhost:3001/api/main/crud-rest/1000/user`
    )
    const users = usersExt.payload
    return { users }
  },
}
</script>
