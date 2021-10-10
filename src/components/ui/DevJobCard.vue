<template>
    <div class="dev-job-card" @click="$emit('user-click-on-card', Job )">
        <div :style="bgColor" class="card-logo-container">
            <img v-on="check" :src="require('../../../static' + Job.logo.substring(1))" alt="" class="card-logo">
        </div>
        <div class="card-content">
            <p>{{Job.postedAt}} <span>{{Job.contract}}</span></p>
            <p class="job-position">{{Job.position}}</p>
            <p>{{Job.company}}</p>
            <p class="job-location">{{Job.location}}</p>
        </div>
    </div>
</template>
<script>

export default {

    props:{
        Job: Object,
    },
    data(){
        return{
            bgColor:{
                backgroundColor: this.Job.logoBackground
            },
        }
    },
    computed:{
        check(){
            if (this.searchValue == ''){
                this.searchSubmit = '';
            }
        },
    }
}
</script>
<style scoped>
    .dev-job-card{
        width: 100%;
        width: 335px;
        height: 228px;
        background-color: var(--card-color);
        position: relative;
        border-radius: 6px;
        margin-bottom: 45px;
    }
    .dev-job-card:hover{
        cursor: pointer;
    }
    .card-logo-container{
        margin-left: 32px;
        width: 50px;
        height: 50px;
        position: absolute;
        top: -30px;
        border-radius: 16px;
    }
    .card-logo{
        position: absolute;
        top: 0;
        bottom: 0;
        left: 0;
        right: 0;
        margin: auto;
    }
    .card-content{
        padding-top: 28px;
    }
    p{
        padding-left: 32px;
        line-height: 1.2rem;
    }
    p > span{
        padding-left: 20px;
    }
    p > span::before{
        content: "●";
        font-size: 1rem;
        position: relative;
        left: -12.5px;
    }
    .job-position{
        font-size: 2rem;
        color: var(--text-position);
        font-weight: bold;
        line-height: 26px;
        max-width: 95%;
    }
    .job-location{
        padding-top: 28px;
        color: var(--text-alt);
        font-weight: bold;
        font-size: 1.4rem;
    }
    @media screen and (min-width: 768px) {
        .dev-job-card{
            margin-bottom: 40px;
        }     
    }
    @media screen and (min-width: 1280px){
        .dev-job-card{
            max-width: 350px;
        }
    }
</style>
