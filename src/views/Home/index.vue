<script lang="ts" setup>
import TabNav from '@/components/TabNav.vue'
const list = [
  {
    icon: 'wxbmingxingdianpu',
    text: 'HOME',
    key: 'home',
  },
  {
    icon: 'comments',
    text: 'INBOX',
    key: 'inbox',
  },
]
const title = ref('TODOLIST')
const avaterHref = ref('/images/avater.jpg')
const avaterText = ref('Camellia')
const onChange = (key: string) => {
  console.log('time to go router ===>' + key)
}
</script>

<template>
  <div class="container">
    <TabNav
      :list="list"
      :title="title"
      :avaterHref="avaterHref"
      :avaterText="avaterText"
      @change="onChange"
      defaultKey="inbox"
      primaryColor="#F09319"
    />
    <main>
      <div class="inner-wrapper">
        <RouterView :key="$route.fullPath" />
      </div>
    </main>
  </div>
</template>

<style lang="scss" scoped>
.container {
  display: flex;
  width: 100%;
  height: 100%;
  main {
    padding: 20px;
    flex: 1;
    .inner-wrapper {
      width: 100%;
      height: 100%;
      background-color: #fefefe;
      border-radius: 10px;
    }
  }
}
</style>
