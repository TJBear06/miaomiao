<template>
    <div class="movie_body">
        <ul>
            <li v-for="item in movieList" :key="item.id">
                <div class="pic_show"><img :src="item.img | setWH('128.180')"></div>
                <div class="info_list">
                    <h2>{{item.nm}} 
                        <div v-show="item.version==='v3d imax'?'v3d imax':'v2d imax'">
                            <img v-if="item.version === 'v3d imax'" src="@/assets/3Dmaxs.png">
                            <img v-else="item.version === 'v2d imax'" src="@/assets/2Dmaxs.png">
                        </div>              
                    </h2>
                    <p v-show="item.sc===0?true:false"><span class="grade">{{item.wish}}</span>人想看</p>
                    <p v-show="item.sc===0?false:true">观众评分 <span class="grade">{{item.sc}}</span></p>
                    <p>主演：{{item.star}}</p>
                    <p>{{item.showInfo}}</p>
                </div>
                <div>
                    <div class="btn_pre" v-show="item.sc===0?true:false">
                        预售
                    </div>
                </div>
                <div class="btn_mall" v-show="item.sc===0?false:true">
                    购票
                </div>
            </li>
        </ul>
    </div>
</template>

<script>
export default {
    name: 'nowPlaying',
    data(){
        // type: "item.version"
        return {
            movieList: []
        }
    },
    mounted(){
        this.axios.get('http://localhost:8081/json/nowPlaying.json').then((res)=>{
            // console.log(res.data.movieList)
            this.movieList = res.data.movieList
        })
    }
}
</script>

<style scoped>
    #content .movie_body{ flex:1; overflow:auto;}
    .movie_body ul{ margin:0 12px; overflow: hidden;}
    .movie_body ul li{ margin-top:12px; display: flex; align-items:center; border-bottom: 1px #e6e6e6 solid; padding-bottom: 10px;}
    .movie_body .pic_show{ width:64px; height: 90px;}
    .movie_body .pic_show img{ width:100%;}
    .movie_body .info_list { margin-left: 10px; flex:1; position: relative;}
    .movie_body .info_list h2{ font-size: 17px; line-height: 24px; width:150px; overflow: hidden; white-space: nowrap; text-overflow:ellipsis;}
    .movie_body .info_list p{ font-size: 13px; color:#666; line-height: 22px; width:200px; overflow: hidden; white-space: nowrap; text-overflow:ellipsis;}
    .movie_body .info_list .grade{ font-weight: 700; color: #faaf00; font-size: 15px;}
    .movie_body .info_list img{ width:50px; position: absolute; right:10px; top: 5px;}
    .movie_body .btn_mall , .movie_body .btn_pre{ width:47px; height:27px; line-height: 28px; text-align: center; background-color: #f03d37; color: #fff; border-radius: 4px; font-size: 12px; cursor: pointer;}
    .movie_body .btn_pre{ background-color: #3c9fe6;}
</style>
