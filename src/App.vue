<template>
  <button @click="flag = !flag">toggle animation</button>

  <!-- transition is a component provided by Vue -->
  <!-- transition will add the following classes:  -->
  <!-- *-enter-from *-enter-active *-enter-to -->
  <!-- *-leave-from *-leave-active *-leave-to -->
  <!-- by default, * is gonna be v so: v-enter-from etc -->
  <!-- to customise *, gotta set "name" attribute on transition component -->

  <!-- <transition name="fade">
       <h1 v-if="flag" key="primary">Hello world! I'm here! I'm ready!</h1>
       </transition> -->

  <!-- by default, Vue will animate the second element in and animate the first element out -->
  <!-- mode attribute determines the order of animation -->
  <!-- the default mode value is "in-out" -->
  <transition name="fade" mode="out-in">
    <h1 v-if="flag" key="primary">Hello world! I'm here! I'm ready!</h1>
    <h2 v-else key="secondary">Another hello!</h2>
  </transition>

  <!-- Vue will pick up the duration from specified CSS -->
  <!-- however it's possible to specify the duration explicitly -->
  <transition name="fade" duration="5000">
    <!-- v-show also works -->
    <p v-show="flag">Hello world! 5sec...</p>
  </transition>

  <button @click="zoom = !zoom">ZOOM</button>

  <!-- type attribute tells Vue to pick up duration from CSS animation, not transition -->
  <transition name="zoom" type="animation">
    <p v-if="zoom">hell(o)</p>
  </transition>
</template>

<script>
export default {
  name: "App",

  data() {
    return {
      flag: false,
      zoom: false
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
  /* Vue will pick up the animation duration from here */
  transition: opacity 0.4s linear;
}

.fade-leave-to {
  opacity: 0;
}

.zoom-enter-active,
.zoom-leave-active {
  transition: all 1s linear;
}

.zoom-enter-active {
  animation: zoom-in 1s linear forwards;
}

.zoom-leave-active {
  animation: zoom-out 1s linear forwards;
}

.zoom-enter-from,
.zoom-leave-to {
  opacity: 0;
}

@keyframes zoom-in {
  from {
    transform: scale(0, 0);
  }

  to {
    transform: scale(1, 1);
  }
}

@keyframes zoom-out {
  from {
    transform: scale(1, 1);
  }

  to {
    transform: scale(0, 0);
  }
}
</style>
