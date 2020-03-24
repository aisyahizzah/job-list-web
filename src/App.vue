<template>
  <div id="app">
    <Header @filter="updateFilter" />
    <div class="container" :class="{
      headerIsFixed: fixedStatus.headerIsFixed
    }">
      <Home :filter="childData"/>
    </div>
  </div>
</template>

<script>
import Home from './components/Home.vue';
import Header from './components/Header.vue';

const createData = () => ({
  threshold: 0,
  headerClass: "vue-fixed-header",
  fixedClass: "vue-fixed-header--isFixed",
  hideScrollUp: false
});

export default ({
  components: {
    Header,
    Home
  },
  data() {
    return {
      fixedStatus: {
        headerIsFixed: false
      },
      propsData: { ...createData() },
      childData: "",
    };
  },
  methods: {
    updateFixedStatus(next) {
      this.fixedStatus.headerIsFixed = next;
    },
    updateFilter(variable) {
      this.childData=variable;
    },
  }
});
</script>

<style>
html,
body,
#app {
  width: 100vw;
  min-height: 150vh;
  margin: 0;
  padding: 0;
  background: #f0fafb;
  overflow-x: hidden;
}

.flex-1 {
  flex: 1;
}

*,
*::before,
*::after {
  box-sizing: border-box;
}

.menu-brand {
  pointer-events: none !important;
}

#app {
  font-family: "Hind", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  text-align: center;
}

.container {
  max-width: 1000px;
  margin-top: 20px;
  margin-left: auto;
  margin-right: auto;
}

nav {
  display: flex;
  width: 100vw;
  margin: 0;
  padding: 0;
  background: #fff;
  border-bottom: 1px #e5e5e5;
}

.el-menu {
  background-color: #5da5a4 !important;
}

nav.vue-fixed-header--isFixed {
  position: fixed;
  left: 0;
  top: 0;
  z-index: 1000;
}

.container.headerIsFixed {
  transform: translateY(56px) !important;
}

.heading {
  margin-top: 0;
  padding-top: 0;
}

ul {
  flex: 1;
  display: flex;
  align-content: stretch;
  justify-content: flex-start;
  list-style: none;
}

li {
  padding: 8px 16px;
}

.justify-right {
  display: flex;
  justify-content: flex-end;
}

</style>