<script setup lang="ts">
import { onMounted, ref, type Ref } from "vue";
import {
  getAllLanguages,
  getRandomLanguage,
  getStoredLanguageSelection,
  LANGUAGES,
  setLanguageSelection,
} from "../data/languages";

defineProps({
  isMenuOpened: Boolean,
});

const rndLng: any = ref({});
let selected: Ref<string[]> = ref([]);
const languages = LANGUAGES;

onMounted(async () => {
  selected.value = getStoredLanguageSelection();
  rndLng.value = getRandomLanguage();
});

function onLanguageChecked() {
  setLanguageSelection(selected.value);
}

function onSelectAll() {
  selected.value = getAllLanguages();
  setLanguageSelection(selected.value);
}
function onSelectNone() {
  selected.value = [];
  setLanguageSelection(selected.value);
}
</script>
<template>
  <div class="language-picker">
    <ul class="nav-idle" :class="{ 'nav-sticky': isMenuOpened }">
      <li v-on:click="onSelectAll()">
        <input type="checkbox" />
        <label class="button">Alle auswählen</label>
      </li>
      <li v-on:click="onSelectNone()">
        <label class="button">Leeren</label>
      </li>
    </ul>
    <ul class="nav">
      <li v-for="item in languages" :key="item.language" class="nav-item">
        <input
          :id="item.language"
          type="checkbox"
          :value="item.language"
          v-model="selected"
          @change="onLanguageChecked"
        />
        <label :for="item.language">
          {{ item.name }}
        </label>
      </li>
    </ul>
  </div>
</template>
<style scoped lang="scss">
.nav-idle {
  opacity: 0;
  transition: 1.5s;
}
.nav-sticky {
  position: sticky;
  opacity: 1;
  top: 0;
  background-color: var(--moss-river);
  padding: 0.25rem 0;
  z-index: 10;
}
ul {
  padding: 0;
  margin: 0;
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  list-style: none;

  li {
    display: inline;
    padding: 0px 2px;

    label {
      display: inline-block;
      background-color: var(--lp-btn-backgrnd);
      border: 2px solid var(--lp-btn-border);
      color: var(--lp-btn-color);
      border-radius: 25px;
      white-space: nowrap;
      margin: 3px 0px;
      -webkit-touch-callout: none;
      -webkit-user-select: none;
      -moz-user-select: none;
      -ms-user-select: none;
      user-select: none;
      -webkit-tap-highlight-color: transparent;
      transition: all 0.2s;
      padding: 8px 12px;
      cursor: pointer;

      &::before {
        display: inline-block;
        font-style: normal;
        font-variant: normal;
        text-rendering: auto;
        -webkit-font-smoothing: antialiased;
        font-family: "Font Awesome 5 Free";
        font-weight: 900;
        font-size: 12px;
        padding: 2px 6px 2px 2px;
        content: "\f067";
        transition: transform 0.3s ease-in-out;
      }

      &.button {
        color: black;
        background-color: var(--yellow);
        border: none;

        i {
          padding-right: 5px;
        }

        &::before {
          content: none;
        }
      }
    }

    input[type="checkbox"] {
      display: none;
    }

    input[type="checkbox"]:checked + label {
      border: 2px solid var(--lp-checked-btn-border);
      background-color: var(--lp-checked-btn-backgrnd);
      color: var(--lp-checked-btn-color);
      transition: all 0.2s;

      &::before {
        content: "\f00c";
        padding: 2px 5px 2px 2px;
        transform: rotate(-360deg);
        transition: transform 0.3s ease-in-out;
      }
    }
  }
}
</style>
