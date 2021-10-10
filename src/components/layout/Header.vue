<template>
    <header>
        <div id="header">
            <div class="logo-container"><img src="../../assets/images/logo.svg" alt="" srcset=""></div>
            <mode-selector/>
        </div>
    </header>
</template>

<script>
import ModeSelector from '../ui/ColorModeSelector.vue'
export default {
    name: 'Header',
    components: {
        ModeSelector
    }
}
</script>

<style scoped>
    header{
        height: 136px;
        background-image: var(--header-img);
        background-repeat: no-repeat;
        background-size: cover;
    }
    #header{
        width: var(--container-width);
        margin: auto;
        padding-top: 35px;
        display: flex;
        justify-content: space-between;
    }
    @media screen and (min-width:768px) {
        header{
            background-position-y: -5px;
        }
    }
</style>