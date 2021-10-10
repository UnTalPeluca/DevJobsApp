<template>
    <div id="search-bar">
        <div class="search-bar-container">
            <img src="../../assets/images/icons/icon-search.svg" alt="">
            <input ref="inputSearch" @keyup.enter="search" v-model="searchValue" class="input" type="text" name="input-job" id="input-job" placeholder="Filter by title...">
        </div>
        <div id="search-overlay-mobile"></div>
        <div v-show="width < 768" class="search-bar-right-mobile">
            <div @click="toggleFilter" class="icon-filter-container">
                <img src="../../assets/images/icons/icon-filter.svg" alt="" srcset="">
            </div>
            <div class="search-btn-mobile" @click="search">
                <img src="../../assets/images/icons/icon-search.svg" alt="" srcset="">
            </div>        
        </div>
        <div v-show="showOverlay" class="overlay"></div>
        <div v-show="showOverlay || width >= 768" class="filter-search-desktop">
            <div class="search-bar-location">
                <img src="../../assets/images/icons/icon-location.svg" alt="">
                <input ref="inputLocation" @keyup.enter="search" @keyup.esc="showOverlay = false" v-model="searchLocation" class="input" type="text" name="input-location" id="input-location" placeholder="Filter by location...">
            </div>
            <div @click="fullTimeChecked = !fullTimeChecked" class="full-time">
                <button>
                    <div v-show="fullTimeChecked" class="check-container">
                        <img src="../../assets/images/icons/icon-check.svg" alt="">
                    </div>
                </button>
                <p id="full-time-only">Full Time Only</p>
                <p id="full-time">Full Time</p>
            </div>
            <div class="submit-wrapper">
                <button @click="search" class="submit-button">Search</button>
            </div>
        </div>
    </div>
</template>
<script>
export default {
    name:"SearchBar",
    data(){
        return{
            searchValue:'',
            searchSubmit:'',
            showOverlay: false,
            width: 0,
            searchLocation:'',
            searchLocationSubmit:'',
            fullTimeChecked:false,
            fullTimeSubmit:false,
        }
    },
    methods:{
        search(){
            this.searchSubmit = this.searchValue
            this.searchLocationSubmit = this.searchLocation
            this.fullTimeSubmit = this.fullTimeChecked
            this.showOverlay = false
        },
        resizedw() {
            this.width = window.innerWidth
            this.showOverlay = this.width >= 768 ? false : this.showOverlay
        },
        toggleFilter(){
            this.showOverlay = true
            setTimeout(() => this.$refs.inputLocation.focus(), 200);
        },
    },
    computed:{

    },
    mounted() {
        this.width = window.innerWidth;
        var doit;
        window.onresize = () => {
        clearTimeout(doit);
        doit = setTimeout(this.resizedw, 10);
        };
        this.$refs.inputSearch.focus()
    },
    destroyed() {
        window.onresize = null;
    },
}
</script>
<style scoped>
    .full-time{
        display: flex;
        justify-content: flex-start;
        align-items: center;
        padding: 0 24px;
        gap: 20px;
    }
    .full-time:hover, .full-time button:hover{
        cursor: pointer;
    }
    .full-time:hover button{
        background-color: #939BF4;
    }
    .full-time button{
        min-height: 24px;
        min-width: 24px;
        max-height: 24px;
        border-radius: 3px;
        border: none;
        background-color: var(--full-time);
        max-width: 24px;
    }
    .full-time p{
        color: var(--text-position);
        font-weight: bold;
    }
    .check-container{
        height: 24px;
        width: 24px;
        display: flex;
        align-items: center;
        justify-content: center;
        background-color: var(--text-alt);
        text-align: start;
        position: relative;
        left: -6px;
        top: -1px;
        border-radius: 3px;
    }
    .overlay{
        z-index: 1;
        background-color: rgba(0,0,0,0.5);
        width:      100%;
        height:     100%; 
        top:        0; 
        left:       0; 
        position:   fixed; 
    }
    .search-bar-container{
        padding-left: 20px;
    }
    .search-bar-container img{
        display: none;
    }
    .filter-search-desktop{
        display: block;
        position: fixed;
        margin: auto;
        top:250px;
        z-index: 1;
        background-color: var(--card-color);
        height: 217px;
        width: var(--container-width);
        border-radius: 6px;
    }
    .submit-wrapper{
        padding: 24px;
    }
    .submit-button{
        width: 100%;
        height: 48px;
        background-color: var(--text-alt);
        border: none;
        color: white;
        border-radius: 5px;
    }
    .submit-button:hover{
        background-color: #939BF4;
        cursor: pointer;
    }
    
    #search-bar{
        width: var(--container-width);   
        max-height: 80px;
        background-color: var(--card-color);
        border-radius: 6px;
        display: flex;
        justify-content: space-between;
    }
    .input{
        width: 100%;
        height: 80px;
        padding: 0;
        background:none;
        border: none;
        outline: none;
        font-size: 1.6rem;
        color: var(--text-position);
        font-family: 'Kumbh Sans', sans-serif;
    }
    ::placeholder{
        color: #8C8F96;
    }
    .search-bar-right-mobile{
        display: flex;
        justify-content: space-between;
        align-items: center;
        padding-right: 16px;
    }
    .icon-filter-container{
        width: 24px;
        height: 24px;
        position: relative;
        left: -24px;
    }
    .icon-filter-container:hover{
        cursor: pointer;
    }
    .icon-filter-container img{
        filter: var(--filter-icon);
        position: absolute;
        top: 0;
        bottom: 0;
        left: 0;
        right: 0;
        margin: auto;
    }
    .search-btn-mobile{
        height: 48px;
        width: 48px; 
        position: relative;
        background-color: var(--text-alt);
        border-radius: 5px;
    }
    .search-btn-mobile:hover{
        background-color: #939BF4;
        cursor:pointer;
    }
    .search-btn-mobile img{
        filter: brightness(10);
        position: absolute;
        top: 0;
        bottom: 0;
        left: 0;
        right: 0;
        margin: auto;
    }
    #input-location{
        height: 72px;
    }
    .search-bar-location{
        padding: 0 24px;
        display: flex;
        justify-content: flex-start;
        align-items: center;
        gap: 20px;
        border-bottom: 1px solid rgba(143, 143, 143, 0.1);
    }
    #full-time{
        display:none;
    }
    @media screen and (min-width:768px) {
        .filter-search-desktop{
            position: static;
            display: flex;
            height: 80px;
            align-items: center;
            width: 66%;
        }
        .search-bar-container{
            width: 33%;
        }
        .search-bar-location{
            border-bottom: none;
            width: 47.5%;
            border-left: 1px solid rgba(143, 143, 143, 0.1);
            border-right:1px solid rgba(143, 143, 143, 0.1);
        }
        .full-time{
            width: 35%;
            padding-right: 0;
            display: flex;
            position: relative;
        }
        .submit-wrapper{
            width: 20%;
        }
        #full-time-only{
            display: none;
        }
        #full-time{
            display: inline;
            text-overflow: clip;
            width: 100%;
        }
        .submit-wrapper{
            padding: 0;
            display: flex;
            justify-content: flex-end;
            padding-right: 16px;
        }
        .submit-button{
            width: 80px;
        }
    }
    @media screen and (min-width:1280px) {
        #full-time{
            display: none;
        }
        #full-time-only{
            display: block;
        }
        .submit-button{
            width: 123px;
        }
    }
</style>