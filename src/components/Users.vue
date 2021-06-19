<template>
<div class="wrapper">
  <h1 class="title">Random Users</h1>
  <ul class="users">
    <template v-for="user in users" :key="user.id.value">
      <User :user="user" />
    </template>
    <div class="loading-wrapper">
      <span v-if="!loading" class="load" @click="load">
        Load more
      </span>
      <loading v-if="loading" class="loading" />
    </div>
  </ul>
</div>
</template>

<script lang="ts">
import { ref, defineComponent, onMounted, Ref, computed } from 'vue'
import { User, getUser } from '../apis/user'
import UserComp from './User.vue'
import LoadingComp from './Loading.vue'

export default defineComponent({
  name: 'Users',
  components: {
    User: UserComp,
    Loading: LoadingComp
  },
  setup: () => {
    const users: User[] = []
    const loading = ref(false)

    const load = async () => {
      loading.value = true
      const usersData = await getUsers()
      loading.value = false
      users.push(...usersData)
    }

    onMounted(load)

    return {
      users,
      loading,
      load
    }
  }
})

function getUsers() {
  return Promise.all(Array.from({ length: 5 }).map(() => getUser()))
}
</script>

<style lang="less" scoped>
.wrapper {
  margin: 0;
  padding: 1em;
  max-width: 400px;
}

.title {
  font-size: 28px;
  padding: 0 16px;
}

.users {
  margin: 0;
  padding: 0;
}

.loading-wrapper {
  padding: 1em;

  .load {
    padding: .5em 0;
    cursor: pointer;
    font-size: 12px;
    color: #666;

    &:hover {
      color: #222;
    }
  }

  .loading {
    margin-left: 16px;
    padding: .5em 0;
  }
}
</style>