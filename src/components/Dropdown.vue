<template>
<div class="dropdown" ref="dropdownRef">
  <a href="#" class="btn btn-outline-light my-2 dropdown-toggle" @click.prevent="toggleOpen">
    {{title}}
  </a>
  <ul class="dropdown-menu" :style="{display: 'block'}" v-if="isOpen">
    <slot></slot>
  </ul>
</div>
</template>

<script lang='ts'>
import { defineComponent, ref, onMounted, onUnmounted } from 'vue'

export default defineComponent({
  name: 'Dropdown',
  props: {
    title: {
      type: String,
      required: true
    }
  },
  setup () {
    // 在setup函数中，可以使用ref函数，用于创建一个响应式数据，当数据发生改变时，Vue会自动更新UI
    // 都必须通过return {xxx,xxx}暴露出去，外界才能使用
    // ref函数仅能监听基本类型的变化，不能监听复杂类型的变化（比如对象、数组）
    const isOpen = ref(false)
    const toggleOpen = () => {
      // 取反
      isOpen.value = !isOpen.value
    }

    // 点击dropdownlist的外部区域自动隐藏dropdownlist功能
    // 在setup函数中dropdownRef初始值为null 可是之后类型会变成dom节点,所以要写上<null | HTMLElement>
    const dropdownRef = ref<null | HTMLElement>(null)
    const handle = (e: MouseEvent) => {
      // dropdownRef.value 就是class="dropdown" 节点
      // if (dropdownRef.value)写这一句是因为class="dropdown" 节点不一定有
      if (dropdownRef.value) {
        // Node.contains() 是否为后代节点，括号里的参数必须是HTMLElement
        // e.target 不一定是dom节点，所以要做一个类型声明  as HTMLElement
        // !dropdownRef.value.contains(e.target as HTMLElement) class="dropdown" 节点不包含我点击的地方。
        if (!dropdownRef.value.contains(e.target as HTMLElement) && isOpen.value === true) {
          console.log(e.target)
          console.log('hahah')
          console.log(isOpen.value)
          isOpen.value = false
        }
      }
      console.log(e.target)
    }
    // 网页渲染的时候给整个网页添加click事件，
    onMounted(() => {
      document.addEventListener('click', handle)
    })
    // 网页消亡的时候删除click事件
    onUnmounted(() => {
      document.removeEventListener('click', handle)
    })
    // 注意dropdownRef 跟 dropdownRef一样 才能获取dom节点
    return {
      isOpen,
      toggleOpen,
      dropdownRef
    }
  }

})
</script>
