<template>
  <button @click="flag = !flag">animate with js</button>

  <!-- hooks provided by Vue:
       before-enter enter after-enter
       before-leave leave after-leave -->
  <!-- @enter-cancelled=""
       @leave-cancelled="" -->
  <!-- :css="false" tells Vue not to check for CSS animation -->
  <transition
    @before-enter="beforeEnter"
    @enter="enter"
    @after-enter="afterEnter"
    @before-leave="beforeLeave"
    @leave="leave"
    :css="false"
  >
    <p v-if="flag">hey</p>
  </transition>
</template>

<script>
export default {
  name: "AppJsAnimation",

  data() {
    return {
      flag: false
    };
  },

  methods: {
    // element argument is passed by Vue
    beforeEnter(el) {
      console.log("before-enter", el);
    },
    // gotta accept done argument in enter() and leave() hooks
    // done is a callback function that tells Vue that animation is complete
    // gotta call done() when animation is complete
    enter(el, done) {
      console.log("enter", el);

      // using animations web api
      // animate function only exists on DOM objects and is not specific to Vue
      // animate() takes 2 arguments:  array of animated properties and settings object
      // don't need to scale the element to original size as the browser will do that for us
      const animation = el.animate([{ transform: "scale3d(0, 0, 0)" }, {}], {
        duration: 2000
      });

      animation.onfinish = () => {
        done();
      };
    },
    afterEnter(el) {
      console.log("after-enter", el);
    },
    beforeLeave(el) {
      console.log("before-leave", el);
    },
    leave(el, done) {
      console.log("leave", el);

      const animation = el.animate([{}, { transform: "scale3d(0, 0, 0)" }], {
        duration: 2000
      });

      animation.onfinish = () => {
        done();
      };
    }
  }
};
</script>

<style scoped></style>
