<template>
  <div class="container">
    <GlobalHeader :user="currentUser"></GlobalHeader>
    <ColumnList :list="list"></ColumnList>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import 'bootstrap/dist/css/bootstrap.min.css'
import ColumnList, { ColumnProps } from './components/ColumnList.vue'
import GlobalHeader, { UserProps } from './components/GlobalHeader.vue'

// test data
const testData: ColumnProps[] = [
  {
    id: 1,
    title: 'test1的专栏',
    avatar: 'https://gravatar.com/avatar/9ddf17a4d4da97c0b974f97031ee5bf4?s=400&d=robohash&r=x',
    description: 'description test1'
  },
  {
    id: 2,
    title: 'test2的专栏',
    avatar: 'https://gravatar.com/avatar/ab75a1555f150e73df0dd48c56a7db47?s=400&d=robohash&r=x',
    description: 'description test2'
  },
  {
    id: 3,
    title: 'test3的专栏',
    avatar: 'https://gravatar.com/avatar/927665565133aecf07f5bb2ec3e74fe4?s=400&d=robohash&r=x',
    description: 'description test3'
  },
  {
    id: 4,
    title: 'test4的专栏',
    avatar: '',
    description: 'description test4'
  }
]

const currentUser: UserProps = {
  isLogin: true,
  name: 'zhang'
}

export default defineComponent({
  name: 'App',
  components: {
    ColumnList,
    GlobalHeader
  },
  setup () {
    return {
      list: testData,
      currentUser
    }
  }
})
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
