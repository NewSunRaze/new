<template>
  <transition name="fade">
      <div class="Main_modal" v-show="showing" @click="close1($event)">
        <div class="modal">
          <p class="closer" @click="$emit('hiddingModal')">× </p>
          <div class="container">
            <h2 class="col-12">{{this.active.name}}</h2>
            <div class="row">
              <div class="col-12 col-md-6 img_cont">
                <img :src="getSrc()" alt="">
              </div>
              <div class="text_cont col-12 col-md-6">
                <div class="cont">
                  <h4>Преимущества:</h4>
                  <ul>
                    <li v-for="(i, index) in active.preim" :key="index">{{active.preim[index]}}</li>
                  </ul>
                </div>
              </div>
            </div>
            <div class="col-12">{{change()}}
                <h4>Стоимость: {{this.active.cost}}</h4>
            </div>
            <div class="col-12">
              <div class="row">
              <div class="btn" @click="$emit('OpenCallMeWindow')">Заказать</div>
              </div>
            </div>
          </div>
        </div>
      </div>
  </transition>
</template>

<script>
export default {
  name: 'modal',
  props: [
    "AdvertisingCounter",
    "showing",
    "TypeOfAdvertising",
    "imgIndex",
  ],
    data(){
        return{
          active: 0,
        }
    },
    methods:{
      close1: function(event){
        if(event.toElement.className == "Main_modal"){
            this.$emit('hiddingModal');
        }
      },
      change(){
        this.active = this.TypeOfAdvertising[this.AdvertisingCounter];
      },
      getSrc(){
        return require(`@/assets/${this.imgIndex}uslugiWindow.png`);
      }
    },

}
</script>

<style lang="less" scoped>

  .fade-enter-active, .fade-leave-active {
    transition: opacity .8s;
  }
  .fade-enter, .fade-leave-to{
    opacity: 0;
  }

  .Main_modal{
    position: fixed;
    width: 100%;
    height: 100vh;
    background: rgba(1, 1, 1, .8);
    z-index: 999;
    display: flex;
    justify-content: center;
    align-items: center;
      @media only screen and (max-width: 968px) {
      overflow: scroll;
      align-items: flex-start;
      }
      @media only screen and (max-height: 800px) {
      align-items: flex-start;
      }
  .modal{
    position: relative;
    display: block;
    padding: 70px 70px;
    max-height: 100vh;
    background: white;
    border: 3px solid orange;
      @media only screen and (max-width: 768px) {
      -webkit-overflow-scrolling: touch;
      overflow: scroll;
      padding: 30px 0px;
      max-height: 100%;
      }
    .closer{
      margin: 0;
      padding: 0;
      position: absolute;
      top: -15px;
      right: 5px;
      font-size: 60px;
      font-weight: 400;
      cursor: pointer;
    }
    h2{
      padding: 0;
      margin-bottom: 50px;
      margin-top: 0;
      text-align: center;
    }
    .cont{
      display: flex;
      flex-direction: column;
      align-items: flex-start;
      ul{
        margin-left: 30px;
        li{  
          max-width: 350px !important;
        }
      }
    h4{
      margin-top: 15px;
      text-align: left;
    }
    }
    .row{
      justify-content: center !important;
    .img_cont{
      display: flex;
      justify-content: center;
      align-items: center;
      img{
        border: 2px solid orange;
        max-width: 100%;
        max-height: 350px;
      }
    }
    }
    .btn{
      font-size: 20px;
      padding: 8px 70px;
      font-weight: 700;      
      margin-top: 30px;
      border-radius: 15px;
      border: 1px solid orange;
      background: linear-gradient(140deg, #F7DB58 30%, #EF7F1A 100%);
    }
  }
  }
</style>
