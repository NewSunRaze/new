<template>
  <div class="container">
    <div v-for="(j,index) in createdWorks" :key="index" class="work_cont">
      <div class="row pointer">
        <div class="img_cont col-12 col-md-6">
          <img :src="getSrc(index)" alt="">
        </div>
        <div class="text_cont col-12 ofset-0 col-md-5 ofset-md-1">
          <h4>{{createdWorks[index].name}}</h4> 
          <p>{{createdWorks[index].result}}</p>
          <div class="butn" @click="additionalInfoShowing(index)">Как мы это сделали <span>▼</span></div>
        </div>
      </div>
      <div class="row additional_cont">
        <div class="img_container col-md-5">
          <img :src="getSrc2(index)" alt="">
          <p>График эффективности рекламных активностей</p>
        </div>
        <div class="container col-md-7">
          <p>{{createdWorks[index].task}}</p>
          <p>{{createdWorks[index].decide}}</p>
        </div>
        <div class="col-12 fullres">
          <p>{{createdWorks[index].fullresult}}</p>
        </div>
        <div class="col-12 lessInfo">
          <p @click="additionalInfoHidding(index)">Скрыть подробную информацию<span>▲</span></p>
        </div>
      </div>
    </div>

    <div class="letMeMore"> 
      <div class="point" @click="seeMore()">
        <h5>{{SeeAllWorks}}</h5>
        <svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" width="60" height="25" viewBox="0 0 60 25" v-bind:style="{transform: kek}">
          <image id="Слой_4" data-name="Слой 4" width="60" height="25" xlink:href="data:img/png;base64,iVBORw0KGgoAAAANSUhEUgAAADwAAAAZCAYAAABtnU33AAAEd0lEQVRYhd2XS1NUVxSFv4YGAUWUIKLQIIJAAyExqTjMPJP8gPyF/LfMMkgyzCSjGGl5BWkeQkAjgqggApI6Vd9JnSIKfXkYk111qulL33vO2mvttffN7e/vYzQA28Ae/584B9QBr4GtcCEP1ADdQB8Q0P/heuz3/2JcBjrEdB1YBn4BVgLgaqAX+BZoAx4CY8BdYMofPwHefABADotLwDWxjLiGgFrge+BeIDAvkHVg1mx8DnwGfOW1SaAETABLwBqw8wEADNEEXAVuJQB7xRGwPQfGPf+zADjUcM4bww8/9aYghU6lEWIVmJPxcRUQZP801sZ7jAuCDOe9DQwK+Ko1+xJYBH4X6CgwLYad1LSCtBuVRjtQBIaBfqDg9ZwgF3zgpA9cOGPw54EWoAf4BPhYUtqV7Kbqm1GJo6ozlOJGasQp4LdlstWH9rnJLb9/BFT5sDk3mZD9OWW/eUKQDSqsR9UNS0KX/9tSZdPuex+YB/6Uzbd6zmGAD27epincTDIcNr8i+HU3jOAD+2WTsllBu8u5T5Mg+wQY9roBXLS9PAIeyGJJda0I9MioFHAatQn4bs2i6KFaDjA/6ZqRiTWZiaYXQNZbLt0JyGGT2WRrfJKAvG8il7yeKY4DOI0qwRc88JArqKBZX9jQRCZl/oFr23v7vWfEpDULctU6LGmSMyaxIiYPA5zTwps8RJDN7jEmrmpr/oaAI5DIfBhwntvXyzLdZqKiMp4KaixJzpySzTIHVInpgmtLde0FwLVa+x1/9NBNwucLN9rPOHXlNbbuRKr91mZB1w3xKmFyPJFrWSZ3Muxb5apLvGbIpIbn/RAw5f1RGMO+kY3H9tt7ZnpeN1zPAHhXcwk19puG02nvvONgkxfkr7a4Gfd+nSS5ksglILv0gBFJvOlZvgN+ioNHXpP4GvjSm86b/UeaTcnsz3ptLQP4eKiapNcX/T6vXLc9WBbZ5p2oOgUXQA6ooIuef8mE/wj8HEiLplXvzQPJ6rXnNnrzitIYMwHlhMWsUWMS9jJ6Rc6JqkuQt01ewXPuJG0reMCYal10Ats7OGnVua4kDX/Av6/L/Lb1VdZ576qCFU3nLKLF5A9aDkOCvmwJxPNMe6Y4+r6QrIomrXql0ZwYQJ91XtD99qy7Getx1HpcPiH4KrvGNUHGGb9HM9wX5GzS7iZM+kZitv+ISvtwrdlsTmomum6nctpNwE9Y85NK7JlMHAXykpIdco+i+7Qq5zXrPr7BjQtyXaBHxnEGj+oEfLuGN2jNd6iKyHzZGppSZsse7lXyvPgeW/Q58e2nVWOKg8uUBhRfU1ft65nipJNWPHCrYAd0yz5BRPCrifym/NzynjidFWW3VkkuWR6jMrkom5lBnjbgNBo1tw5Zim9YHdbkm4SxbeuxTb94mYAsmZgFzaciuVYSpw04jQbBF6z1YtLyWpNRckFwkckFgZ+IyXfFWQJO45xMdtpWvrAXl6zLWUfZU2PyXfG+AKeRd76u0cSyTm0nin8D8N97+/n+DgD8BeWnnApUvR9/AAAAAElFTkSuQmCC"/>
        </svg>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  props: [
    "OurWorksModalShow",
  ],
  data(){
    return{
      one: true,
      SeeMoreBtn: true,
      kek: "",
      SeeAllWorks: "Смотреть все работы",
      createdWorks:[
        {name:"Макдональдс", task:"Задача: увеличение и поддержание входящего потока в конкретно взятом ресторане, т.к. с момента открытия он являлся отстающим по продажам от других в г.Ставрополь", decide:"Решение: оповестить население ближайшего мкр. Перспективный о ресторане и его предложениях с помощью размещения рекламы на стендах в лифтах, данный источник был в новинку для компании, но хорошо себя зарекомендовал (размещение походит периодически сроком в 2 месяца). Так же были установлены ситиформаты - указатели на отставках общественного транспорта, которые находятся в шаговой доступности, и панели на подземной парковке городского рынка, установлен билборд в парке победы", result:"Мы увеличили поток клиентов в ресторане на 20%", fullresult:"Результат – комплексный подход позволил охватить рекламой всю необходимую часть юго-западного района г.Ставрополь. После запуска проекта было замечено увеличение трафика на 20%. Т.к. размещение происходит не прерывно, меняются только предложения которые размещены на носителях, это дает ежемесячное увеличение трафика в ресторане"},
        {name:"ДОДО пицца", task:"Задача: создать входящий поток в ресторан и обеспечить поступление заказов на доставку.", decide:"Решение: т.к. у компании есть строгие требования к времени на доставку готовых блюд, нам необходимо было охватить не весь г.Ставрополь, а только три его четверти. Для этого нами были произведены и размещены дорхенгеры (реклама на дверной ручке) и реклама в лифтах, было сделано оформление самого ресторана. Так же, для данной компании мы предоставляем всю используемую у них продукцию типографии.", result:"586 новых клиентов за 1 месяц", fullresult:"Результат – дорхенгеры принесли в месяц порядка 280 новых клиентов в зависимости от объемов распостронения, реклама в лифтах 306 заказов по промо коду из лифта"},
        {name:"Пивотека", task:"Задача: в короткие сроки повещать население о проводящихся акциях и новинках в магазинах, так как сеть достаточно большая, а мероприятия в магазинах проводятся в разное время, необходимо охватывать сектора города которые приближены к той или иной точке продаж.", decide:"Решение: под поставленную задачу заказчиком, лучше всего подходит источник дорхенгеры (реклама на дверной ручке) нами были составлены сектора охвата, составлен график и разработано предложение. Короткие сроки реализации позволяют сразу приступать к выполнению работ.", result:"930 человек за 3 дня", fullresult:"Результат - каждая рекламная активность показывает порядка 3-4% конверсии в средних объемах заказов это 930 человек за 3 дня"},
      ],
      moreWorks:[
        {name:"Фабрика Снов", task:"Задача: за годы работы у компании накопились большие объему используемой рекламы в разной стилистики ,наша задача привести все к одному стилю и создать у клиентов понимание того что это сеть фирменных магазинов мебели", decide:"Решение: мы изменили все макеты которые использовались ранее привели все к одной цветовой гамме и стилистике, демонтировали старые конструкции, установили новые, оформили точки продаж картинами с товаром, создали систему навигации по предприятию где производится продукция", result:"Мы увеличили входящий поток на 18%", fullresult:"Результат – увеличение входящего потока в точках продаж на 18%"},
        {name:"Лаборатория Архимед", task:"Задача – оповестить население всего г.Ставрополь о услугах данной компании и адресах лабораторий", decide:"Решение – было решено использовать рекламу на общественном транспорте сроком на 6 месяцев ,так как сфера не частого спроса был выбран именно такой срок размещения и подобраны различные предложения которые соответствовали всем требованиям закона о рекламе", result:"Увеличили преходы на сайт компании на 15% и входящие звонки на 20%", fullresult:"Результат – увеличились переходы на интернет сайт компании на 15% и поступления входящих звонков в лабораторию на 20%"},
      ],
    }
  },
  methods:{
    seeMore(){
      if(this.createdWorks.length <= 3){
        for(let i=0;i<this.moreWorks.length;i++){
          this.createdWorks.push(this.moreWorks[i]);
        }
        this.SeeAllWorks = "Показать меньше";
        this.kek = "rotate(180deg)";
      }
      else{
        for(let j=0;j<this.moreWorks.length;j++){
          this.createdWorks.splice(-1,1);
        }
        this.SeeAllWorks = "Смотреть все работы";
        this.kek = "rotate(360deg)";
      }
    },
    getSrc(index){
        return require(`@/assets/${index}.jpg`);
    },
    getSrc2(index){
        return require(`@/assets/${index}chart.png`);
    },
    additionalInfoShowing(index){
      document.getElementsByClassName("additional_cont")[index].style.display = "flex";
    },
    additionalInfoHidding(index){
      document.getElementsByClassName("additional_cont")[index].style.display = "none";
      this.SeeMoreBtn = true;
    }
  },
}
</script>

<style lang="less" scoped>
.kek-enter-active, .kek-leave-active {
    transition: transition 1s;
}
.kek-enter, .SeemoreWorks-leave-to{
    opacity: 0;
}
  .work_cont{
    margin-bottom: 50px;
    .pointer{
      cursor: pointer;
    }  
    .img_container{
      display: flex;
      justify-content: center;
      flex-direction: column;
      img{
        width: 100%;
      }
      p{
        padding-top: 10px;
        font-size: 14px !important;
        text-align: center !important;
      }
    }
    .additional_cont{
      display: none;
      padding-top: 30px;
      p{
        text-align: left;
        font-size: 16px;
        font-weight: 400;
        line-height: 1.2;
      }
      .lessInfo{
        padding-top: 10px;
        cursor: pointer;
        p{
          color:orange;
          text-align: center;
          span{
          padding-left: 5px;
          }
        }
      }
      .fullres{
        padding-top: 10px;
      }
    }
    .img_cont{
      width: 540px;
      height: 250px;
        @media only screen and (max-width: 768px) {
        width: 270px;
        height: 150px;
      }
      img{
        width: 100%;
        height: 100%;
        border: 3px solid orange;
        border-radius: 5px 45px 5px 45px;
      }
    }
  }
  .text_cont{
    display: flex;
    justify-content: flex-start;
    flex-direction: column;
    h4{
      font-weight: 900;
      margin-top: 0px;
      margin-bottom: 20px;
      @media only screen and (max-width: 768px) {
      margin-top: 30px;
    }
    }
    p{
      font-size: 18px;
      font-weight: 400;
      line-height: 1.3;
      margin-bottom: 30px;
      text-align: left;
    }
    .butn{
      font-size: 20px;
      font-weight: 700;
      text-align: left;
      padding: 0;
      color: orange;
      border-radius: 15px;
    }
  }
</style>
