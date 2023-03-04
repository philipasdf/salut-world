<script setup lang="ts">
import { onMounted, ref, type Ref } from "vue";
import DisplayHelloContainer from "./components/DisplayHelloContainer.vue";
import BurgerButton from "./components/BurgerButton.vue";
import LanguagePicker from "./components/LanguagePicker.vue";
import RefreshButton from "./components/RefreshButton.vue";
import { getRandomLanguage } from "./data/languages";
import { getRandomPhrase } from "./data/phrases";

const rndLng: any = ref({});
const isMenuOpened: Ref<Boolean> = ref(false);
const rndText: any = ref({});

onMounted(async () => {
  rndText.value = getRandomPhrase();
  rndLng.value = getRandomLanguage();
});

function toggleMenu(_isMenuOpened: boolean) {
  isMenuOpened.value = _isMenuOpened;
}

function refresh() {
  rndText.value = getRandomPhrase();
  rndLng.value = getRandomLanguage();
}
</script>

<template>
  <div class="container">
    <div class="menu" :class="{ opened: isMenuOpened }">
      <div class="menu-btn">
        <BurgerButton @on-click="toggleMenu($event)" />
      </div>
      <div class="menu-settings">
        <LanguagePicker />
      </div>
    </div>

    <section class="content">
      <DisplayHelloContainer
        v-if="!!rndLng"
        :random-text="rndText.de"
        :language-name="rndLng.name"
        :translated-text="rndText[rndLng.language]"
      ></DisplayHelloContainer>
    </section>
    <RefreshButton @on-click="refresh" />
  </div>
</template>

<style lang="scss">
$transition-duration: 1.5s;
$transition-delay: 0.05s;

.container {
  display: flex;
  flex-direction: column;
  height: 100%;
  width: 100%;
  position: relative;
}

.content {
  flex-grow: 1;
  position: relative;
  transition: $transition-duration;
  background: var(--background);
  padding-top: 2rem;
  padding-bottom: 2rem;

  /* content shadow if menu opened */
  &:before {
    position: absolute;
    content: "";
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: transparent;
    z-index: 2;
    transition: $transition-duration;
  }
}

.menu {
  height: 0;
  max-height: 0;
  transition: $transition-duration;
  transition-delay: $transition-delay;
  display: flex;
  flex-direction: row-reverse;
  width: 100%;
  max-width: 100%;
  background-color: var(--lp-background);

  .menu-btn {
    padding: 1rem;
  }
  .menu-settings {
    padding: 0.5rem;
    min-width: 0;
    flex-shrink: 20;
  }
}

@media only screen and (min-width: 768px) {
  .menu {
    .menu-btn {
      padding: 2rem;
    }
    .menu-settings {
      padding: 1rem;
    }
  }
}

.menu.opened {
  height: auto;
  max-height: 2000px; // it will never reach that. Just for the transition of 'height: auto'
  transition: $transition-duration;
  transition-delay: $transition-delay;
  /* Any element you need to change the style if menu is open goes here, using the sibling selector (~) */

  & ~ .content {
    // padding-top: 30px;

    /* content shadow if menu opened */
    &:before {
      background-color: rgba(0, 0, 0, 0.3);
    }
  }
}
</style>
