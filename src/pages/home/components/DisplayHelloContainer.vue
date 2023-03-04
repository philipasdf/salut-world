<script setup lang="ts">
defineProps({
  randomText: String,
  languageName: String,
  translatedText: String,
});
</script>

<template>
  <div class="main-container">
    <div class="border">
      <p class="language-name">
        {{ languageName }}
      </p>
      <span class="random-text">{{ randomText }}</span>
      <div class="inner-cutout">
        <p class="knockout translated-text">{{ translatedText }}</p>
      </div>
    </div>
  </div>
</template>

<style scoped lang="scss">
.main-container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100%;
  background: var(--background);
}

@-webkit-keyframes Gradient {
  0% {
    background-position: 30% 50%;
  }
  50% {
    background-position: 25% 50%;
  }
  100% {
    background-position: 30% 50%;
  }
}

.border {
  position: relative;
  max-width: 90vw;
  background: linear-gradient(
      110deg,
      var(--font-primary) 33%,
      rgba(0, 0, 0, 0) 33%
    ),
    linear-gradient(110deg, #c5e7d7 34%, #88d8b0 34%);
  background-size: 400% 400%;
  background-position: 25% 50%;
  -webkit-animation: Gradient 15s ease infinite;
  -moz-animation: Gradient 5s ease infinite;
}
.inner-cutout {
  position: relative;
  display: block;
  margin: 0.5rem;
  min-width: 80vw;
  background: var(--background);
  background-size: 300%;
  background-position: 50% 50%;
}

.random-text {
  font-size: 1.25em;
  font-weight: bold;
  position: absolute;
  top: -18px;
  left: 0px;
  text-transform: uppercase;
  background: var(--font-primary);
  -webkit-text-fill-color: transparent;
  -webkit-background-clip: text;
}

.language-name {
  width: 100%;
  margin: -4px 0;
  padding: 0;
  text-align: end;
  font-size: 1.5em;
  font-weight: lighter;
  position: absolute;
  top: 100%;
  background: var(--font-primary);
  background-size: 400%;
  -webkit-text-fill-color: transparent;
  -webkit-background-clip: text;
}

.knockout {
  animation: Gradient 5s ease infinite;
  -webkit-animation: Gradient 15s ease infinite;
  -moz-animation: Gradient 5s ease infinite;
  background: linear-gradient(
      110deg,
      var(--font-primary) 33%,
      rgba(0, 0, 0, 0) 33%
    ),
    linear-gradient(110deg, #c5e7d7 34%, #88d8b0 34%);
  background-size: 400%;
  -webkit-text-fill-color: transparent;
  -webkit-background-clip: text;
}
.translated-text {
  font-family: "Noto Sans", sans-serif;
  font-size: 3em;
  font-weight: bold;
  text-align: center;
  margin: 0;
  padding: 4rem 0;
}

@media only screen and (min-width: 768px) {
  .translated-text {
    font-size: 6em;
  }
  .random-text {
    font-size: 2em;
    top: -29px;
  }
  .language-name {
    margin: -10px;
    text-align: center;
    font-weight: lighter;
    top: 50%;
    transform: translateX(-50%) rotate(-90deg);
    background: var(--font-primary);
    background-size: 400%;
    -webkit-text-fill-color: transparent;
    -webkit-background-clip: text;
  }

  .border {
    max-width: 66vw;
  }

  .inner-cutout {
    min-width: 30vw;
  }
}
</style>
