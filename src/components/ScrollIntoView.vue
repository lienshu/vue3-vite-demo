<template>
  <div class="h-8 w-160 m-5 whitespace-nowrap overflow-x-auto overflow-y-hidden wrap">
    <div v-for="(item, index) in tabs" class="mr-6 inline-flex items-center justify-center cursor-pointer" @click="onClick(index)" :ref="(el) => getTab(el, index)">
      {{ item.name }}
    </div>
  </div>
  <div class="my-tabs w-700px whitespace-nowrap overflow-x-auto overflow-y-hidden">
    <div class="my-tabs-item inline-flex items-center justify-center px-4 mr-1 relative" v-for="(item,index) in tabs" :key="index" @click="change(index)" :ref="el => secondTab[index] = el">
      {{ item.name }}
    </div>
  </div>
  <div>state1: {{ state1 }}</div>
  <div>state2: {{ state2 }}</div>
  <a-button type="primary" class="mr-4" @click="onClick1">state1</a-button>
  <a-button type="primary" @click="onClick2">state2</a-button>
  <p>{{ shallowState.a }}</p>
	<p>{{ shallowState.first.b }}</p>
	<p>{{ shallowState.first.second.c }}</p>
	<a-button type="primary" @click="change1">改变1</a-button>
	<a-button type="primary" @click="change2">改变2</a-button>
</template>

<script lang="ts" setup>
import { ref, toRef, toRefs, shallowReactive } from 'vue'
// import type { ComponentPublicInstance } from "vue-demi";
const tabs = ref<{name: String}[]>([{name: '中国'},{name: '韩国'},{name: '日本'},{name: '新加坡'},{name: '泰国'},{name: '美国'},{name: '英国'},{name: '瑞士'},{name: '法国'},{name: '加拿大'},{name: '意大利'},{name: '澳大利亚'}])
const tabsRef = ref()
const object = {
  name: '张三',
  age: '20',
  gender: 0
}
const state = toRefs(object)
console.log(state, 'state')
const obj = {count: 1}
/** ref 是对传入数据的拷贝；toRef 是对传入数据的引用 */
/** ref 的值改变会更新视图；toRef 的值改变不会更新视图 */
/** toRef: 值是响应式的，视图不会更新，obj页会改变，浅拷贝 */
const state1 = toRef(obj, 'count')
/** ref: obj不改变 */
const state2 = ref(obj.count)

const onClick1 = () => {
  state1.value ++
  console.log('原始值: ', obj)
  console.log('响应式数据对象: ', state1.value)
}

const onClick2 = () => {
  state2.value ++
  console.log('原始值: ', obj)
  console.log('响应式数据对象: ', state2.value)
}

const shallowObj = {
  a: 1,
  first: {
    b: 2,
    second: {
      c: 3
    }
  }
}

/** shallowReactive监听第一层属性值变化，发生变化视图更新 */
const shallowState = shallowReactive(shallowObj)

function change1() {
  shallowState.a = 7
}

function change2() {
  shallowState.first.b = 8
  shallowState.first.second.c = 9
  console.log(shallowState);
}

const tab = ref<Array<Element | null>>([])
const secondTab = ref<Array<Element | null>>([])
const active = ref(0)

const getTab = (el: any, index: number) => {
  if(el){
    // console.log(el, 'el')
    tab.value[index] = el
  }
  // return tab.value[index]
}
const onClick = (index: number) => {
  tab.value[index].scrollIntoView({behavior: 'smooth', block:'nearest', inline:'center'})
}
const change = ( i:number )=> {
  // active.value = i;
  // swiper.value.$swiper.slideTo(i, 500);
  active.value = i
  secondTab.value[i].scrollIntoView({ behavior: "smooth",inline:'center',block:'nearest'})
}

</script>

<style scoped>
.wrap {
  -ms-overflow-style: none;
}
.wrap::-webkit-scrollbar {
  display: none;
}
.my-tabs {
  -ms-overflow-style: none;
}
.my-tabs::-webkit-scrollbar{
  display: none;
}
.my-tabs-item {
  height: 40px;
  font-size: 16px;
  font-weight: 500;
  cursor: pointer;
}

/* .my-tabs-item.active {
  color: #fff;
  background-color: $color-black-2;
  border-radius: 4px;
} */
</style>