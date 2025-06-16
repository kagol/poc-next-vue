<script setup lang="ts">
import { reactive } from 'vue'
import { useNextServer } from '@opentiny/next-vue'
import { z } from 'zod'

defineProps<{ msg: string }>()

const { server } = useNextServer({
  serverInfo: { name: 'company-list', version: '1.0.0' }
})

server.tool('set_selected', '选中一家公司', {
  id: z.string().describe('公司 ID'),
  selected: z.boolean().describe('是否选中')
}, async ({ id, selected }) => {
  console.log('set_selected called')
  setSelected(id, selected)
  return {
    content: [
      {
        type: 'text',
        text: 'success'
      }
    ]
  }
})

const companyList = reactive([
  {
    id: '1',
    name: 'GFD 科技 YX 公司',
    city: '福州',
    employees: 800,
    createdDate: '2014-04-30 00:56:00',
    checked: false,
  },
  {
    id: '2',
    name: 'WWW 科技 YX 公司',
    city: '深圳',
    employees: 300,
    createdDate: '2016-07-08 12:36:22'
  },
  {
    id: '3',
    name: 'RFV 有限责任公司',
    city: '中山',
    employees: 1300,
    createdDate: '2014-02-14 14:14:14',
  },
  {
    id: '4',
    name: 'TGB 科技 YX 公司',
    city: '龙岩',
    employees: 360,
    createdDate: '2013-01-13 13:13:13'
  },
  {
    id: '5',
    name: 'YHN 科技 YX 公司',
    city: '韶关',
    employees: 810,
    createdDate: '2012-12-12 12:12:12'
  },
  {
    id: '6',
    name: 'WSX 科技 YX 公司',
    city: '黄冈',
    employees: 800,
    createdDate: '2011-11-11 11:11:11'
  },
  {
    id: '7',
    name: 'KBG 物业 YX 公司',
    city: '赤壁',
    employees: 400,
    createdDate: '2016-04-30 23:56:00',
  },
  {
    id: '8',
    name: '深圳市福德宝网络技术 YX 公司',
    city: '厦门',
    createdDate: '2016-06-03 13:53:25',
    employees: 540
  },
  {
    id: '9',
    name: '深圳市菊厂有限公司',
    city: '深圳',
    createdDate: '2018-06-03 13:53:25',
    employees: 10000
  }
])

const setSelected = (id: string, selected: boolean) => {
  companyList.forEach(company => {
    if (company.id === id) {
      company.checked = selected
    }
  })
}

// setSelected('2', true)
</script>

<template>
  <h1>{{ msg }}</h1>

  <h3>公司列表</h3>
  <ul>
    <li v-for="company in companyList" :key="company.id">
      <input type="checkbox" v-model="company.checked" />
      <span class="space">{{ company.id }}</span>
      <span class="space">{{ company.name }}</span>
      <span class="space">{{ company.city }}</span>
      <span class="space">{{ company.employees }}</span>
    </li>
  </ul>
</template>

<style scoped>
.space {
  display: inline-block;
  margin: 12px;
}
</style>
