<template>
  <div class="container">
    <global-header :user="currentUser"></global-header>
    <!--<column-list :list="list"></column-list>-->
    <validate-form @form-submit="onFormSubmit">
      <div class="mb-3">
        <label class="form-label">邮箱地址</label>
        <validate-input type="text"
                        placeholder="请输入邮箱"
                        :rules="emailRules"
                        v-model="emailRef">
        </validate-input>
      </div>
      <div class="mb-3">
        <label class="form-label">密码</label>
        <validate-input type="password"
                        placeholder="请输入密码"
                        :rules="pwdRules"
                        v-model="pwdRef">
        </validate-input>
      </div>
      <template #submit>
        <span class="btn btn-primary">提交</span>
      </template>
    </validate-form>
  </div>
</template>

<script lang="ts">
  import { defineComponent, reactive, ref } from 'vue'
  import 'bootstrap/dist/css/bootstrap.min.css'
  import ColumnList, { ColumnProps } from "@/components/ColumnList.vue";
  import GlobalHeader, { UserProps } from "@/components/GlobalHeader.vue";
  import ValidateInput, { RulesProp } from '@/components/validateInput.vue';
  import ValidateForm from "@/components/ValidateForm.vue"

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
      // ColumnList,
      GlobalHeader,
      ValidateInput,
      ValidateForm,
    },

    setup() {
      const emailRef = ref('nick');
      const pwdRef = ref('')
      const emailRules: RulesProp = [
        {
          type: 'required',
          message: '电子邮箱不能为空'
        },
        {
          type: 'email',
          message: '邮箱格式不正确',
        }
      ]

      const pwdRules: RulesProp = [
        {
          type: 'required',
          message: '密码不能为空'
        },
      ]

      const onFormSubmit = (result: boolean) => {
        console.log('result',result)
      }

      return {
        onFormSubmit,
        pwdRef,
        pwdRules,
        emailRef,
        emailRules,
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
