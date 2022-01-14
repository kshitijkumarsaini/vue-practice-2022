<template>
  <!-- <button type="button" @click="flag = !flag">Toggle</button> -->

  <!-- <transition name="fade" mode="out-in">
    <h2 v-if="flag" key="main">Hello World!</h2>
    <h2 v-else key="secondary">Another Hello</h2>
  </transition> -->

  <!-- 
  Appear: this attribute is used to run the animation when page loads
  type: this attribute is used to control the duration of animation (accept duration from transition/animation effects)
 -->
  <!-- <transition name="zoom" appear>
    <h2 v-if="flag">Hello</h2>
  </transition> -->

  <!-- Animation with Javascript in Vue -->
  <!-- [css="false"] it will allow vue to understand we don't have any css animation for the element
    so it will use javascript animations which will help optimize the animations
  -->
  <!-- <transition
    @before-enter="beforeEnter"
    @enter="enter"
    @after-enter="afterEnter"
    @before-leave="beforeLeave"
    @leave="leave"
    @after-leave="afterLeave"
    :css="true"
    name="fade"
  >
    <h2 v-if="flag">Hello</h2>
  </transition> -->

  <!-- Animating a list -->
  <button type="button" @click="addItem">Add</button>

  <ul>
    <transition-group name="fade">
      <li v-for="(n, index) in num" :key="n" @click="removeItem(index)">
        {{ n }}
      </li>
    </transition-group>
  </ul>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      flag: false,
      num: [1, 2, 3, 4, 5],
    };
  },
  methods: {
    addItem() {
      //get random number
      const number = Math.floor(Math.random() * 100 + 1);
      // get random index from array
      const index = Math.floor(Math.random() * this.num.length);
      // push a number in the array instead of removing
      this.num.splice(index, 0, number);
    },
    removeItem(index) {
      this.num.splice(index, 1);
    },
    beforeEnter(el) {
      console.log("before Enter ", el);
    },
    enter(el) {
      // can also use done as 2nd param
      console.log("enter ", el);
      // const animation = el.animate([{ transform: "scale3d(0, 0, 0)" }, {}], {
      //   duration: 1000,
      // });
      // animation.onfinish = () => {
      //   done();
      // };
    },
    afterEnter(el) {
      console.log("after enter ", el);
    },
    beforeLeave(el) {
      console.log("before Leave ", el);
    },
    leave(el) {
      // can also use done as 2nd param
      console.log("leave ", el);
      // const animation = el.animate([{}, { transform: "scale3d(0, 0, 0)" }], {
      //   duration: 1000,
      // });
      // animation.onfinish = () => {
      //   done();
      // };
    },
    afterLeave(el) {
      console.log("after leave ", el);
    },
  },
};
</script>

<style scoped>
li {
  font-size: 22px;
  cursor: pointer;
}

h2 {
  width: 400px;
  padding: 20px;
  margin: 20px;
}

.fade-enter-from {
  opacity: 0%;
}

.fade-enter-active {
  transition: all 0.5s linear;
}

.fade-leave-to {
  transition: all 0.5s linear;
  opacity: 0%;
}

.fade-move {
  transition: all 1s linear;
}

.fade-leave-active {
  position: absolute;
}

.zoom-enter-active {
  animation: zoom-in 1s linear forwards;
}

.zoom-leave-active {
  animation: zoom-out 1s linear forwards;
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
