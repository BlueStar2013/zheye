<template>
  <div class="container">
    <global-header :user="currentUser"></global-header>
    <column-list :list="list"></column-list>
  </div>
</template>

<script lang="ts">
  import { defineComponent } from 'vue'
  import 'bootstrap/dist/css/bootstrap.min.css'
  import ColumnList, { ColumnProps } from "@/components/ColumnList.vue";
  import GlobalHeader, { UserProps } from "@/components/GlobalHeader.vue";

  const currentUser: UserProps = {
    isLogin: true,
    name: 'nick',
    id: 7,
  };
  const testData: ColumnProps[] = [
    {
      id: 1,
      title: 'test1的专栏',
      description: '这是的test1专栏，有一段非常有意思的简介，可以更新一下欧, 这是的test1专栏，有一段非常有意思的简介，可以更新一下欧',
      avatar: 'http://vue-maker.oss-cn-hangzhou.aliyuncs.com/vue-marker/5ee22dd58b3c4520912b9470.jpg?x-oss-process=image/resize,m_pad,h_150,w_150'
    },
    {
      id: 2,
      title: 'test2的专栏',
      description: '这是的test2专栏，有一段非常有意思的简介，可以更新一下欧',
      avatar: 'http://vue-maker.oss-cn-hangzhou.aliyuncs.com/vue-marker/5ee22dd58b3c4520912b9470.jpg?x-oss-process=image/resize,m_pad,h_100,w_100'
    },
    {
      id: 3,
      title: 'test3的专栏',
      description: '这是的test1专栏，有一段非常有意思的简介，可以更新一下欧 这是的test1专栏，有一段非常有意思的简介，可以更新一下欧',
      avatar: 'http://vue-maker.oss-cn-hangzhou.aliyuncs.com/vue-marker/5ee22dd58b3c4520912b9470.jpg?x-oss-process=image/resize,m_pad,h_100,w_100'
    },
    {
      id: 4,
      title: 'test4的专栏',
      description: '这是的test2专栏，有一段非常有意思的简介，可以更新一下欧',
      avatar: 'http://vue-maker.oss-cn-hangzhou.aliyuncs.com/vue-marker/5ee22dd58b3c4520912b9470.jpg?x-oss-process=image/resize,m_pad,h_100,w_100'
    }
  ];

  export default defineComponent({
    name: 'App',
    components: {
      ColumnList,
      GlobalHeader,
    },

    setup() {

      return {
        list: testData,
        currentUser,
      }
    }
  });
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>
