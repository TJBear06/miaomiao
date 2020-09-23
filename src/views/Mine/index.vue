<template>
    <div id="main">
        <Header title="我的喵喵"/>
        <div id="content">
            <Login/>
        </div>
        <TabBar/>
    </div>
</template>

<script>
import Vue from 'vue'
import Header from '@/components/Header'
import TabBar from '@/components/TabBar'
import Login from '@/components/Login'

export default Vue.extend({
    name: 'Mine',
    components: {
        Header,
        TabBar,
        Login
    }
})
</script>

<style scoped>

</style>
