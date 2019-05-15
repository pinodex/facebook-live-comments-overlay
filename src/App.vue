<template>
  <router-view />
</template>

<style lang="scss">
@import 'bulma';

html, body {
  background: transparent;
  overflow: auto;
}

.slide-fade-enter-active,
.slide-fade-leave-active {
  transition: all .3s ease;
}

.slide-fade-enter,
.slide-fade-leave-to {
  transform: translateY(10px);
  opacity: 0;
}
</style>
