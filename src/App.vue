<template>
  <div class="container">
    <Header/>
    <main>
      <apply-section :Job="applyData" v-if="Object.keys(applyData).length > 0" @click-close="closeCard"/>
      <div class="app-container">
        <div v-show="Object.keys(applyData).length == 0" class="app-wrapper">
          <search-bar ref="searchBar"/>
          <div class="jobs-container" v-if="waitMount">
            <DevJobCard @user-click-on-card="userClickOnCard" :Job="item" v-for="item in filterSearch" v-bind:key="item.id"/>
          </div>
          <button class="load-more" v-if="!loadMore" @click="loadMore = !loadMore">Load More</button>
        </div>
      </div>
    </main>
  </div>
</template>

<script>
import JobsData from './assets/json/data.json'
import Header from './components/layout/Header.vue'
import SearchBar from './components/ui/SearchBar.vue'
import ApplySection from './components/layout/ApplySection.vue'
import DevJobCard from './components/ui/DevJobCard.vue'

export default {
  components: {
    Header,
    SearchBar,
    ApplySection,
    DevJobCard,
  },
  data(){
    return{
      Jobs: JobsData,
      waitMount: false,
      applyData:{},
      loadMore: false,
    }
  },
  methods:{
    userClickOnCard(Job) {
      this.applyData = Job
    },
    closeCard(){
      this.applyData = {}
    },
    loadMoreCards(){

    }
  },
  computed:{
    filterSearch () {
      let jobsFiltered = this.Jobs.filter(job => {
        return job.position.toLowerCase().includes(this.$refs.searchBar.searchSubmit.toLowerCase())
      })
      let locationsFiltered = jobsFiltered.filter(job => {
        return job.location.toLowerCase().includes(this.$refs.searchBar.searchLocationSubmit.toLowerCase())
      })
      let fullTimeFiltered = function (){
              if (this.$refs.searchBar.fullTimeSubmit === true){
        return locationsFiltered.filter(job => {
          return job.contract === "Full Time"
        })
        } else{
          return locationsFiltered
        }
      }
      let count = 0;
      return jobsFiltered.filter(job => {
        count++
        if(this.loadMore == false){
          return count <= 12
        }
        return true
      })
    },
    showApply(){
      return Object.keys(this.applyData).length > 0;
    }
  },
   mounted(){
    this.waitMount = true
    document.documentElement.setAttribute("data-theme", "dark");
  }
};
</script>
<style>
@import url('https://fonts.googleapis.com/css2?family=Kumbh+Sans:wght@400;700&display=swap');

:root{
  --text-color: #6E8098;
  --text-alt: #5964E0;
  --d-blue: #19202D;
  --vd-blue: #121721;
  --header-img: url('./assets/images/mobile/bg-pattern-header.svg');
  --container-width: 327px;
}
[data-theme="dark"] {
  --bg-color: var(--vd-blue);
  --card-color: var(--d-blue);
  --text-position: white;
  --filter-icon: brightness(10);
  --round: 25px;
  --full-time: rgba(255,255,255,0.1);
  --apply-color: #9DAEC2;
  --company-site-desktop-color: white;
  --company-site-desktop-bg: rgba(255, 255, 255, 0.1);
  --company-site-desktop-hover: rgba(201, 201, 201, 0.25);
}
[data-theme="light"] {
  --bg-color: #F4F6F8;
  --card-color: white;
  --text-position: var(--d-blue);
  --filter-icon: brightness(0.5);
  --round: -25px;
  --full-time: rgba(0,0,0,0.05);
  --apply-color:var(--text-color);
  --company-site-desktop-color: var(--text-alt);
  --company-site-desktop-bg: rgba(89, 100, 224, 0.1);
  --company-site-desktop-hover: rgba(89, 100, 224, 0.25);
}
body{
  margin: 0;
  background-color: var(--bg-color);
  color: var(--text-color);
  font-family: 'Kumbh Sans', sans-serif;
  font-size: 1.6rem;
}
.load-more{
  height: 48px;
  width: 141px;
  background-color: var(--text-alt);
  border: none;
  border-radius: 5px;
  color: white;
  margin: auto;
  display: block;
  margin-bottom: 40px;
}
.load-more:hover{
  background-color: #939BF4;
  cursor: pointer;
}
button{
  font-size: 1.6rem;
  font-weight: bold;
  font-family: 'Kumbh Sans', sans-serif;
}
html{
  font-size: 62.5%;
}
*{
  box-sizing: border-box;
}
.app-container{
  max-width: var(--container-width);
  margin: auto;
  padding-top: 100px;
}
.jobs-container{
  margin: auto;
  display: flex;
  justify-content: space-between;
  flex-wrap: wrap;
  align-items: center;
  padding-top: 10px;
}
#search-bar{
  position: absolute;
  top: 100px;
}
#apply-section{
  position: absolute;
  left: 0; 
  right: 0; 
  margin: auto;
  top: 100px;
}
@media screen and (min-width:768px) {
  :root{
    --container-width: clamp(690px, 87.5vw, 1110px);
    --header-img: url('./assets/images/tablet/bg-pattern-header.svg');
  }
  .jobs-container{
    gap:0px;
    width: clamp(690px,75vw,750px);
  }
  header{
    border-bottom-left-radius: 80px;
  }
}
@media screen and (min-width:1280px) {
  :root{
    --container-width: 1110px;
  }
  .jobs-container{
    width: clamp(690px,87.5vw,100%);
    justify-content:flex-start;
    gap: 30px;
    margin: auto;
    padding-top: 50px;
  }
}
</style>