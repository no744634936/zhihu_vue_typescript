<template>
  <div class="row">
      <div v-for="column in columnList" :key="column.id" class="col-4 mb-4">
          <div class="card-body">
            <div class="card h-100 shadow-sm" >
                <img :src="column.avatar" :alt="column.title">
                <h5>{{column.title}}</h5>
                <p>{{column.description}}</p>
                <a href="#" class="btn btn-primary">进入专栏</a>
            </div>
          </div>

      </div>
  </div>
</template>

<script lang='ts'>
import { computed, defineComponent, PropType } from 'vue'

export interface ColumnProps{
    id: number;
    title: string;
    avatar?: string;
    description: string;
}

export default defineComponent({
  name: 'ColumnList',
  props: {
    list: {
      type: Array as PropType<ColumnProps[]>,
      require: true
    }
  },
  // 将App.vue 那边传过来的list 做一下调整，如果没有avatar，就添加一个默认的avatar
  // 然后这个component用的就是columnList。
  setup (props) {
    const columnList = computed(() => {
      // 由于传值是异步，所以要检查props.list 是否有值。没有值的时候返回空数组。
      if (!props.list) return []
      return props.list.map(column => {
        if (!column.avatar) {
          column.avatar = require('../assets/default_avatar.jpg')
        }
        return column
      })
    })
    return { columnList: columnList }
  }
})
</script>
