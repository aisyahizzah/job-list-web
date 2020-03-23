<template>
  <div>
      <el-row>

        <el-col v-bind:key="job" v-for="job in getJobs">
          <el-card class="job_list">
            <div class="job_container">
              <div>
                <img class="company_logo" src="../assets/logo.png">
              </div>
              <div class="job_info">
                <div class="job_position"> {{ job.position }} </div>
                <div class="company_name"> {{ job.name }} </div>
                <div class="job_location"> {{ job.location }} </div>
                <div class="job_detail"> {{ job.type }} · {{ job.salary }} </div>
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
        { position: 'Software Engineer', name: 'MyCompany', location: "Jakarta, Indonesia", type: "Full-time", salary: "2,500,000 IDR/month", posted:2, tag: ["Intern","Fullstack","Javascript","PHP"]},
        { position: 'Front-end Engineer', name: 'HelloWorld', location: "Bandung, Indonesia", type: "Part-time", salary: "3,500,000 - 4,000,000 IDR/month", posted:3, tag: ["Intern","Frontend","Java"]},
        { position: 'Data Analyst', name: 'Strawberry', location: "Bandung, Indonesia", type: "Full-time", salary: "2,500,000 - 3,500,000 IDR/month", posted:5, tag: ["Junior","Data","NoSQL"]},
        { position: 'AI Engineer', name: 'Panda', location: "Jakarta, Indonesia", type: "Part-time", salary: "3,500,000 - 4,500,000 IDR/month", posted:10, tag: ["Senior","Python"]},
      ]
    }
  },
  computed: {
    getJobs() {

      var jobs = this.jobs.filter(job => {
        return job.position.toLowerCase().includes(this.filter.toLowerCase());
      });

      if (this.sort == 'views') {
        return jobs.sort(function (a, b) {
          return b.views - a.views;
        });
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

.search-wrapper {
  margin: 10px 0;
}

.col-space {
  content: '&nbsp;';
  @media screen and (max-width: 767px) { display: none; }
}

.el-select {
  width: 100%;
}

.filter {
  width: 1110;
  padding: 5px;
  margin: 10px 0px 10px 0px;
  background-color: #ade0e0;
}

.job_list{
  text-align: left !important;
}

.job_container{
  display: flex;
  justify-content: space-between;
}

.job_info{
  flex-basis: 800px;
}

.company_name{
  color: #7C7C7C;
  font-size: 15px;
}

.company_logo{
  height: 50px;
  width: 50px;
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
