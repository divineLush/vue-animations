<template>
  <button @click="flag = !flag">toggle animation</button>

  <!-- transition is a component provided by Vue -->
  <!-- transition will add the following classes:  -->
  <!-- *-enter-from *-enter-active *-enter-to -->
  <!-- *-leave-from *-leave-active *-leave-to -->
  <!-- by default, * is gonna be v so: v-enter-from etc -->
  <!-- to customise *, gotta set "name" attribute on transition component -->
  <transition name="fade">
    <h1 v-if="flag">Hello world! I'm here! I'm ready!</h1>
  </transition>
</template>

<script>
export default {
  name: "App",

  data() {
    return {
      flag: false
    };
  }
};
</script>

<style>
#app {
  font-family: monospace;
  font-size: 1.6rem;
  color: #2c3e50;
  padding: 4rem;
}

button {
  background: transparent;
  font: inherit;
  padding: 0.4rem 0.8rem;
  border: 2px solid #2c3e50;
  cursor: pointer;
}

/* applied to elements entering the page */
/* don't need to set opacity to 1 at the end of animation */
/* as this class will be removed by Vue */
.fade-enter-from {
  opacity: 0;
}

.fade-enter-active,
.fade-leave-to {
  transition: opacity 0.4s linear;
}

.fade-leave-to {
  opacity: 0;
}
</style>
