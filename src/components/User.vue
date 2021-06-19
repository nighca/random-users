<template>
  <li class="user">
    <div class="avatar-wrapper">
      <img class="avatar" :src="info.avatar" :alt="info.name">
    </div>
    <div class="info-wrapper">
      <h4 class="name">
        <span class="title">{{info.title}}</span>
        {{info.name}}
      </h4>
      <p class="contact">
        <a :href="'mailto:' + info.email">{{info.email}}</a>
        <a :href="'tel:' + info.phone">{{info.phone}}</a>
      </p>
    </div>
  </li>
</template>

<script lang="ts">
import { computed, defineComponent } from 'vue'
import { User } from '../apis/user'

export default defineComponent({
  props: ['user'],
  setup(props) {
    const user: User = props.user

    const info = computed(() => ({
      name: `${user.name.first} ${user.name.last}`,
      title: user.name.title + '.',
      avatar: user.picture.thumbnail,
      email: user.email,
      phone: user.phone
    }))

    return {
      info
    }
  },
})
</script>

<style lang="less" scoped>
.user {
  list-style: none;
  display: flex;
  width: auto;
  padding: 1em;

  + .user {
    margin-top: .5em;
  }

  &:hover {
    // background-color: #F5F5F5;

    .name {
      color: #222;
    }
  }
}

.avatar-wrapper {
  flex: 0 0 auto;
  display: flex;
  flex-direction: column;

  .avatar {
    margin-top: 4px;
    width: 48px;
    height: 48px;
    border-radius: 100%;
  }
}

.info-wrapper {
  margin-left: 1em;
  flex: 1 1 0;
  padding: 2px 0;
  display: flex;
  flex-direction: column;
  justify-content: space-between;

  .name {
    margin: 0;
    font-size: 18px;

    .title {
      font-size: 12px;
      color: #666;
    }
  }

  .contact {
    margin: 0;
    font-size: 12px;
    color: #666;

    a {
      color: inherit;
      text-decoration: none;

      &:hover {
        text-decoration: underline;
      }

      + a {
        margin-left: .5em;
      }
    }
  }
}
</style>