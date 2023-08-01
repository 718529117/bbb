<template>
  <div class="container">
    <div class="poster">
      <div class="poster_bill">
        <div class="poster_border">
          <div class="bill_top">
            <div class="semicircle semicircle_left"></div>
            <div class="semicircle semicircle_right"></div>
            <img class="title_logo" src="../static/title_logo.svg">
            <div class="poster_title">
              <div class="poster_title_item">球</div>
              <div class="poster_title_item">费</div>
              <div class="poster_title_item">清</div>
              <div class="poster_title_item">单</div>
            </div>
          </div>
          <div class="bill_bottom">
            <ul class="bill_detail">
              <li class="bill_item">
                <div class="bill_title">
                  <img class="item_logo" src="../static/logo.svg">
                  {{ bill.ball_price_mode_name }}
                </div>
                <div class="bill_num">{{ bill.ball_price }}元</div>
              </li>
              <li class="bill_item">
                <div class="bill_title">
                  <img class="item_logo" src="../static/logo.svg">使用个数
                </div>
                <div class="bill_num">{{ bill.ball_num }}元</div>
              </li>
              <li class="bill_item">
                <div class="bill_title">
                  <img class="item_logo" src="../static/logo.svg">
                  {{ bill.site_price_mode_name }}
                </div>
                <div class="bill_num">{{ bill.site_price }}元</div>
              </li>
              <li class="bill_item" v-if="bill.site_time">
                <div class="bill_title">
                  <img class="item_logo" src="../static/logo.svg">场地时长
                </div>
                <div class="bill_num">{{ bill.site_time }}时</div>
              </li>
              <li class="bill_item">
                <div class="bill_title">
                  <img class="item_logo" src="../static/logo.svg">参与人数
                </div>
                <div class="bill_num">{{ bill.person_num }}人</div>
              </li>
              <li class="bill_item" v-if="bill.other_price">
                <div class="bill_title">
                  <img class="item_logo" src="../static/logo.svg">其他费用
                </div>
                <div class="bill_num">{{ bill.other_price }}元</div>
              </li>
              <li class="bill_item" v-if="bill.remark">
                <div class="bill_title">
                  <img class="item_logo" src="../static/logo.svg">备注
                </div>
                <div class="bill_num">{{ bill.remark }}</div>
              </li>
            </ul>
            <div class="bill_count">
              <div class="bill_count"></div>
              <div class="bill_count">
                <div>总计:</div>
                <div class="count_num">{{ count.toFixed(2) || 0 }}</div>
              </div>
              <div class="bill_count">
                <div>人均:</div>
                <div class="count_num">{{ average.toFixed(2) || 0 }}</div>
              </div>
            </div>
          </div>
        </div>
      </div>
      <div class="applet">
        <div class="wx_applet">
          <img class="applet_url" src="../static/applet.png">
          <div class="applet_text">
            <div class="applet_title">长按扫码进入小程序</div>
            <!-- <div class="applet_item"><span class="semicircle_item"></span>体验高度自定义步伐训练</div>
						<div class="applet_item"><span class="semicircle_item"></span>体验上下滑动计分器</div> -->
            <div class="applet_item">体验更多有趣的功能</div>
          </div>
        </div>
        <div class="bill_time">
          {{ getNowTime() }}
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { reactive, ref, onMounted } from "vue"

let bill = reactive({})
let poster = ref('')
let count = ref(0)
let average = ref(0)
let copy_text = ref('')
let width = ref(300)
let height = ref(600)

// onMounted(() => {
// countBill()
// }),

//   const countBill = () => {
//   this.bill = uni.getStorageSync('bill')
//   if (this.bill.ball_price_mode == 0 && this.bill.site_price_mode == 0) {
//     this.count = (this.bill.ball_price * this.bill.ball_num) + (this.bill.site_price * this.bill
//       .site_time) + this.bill.other_price * 1
//   } else if (this.bill.ball_price_mode == 0 && this.bill.site_price_mode == 1) {
//     this.count = (this.bill.ball_price * this.bill.ball_num) + this.bill.site_price * 1 + this.bill
//       .other_price * 1
//   } else if (this.bill.ball_price_mode == 1 && this.bill.site_price_mode == 0) {
//     this.count = (this.bill.ball_price / 12 * this.bill.ball_num) + (this.bill.site_price * this.bill
//       .site_time) + this.bill.other_price * 1
//   } else if (this.bill.ball_price_mode == 1 && this.bill.site_price_mode == 1) {
//     this.count = (this.bill.ball_price / 12 * this.bill.ball_num) + this.bill.site_price * 1 + this.bill
//       .other_price
//   }
//   this.average = this.count / this.bill.person_num
// }


const getNowTime = () => {
  let date = new Date();
  let year = date.getFullYear();
  let month = date.getMonth() + 1;
  let day = date.getDate();
  let time = year + '/' + addZero(month) + '/' + addZero(day);
  return time;
}
const addZero = (s) => {
  return s < 10 ? ('0' + s) : s;
}

</script>

<style lang="scss">
* {
  box-sizing: border-box;
  padding: 0;
  margin: 0;
}


.poster {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  padding: 20px;
  margin: 20px auto 10px;
  width: 100%;
  min-width: 250px;
  background: linear-gradient(145deg, #BFFFD8, #D4FCFF);

  .poster_bill {
    width: 100%;
    height: 85%;
    padding: 10px;
    background-color: #fff;

    .poster_border {
      width: 100%;
      height: 100%;
      border: 1px solid #022b00;

      .bill_top {
        position: relative;
        padding: 10px;
        width: auto;
        height: 25%;
        border-bottom: 1px #000 dashed;
        display: flex;
        justify-content: center;
        align-items: center;
        flex-direction: column;

        .title_logo {
          width: 60%;
          height: 20px;
          margin-bottom: 10px;
        }

        .semicircle {
          position: absolute;
          bottom: 0;
          width: 20px;
          height: 20px;
          border-radius: 10px;
          background-color: #fff;
        }

        .semicircle_left {
          left: 0;
          transform: translate(-50%, 50%);
          border-right: 1px solid #000;

        }

        .semicircle_right {
          right: 0;
          transform: translate(50%, 50%);
          border-left: 1px solid #000;

        }

        .poster_title {
          display: flex;
          justify-content: center;
        }

        .poster_title_item {
          width: 30px;
          height: 30px;
          text-align: center;
          line-height: 30px;
          margin: 5px;
          background-color: #38C189;
          box-shadow: 2px -2px 0 0 #009A89;
          color: #fff;
        }


      }

      .bill_bottom {
        padding: 10px;
        width: auto;
        height: 75%;

        .bill_detail {
          padding-top: 10px;
          display: flex;
          flex-direction: column;

          .bill_item {
            padding: 3px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            border-bottom: 1px #e6e6e6 dashed;
            font-size: 14px;

            &:last-child {
              border-bottom: none;
            }

            .bill_title {
              display: flex;
              align-items: center;
            }

            .item_logo {
              width: 15px;
              height: 15px;
              margin-right: 10px;
            }

          }
        }

        .bill_count {
          padding-top: 5px;
          display: flex;
          justify-content: space-between;
          align-items: flex-end;
          font-size: 14px;
        }

        .count_num {
          padding-left: 10px;
          font-size: 16px;
          font-weight: bold;
        }
      }
    }
  }
}

.applet {
  width: 100%;
  padding-top: 10px;
  display: flex;
  justify-content: space-between;
  align-items: flex-end;

  .wx_applet {
    display: flex;
    align-items: flex-end;

    .applet_url {
      width: 50px;
      height: 50px;
      margin-right: 10px;
    }

    .applet_title {
      font-size: 12px;
    }

    .applet_item {
      font-size: 12px;
    }
  }

  .bill_time {
    font-size: 12px;

  }
}

// .semicircle_item {
// 	display: inline-block;
// 	background-color: #000;
// 	width: 5px;
// 	height: 10px;
// 	border-radius: 0 5px 5px 0;
// 	line-height: 10px;
// }
</style>
