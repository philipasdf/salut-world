<script setup lang="ts">
import { ref } from "vue";

const emit = defineEmits<{
  (e: "onClick", value: boolean): void;
}>();

const isMenuOpened = ref(false);
function toggleMenu() {
  isMenuOpened.value = !isMenuOpened.value;
  emit("onClick", isMenuOpened.value);
}
</script>

<template>
  <div class="burger-btn" :class="{ close: isMenuOpened }" @click="toggleMenu">
    <div class="burger-line"></div>
  </div>
</template>

<style scoped lang="scss">
@mixin rotate($params) {
  -webkit-transform: rotate($params);
  -moz-transform: rotate($params);
  -khtml-transform: rotate($params);
  -o-transform: rotate($params);
  transform: rotate($params);
}
@mixin transition($params) {
  -webkit-transition: $params;
  -moz-transition: $params;
  -khtml-transition: $params;
  -o-transition: $params;
  transition: $params;
}

.burger-btn {
  height: 30px;
  width: 30px;
  box-sizing: border-box;
  position: relative;
  z-index: 30;
  cursor: pointer;
  @include transition(all 0.4s ease-out);

  .burger-line {
    height: 5px;
    background: var(--font-primary);
    border-radius: 25px;
    transform: translateY(-1px);
    @include transition(all 0.5s ease-out);
  }

  &:hover {
    box-shadow: 0 0 0 8px rgba(0, 0, 0, 0.1),
      inset 0 0 0 20px rgba(0, 0, 0, 0.1);
  }
  &:before,
  &:after {
    content: "";
    display: block;
    position: absolute;
    height: 5px;
    width: 30px;
    border-radius: 10px;
    background: var(--font-primary);
    @include transition(all 0.4s ease-out);
  }
  &:before {
    left: 0;
    top: 12px;
  }
  &:after {
    left: 0;
    bottom: 0;
  }

  &.close {
    .burger-line {
      background: transparent;
    }

    &:before {
      @include rotate(45deg);
      width: 33px;
      left: -2px;
      top: 11px;
    }
    &:after {
      @include rotate(135deg);
      bottom: 14px;
      width: 33px;
      left: -2px;
    }
  }
}
</style>
