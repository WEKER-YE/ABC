<template>
  <div id="home">
    <Header2 />
    <!-- 這裡是 Section 和 MainComponent 並排顯示的區塊 -->
    <div class="content-layout">
     <!-- <Article /> -->
      <Aside />
    </div>

    <!-- CarouselComponent 單獨出來的區塊 -->


    <!-- ProductGridComponent 插入到頁面中 -->
    <div class="product-grid-layout">
      <Product2 />
    </div>

    <!-- CalendarComponent 插入到頁面中 -->
    <div class="calendar-layout">
      <Calendar />
    </div>

    <!-- Instagram 貼文輪播區塊 -->
    <div class="instagram-carousel-layout">
      <InstagramCarousel />
    </div>
    <Footer />
    
  </div>
</template>

<script>
import { defineComponent } from 'vue';
import Header2 from '@/components/Header2.vue';
import Footer from '@/components/Footer.vue';
import Article from '@/components/index/Article.vue';
import Calendar from '@/components/index/Calendar.vue';
// import ProductGrid from '@/components/index/ProductGrid.vue';
import InstagramCarousel from '@/components/index/InstagramCarousel.vue';
import Aside from '@/components/index/Aside.vue';
import Product2 from '../components/index/Product/Product2.vue';


export default  defineComponent({
  name:'HomeView',
  components: {
    Header2,
    Article,
    Footer,
    // ProductGrid,
    Calendar,
    InstagramCarousel, // 註冊 InstagramCarousel
    Aside,
    Product2,
  },
});
</script>

<style>
/* 設置背景圖片 */
template {
   /* 背景圖片路徑 */
  background-size: cover; /* 背景圖片覆蓋整個頁面 */
  background-position: top; /* 背景圖片從頂部顯示 */
  background-repeat: no-repeat; /* 防止背景重複 */
  min-height: 100vh; /* 確保背景圖片覆蓋整個瀏覽器視窗 */
}

/* 設置主要佈局 */
.content-layout {
  height: 80vh;
  margin: 20px;
  /* border: #000 2px solid; */
}

/* CarouselComponent 獨立的樣式 */
.carousel-layout {
  margin-top: 2rem; /* CarouselComponent 與上面的區塊保持間距 */
  padding: 2rem;
  text-align: center; /* 讓 CarouselComponent 居中對齊 */
  /* border: #000 2px solid; */
}

/* ProductGridComponent 獨立的樣式 */
.product-grid-layout {
  margin-top: 2rem;
  padding: 2rem;
  text-align: center; /* 讓 ProductGridComponent 居中對齊 */
  /* border: #000 2px solid; */
}

/* CalendarComponent 獨立的樣式 */
.calendar-layout {
  margin-top: 2rem;
  padding: 2rem;
  text-align: center; /* 讓 CalendarComponent 居中對齊 */
  /* border: #000 2px solid; */
}

/* Instagram 貼文輪播的樣式 */
.instagram-carousel-layout {
  margin-top: 2rem;
  padding: 2rem;
  text-align: center; /* 讓 InstagramCarousel 居中對齊 */
  /* border: #000 2px solid; */
}

@media (max-width: 768px) {
  .content-layout {
    flex-direction: column; /* 小螢幕下切換為垂直佈局 */
    padding: 1rem;
  }

  .carousel-layout,
  .product-grid-layout,
  .calendar-layout,
  .instagram-carousel-layout {
    padding: 1rem;
  }
}
</style>
