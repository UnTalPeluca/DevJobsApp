<template>
    <div id="color-mode-selector">
        <div class="icon-container"><img src="../../assets/images/icons/icon-sun.svg" alt=""></div>
        <div ref="theme-toggle" @click="toggleTheme" class="color-box"><div id="round"></div></div>
        <div class="icon-container"><img src="../../assets/images/icons/icon-moon.svg" alt=""></div>
    </div>
</template>
<script>
export default {
    name:'ModeSelector',
    data(){
        return{
            userPrefersDark: true
        }
    },
    methods:{
        toggleTheme(){
            if (this.userPrefersDark){
                document.documentElement.setAttribute("data-theme", "light");
                this.userPrefersDark = false;
            } else{
                document.documentElement.setAttribute("data-theme", "dark");
                this.userPrefersDark = true;
            }
        }
    }
}

</script>
<style scoped>
    #color-mode-selector{
        display: flex;
        align-items: center;
    }
    .color-box{
        width: 48px;
        height: 24px;
        background-color: white;
        border-radius: 12px;
        margin: 0 15px;
        position: relative;
    }
    .color-box:hover{
        cursor: pointer;
    }
    .color-box:hover>#round{
        background-color: #939BF4;
    }
    #round{
        width: 14px;
        height: 14px;
        background-color: var(--text-alt);
        position: absolute;
        top: 0;
        bottom: 0;
        right: 0;
        left: var(--round);
        margin: auto;
        border-radius: 20px;
        left: width 2s, height 2s, background-color 2s, transform 2s;;
    }
</style>