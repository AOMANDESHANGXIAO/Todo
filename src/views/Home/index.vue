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
</script>

<template>
  <TabNav
    :list="list"
    :title="title"
    :avaterHref="avaterHref"
    :avaterText="avaterText"
    primaryColor="#F09319"
  />
</template>

<style lang="scss" scoped></style>
