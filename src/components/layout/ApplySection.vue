<template>
    <div id="apply-section">
        <div class="content-wrapper">
            <div class="site-section">
                <div class="close-btn-container">
                    <button class="close" @click="$emit('click-close')">X</button>
                </div>
                <div :style="bgColor" class="logo-container">
                    <img class="logo" :src="require('../../../static' + Job.logo.substring(1))" alt="">
                </div>
                <div class="company-wrapper">
                    <p class="company">{{Job.company}}</p>
                    <p class="company-site">{{Job.company.toLowerCase() + '.com'}}</p>
                </div>
                <button><a :href="Job.website">Company Site</a></button>
            </div>
            <div class="apply-job-section">
                <div class="apply-wrapper">
                    <div class="apply-header">
                        <div class="header-wrapper">
                            <div class="left-header">
                                <p>{{Job.postedAt}} <span>{{Job.contract}}</span></p>
                                <p class="job-position">{{Job.position}}</p>
                                <p class="job-location">{{Job.location}}</p>
                            </div>
                            <div class="right-header">
                                <button class="apply-btn">Apply Now</button>
                            </div>
                        </div>

                        <div class="apply-content">
                            <p class="apply-description">{{Job.description}}</p>
                            <div class="apply-requirements">
                                <p class="title">Requirements</p>
                                <p class="requirements-content">{{Job.requirements.content}}</p>
                                <ul>
                                    <li v-for="item in Job.requirements.items" v-bind:key="item.id">{{item}}</li>
                                </ul>
                            </div>
                            <div class="apply-role">
                                <div class="title">What You Will Do</div>
                                <p class="role-content">{{Job.role.content}}</p>
                                <ol>
                                    <li v-for="item in Job.role.items" v-bind:key="item.id" >{{item}}</li>
                                </ol>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        <div class="apply-footer">
            <div class="footer-wrapper">
                <div class="watermark">
                    <p class="title">{{Job.position}}</p>
                    <p>So Digital Inc.</p>
                </div>
            <button class="apply-btn">Apply Now</button>
            </div>
        </div>
    </div>
</template>
<script>
export default {
    data(){
        return{
            bgColor:{
                backgroundColor: this.Job.logoBackground
            },
        }
    },
    props:{
        Job: Object,
    },
}
</script>
<style scoped>
    .close-btn-container{
        height: 0px;
        position: relative;
    }
    .close{
        position: absolute;
        background-color: #303742;
        width: 30px;
        height: 30px;
        border: 1px solid black;
        right: -15px;
        top: -15px;
        border-radius: 20px;
        line-height: 0px;
        z-index: 1;
        color:white;
        font-size: 12px;
    }
    .close:hover{
        background-color: #525253;
        cursor: pointer;
    }
    .apply-btn:hover{
        background-color: #939BF4;
        cursor:pointer;
    }
    .site-section{
        text-align: center;
        background-color: var(--card-color);
        height: 205px;
        border-radius: 6px;
        line-height: 100%;
        width: var(--container-width);
        margin: auto;
    }
    .logo-container{
        width: 50px;
        height: 50px;
        position: absolute;
        top: -5px;
        left: 0;
        right: 0;
        margin: auto;
        border-radius: 16px;
    }
    .logo{
        position: absolute;
        top: 0;
        bottom: 0;
        left: 0;
        right: 0;
        margin: auto;
    }
    .company{
        padding-top: 50px;
        font-weight: bold;
        color:var(--text-position);
        font-size: 2rem;
    }
    .company-site{
        padding-bottom: 10px;
    }
    .site-section > button{
        background-color: rgba(89, 100, 224, 0.1);
        border:none;
        border-radius: 5px;
        height: 48px;
        width: 150px;
    }
    .site-section > button:hover{
        background-color: var(--company-site-desktop-hover);
        cursor: pointer;
    }
    a{
        color: var(--text-alt);
        text-decoration: none;
    }
    .apply-job-section{
        padding-bottom: 50px;
        padding-top: 26px;
    }
    .apply-wrapper{
        background-color: var(--card-color);
        border-radius: 6px;
        width: var(--container-width);
        color: var(--apply-color);
        padding-top: 20px;
        margin-top: 20px;
        line-height: 2.6rem;
        margin: auto;
    }
    .left-header p{
        line-height: 1.1rem;
    }
    .left-header p > span{
        padding-left: 20px;
    }
    .left-header p > span::before{
        content: "●";
        font-size: 1rem;
        position: relative;
        left: -12.5px;
    }
    .apply-header{
        max-width: 279px;
        margin: auto;
    }
    .job-position{
        font-size: 2rem;
        color: var(--text-position);
        font-weight: bold;
    }
    .job-location{
        color: var(--text-alt);
        font-weight: bold;
        font-size: 1.4rem;
    }
    .right-header{
        padding-top: 40px;
        padding-bottom: 14px;
    }
    .apply-btn{
        height: 48px;
        background-color: var(--text-alt);
        color: white;
        border: none;
        width: 279px;
        display: block;
        border-radius: 5px;
    }
    .title{
        color: var(--text-position);
        font-size: 2rem;
        font-weight: bold;
        padding: 10px 0;
    }
    ul, ol{
        list-style: none;
        padding-left: 0;
        padding-top: 16px;
        line-height: 2.6rem;
        position: relative;
    }
    li{
        padding-bottom: 10px;
        padding-left: 30px;
    }
    ul li::before {
        content: "\2022";
        color: var(--text-alt);
        font-weight: bold;
        width: 16px;
        position: absolute;
        left: 0;
    }
    ol{
        counter-reset: li;
        padding-bottom: 26px;
    }
    ol li{
        counter-increment:li;
    }
    ol li::before {
        content: counter(li);
        color: var(--text-alt);
        font-weight: bold;
        width: 16px;
        position: absolute;
        left: 0;
    }
    .apply-footer{
        background-color: var(--card-color);
        height: 96px;
    }
    .watermark{
        display: none;
    }
    .footer-wrapper{
        display: flex;
        justify-content: center;
        align-items: center;
        height: 100%;
    }
    .apply-footer button{
        width:327px;
    }
@media screen and (min-width: 768px) {
    .apply-header{
        max-width: 593px;
    }
    .apply-header{
        flex-wrap: wrap;
    }
    .site-section{
        display: flex;
        align-items: center;
        height: 140px;
    }
    .logo-container{
        display: block;
        position: relative;
        margin: 0;
        height: 140px;
        width: 140px;
        border-radius: 0;
        top: 0;
        border-bottom-left-radius: 6px;
    }
    .logo{
        width: 81px;
        height: 100%;
        object-fit: contain;
    }
    .company-wrapper{
        padding-left: 40px;
    }
    .company{
        padding-top: 0;
        text-align: start;
        font-size: 2.4rem;
    }
    .site-section, .apply-wrapper{
        max-width: 690px;
    }
    .site-section > button{
        margin-left: auto;
        margin-right: 40px;
        background-color: var(--company-site-desktop-bg);
    }
    .site-section a{
        color: var(--company-site-desktop-color);
    }
    .job-position{
        font-size: 2.6rem;
    }
    .watermark{
        display:inline-block;
        overflow: hidden;
    }
    .watermark .title{
        padding: 0;
        line-height: 1.2rem;
    }
    .footer-wrapper{
        justify-content: space-between;
        width: 690px;
        margin: auto;
    }
    .header-wrapper{
        display: flex;
        justify-content: space-between;
    }
    .apply-btn, .apply-footer button {
        width: 141px;
    }
    .close-btn-container{
        left: 100%;
    }
    .close{
        top: -85px;
    }
}
</style>