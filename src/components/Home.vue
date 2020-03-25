<template>
  <div>
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
      <el-row>

        <el-col class="job_card" v-bind:key="job" v-for="job in getJobs">
          <el-card class="job_list">
            <div class="job_container">
              <div class="nested_flex">
                <div class="logo_container">
                  <img class="company_logo" :src="job.photo">
                </div>
                <div class="job_info">
                  <div class="job_position"> {{ job.position }} </div>
                  <div class="company_name"> {{ job.name }} </div>
                  <div class="job_location"> {{ job.location }} </div>
                  <div class="job_detail"> {{ job.type }} · {{ job.salary }} </div>
                </div>
              </div>
              <div>
                <div class=job_timestamp>Posted {{ job.posted }} days ago</div>
                <div class="tags_container">
                  <div class="job_tag" v-bind:key="tag" v-for="tag in job.tag">{{tag}}</div>
                </div>
              </div>
            </div>
          </el-card>
        </el-col>

        <el-col v-if="getJobs.length === 0">
          <div> No Match Found</div>
        </el-col>

      </el-row> <!-- results -->

 </div> <!-- container -->

</template>

<script>
export default {
  name: 'Home',
  props: {
    filter: {
      type: String
    }
  },
  data: function() {
    return { 
      jobs: [
        { photo: require('../assets/MyCompany.png'), position: 'Software Engineer', name: 'MyCompany', location: "Jakarta, Indonesia", type: "Full time", salary: "2500000 - 3500000 IDR/month", posted:2, tag: ["Intern","Fullstack","Javascript","PHP"]},
        { photo: require('../assets/HelloWorld.png'), position: 'Frontend Engineer', name: 'HelloWorld', location: "Bandung, Indonesia", type: "Part time", salary: "4000000 - 4500000 IDR/month", posted:3, tag: ["Intern","Frontend","Java"]},
        { photo: require('../assets/Puzzles.png'), position: 'Data Analyst', name: 'Puzzles', location: "Bandung, Indonesia", type: "Full time", salary: "2500000 - 3000000 IDR/month", posted:5, tag: ["Junior","Data","NoSQL"]},
        { photo: require('../assets/Panda.png'), position: 'AI Engineer', name: 'Panda', location: "Jakarta, Indonesia", type: "Part time", salary: "3500000 - 4000000 IDR/month", posted:10, tag: ["Senior","Python"]},
      ],
      hint_sort: '',
      value_type: [],
      value_level: [],
      value_location: [],
      value_language: [],
      options_sort: [
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
  },
  computed: {
    getJobs() {

      var jobs = this.jobs.filter(job => {
        
        // search bar
        var lower_case_filter = this.filter.toLowerCase()
        const regex = RegExp("^[A-Za-z0-9 ]*" + lower_case_filter + "[A-Za-z0-9 ]*$");
        const match_pos = regex.test(job.position.toLowerCase());
        const match_com = regex.test(job.name.toLowerCase());
        if ((match_pos) || (match_com)){
          return job;
        }
        if (this.filter == ''){
          return job;
        }
      })

      // location 
      if (this.value_location != ""){
         jobs = jobs.filter(job => {
           for (const loc of this.value_location){
             const regex_loc = RegExp(loc);
             const match_loc = regex_loc.test(job.location);
             if (match_loc){
               return job;
             }
           }
         })
      }
      
      // Job type 
      if (this.value_type != ""){
         jobs = jobs.filter(job => {
           for (const type of this.value_type){
             const regex_type = RegExp(type);
             const match_type = regex_type.test(job.type);
             if (match_type){
               return job;
             }
           }
         })
      }

      // Job Level 
      if (this.value_level != ""){
         jobs = jobs.filter(job => {
           for (const level of this.value_level){
             const regex_level = RegExp(level);
             for (const tag1 of job.tag){
                const match_level = regex_level.test(tag1);
                if (match_level){
                  return job;
                }
             }
           }
         })
      }

      // Job Prog Language 
      if (this.value_language != ""){
         jobs = jobs.filter(job => {
           for (const language of this.value_language){
             const regex_language = RegExp(language);
             for (const tag2 of job.tag){
                const match_language = regex_language.test(tag2);
                if (match_language){
                  return job;
                }
             }
           }
         })
      }

      // sort
      if (this.hint_sort == 'Time') {
        return jobs.sort(function (a, b) {
          return a.posted - b.posted;
        });
      } if (this.hint_sort == 'Salary') {
        return jobs.sort(function (a, b) {
          var a_salary = a.salary.substring(0, 7);
          var b_salary = b.salary.substring(0, 7);
          return b_salary - a_salary;
        })
      } else {
        return jobs;
      }

    } 
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
@import url('https://fonts.googleapis.com/css?family=Open+Sans');

.input.style{
  height: 30px !important;
}

.search-wrapper {
  margin: 10px 0;
}

.col-space {
  content: '&nbsp;';
  @media screen and (max-width: 767px) { display: none; }
}

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

.job_card{
  margin-bottom: 5px;
}

.job_list{
  text-align: left !important;
}

.job_container{
  display: flex;
  justify-content: space-between;
}

.nested_flex{
  display: flex;
  position: relative;
}

.company_name{
  color: #7C7C7C;
  font-size: 15px;
}

.company_logo{
  display: block;
  margin: auto 0;
  height: 50px;
  width: 50px;
}

.logo_container{
  position: absolute;
  top: 50%;
  -ms-transform: translateY(-50%);
  transform: translateY(-50%);
}

.job_info{
  margin-left: 70px;
}

.job_position{
  color: #64BABB;
  font-size: 20px;
  font-weight: 600;
}

.job_location{
  color: #7C7C7C;
  font-size: 13px;
}

.job_detail{
  color: #9C9B9B;
  font-size: 13px;
}

.job_timestamp{
  text-align: right;
  color: #9C9B9B;
  font-size: 13px;
}

.tags_container{
  display: flex;
  justify-content: space-between;
  margin-top: 5px;
}

.job_tag{
  background-color: #F0FAFB;
  padding: 5px 10px;
  margin-left: 10px;
  color: #5DA5A4;
  font-size: 15px;
  font-weight: 600;
}

</style>
