<template>
  <div>
    <h1>{{ title }}</h1>
    <p>计数: {{ count }}</p>
    <button @click="increment">点我+1</button>
    <p>用户信息: {{ user.name }} - {{ user.age }}岁</p>
    <button @click="growOld">长大一岁</button>
  </div>
</template>

<script setup lang="ts">
// 1. 定义响应式数据 - 这是你第一个TS接口(Interface)
import { ref, reactive } from 'vue'

// 1.1 用ref定义基本类型数据，TS会自动推断类型为 number
const count = ref(0)

// 1.2 为复杂数据定义“形状”（接口）
interface User {
  name: string
  age: number
  isAdmin?: boolean // 问号表示这个属性是可选的
}

// 1.3 用reactive定义复杂对象，并用“: User”告诉TS它的形状
const user = reactive<User>({
  name: '元宝',
  age: 1
})

// 2. 定义计算属性/方法
const title = '我的第一个TS+Vue3组件'

// 3. 定义方法，并指定参数类型
function increment(): void { // : void 表示这个函数不返回值
  count.value++ // 注意：ref定义的数据，需要用 .value 访问
}

function growOld(): void {
  user.age++ // reactive定义的数据，可以直接修改
}

// 4. 定义一个带参数和返回值类型的方法
function add(a: number, b: number): number { // 参数和返回值都明确类型
  return a + b
}
// 试试调用：console.log(add(1, 2)) // 正确
// 如果写错类型：console.log(add('1', 2)) // TS会在你写代码时就报错，防患于未然
</script>

<style scoped>
/* 样式 */
</style>