<script setup lang="ts">
const emit = defineEmits<{
  (e: "onClick"): void;
}>();

function refresh() {
  emit("onClick");
}
</script>

<template>
  <input type="checkbox" id="refresh" />
  <label for="refresh" class="fa fa-sync-alt" @click="refresh"></label>
</template>

<style scoped lang="scss">
@mixin transition($params) {
  -webkit-transition: $params;
  -moz-transition: $params;
  -khtml-transition: $params;
  -o-transition: $params;
  transition: $params;
}

@-webkit-keyframes spin {
  from {
    transform: rotate(-360deg);
  }
  to {
    transform: rotate(0deg);
  }
}

@keyframes spin {
  from {
    transform: rotate(-360deg);
  }
  to {
    transform: rotate(0deg);
  }
}

@-webkit-keyframes spin-checked {
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(360deg);
  }
}

@keyframes spin-checked {
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(360deg);
  }
}

#refresh {
  display: none;

  &:checked {
    & ~ label {
      animation: spin-checked 1s forwards;
    }
  }

  &:not(:checked) {
    & ~ label {
      animation: spin 1s forwards;
    }
  }
}
label {
  position: fixed;
  bottom: 1rem;
  right: 1rem;
  z-index: 100;
  padding: 1rem;
  font-size: 1.5rem;
  background-color: transparent;
  cursor: pointer;
  border-radius: 100%;
  @include transition(all 0.5s linear);
  color: var(--font-primary);
  -webkit-tap-highlight-color: transparent;

  &:hover {
    box-shadow: 0 0 0 8px rgba(0, 0, 0, 0.1),
      inset 0 0 0 30px rgba(0, 0, 0, 0.1);
  }
}
</style>
