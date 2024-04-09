<script setup>
import { ref } from 'vue';
import AboutMe from './components/AboutMe.vue';
import Links from './components/Links.vue';
import FindMe from './components/FindMe.vue';

const listTabs = {
  AboutMe,
  Links,
  FindMe
};
const currentTab = ref('AboutMe');

</script>

<template>
  <div class="container">

    <div class="container-header">
      <img src="./assets/avatar.jpg" />
      <span>Ailelix</span>
    </div>

    <div class="container-main">
      <button
        class="tab-selection"
        v-for="(_, tab) in listTabs"
        :key="tab"
        @click="currentTab = tab"
        @mouseup=""
      >{{ tab }}</button>
      <div>
        <Transition name="fade" mode="out-in">
          <component class="tab-container" :is="listTabs[currentTab]"/>
        </Transition>
      </div>
    </div>

  </div>

</template>

<style scoped>
.container {
  display: flex;
  flex-direction: column;

  padding: 20px min(20px, 2vw) 20px min(20px, 2vw);

  border-radius: 20px;

  margin: 15vh auto auto auto;

  width: 90vw;
  max-width: 1200px;

  background-color: #1d1d1f;
}
.container-header {
  display: flex;
  flex-direction: row;
  align-items: center;

  padding-bottom: 20px;
  border-bottom: #00B294 solid 2px;
  margin-bottom: 1vh;
}
img {
  border-radius: 20px;
  width: 5vw;
  min-width: 80px;
}
span {
  padding-left: 20px;
  
  color: #f2f2f7;
  font-size: min(10vw, 4em);
}
.tab-selection {
  padding: 10px;

  border: none;

  margin-right: 10px;
  
  color: #f2f2f7;
  font-family: "Noto Sans SC";
  font-size: min(4vw, 1.2em);
  
  background-color: #1d1d1f;
  cursor: pointer;
  transition: color 0.5s;
}
.tab-selection:hover {
  color: #00B294;
}
.tab-container {
  padding: 10px 20px 10px 20px;
  margin-top: 1vh;

  border: #f2f2f7 solid 2px;
  border-radius: 10px;
}
</style>

<style>
html {
  height: 100%;
}
#app {
  font-family: "Noto Sans SC";
}
body {
  background: url("./assets/background.jpg") no-repeat center fixed;
  background-size: cover;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s ease;
}
.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>
