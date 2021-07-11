<template>
  <button @click="flag = !flag">animate with css and js</button>

  <transition
    @before-enter="beforeEnter"
    @enter="enter"
    @after-enter="afterEnter"
    @before-leave="beforeLeave"
    @leave="leave"
    :css="true"
    name="fade"
  >
    <p v-if="flag">hey</p>
  </transition>
</template>

<script>
export default {
  name: "AppCSSAndJsTransitions",

  data() {
    return {
      flag: false
    };
  },

  methods: {
    beforeEnter(el) {
      console.log("before-enter", el);
    },
    // gotta remove done() argument as Vue will assume that we want JS animation
    // without done() Vue will pick up CSS duration to determine when animation is complete
    enter(el) {
      console.log("enter", el);
    },
    afterEnter(el) {
      console.log("after-enter", el);
    },
    beforeLeave(el) {
      console.log("before-leave", el);
    },
    leave(el) {
      console.log("leave", el);
    }
  }
};
</script>

// using animations web api // animate function only exists on DOM objects and
is not specific to Vue // animate() takes 2 arguments: array of animated
properties and settings object // don't need to scale the element to original
size as the browser will do that for us
