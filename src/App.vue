<script setup lang="ts">
import CompanyList from './components/CompanyList.vue'
import { useNextClient } from '@opentiny/next-vue'

let id: any
if (sessionStorage.getItem('sessionId')) {
  id = sessionStorage.getItem('sessionId')
} else {
  id = crypto.randomUUID()
  sessionStorage.setItem('sessionId', id)
}

const { sessionId } = useNextClient({
  clientInfo: { name: 'demo-vite-next-vue', version: '1.0.0' },
  proxyOptions: { url: 'https://agent.icjs.ink/sse', token: '', sessionId: id },
})

</script>

<template>
  <p>sessionId: https://agent.icjs.ink/sse?sessionId={{ sessionId }}</p>
  <div>
    <a href="https://vitejs.dev" target="_blank">
      <img src="/vite.svg" class="logo" alt="Vite logo" />
    </a>
    <a href="https://vuejs.org/" target="_blank">
      <img src="./assets/vue.svg" class="logo vue" alt="Vue logo" />
    </a>
  </div>
  <CompanyList msg="Vite + Vue + @opentiny/next-vue" />
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
