<template>
  <button @click="addItem">add item</button>

  <ul>
    <!-- transition-group components is specifically for animating items in a loop -->
    <!-- can't set mode property on transition-group -->

    <!-- Vue will add a *-move class to elements that are being moved over -->
    <transition-group name="fade">
      <li v-for="(number, index) in numbers" :key="number">
        <button @click="removeItem(index)">
          {{ number }}
        </button>
      </li>
    </transition-group>
  </ul>
</template>

<script>
export default {
  name: "AppAnimatedList",

  data() {
    return {
      flag: false,
      numbers: [0, 1, 2, 3, 4, 5, 6]
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
    },
    addItem() {
      // generate random number in [1, 100]
      const num = Math.floor(Math.random() * 100 + 1);
      const index = Math.floor(Math.random() * this.numbers.length);
      this.numbers.splice(index, 0, num);
    },
    removeItem(index) {
      this.numbers.splice(index, 1);
    }
  }
};
</script>

<style>
.fade-move {
  transition: all 1s linear;
}

/* by using the absolute positioning the item fading away will give up its space forcing the other elements to move up */
.fade-leave-active {
  position: absolute;
}
</style>
