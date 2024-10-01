<template>
    <div class="container-fluid">
        <div class="d-flex justify-content-center">
            <router-link to="page"><img src="../../../assets/抹茶蜜柚蘭姆栗子/494007.jpg" alt="" class="img-fulid"></router-link>
            <router-link to="page"><img src="../../../assets/梨山烏龍 芋泥 抹茶淋醬 酥餅/476236.jpg" alt="" class="img-fulid"></router-link>
            <router-link to="page"><img src="../../../assets/水蜜桃布丁燒/461801_0.jpg" alt="" class="img-fulid"></router-link>
        </div>
        <div class="d-flex justify-content-center">
            <router-link to="showbody"><button class="btn">觀看全部</button></router-link>
        </div>
    </div>
</template>

<style>
    .img-fulid {
        width: 200px;
        height: 200px;
        margin: 10px;
    }

    .btn {
        background-color:mediumspringgreen; 
        font-size: 20px;
        width: 120px;
        height: 60px;
        opacity: 1;
    }
    .btn:hover {
        opacity: 1;
        background-color:mediumspringgreen; 
    }
</style>

<script>
export default {
    name:'Product2'
}
</script>