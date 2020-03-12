<template>
    <transition name="showMe">
        <div class="CallMe_modal" v-show="CallMeModalShow" @click="close($event)">
        <div class="cont main">
                <div class="closer">
                    <p @click="[$emit('hiddingModal')],[clear()]" >×</p>
                </div>
            <div class="container">
                <h4 class="col-12">Оставьте Ваши контактные данные</h4>
                <h3>и мы свяжемся с вами</h3>
                    <div class="container">
                        <div class="container input_cont">
                            <input
                            v-model="name"
                            type="text"
                            placeholder="Ваше имя"
                            class="col-12">
                        </div>
                        <div class="container input_cont">
                            <input
                            v-model="phone"
                            type="text"
                            placeholder="Ваш номер телефона"
                            class="col-12">
                            <p>{{this.details}}</p> 
                        </div>
                        <div class="btn" @click="send()" v-bind:style="{background: this.bgc}">{{btnVal}}</div>
                        <div class="container">
                            <p>Нажимая "отправить" вы автоматически соглашаетесь на обработку <a href="politica.html" target="_blank">персональных данных</a></p>
                        </div>
                    </div>
            </div>
        </div>
        </div>
    </transition>
</template>
<script>
export default {
  props: [
    "CallMeModalShow",
  ],
  data(){
      return{
          bgc:"linear-gradient(140deg, #F7DB58 30%, #EF7F1A 100%)",
          btnVal:"Отправить",
          name:"",
          phone:"",
          details: "",
      }
  },
  methods:{
      close: function(event){
        if(event.toElement.className == "CallMe_modal"){
            this.$emit('hiddingModal');
        }
      },
      clear(){
        this.name="";
        this.phone="";
        this.details="";
        this.btnVal = "Отправить";
        this.bgc="linear-gradient(140deg,#F7DB58 30%, #EF7F1A 100%)";
      },
      send(){
          if(this.name == "" && this.phone == ""){
              this.details="Заполненны не все поля";
          }
          else{
              this.fet();
              this.name="";
              this.phone="";
              this.btnVal = "Отправленно";
            //   this.bgc = "linear-gradient(170deg,rgba(250,239,5,1) 30%, rgba(95,255,0,1) 100%)"
              this.bgc = "linear-gradient(170deg, #F7DB58 40%, rgba(95,255,0,1) 80%)"

          }
      },
      fet(){
          fetch('send.php',{ 
            method: 'post', 
            headers: { 
            'Content-Type': 'application/x-www-form-urlencoded;charset=utf-8' 
            }, 
            body: "phone=" + this.phone + "&name=" + this.name,
            contentType: false,
            }).then(()=>{
            this.details ="Мы свяжемся с Вами в ближайшее время!";
            // console.log(response); 
            }).catch(()=>{ 
            this.details ="Что-то пошло не так... Мы передадим эту информацию в службу тех. поддержки";
            // console.log(error); 
            });
      },
  }
}
</script>

<style lang="less" scoped>
.showMe-enter-active, .showMe-leave-active {
    transition: opacity .8s;
}
.showMe-enter, .showMe-leave-to{
    opacity: 0;
}


.CallMe_modal{
    position: fixed;
    width: 100%;
    height: 100vh;
    background: rgba(1, 1, 1, .8);
    z-index: 999;
    display: flex;
    justify-content: center;
    align-items: center;
    .cont{
      border: 2px solid orange;
      border-radius: 15px;
      background: rgba(255, 255, 255, .9);
      .container{
          text-align: center;
          h4{
              font-weight: 400;
                @media only screen and (max-width: 768px) {
                    font-size: 18px;
                }
          }
          h3{
              text-transform: uppercase;
              font-weight: 900;
              margin-bottom: 20px;
                @media only screen and (max-width: 768px) {
                    font-size: 18px;
                }
          }
          .input_cont{           
                margin-bottom: 20px;   
            input{
                width: 300px;
                border-radius: 5px;
                outline: none;
                @media only screen and (max-width: 768px) {
                width: 200px;
                }
            }
            p{
                padding: 0;
                margin-top: 10px;
                font-size: 16px;
                color: orange;
            }
          }
          .btn{
            font-size: 20px;
            padding: 8px 70px;
            font-weight: 700;      
            border-radius: 15px;
            border: 1px solid orange;
            transition: 1s all !important;
            margin-bottom: 40px;  
            margin-top: 5px;
          }
          p{
              font-size: 12px;
              a{
                  color: orange;
              }
          }
      }
      .closer{
          display: flex;
          justify-content: flex-end;
          margin-top: 0;
          cursor: pointer;
          p{
              margin-top: 0;
              font-size: 60px;
              margin-right: 20px;
              cursor: pointer;
                @media only screen and (max-width: 768px) {
                    font-size: 40px;
                }
          }
      }
    }
}
</style>