<template>
  <div class="home">
    <!-- <img alt="Vue logo" src="../assets/logo.png" /> -->
    <HelloWorld msg="Welcome to Your Vue3.0" />
    <p>{{content}}</p>
    <p>{{title}}</p>

  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from "@/components/HelloWorld.vue";
// CompositionAPI
import {computed, reactive, toRefs, watch,ref} from 'vue'
import {useRoute} from 'vue-router'
import {useStore} from 'vuex'
export default {
  name: "Home",
  // 默认只执行一次 没有this
  setup(props, context){
    // props 穿过来的数据
    // context包含 attr/ slots emit
    console.log('setup')
    const route = useRoute();
    const store = useStore();
    const state = reactive({
      content: '今天来学习vue3新语法,哈哈666',
      title: ref(store.getters.title) // 包装成对象
    })
    console.log(toRefs(state),'toRefs')

    watch(state, (newVal) => {
      console.log(newVal,'newVal')
    },{immediate:true})

    watch(() => route.path, (newVal) => {
      console.log(newVal,'newVal')
    },{immediate:true})

    const content = computed( () => {
      return `${content}，你好`
    })


    return {
      ...toRefs(state)
    }
  },
  // options Api
  // data(){
  //   return {
  //     content: '今天来学习vue3新语法,哈哈'
  //   }
  // },
  components: {
    HelloWorld
  }
};
</script>
