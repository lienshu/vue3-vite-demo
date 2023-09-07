<template>
  <div class="h-8 w-90 whitespace-nowrap overflow-x-auto overflow-y-hidden wrap">
    <div v-for="(item, index) in tabs" class="mr-2 inline-flex items-center justify-center cursor-pointer" @click="onClick(index)" :ref="(el) => getTab(el, index)">
      {{ item.name }}
    </div>
  </div>
  <div class="my-tabs w-700px whitespace-nowrap overflow-x-auto overflow-y-hidden">
    <div class="my-tabs-item inline-flex items-center justify-center px-4 mr-1 relative" v-for="(item,index) in tabs" :key="index" @click="change(index)" :ref="el => secondTab[index] = el">
      {{ item.name }}
    </div>
  </div>
</template>

<script lang="ts" setup>
import { ref } from 'vue'
// import type { ComponentPublicInstance } from "vue-demi";
const tabs = ref<{name: String}[]>([{name: '中国'},{name: '韩国'},{name: '日本'},{name: '新加坡'},{name: '泰国'},{name: '美国'},{name: '英国'},{name: '瑞士'},{name: '法国'},{name: '加拿大'},{name: '意大利'},{name: '澳大利亚'}])
const tabsRef = ref()
const tab = ref<Array<Element | null>>([])
const secondTab = ref<Array<Element | null>>([])
const active = ref(0)

const getTab = (el: any, index: number) => {
  if(el){
    console.log(el, 'el')
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