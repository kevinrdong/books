<template>
  <div id="app">
    <h1>使用Vue.js計算呈現資訊/v-if</h1>
  <h3>
    實戰博客來排行榜資料轉換html
    <span><img src="http://pk.ixpanel.com/images/pk/201108/0824/BOOKS.gif" class="bkl_icon"></span>  
    <a href="https://www.books.com.tw/web/sys_newtopb/books/01/?loc=P_0025_1_short_001" target="_blank">(連結網址)</a>
  <br>
  <label>詳細模式<input type="checkbox" v-model="mode_detail"></label>
 </h3>
 <br>
<label>優惠價</label>
<span v-for="(id,book) in books" :key="book">
  <label>{{id+1}}</label>
  <input type="checkbox" v-model="book.is_discount"/>
</span>

<label>
  小呈現
  <input type="radio" v-model="mode_size" value="small" />
</label>
<label>
  大呈現
  <input type="radio" v-model="mode_size" value="big" />
</label>
  
  <div class="book_container" :class="{ detail: mode_detail }">
    <div class="book"  :class="`${mode_size} ${mode_detail ? 'detail' : ''}`" v-for="book in books" :key="book">
      <img :src="book.img">
      <div class="info">
        <h2 class="name" v-if="!mode_detail"><a :href="book.link_book" target="_blank">{{book.name.substring(0,18)}}</a></h2>
        <h2 class="name" v-if="mode_detail"><a :href="book.link_book" target="_blank">{{book.name}}</a></h2>
        <h4 class="author">作者：<a :href="book.link_author" target="_blank">{{book.author}}</a></h4>
        <h4 class="publish" v-if="mode_detail">出版社：<a :href="book.publish_house" target="_blank">{{book.publish_house}}</a></h4>
        <h4 class="price" v-if="book.is_discount">優惠價：<span class="red">{{book.discount*100}}</span>折<span class="red">{{parseInt(book.price*book.discount)}}</span>元</h4>
        <h4 class="price" v-if="!book.is_discount">原售價：<span class="red">{{book.price}}</span>元</h4>
        <h4 class="date" v-if="mode_detail">出版日期：<a :href="book.date" target="_blank">{{book.date}}</a></h4>
      </div>
    </div>    
  </div>
  </div>
</template>

<script>
export default {

  name: "app",
  data() {
    return {
      mode_detail: false,
      mode_size: "big",
      books: [
    {
      name:"歡迎光臨夢境百貨：您所訂購的夢已銷售一空",
      author: "이미예",
      publish_house: "寂寞",
      img: "https://im1.book.com.tw/image/getImage?i=https://www.books.com.tw/img/001/089/77/0010897792.jpg&v=60eebcd2&w=348&h=348",
      price: 430,
      is_discount: true,
      discount: 0.79,
      link_book: "https://www.books.com.tw/products/0010897792?loc=P_0003_001",
      link_author: "https://search.books.com.tw/search/query/key/%E6%9D%8E%E7%BE%8E%E8%8A%AE/adv_author/1/",
      date: "2021/08/01",
    },{
      name: "寫字的力量限量超值套組：《寫字的力量》+《美字基本功》(加贈日本原裝Preppy本格鋼筆+專屬炫彩墨水2入)",
      author: "侯信永",
      publish_house: "遠流",
      img: "https://im1.book.com.tw/image/getImage?i=https://www.books.com.tw/img/001/070/99/0010709943_b_01.jpg&v=56eaa353&w=348&h=348",
      price: 540,
      is_discount: true,
      discount: 0.75,
      link_book: "https://www.books.com.tw/products/0010709943?loc=P_003_002",
      link_author:
      "https://search.books.com.tw/exep/prod_search.php?key=%E4%BE%AF%E4%BF%A1%E6%B0%B8&f=author",
      date: "2016/03/30"
    },{
      name: "好音樂的科學：破解基礎樂理和美妙旋律的音階秘密",
      author: "約翰‧包威爾",
      publish_house: "大寫出版 ",
      img: "https://im1.book.com.tw/image/getImage?i=https://www.books.com.tw/img/001/071/87/0010718777.jpg&v=5756a26b&w=348&h=348",
      price: 350,
      is_discount: false,
      discount: 0.79,
      link_book: "https://www.books.com.tw/products/0010718777?loc=P_003_003",
      link_author:
      "https://search.books.com.tw/exep/prod_search.php?key=%E7%B4%84%E7%BF%B0%E2%80%A7%E5%8C%85%E5%A8%81%E7%88%BE&f=author",
      date: "2016/06/21"
    },{
      name: "Design by wangzhihong.com：A Selection of Book Designs, 2001-2016(王志弘作品選2001-2016)",
      author: "王志弘",
      publish_house: "臉譜",
      img: "https://im1.book.com.tw/image/getImage?i=https://www.books.com.tw/img/001/072/55/0010725522.jpg&v=57b6fbcb&w=348&h=348",
      price: 3000,
      is_discount: true,
      discount: 0.79,
      link_book: "https://www.books.com.tw/products/0010725522?loc=P_003_004",
      link_author:
      "https://search.books.com.tw/exep/prod_search.php?key=%E7%8E%8B%E5%BF%97%E5%BC%98&f=author",
      date: "2016/09/01"
    },{
      name: "手寫英文書法聖經：從握筆、筆順到數字、符號，全方位掌握藝術美字書寫技法。",
      author: "Julien Chazal",
      publish_house: "野人",
      img: "https://im2.book.com.tw/image/getImage?i=https://www.books.com.tw/img/001/071/98/0010719843.jpg&v=57c7bcda&w=348&h=348",
      price: 665,
      is_discount: true,
      discount: 0.75,
      link_book: "https://www.books.com.tw/products/0010719843?loc=P_003_005",
      link_author:
      "https://search.books.com.tw/exep/prod_search.php?key=Julien+Chazal&f=author",
      date: "2016/09/07"
    },{
      name: "手寫美「行」：鋼筆字冠軍的日常行書超值套組《手寫美「行」》+《美「行」小練習》【博客來獨家德國e+m原木筆桿&日本NIKKO沾水筆尖&鋼筆紙箋（Conifer／珠友文化隨機出貨）】",
      author: "葉曄",
      publish_house: "遠流",
      img: "https://im1.book.com.tw/image/getImage?i=https://www.books.com.tw/img/001/072/35/0010723527_b_01.jpg&v=579b5a78&w=348&h=348",
      price: 520,
      is_discount: false,
      discount: 0.75,
      link_book: "https://www.books.com.tw/products/0010723527?loc=P_003_006",
      link_author:
      "https://search.books.com.tw/exep/prod_search.php?key=%E8%91%89%E6%9B%84&f=author",
      date: "2016/08/05"
    },{
      name: "Typography 字誌：Issue 02 來做LOGO吧！",
      author: "Graphic社編輯部",
      publish_house: "臉譜",
      img: "https://im1.book.com.tw/image/getImage?i=https://www.books.com.tw/img/001/072/92/0010729204.jpg&v=57e27d49&w=348&h=348",
      price: 420,
      is_discount: true,
      discount: 0.79,
      link_book: "https://www.books.com.tw/products/0010729204?loc=P_003_007",
      link_author:
      "https://search.books.com.tw/exep/prod_search.php?key=Graphic%E7%A4%BE%E7%B7%A8%E8%BC%AF%E9%83%A8&f=author",
      date: "2016/10/06"
    }
  ],
    }
  }
}
</script>

<style lang="scss">
* {
  font-family: 微軟正黑體;
}

body {
  padding: 20px; 
}

.bkl_icon {
  width: 100px;
}

.book {
  padding: 10px;
  display: flex;
  flex-direction: column;
  text-align: center;
  align-items: center;
  width: 175px;
  border: solid 1px;
}
img {
    width: 100%;
}
  
  

  
.author,.price,.publish,.date {
  font-weight: nomal;
  margin: 0px;
  font-size: 14px;
  color: #555;
  }

  .author {
   margin-top: 5px;
  }
  
  .name {
   font-size: 18px;
   margin: 0px;
  }
  a {
  color: #555;
  }
  
  .red {
    color: #d93800;
    font-weight: 900;
  }

.book_container {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  
  
  &.detail {
    display:flex;
    flex-direction: column;
  
  .book {
    &.detail{
      width:80%;
      display: flex;
      flex-direction: row;
      text-align: left;
      padding: 20px;
    }
  
    img {
      width: 150px;
    }
    
    &.big {
      img {
        width: 250px;
        
      .info {
         width: calc(100% - 220px - 20px);  
      }
     }
    }
    .info {
      width: calc(100% - 150px - 20px);
      
    }
  }

    
  }
}

.big {
  width:280px;
  
  img {
    margin-top: 5px;
  }
}
</style>
