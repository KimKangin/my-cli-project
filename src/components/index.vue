<template>
    <div>
        <div class="section">
            <div class="location">
                <span>当前位置：</span>
                <a href="#/" class="router-link-active">首页</a> &gt;
                <a href="#/site/goodslist" class="router-link-exact-active router-link-active">购物商城</a>
            </div>
        </div>
        <div class="section">
            <div class="wrapper">
                <div class="wrap-box">
                    <div class="left-220" style="margin: 0px;">
                        <div class="banner-nav">
                            <ul>
                                <li v-for="item in catelist" :key="item.id">
                                    <h3>
                                        <i class="iconfont icon-arrow-right"></i>
                                        <span>{{ item.title }}</span>
                                        <p>
                                            <span v-for="item1 in item.subcates" :key="item1.id">
                                                {{ item1.title }}&nbsp;
                                            </span>
                                        </p>
                                    </h3>
                                    <div class="item-box">
                                        <dl>
                                            <dt>
                                                <a href="/goods/40.html">{{ item.title }}</a>
                                            </dt>
                                            <dd>
                                                <a href="/goods/43.html" v-for="item1 in item.subcates" :key="item1.id">{{ item1.title }}</a>
                                            </dd>
                                        </dl>
                                    </div>
                                </li>
                            </ul>
                        </div>
                    </div>
                    <!--幻灯片-->
                    <div class="left-705 carousel">
                        <el-carousel height="341px">
                            <el-carousel-item v-for="item in sliderlist" :key="item.id">
                                <img :src="item.img_url" alt="">
                            </el-carousel-item>
                        </el-carousel>
                    </div>
                    <!--/幻灯片-->
                    <div class="left-220">
                        <ul class="side-img-list">
                            <li v-for="(item, index) in toplist" :key="item.id">
                                <div class="img-box">
                                    <label>{{ index+1 }}</label>
                                    <img :src="item.img_url">
                                </div>
                                <div class="txt-box">
                                    <a href="/goods/show-98.html">{{ item.title }}</a>
                                    <span>{{ item.add_time | beautifyTime('年','月','日') }}</span>
                                </div>
                            </li>
                        </ul>
                    </div>
                </div>
            </div>
        </div>
        <div class="section" v-for="item in productlist" :key="item.level1cateid">
            <div class="main-tit">
                <h2>{{ item.catetitle }}</h2>
                <p>
                    <a href="/goods/43.html" v-for="item1 in item.level2catelist" :key="item1.subcateid">
                    {{ item1.subcatetitle }}
                    </a>
                    
                    <a href="/goods/40.html">更多
                        <i>+</i>
                    </a>
                </p>
            </div>
            <div class="wrapper clearfix">
                <div class="wrap-box">
                    <ul class="img-list">
                        <li v-for="item2 in item.datas" :key="item2.artID">
                            <router-link :to="`/detail/${item2.artID}`">
                            <!-- <a :href="`#/site/goodsinfo/${item2.artID}`" class=""> -->
                                <div class="img-box">
                                    <img v-lazy="item2.img_url">
                                </div>
                                <div class="info">
                                    <h3>{{ item2.artTitle }}</h3>
                                    <p class="price">
                                        <b>{{ item2.sell_price }}</b>元</p>
                                    <p>
                                        <strong>库存 {{ item2.stock_quantity }}</strong>
                                        <span>市场价：
                                            <s>{{ item2.market_price }}</s>
                                        </span>
                                    </p>
                                </div>
                            </router-link>
                            <!-- </a> -->
                        </li>
                    </ul>
                </div>
            </div>
        </div>
    </div>
</template>
<script>

export default {
    name: 'index',
    data(){
        return {
            catelist: [],
            sliderlist: [],
            toplist: [],
            productlist: []
        }
    },

    created() {
        this.$axios.get('/site/goods/gettopdata/goods').then(res=>{
            // console.log(res);
            this.catelist = res.data.message.catelist;
            this.sliderlist = res.data.message.sliderlist;
            this.toplist = res.data.message.toplist;
        });
        this.$axios.get('/site/goods/getgoodsgroup').then(res=>{
            // console.log(res);
            this.productlist = res.data.message;
        });
    }
}
</script>
<style>
    .carousel img{
        width: 100%;
        height: 100%;
    }
</style>


