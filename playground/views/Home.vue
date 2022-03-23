<template>
  <div>
    <div>Home</div>
    <p>My Data is: {{ someData }}</p>
    <p v-if="waited != null">I waited for {{ waited }}</p>
    toggle: {{ log(toggle) }}
    <button @click="counter++">{{ counter }}</button>
  </div>
</template>

<script>
import {defineComponent, getCurrentInstance, ref} from 'vue'

export default defineComponent({
  name: 'Home',
  props: ['waited'],
  data: () => ({
    toggle: false,
    counter: 0,
  }),
  methods:{
    addCounter(){
      this.counter ++
    }
  },
  setup() {
    const me = getCurrentInstance()

    function log(value) {
      console.log(value)
      return value
    }

    return {
      log,
      someData: ref(0),
    }
  },
  beforeRouteEnter(to, from, next) {
    next(vm => {
      // 通过 `vm` 访问组件实例
      vm.addCounter()
      console.log(vm.counter)
    })
  },
  _beforeRouteEnter() {
    this.toggle = true
  },
})
</script>
