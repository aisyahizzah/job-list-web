<template>
    <div class="filter_container">
        <el-select style="width: 100px !important" v-model="hint_sort" placeholder="Sort by">
          <el-option
              v-bind:key="item.value"
              v-for="item in options_sort"
              :label="item.label"
              :value="item.value">
          </el-option>
        </el-select>
        <el-select style="width: 110px !important" v-model="value_location" multiple placeholder="Location">
          <el-option
              v-bind:key="item.value"
              v-for="item in options_location"
              :label="item.label"
              :value="item.value">
          </el-option>
        </el-select>
        <el-select style="width: 110px !important" v-model="value_type" multiple placeholder="Job Type">
          <el-option
              v-bind:key="item.value"
              v-for="item in options_type"
              :label="item.label"
              :value="item.value">
          </el-option>
        </el-select>
        <el-select style="width: 160px !important" v-model="value_level" multiple placeholder="Experience Level">
          <el-option
              v-bind:key="item.value"
              v-for="item in options_level"
              :label="item.label"
              :value="item.value">
          </el-option>
        </el-select>
        <el-select style="width: 205px !important" v-model="value_language" multiple placeholder="Programming Language">
          <el-option
              v-bind:key="item.value"
              v-for="item in options_language"
              :label="item.label"
              :value="item.value">
          </el-option>
        </el-select>
    </div>
</template>

<script>
export default {
  name: 'Filter',
  data: function() {
    return {
      hint_sort: '',
      value_type: [],
      value_level: [],
      value_location: [],
      value_language: [],
      options_sort: [
      { label: 'Default', value: 'none' },
      { label: 'Time', value: 'Time' },
      { label: 'Salary', value: 'Salary' }],
      options_type: [
      { label: 'Full time', value: 'Full time' },
      { label: 'Part time', value: 'Part time' },
      { label: 'Contract', value: 'Contract' },
      { label: 'Freelance', value: 'Freelance' }],
      options_level: [
      { label: 'Intern', value: 'Intern' },
      { label: 'Junior', value: 'Junior' },
      { label: 'Senior', value: 'Senior' }],
      options_location: [
      { label: 'Jakarta', value: 'Jakarta' },
      { label: 'Bandung', value: 'Bandung' }],
      options_language: [
      { label: 'Python', value: 'Python' },
      { label: 'Java', value: 'Java' },
      { label: 'HTML', value: 'HTML' },
      { label: 'CSS', value: 'CSS' },
      { label: 'PHP', value: 'PHP' },
      { label: 'JavaScript', value: 'JavaScript' }],  
    }
  }
}
</script>

<style scoped>
.el-select {
  margin: 20px 5px;
}

.filter_container{
  background-color: white;
  margin-bottom: 15px;
  padding-left: 50px;
  display: flex;
}

.filter {
  width: 70;
  padding: 2px;
  margin: 0px 5px 0px 5px;
}
</style>
