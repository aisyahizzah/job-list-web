<template>
    <div id="header">
        <VueFixedHeader
        @change="updateFixedStatus"
        :threshold="propsData.threshold"
        :headerClass="propsData.headerClass"
        :fixedClass="propsData.fixedClass"
        :hideScrollUp="propsData.hideScrollUp"
        >
        <nav>
            <div class="menu">
                <el-row>
                    <img class="logo" src="../assets/logo.png"/>
                </el-row>
                <el-row class="search-wrapper">
                   <el-input class="search_bar" placeholder="Search position or company" prefix-icon="el-icon-search" v-model="filter"></el-input>
                </el-row>
            </div>
        </nav>
        </VueFixedHeader>
    </div>
</template>

<script>
import Vue from "vue";
import VueFixedHeader from "vue-fixed-header";

const createData = () => ({
  threshold: 0,
  headerClass: "vue-fixed-header",
  fixedClass: "vue-fixed-header--isFixed",
  hideScrollUp: false
});

export default Vue.extend({
  components: {
    VueFixedHeader,
  },
  data() {
    return {
      fixedStatus: {
        headerIsFixed: false
      },
      propsData: { ...createData() },
      filter: '',
      sort: '',
      value: [],
      options: [
      { label: 'Default', value: 'none' },
      { label: 'Timestamp', value: 'Timestamp' },
      { label: 'Salary', value: 'Salary' }],
    };
  },
  methods: {
    updateFixedStatus(next) {
      this.fixedStatus.headerIsFixed = next;
    }
  },
  watch: {
    filter: function() {
      this.$emit("filter", this.filter);
    }
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

nav {
  display: flex;
  margin: 0;
  padding: 10px 0px !important;
  background-color: #5da5a4 !important;
}

.menu {
    display: flex;
    justify-content: flex-start;
    width: 1000px;
    margin: 0 auto;
}

.heading {
  margin-top: 0;
  padding-top: 0;
}

.justify-right {
  display: flex;
  justify-content: flex-end;
}

.search-wrapper {
    max-width: 300px;
    padding-left: 10px !important;
}

.logo {
  display: block;
  margin: auto auto;
  width: 40px;
  height: 40px;
}

.search_bar{
  width: 250px !important;
}

</style>