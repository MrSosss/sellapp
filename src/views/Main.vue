<template>
  <div>
    <div class="top">
      <div class="mbc" :style="{backgroundImage:'url('+data.avatar+')'}"></div>
      <div class="sign">
        <div class="signleft">
          <img :src="data.avatar" alt />
        </div>
        <div class="signright">
          <p class="shop">
            <img src="../assets/imgs/brand@2x.png" alt />
            {{data.name}}
          </p>
          <p class="time">{{data.description}}/{{data.deliveryTime+'分钟'}}</p>
          <p class="discount">
            <img src="../assets/imgs/decrease_1@3x.png" alt />
            {{data.supports[0].description}}
          </p>
        </div>
      </div>
      <div class="notice">
        <img src="../assets/imgs/bulletin@2x.png" alt />
        <p>{{data.bulletin}}</p>
      </div>

      <div class="routerdiv">
        <router-link to="/goods">商品</router-link>
        <router-link to="/evaluate">评价</router-link>
        <router-link to="/merchant">商家</router-link>
      </div>
    </div>
    <!-- 路由出口 -->
    <router-view></router-view>
    <div class="shopcar-bar">
      <div>
        <img src="../assets/imgs/shop.png" alt />
        <p>￥0</p>
      </div>
      <div>
        <p>另需配送费￥4元</p>
      </div>
      <div>
        <p>￥20起送</p>
      </div>
    </div>
  </div>
</template>

<script>
import { getSeller } from "../api/apis.js";
export default {
  data() {
    return {
      data: { supports: [{ description: "" }] }
    };
  },
  created() {
    getSeller().then(res => {
      // console.log(res.data.data.supports[0].description)
      this.data = res.data.data;
    });
  }
};
</script>

<style lang='less' scoped>
.routerdiv {
  display: flex;
  justify-content: space-around;
  background: #fff;
  height: 30px;
  line-height: 30px;
  border-bottom: 1px solid #ccc;
  a {
    text-decoration: none;
    color: #141c27;
  }
  a:hover {
    color: red;
  }
}
.shopcar-bar {
  position: fixed;
  height: 50px;
  width: 100%;
  bottom: 0;
  left: 0;
  background-color: #141c27;
  display: flex;
  justify-content: space-around;
  align-items: center;
  color: #ccc;
  div:nth-of-type(1) {
    display: flex;
    p {
      margin-left: 20px;
    }
    img {
      width: 40px;
      height: 40px;
      position: fixed;
      bottom: 20px;
      left: 10px;
    }
  }
}
.top {
  position: relative;
  .mbc {
    position: absolute;
    top: 0;
    width: 100%;
    z-index: -5;
    height: 120px;
    filter: blur(5px);
  }
  .sign {
    display: flex;
    width: 100%;
    height: 120px;
    justify-content: space-around;
    align-items: center;
    background: rgba(0, 0, 0, 0.4);
    color: #fff;
    .signleft {
      img {
        width: 80px;
        height: 80px;
      }
    }
    .signright {
      .shop {
        display: flex;
        align-items: center;
        img {
          width: 30px;
          height: 20px;
          margin-right: 10px;
        }
      }
      .discount {
        display: flex;
        align-items: center;
        img {
          width: 20px;
          height: 20px;
          margin-right: 10px;
        }
      }
    }
  }
}
.notice {
  height: 30px;
  width: 100%;
  background: #141c27;
  color: #fff;

  display: flex;
  align-items: center;
  img {
    margin-left: 20px;
    margin: 10px;
  }
  p {
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
  }
}
.top {
  height: 180px;
}
router-view {
  flex: 1;
}
</style>
