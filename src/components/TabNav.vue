<script lang="ts" setup>
defineOptions({
  name: 'tab-nav',
})
interface TabNavProps {
  title: string
  list: {
    icon: string
    text: string
    key: string
  }[]
  avaterHref: string
  avaterText: string
  primaryColor?: string
}
const props = withDefaults(defineProps<TabNavProps>(), {
  title: '',
  list: () => [],
  avaterHref: '',
  avaterText: '',
  primaryColor: '#ff77b7',
})
const emits = defineEmits<{
  (e: 'change', key: string): void
}>()
const activeKey = ref(props.list[0].key)
const activeScrollBarRef = ref<HTMLElement | null>(null)
const change = (e: MouseEvent, key: string) => {
  emits('change', key)
  activeKey.value = key
  const activeDom = e.target as HTMLElement
  if (activeDom && activeScrollBarRef.value) {
    activeScrollBarRef.value.style.top = `${activeDom.offsetTop}px`
  }
}
</script>

<template>
  <div class="nav-tab-container">
    <nav class="nav-tab">
      <header>{{ props.title }}</header>
      <main>
        <div class="active-scroll-bar" ref="activeScrollBarRef"></div>
        <div
          :class="{ 'is-active': item.key === activeKey }"
          v-for="item in props.list"
          :key="item.key"
          @click="
            (e: MouseEvent) => {
              change(e,item.key)
            }
          "
        >
          <span :class="`iconfont icon-${item.icon}`"></span
          ><span>{{ item.text }}</span>
        </div>
      </main>
      <footer>
        <section class="avater-container">
          <img :src="props.avaterHref" alt="" />
        </section>
        <section>{{ props.avaterText }}</section>
      </footer>
    </nav>
  </div>
</template>

<style scoped lang="scss">
/* 版本2的beautyNavTab，做了上下滑动的提示条 */
$color-dark: #131422;
$color-light: #fefefe;
$color-primary: v-bind(primaryColor);
$item-height: 45px;
$item-padding: 25px;
// $item-font__family: 'PingFangRegualar', 'Microsoft YaHei Light', sans-serif;
$item-font__family: 'PingFangLight';
* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
  font-family: $item-font__family;
}
div,
span,
section,
p {
  cursor: default;
}
body {
  background-color: $color-dark;
}
.nav-tab-container {
  width: 200px;
  height: 100vh;
  background-color: $color-light;
  padding-left: $item-padding;
}
.nav-tab {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  height: 100%;
  /* padding: 10px; */
  box-sizing: border-box;
  // font-family: $item-font__family;
}
.nav-tab header {
  display: flex;
  /* justify-content: center; */
  align-items: center;
  height: $item-height;
  /* padding: var(item-padding); */
  /* text-align: center; */
  color: $color-dark;
  font-size: 18px;
  font-weight: 900;
  /* font-family: var(item-font__family); */
}
.nav-tab main {
  position: relative;
  flex: 1;
  margin-top: 30px;
  /* overflow-y: auto; */
  /* background-color: pink; */
  display: flex;
  flex-direction: column;
  /* justify-content: space-between; */
}
.nav-tab main div {
  position: relative;
  display: flex;
  align-items: center;
  padding: 4px;
  /* padding: var(item-padding); */
  gap: 10px;
  height: $item-height;
  /* flex: 1; */
  font-size: 14px;
  border-radius: calc($item-height / 2) 0 0 calc($item-height / 2);
  transition: all 0.3s;
}
.nav-tab main div:hover:not(.is-active) {
  background-color: $color-primary;
  color: $color-light;
}
.nav-tab main div .iconfont {
  border-radius: 50%;
  padding: 10px;
}
.nav-tab main div.active-scroll-bar {
  position: absolute;
  top: 0;
  left: 0;
  height: $item-height;
  width: 100%;
  border-radius: calc($item-height / 2) 0 0 calc($item-height / 2);
  background-color: $color-dark;
  transition: all 0.5s;
}
.nav-tab main div.active-scroll-bar::after,
.nav-tab main div.active-scroll-bar::before {
  content: '';
  position: absolute;
  width: 20px;
  height: 20px;
  /* 制作外圆角的精髓 */
  background: radial-gradient(
    circle at 0% 0%,
    transparent 20px,
    $color-dark 0
  );
  z-index: 10;
}
.nav-tab main div.active-scroll-bar::after {
  right: 0;
  bottom: -20px;
  transform: rotate(-90deg);
}
.nav-tab main div.active-scroll-bar::before {
  right: 0;
  top: -20px;
  transform: rotate(-270deg) rotateX(180deg);
}
.nav-tab main div.is-active {
  /* background-color: var(color-dark); */
  color: $color-light;
}
.nav-tab main div .iconfont {
  transition: all 0.3s;
}
.nav-tab main div.is-active .iconfont {
  background-color: $color-primary;
}
.nav-tab footer {
  display: flex;
  align-items: center;
  gap: 10px;
  height: $item-height;
}
.nav-tab footer .avater-container {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 25px;
  height: 25px;
  border-radius: 50%;
  overflow: hidden;
}
.nav-tab footer .avater-container img {
  width: 100%;
  height: 100%;
}
</style>
