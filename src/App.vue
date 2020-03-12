<template>
  <div id="app">
    <modal-window 
    :AdvertisingCounter="AdvertisingCounter"
    :TypeOfAdvertising="TypeOfAdvertising"
    v-on:hiddingModal="modalShow = false"
    :showing="modalShow"
    v-on:OpenCallMeWindow="modalShow = false, CallMeModalShow = true"
    :imgIndex="imgIndex"
    >
    </modal-window>
    <CallMeModal
    :CallMeModalShow="CallMeModalShow"
    v-on:hiddingModal="CallMeModalShow = false"
    ></CallMeModal>
    <header class="header">
        <div class=" container-fluid red ">
          <div class="container mt60">
            <div class="row ">
              <div class="col-12 col-md-4 logo">
                <img src="~@/assets/logo.png" alt="logo">
                <a href="http://sunraze.new-era-media.ru/" target="_blank"></a>
              </div>
              <div class="row col-4">
                <div class="center">
                  <svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" width="27" height="36" viewBox="0 0 27 36">
                    <image id="Geo_icon" width="27" height="36" xlink:href="data:img/png;base64,iVBORw0KGgoAAAANSUhEUgAAABsAAAAkCAYAAAB4+EEtAAACZklEQVRIib2Xu09UQRTGfxB8EOIDItEQEuyw8JEYE5BGE5stDA3EhoJQamGrxob/QGsLE2oDkkBBYysU8nBjIQU2sBRGDRo3PEQ0Y74hk3Hm3rm7q18yO8k93znfPM6cmW0iDUeBK0AvcAY4CXwDPgGrwFtgLzFWEGYgJWAS2AZ+ZbRt8UryKwQzi/kcgVibl38SRoHdGoVs21WcTIzVKeK3MX9fLK4Br4EjkYEY5yWgDGwBp4HLwNWMffoBDABv3I/NwHJkdCbLngLdkYDdsu9F/JcV/xBDEeKmRmbRBtwC7qhvc2wD4ofiDLlicwGCOUcXHJEnwI7H2dF3K9orPz/WnBVqjSzBfdlPASs5ibAiHvILbUWrnb5v/Ai0yHkiMfMmxG+Rv2//sx0jAcMzOXYBB4liB+Ijf98+YrKkM5Bhq+r7CpSfJvFdfxedzToLPqrqjycKWVh+NWDbN2IbAUOP+vcFxSy/J2BbNz9nA+u76JDKiXtWdnwWA/Zz1rgQyx7tQ8oVY/crlN0L7hTvBgimDh6T/SZQiQhVZEf8pQDnnit2QsXVJ720h1G9uTaeA9PqRz37VCDGlnPgDzGeUUj7cxKjP6OQj1uSe4bMlfEBaI8EfAXMAu/09jBvkYvAbRXlEL4C5zW7v/AgMfNS26Os5TCHcq1BQmtOgkVRapDYYJ6QxWSdQlOpQui0f65R6ItbLVIRunpSWu4TLoaiy/miViGDDt0KKUIV8evCDeBnjtC+eA3B4xyxh40SQmVtNiI0U8s/lzy0q3a6Qlm1tG5cAr5LqKq3/j/FsJ5tpv8vuF7YA/gNrOi6H8GvAk0AAAAASUVORK5CYII="/>
                  </svg>
                  <p class="ac ta-l">Ставполь,<br> ул. Доваторцев, д 38(этаж 3)</p>
                </div>
              </div>
              <div class="col-12 col-md-4 row right">
                <div class="button">
                  <a href="tel:+79383025242">
                    <div class="btn">
                      <svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" width="33" height="32" viewBox="0 0 33 32">
                        <image id="phone_icon" data-name="phone icon" width="33" height="32" xlink:href="data:img/png;base64,iVBORw0KGgoAAAANSUhEUgAAACEAAAAgCAYAAACcuBHKAAADM0lEQVRYha2YbWiOYRTHf54Zks2MvC7zFpuXMqFZkTaipJiUly8+CMXKBz4qxQeKKF9oJpGiFEmxLCEy85LQFOU9YdiSYTObjv63ru7d9/M893PvX1f3dq5zzvW/rp3rXOesF+kjG1gELABmAhOBfCALaAXeAo3AdeAC8CqC75QYAuwGPgNdaY5OoA4oj7u4ndIGoNlxbrs9CKwAioE8jeHAXGArUAv8cWzsVAoyITAAOOc4ug8sBRJp2o8S2TbZfwEWRyEwCLgr419AVYTF/bC4aZCvdmBtOkb9gFsyalIAxoUF9HH57ACWpDI47BzfZN9c/xhELL6OyXcLMDZMcaGULKgqHPk04Lnmrum2ZILewE35uRqkkNAdN4V9jrxYfxb3+h3NkIRhtHKK+Vnun1ypCcsFOY78dEAOaIoRqIad8vPAP1GriR0++fmQZDQjBok85zRK0I4GKhUbTvgMmkMcFccg0aLNoaT3j4RlOvs+AV77DJ4FOOlQHomDi/pWeCQs+g13ApRvB8jWhZCLgnp9p3gkxkgQ5NhIfPPJHsUkgE68Q5cgL+HchpYAZcv9Z3yyzT1AolPBiUfCGKFkEoQDimQP63sonf8nlHCOe3CI0lOgxvndipizwIgYC/cBcvXzV1QD2E5PJTGyCuqdL1e8cILag70vZcDIFCSmyscnTzBfAv/19GMO8MNHxGJmrxY1Qu+duceayw/wtUk6l92j+Z5mJrTC5mdIOecn6I2GgDTvZejtrvCkhEdSkDDMAz5EqDdtFDn24/VSG/FC13Gpc7yF3dfthqEhj1vQaFO15qHGqT27oS7ZZAhKdVPaQwjYjtc4+mU6ARuzgxwWOYVpVQQiKPhWAYeAK8BDvS+Vjo4VQy/lvzqZsy3ODpZFJJIMuXovulSl5aQyqHaIbOwBAgVqGbyCaFI6RllO8HQpAIdlSGC107l9BKZHMbbqeBvwWw4ste9xXtxkyFb9WO9spCGZbaqGuERtgBfJ5vCemt5GHW+bqrNx0it3rmSr+tj92lDGMKLWwl3y9ZjJxhtgV7rtQZR/DRjMqZVks4AJKlr7Ku1bs2wl4g1V0pYLUgP4C0zZE8P1FDw4AAAAAElFTkSuQmCC"/>
                      </svg>
                      <a>8 (938)-302-52-42</a >
                    </div>
                  </a>
                </div>
              </div>
            </div>
          </div>
        </div>
      <div class="container">
        <h1 class="col-12">Южная <span>Р</span>екламная Компания</h1>
        <h2 class="col-12" >Изготовление и размещение рекламы</h2>
        <div class="main_btn col-12">
          <div class="btn" @click="CallMeModalShow = true">
            ЗАКАЗАТЬ РЕКЛАМУ
          </div>
        </div>
        <div class="col-12">
          <div class="row box">
            <div v-for="(icons,index) in headerIcons" :key="index"  class="first_box">
              <div class="imag_cont">
                <img :src="getHeaderSrc(index)" alt="">
              </div>
              <p>{{headerIcons[index]}}</p>
            </div>
          </div>
        </div>
      </div>
    </header>
    <section class="page2">
      <div class="container">
        <h2>Разработка и изготовление всех видов рекламы</h2>
        <div class="row">
          <div v-for="(i, index) in TypeOfAdvertising" :key="index" class="page2_item" @click="mod(index)">
            <div class="page2_item__cont">
              <h4>Подробнее</h4>
            </div>
            <p>{{TypeOfAdvertising[index].name}}</p>
          </div>
        </div>
      </div>
    </section>
    <section class="aboutus_page con">
      <div class="container">
        <h2>о нашей компании</h2>
        <div class="row">
          <div class="text_cont col-12 col-md-6">
            <h4>Компания «Ю<span>Р</span>К»</h4>
            <p>Pекламная компания полного цикла. Нашей основной задачей является привлечение
              клиентов в Ваш бизнес. Для этого мы используем различные инструменты: 
              начиная печатью листовок, заканчивая разработкой стратегии развития компании 
              и создания положительного образа на рынке. 
            </p>
            <p>В нашем распоряжении имеется:</p>
            <ul>
              <li>Cобственное производство наружной рекламы любой сложности.</li>
              <li>	Развитая сеть собственных поверхностей в лифтах </li>
              <li>Типография с самым современным оборудованием </li>
              <li>Команда опытных разносчиков, которая доставит Вашу рекламу точно по месту жительства Ваших потенциальных клиентов.</li>
              <li>В штате имеются опытные маркетологи ,которые помогут правильно подобрать предложение с учетом особенностей и специфики Вашего бизнеса.</li>
              <li>На базе компании ЮРК образована WEB-студия в которой собраны лучшие специалисты по интернет продвижению.</li>
            </ul>
            <p>Все это позволит воплотить Ваши планы по привлечению клиентов в одном месте. </p>
            <p>Мы работаем ,что бы Вы не сидели на месте!</p>
          </div>
          <div  class="col-12 col-md-6 aboutUs_img">
          </div>
        </div>
      </div>
    </section>
    <section class="our_works">
      <div class="container">
        <h2>Результаты наших работ</h2>
      </div>
      <ourWorksSection
      :OurWorksModalShow="OurWorksModalShow"
      v-on:hiddingModal="OurWorksModalShow = false"
      ></ourWorksSection>
    </section>
    <section class="contact">
      <div class="container">
        <h2>Контакты</h2>
        <div class="row">
          <div class="text col-12 col-md-4">
            <h4>Адрес:</h4>
            <p>г. Ставрополь, ул. Доваторцев, 38Д (3 этаж)</p>
            <h4>Номер телефона:</h4>
            <a href="tel:+79383025242"> <p>+7 (938) 302-52-42</p> </a>
            <h4>Электронная почта:</h4>
            <a href="mailto:zakaz@urk-biznes.ru"><p>zakaz@urk-biznes.ru</p></a>
            <div class="another_questions">
              <h4>Остались еще вопросы?</h4>
              <div class="btn" @click="CallMeModalShow = true">Да, перезвоните мне</div>
            </div>
          </div>
          <div class="map col-12 col-md-8">
            <iframe src="https://yandex.ru/map-widget/v1/-/CGtpf4ID" width="100%" height="100%" frameborder="1" allowfullscreen="true"></iframe>
          </div>
        </div>
      </div>
    </section>
    <footer>
      <div class="container">
        <div class="row">
          <div class="left_side_footer col-md-4 col-12">
            <div class="row">
            <div class="container">
                <img src="~@/assets/KEK_LOGO.png" alt="logo">
                <P>южная рекламная компания</P>
            </div>
            <div class="container">
              <h4>Рекламно-производственная компания</h4>
            </div>
          </div>
          </div>
          <div class="center_footer col-md-4 col-12">
            <p>© Южная рекламная компания, 2020  </p>
          </div>
          <div class="right_side_footer col-md-4 col-12">
                <!-- <img src="~@/assets/whatsapp.svg" alt=""> -->
              <a href="">
                <div class="row">
                  <img src="~@/assets/NewEra.png" alt="">
                  <p>Разработанно совместно с: <br> New Era Media</p>
                </div>
              </a>
          </div>
        </div>
      </div>
    </footer>
  </div>
</template>

<script>
import modalWindow from './components/modalWindow.vue'
import OurWorksSection from './components/OurWorksSection.vue'
import CallMeModal from './components/CallMeModal.vue'

export default {
  name: 'app',
  components: {
    modalWindow,
    OurWorksSection,
    CallMeModal
  },
  data(){
    return{
      imgIndex: 0,
      AdvertisingCounter: 0,
      modalShow: false,
      OurWorksModalShow: false,
      CallMeModalShow: false,
      headerIcons:['Производство вывесок',"Услуги типографии","Реклама на транспорте","Создание сайтов","Реклама в лифтах","Наружная реклама","Реклама на дверных ручках", "Реклама в интернете"],
      TypeOfAdvertising:[
        {name:"Реклама в лифте", preim:['Стенд привлекает внимане','Работает 24/7','Фотоотчет','Время контакта от 30 сек., 2 раза в день',"Возможность охвата определенного района", "Возможность выбора места на стенде"], cost:'от 40 руб.'},
        {name:"Билборды", preim:['Локальность','Престижность','Ненавязчивость','Возможность территориальной выборки размещения', "Широкий охват"], cost:'от 200 руб.'},
        {name:"Реклама на авто", preim:['Массовая доступность','Широкая география транспортной рекламы','Избирательность маршрутов','Комфортное восприятие информации', "Ненавязчивость", "Брендирование корпоративного транспорта"], cost:'от 2 000 руб.'},
        {name:"Реклама на ручках", preim:['Адресная доставка по квартирам - гарантированный контакт с потребителем','Выход на квартиры в новостройках, где еще нет почтовых ящиков либо консьержей и невозможны другие виды рекламы','Идеально для отрасли строительства, ремонта, мебельных магазинов, магазинов декора'], cost:'от 2.5 руб. за 1 шт.'},
        {name:"Вывески", preim:['Широкий охват аудитории','Рабочий режим 24 часа','Разнообразие дизайнерских решений','Повышает уровень клиентского доверия', "Запускает так называемое «сарафанное радио»", "Хорошее дополнение к другим типам рекламы"], cost:'от 5 000 руб.'},
        {name:"Реклама в интернете", preim:['Точный таргетинг','Контакт «один на один»','Полное соответствие интересам пользователей', "Гибкость и оперативность"], cost:'от 9 000 руб.'},
      ],
    }
  },
  methods:{
    mod(index){
      this.AdvertisingCounter=index;
      this.modalShow = true;
      this.imgIndex = index;
    },
    getHeaderSrc(index){
        return require(`@/assets/${index}header.png`);
    }
  },
}
</script>

<style lang="less">
@orange:  #EF7F1A;
@secondColor: #5B5B5B;
*{
  font-family: 'Roboto', sans-serif;
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  a{
    color: black;
  }
  a:hover{
    color: black;
    text-decoration: none;
  }
}
.mt60{
  margin-top: 40px;
    @media only screen and (max-width: 768px) {
    margin-top: 0px;
  }
}
.btn:hover{
  // box-shadow:  -4px 5px 0px  rgb(230, 229, 229) !important;
  // border: 1px solid rgb(187, 187, 187)  !important;
  background: linear-gradient(140deg, #EF7F1A 30%, #F7DB58 100%) !important;
}
header{
  background: url(~@/assets/main_bg.png) no-repeat;
  // background-position: center 130px;
  background-size: cover;
  overflow: hidden;
  color: black;
    @media only screen and (max-width: 768px) {
    // overflow: none;
    // background-position: center 220px;
  }
}
.logo{
  margin-top: 15px;
  display: flex;
  justify-content: flex-start;
  align-items: center;
    @media only screen and (max-width: 768px) {
  justify-content: center;
  margin-bottom: 20px;
  }
  img{
  height: 90px;
  }
}
.red{
  width: 110%;
  margin-bottom: 150px;
  margin-left: -5%;
  background: white;
    @media only screen and (max-width: 768px) {
    margin-bottom: 70px;
    // margin-bottom: 50px;
    background: transparent;
  }
}
p{
  text-align: center;
  font-size: 20px;
  font-weight: 400;
  line-height: 1;
}
.ac{
  text-transform: uppercase;
}
.ta-l{
  text-align: left;
}
.right{
  display: flex;
  justify-content: flex-end !important;
    @media only screen and (max-width: 768px) {
  justify-content: center !important;
  padding-left: 50px !important;
    }
}
.button{
  display: flex;
  align-items: center;
  .btn{
  display: flex;
  align-items: center;
  border-radius: 15px;
  border: 1px solid @orange;
  background: linear-gradient(140deg, #F7DB58 30%, #EF7F1A 100%);
  svg{
    margin-right: 10px;
  }
  a{
    font-size: 22px;
    margin: 0;
    padding: 0;
    @media only screen and (max-width: 768px) {
    font-size: 16px;
    }
  }
}
}
.center{
  display: flex;
  align-items: center;
  svg{
    margin-right: 10px;
  }
  p{
    font-size: 18px;
    margin: 0;
    padding: 0;
  }
  @media only screen and (max-width: 768px) {
    display: none;
}
}
h1{
  span{
    color: @orange;
  }
  text-transform: uppercase;
  font-weight: 900;
  font-size: 72px;
    @media only screen and (max-width: 768px) {
    font-size: 36px;
  }
}
h2{
  margin-top: 25px;
  text-transform: uppercase;
  font-size: 36px;
  margin-bottom: 150px;
  font-weight: 900;
    @media only screen and (max-width: 768px) {
    font-size: 25px;
    margin-bottom: 50px;
  }

}
.main_btn{
display: flex;
justify-content: center;
margin-bottom: 50px;
  .btn{
    font-size: 28px;
    font-weight: 700;
    border: 1px solid black;
    border-radius: 15px;
    background: linear-gradient(140deg, #F7DB58 30%, #EF7F1A 100%);
    transition: background 1s;
    @media only screen and (max-width: 768px) {
    font-size: 18px;
    margin-bottom: 20px;
  }
  }
}
.box{
  justify-content: center;
  border-radius: 15px;
  margin-bottom: 120px;
          @media only screen and (max-width: 768px) {
        margin-right: 0px;
      margin-bottom: 30px;
        }
  .first_box{
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 5px;
          @media only screen and (max-width: 768px) {
          width: 33.333%;
        }
    .imag_cont{
        margin-right: 20px;
          @media only screen and (max-width: 768px) {
          margin-right: 0px;
        }
    }
    p{
      font-size: 18px;
      max-width: 170px;
      text-transform: uppercase;
      text-align: left;
        @media only screen and (max-width: 768px) {
        display: none;
      }
    }
  }
  // .first_box:hover{
  //   border: 3px solid black;
  // }
}
section{
  padding-bottom: 50px;
  h2{
    margin-top: 50px;
    margin-bottom: 50px;
    text-align: center;
    font-weight: 700;
  }
  .page2_item{
    position: relative;
    width: 300px;
    height: 300px;
    background: #000;
    margin-top: 50px;
    display: flex;
    flex-direction: column;
    justify-content: flex-end;
    background-size: cover !important;
    overflow: hidden;
    // box-shadow: 0 0 5px 1px #000;
    cursor: pointer;
    p{
      padding: 15px;
      margin: 0;
      background: @secondColor;
      color: white;
      text-transform: uppercase;
      transition: 1s height ;
      font-size: 16px;
    }
  }
  .page2_item:hover p {
    display: none;
  }
  .page2_item__cont{
    display: none;
    justify-content: center;
    align-items: center;
    width: 100%;
    height: 100%;
    color: white;
    text-transform: uppercase;
    background: rgba(91,91,91, .6);
    transition: all 1s;
    h4{
      font-size: 16px;
      padding: 10px 40px;
      border: 2px solid @orange;
      border-radius: 15px;
    }
  }
  .page2_item:hover .page2_item__cont {
    display: flex;
  }
  .page2_item:nth-child(1){
    background: url(~@/assets/0uslugi.png) no-repeat top center;
  }
    .page2_item:nth-child(1):before{
      content: "от 40 ₽";
      position: absolute;
      top: 15px;
      left: -35px;
      color: white;
      float: right; 
      transform: rotate(-35deg);
      font-size: 20px;
      background: red;
      padding: 5px 60px 5px 50px;
    }
  .page2_item:nth-child(2){
    background: url(~@/assets/1uslugi.png)  no-repeat top center;
  }
      .page2_item:nth-child(2):before{
      content: "от 5 000 ₽";
      position: absolute;
      top: 15px;
      left: -35px;
      color: white;
      float: right; 
      transform: rotate(-35deg);
      font-size: 20px;
      background: red;
      padding: 5px 60px 5px 40px;
    }
  .page2_item:nth-child(3){
    background: url(~@/assets/2uslugi.png) no-repeat top center;
  }
      .page2_item:nth-child(3):before{
      content: "от 2 000 ₽";
      position: absolute;
      top: 15px;
      left: -35px;
      color: white;
      float: right; 
      transform: rotate(-35deg);
      font-size: 20px;
      background: red;
      padding: 5px 60px 5px 40px;
    }
  .page2_item:nth-child(4){
    background: url(~@/assets/3uslugi.png) no-repeat top center;
  }
      .page2_item:nth-child(4):before{
      content: "от 2.5 ₽";
      position: absolute;
      top: 15px;
      left: -35px;
      color: white;
      float: right; 
      transform: rotate(-35deg);
      font-size: 20px;
      background: red;
      padding: 5px 60px 5px 45px;
    }
  .page2_item:nth-child(5){
    background: url(~@/assets/4uslugi.png) no-repeat top center;
  }
      .page2_item:nth-child(5):before{
      content: "от 5 000 ₽";
      position: absolute;
      top: 15px;
      left: -35px;
      color: white;
      float: right; 
      transform: rotate(-35deg);
      font-size: 20px;
      background: red;
      padding: 5px 60px 5px 40px;
    }
  .page2_item:nth-child(6){
    background: url(~@/assets/5uslugi.png) no-repeat top center;
  }
      .page2_item:nth-child(6):before{
      content: "от 9 000 ₽";
      position: absolute;
      top: 15px;
      left: -35px;
      color: white;
      float: right; 
      transform: rotate(-35deg);
      font-size: 20px;
      background: red;
      padding: 5px 60px 5px 45px;
    }
  .row{
    justify-content: space-between;
    align-content: space-around;
        @media only screen and (max-width: 768px) {  
      justify-content: center;
      }
  }
  
}
.aboutus_page{
  // background-image: 
  //                   linear-gradient(150deg, rgba(247, 4, 4, 0) 20%, rgba(255, 255, 255, 1) 50%),
  //                       url(~@/assets/our_works.jpg);
  // background-position: center center;
  // background-size: cover;
  h2{
    padding-top: 40px;
  }
  .text_cont{
    ul{
      margin-left: 35px;
    }
    h4{
      font-weight: 700;
      text-transform: uppercase;
      margin-bottom: 30px;
    span{
      color: @orange;
    }
    }
    p{
    font-size: 16px;
    text-align: left;
    }
  }
}
.aboutUs_img{
  background: url(~@/assets/aboutUS.jpg);
  background-size: cover;
  clip-path: polygon(00% 0%,100% 0%, 100% 65%, 50% 100%, 0% 65%);
  min-height: 450px;
}
.our_works{
  .container{
        @media only screen and (max-width: 768px) {
          padding-top: 20px;
    }
  }
  background-image: 
                    linear-gradient(114.16deg, rgba(15, 23, 26, 0.93) 2.57%, rgba(38, 50, 56, 0.74) 61.82%, rgba(38, 50, 56, 0) 100.66%),
                        url(~@/assets/our_works.jpg);
  background-position: center center;
  background-size: cover;
  color: white;
  h2{
    margin-top: 0 !important;
    padding-top: 100px;
    padding-bottom: 20px;
        @media only screen and (max-width: 768px) {
    padding: 0px;
    }
  }
  .letMeMore{
    display: flex;
    justify-content: center;
    flex-direction: column;
    align-items: center; 
    .point{
    display: flex;
    justify-content: center;
    flex-direction: column;
    align-items: center; 
    cursor: pointer;   
    h5{
      text-align: center;
    }
    }
  }
}
.contact{
  margin-bottom: 50px;
  h2{
    font-weight: 900;
  }
  .text{
    h4{
      font-weight: 700;
      margin-bottom: 20px;
    }
    p{
      margin-bottom: 20px;
    text-align: left;
    }
    .another_questions{
      padding: 25px;
      margin-top: 30px;
      border: 2px solid @orange;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      h4{
        text-align: center;
      }
      .btn{
        width: 200px;
        background: linear-gradient(140deg, #F7DB58 30%, #EF7F1A 100%);
        border: 1px solid @orange;
        border-radius: 15px;
      }
    }
  }
  .map{
    iframe{
      border: none;
      box-shadow: 0px 0px 20px 1px black;
        @media only screen and (max-width: 768px) {
        margin-top: 50px;
      }
    }
  }
}
footer{
  background: linear-gradient(40deg, rgba(91,91,91) 32%, rgba(239,127,26) 32.3%, rgba(239,127,26) 62%, rgba(91,91,91) 62.2%);
  p{
    font-size: 16px;
    font-weight: 400;
  }
  .left_side_footer{
    margin-top: 30px;
    display: flex;
    justify-content: flex-start;
    align-items: flex-end;
        @media only screen and (max-width: 768px) {
        justify-content: center;
      }
      .row{
        h4{
          font-size: 18px;
          color: white;
        }
        .container{
          display: flex;
          justify-content: flex-start;
          align-items: flex-start;
        @media only screen and (max-width: 768px) {
          justify-content: center;
          align-items: center;
      }
          img{
            height: 70px;
          }
          p{
            padding-left: 5px;
            max-width: 80px;
            font-size: 18px;
            display: inline-block;
          }
          .row{
            justify-content: center;
            align-items: flex-start;
            flex-direction: row;
            p{
              margin: 0;
              font-size: 17px;
              text-transform: uppercase;
            }
          }
          p{
            color: white;
            text-align: left;
          }
        }
      }
    h3{
      color: white;
      margin-top: 30px;
      margin-bottom: 30px;
      padding: 0;
    }
  }
  .center_footer{
    display: flex;
    justify-content: center;
    align-items: flex-end;
    p{
    color: white;
    margin-bottom: 10px;
    }
  }
  .right_side_footer{
    color: white;
    display: flex;
    align-items: flex-end;
    justify-content: flex-end;
        @media only screen and (max-width: 768px) {
          justify-content: center;
          align-items: center;
      }
        img{
          display: block;
          width: 35px;
          margin-top: 20px;
          margin-bottom: 15px;
        }
    a{
      .row{
      display: flex;
      justify-content: center;
      align-items: center;
      p{
        line-height: 1.3;
        margin: 0;
        color: white;
      }
      }
      img{
        margin-right: 7px;
        width: 40px;
        height: 40px;
      }
    }
  }
}
</style>
