<template>
  <div class="main_page">
    <Header id="header" :isMain="isMain" v-if="!loading" />
    <Loading :loading="loading" />
    <div class="home" v-if="!loading" id="home123">
      <video width="100%" height="100%" id="video_1" autoplay loop muted style="background: rgba(57, 57, 57, 0.49);transform: matrix(-1, 0, 0, 1, 0, 0);">
        <source src="../assets/final.mp4" type='video/mp4'>
        Тег video не поддерживается вашим браузером. 
      </video>

      <picture>
        <source srcset="../assets/image33.webp" type="image/webp">
        <img class="home_main_img" id="home_main_img" src="../assets/image33.png" alt="">
      </picture>

      <p id="p1" v-scroll-to="{el: '#about',  offset: -100,}" class="home_1">a</p>
      <a href="/vacancies" class="home_2">a</a>
      <p @click="popup = true" class="home_3">a</p>
      <p v-scroll-to="{el: '#footer',  offset: -100,}" class="home_4">a</p>
      <p v-scroll-to="{el: '#header',  offset: -100,}" class="home_5">a</p>
      <p v-scroll-to="{el: '#education',  offset: -100,}" class="home_6">a</p>
      <p v-scroll-to="{el: '#cert',  offset: -100,}" class="home_7">a</p>
      <a href="/Sudy" class="home_8">a</a>
    </div>
    <div class="home_mobile">
      <p style="text-transform:uppercase">Трудоустройство морского персонала</p>
      <v-btn
        depressed
        color="primary"
        @click="(popupMobile = true)"
        style="letter-spacing:0.01em;text-transform:initial;font-size:3.4vw;font-weight:bold;font-family: 'Montserrat', sans-serif;"
      >
        Отправить анкету
      </v-btn>
      <img class="home_mobile_down" v-scroll-to="{el: '#footer',  offset: -100,}" src="../assets/down.png" alt="">
      <img class="home_mobile_wave" src="../assets/wave.png" alt="">
    </div>
    <div class="about" id="about">
      <!-- <img class="about_1" src="../assets/hat.png" alt=""> -->
      <div class="about_info">
        <div class="about_div"></div>
        <h1 style="font-weight: 900 !important">О нас.</h1>
      </div>
      <div class="about_text">
        <div class="about_text_1">
          <p>{{ about_3 }}</p>
          <picture>
            <source srcset="../assets/image2.webp" type="image/webp">
            <img src="../assets/image2.png" alt="">
          </picture>
          <strong>{{ about_4 }}</strong>
          <!-- <h2>Павел Нахимов</h2> -->
        </div>
        <div class="about_text_2">
          <p>{{ about_1 }}</p>
          <p>{{ about_2 }}</p>
        </div>
      </div>
    </div>

    <div class="about_mobile">
      <p>О нас.</p>
      <img src="../assets/hat.png" alt="">

      <div class="about_mobile_info">
        <picture>
            <source srcset="../assets/image2.webp" type="image/webp">
            <img src="../assets/image2.png" alt="">
          </picture>
        <p>{{ about_1 }}</p>
          <p>{{ about_2 }}</p>
      </div>
    </div>

    <div style="width: 100vw; height: 10vw;background-color: white;"></div>

    <div class="education" id="education">
      <div class="education_info">
        <div class="education_info_img">  
          <picture>
            <source srcset="../assets/wheel.webp" type="image/webp">
            <img src="../assets/wheel.png" alt="">
          </picture>
        </div>
         <div style="width: 95px;height: 4px;background: #01DFFD;"></div>
         <h1 style="font-weight: 900 !important">Обучение.</h1>
         <div class="education_info_text">
           <p>{{ education_1 }}</p>
           <p style="margin-bottom: 38px;">{{ education_2 }}</p>
            <!-- <v-btn
            depressed
            color="primary"
            style="position:absolute;bottom:0%;right:0%;letter-spacing:0.01em;text-transform:initial;font-size:0.9vw;font-weight:bold;font-family: 'Montserrat', sans-serif;"
          >
            Начать обучение
          </v-btn>         -->
         </div>


      </div>

      <img src="../assets/image1.png" alt="">
    </div>

    <div class="education_mobile">
      <h1>Обучение.</h1>
      <picture>
            <source srcset="../assets/wheel.webp" type="image/webp">
            <img class="education_mobile_img" src="../assets/wheel.png" alt="">
          </picture>
      <div class="education_mobile_info">
        <div class="education_mobile_info_1">
          <p>{{ education_1 }}</p>
          <p>{{ education_2 }}</p>
        </div>
        <div class="education_mobile_info_2">
          <img src="../assets/image1.png" alt="">
        </div>
      </div>


      <!-- <a href="/vacancies"><v-btn color="primary" style="letter-spacing:0.01em;text-transform:initial;font-size:3.4vw;font-weight:bold;font-family: 'Montserrat', sans-serif;width:49vw;margin-left:20vw;margin-top:20px;">Начать обучение</v-btn></a> -->
    </div>

    <div class="vac" id="vac">
      <img class="vac_1" src="../assets/star1.png" alt="">
      <img class="vac_2" src="../assets/star2.png" alt="">
      <img class="vac_3" src="../assets/star3.png" alt="">
      <h1 style="font-weight: 900 !important">Вакансии.</h1>
     <div class="vac_list_item" v-for="(item, index) in vacancies.slice(0, 2)" :key="index">
          <div class="vac_list_item_main">
            <h1>{{ item.nameVac }} | {{ item.count }} позиция</h1>
            <p>{{ item.text }}</p>
            <v-btn
              depressed
              color="primary"
              @click="(example = item.nameVac), (popup = true)"
              style="letter-spacing:0.01em;text-transform:initial;font-size:1vw;font-weight:bold;font-family: 'Montserrat', sans-serif;"
            >
              Отправить анкету
            </v-btn>
          </div>
          <div style="background: #C4C4C4;height:1px;width:10%;display:inline-block;position:relative;top:-100px;"></div>
          <div class="vac_list_item_dop">
            <p class="vac_list_item_dop_1">Судно</p>
            <p class="vac_list_item_dop_2">{{ item.sudno }}</p>
            <v-divider></v-divider>
            <p class="vac_list_item_dop_1">Продолжительность контракта</p>
            <p class="vac_list_item_dop_2">{{ item.date }}</p>
            <v-divider></v-divider>
            <p class="vac_list_item_dop_1">Заработная плата</p>
            <p class="vac_list_item_dop_2">{{ item.price }}</p>
          </div>
      </div>
      <a href="/vacancies">
      <v-btn depressed
            color="primary"
            style="height: 50px;margin-left:32%;margin-top: 5%;margin-bottom:5%;width: 25%;letter-spacing:0.01em;text-transform:initial;font-size:1vw;font-weight:bold;font-family: 'Montserrat', sans-serif;"
            >
            Показать больше вакансий</v-btn>
      </a>
    </div>

    <div class="vac_mobile">
      <h1>Вакансии.</h1>
      <img class="vac_mobile_1" src="../assets/star1.png" alt="">
      <img class="vac_mobile_2" src="../assets/star2.png" alt="">
      <img class="vac_mobile_3" src="../assets/star3.png" alt="">
      <div class="vac_mobile_card" v-for="(item, index) in vacancies.slice(0, limit)" :key="index">
        <div class="vac_mobile_card_name">
          <h1>{{ item.nameVac }} | <span> {{ item.count }} позиции</span></h1>  
          <p>{{ item.text }}</p>        
        </div>
        <div class="vac_mobile_card_line"></div>
        <div class="vac_mobile_card_dop">
          <div class="vac_mobile_card_dop_1">
            <h2>Cудно:</h2>
            <p style="margin-top: 10px;">{{ item.sudno }}</p>
          </div>

          <div class='vac_mobile_card_dop_2'>
            <h2>Продолжительность контракта:</h2>
            <p>{{ item.date }}</p>
          </div>

          <h2 class="vac_mobile_card_dop_price">Заработная плата: <span>{{ item.price }}</span> </h2>
        </div>
      </div>  

      <v-btn color="primary" outlined style="font-size:3.4vw;width:40vw;display:inline-block;letter-spacing:0.01em;text-transform:initial;font-weight:500;font-family: 'Montserrat', sans-serif;" @click="limit = 4">
        Показать больше
      </v-btn>

      <a href="/vacancies"><v-btn color="primary" style="letter-spacing:0.01em;text-transform:initial;font-size:3.4vw;font-weight:bold;font-family: 'Montserrat', sans-serif;width:46vw;margin-left:3vw;">
        Подробнее
      </v-btn></a>
    </div>




    <!-- <div class="work">
      <h1>Вакансии.</h1>
      <div class="work_item" v-for="(item, index) in workItems" :key="index">
        <h2>{{ item.name }}</h2>
        <h3>{{ item.count }} позиции</h3>
        <a href="/vacancies">
          <v-btn depressed
            color="primary"
            style="height: 50px;margin-left:68%;margin-top: 5%;width: 25%"
            >
          Подробнее    
        </v-btn>
        </a>
      </div>

      <a href="/vacancies">
      <v-btn depressed
            color="primary"
            style="height: 50px;margin-left:32%;margin-top: 5%;margin-bottom:5%;width: 25%"
            >
            Показать больше вакансий</v-btn>
      </a>
    </div> -->

    <div class="cert" id="cert">
      <h1 style="font-weight: 900 !important">Сертификаты.</h1>
      <picture>
        <source srcset="../assets/rock1.webp" type="image/webp">
        <img class="cert_1" src="../assets/rock1.png" alt="">
      </picture>
      <picture>
        <source srcset="../assets/rock2.webp" type="image/webp">
        <img class="cert_2" src="../assets/rock2.png" alt="">
      </picture>
      <!-- <img class="cert_3" src="../assets/tower2.png" alt=""> -->
      <div class="cert_img">
        <div>
          <picture>
            <source srcset="../assets/slide1.webp" type="image/webp">  
            <img @click="changeImage($event.target)" src="../assets/slide1.png" alt="">
          </picture>
          <picture>
            <source srcset="../assets/slide1upd.webp" type="image/webp">
            <img @click="changeAnotherImage($event.target)" style="left: 0vw;" class="cert_img_upd" src="../assets/slide1upd.png" alt="">
          </picture>
        </div>

        <div>
          <picture>
            <source srcset="../assets/slide2.webp" type="image/webp">  
            <img @click="changeImage($event.target)" src="../assets/slide2.png" alt="">
          </picture>
          <picture>
            <source srcset="../assets/slide2upd.webp" type="image/webp">
            <img @click="changeAnotherImage($event.target)" style="left: 0vw;" class="cert_img_upd" src="../assets/slide2upd.png" alt="">
          </picture>
        </div>

        <div>
          <picture>
            <source srcset="../assets/slide3.webp" type="image/webp">  
            <img @click="changeImage($event.target)" src="../assets/slide3.png" alt="">
          </picture>
          <picture>
            <source srcset="../assets/slide3upd.webp" type="image/webp">
            <img @click="changeAnotherImage($event.target)" style="left: 0vw;" class="cert_img_upd" src="../assets/slide3upd.png" alt="">
          </picture>
        </div>

        <div>
          <picture>
            <source srcset="../assets/slide4.webp" type="image/webp">  
            <img @click="changeImage($event.target)" src="../assets/slide4.png" alt="">
          </picture>
          <picture>
            <source srcset="../assets/slide4upd.webp" type="image/webp">
            <img @click="changeAnotherImage($event.target)" style="left: 0vw;" class="cert_img_upd" src="../assets/slide4upd.png" alt="">
          </picture>
        </div>
      </div>
    </div>

    <div class="cert_mobile">
      <h1>Сертификаты.</h1>
      <div class="cert_img">
        <div>
          <picture>
            <source srcset="../assets/slide1.webp" type="image/webp">  
            <img @click="changeImage($event.target)" src="../assets/slide1.png" alt="">
          </picture>
          <picture>
            <source srcset="../assets/slide1upd.webp" type="image/webp">
            <img @click="changeAnotherImage($event.target)" style="left: 0vw;" class="cert_img_upd" src="../assets/slide1upd.png" alt="">
          </picture>
        </div>

        <div>
          <picture>
            <source srcset="../assets/slide2.webp" type="image/webp">  
            <img @click="changeImage($event.target)" src="../assets/slide2.png" alt="">
          </picture>
          <picture>
            <source srcset="../assets/slide2upd.webp" type="image/webp">
            <img @click="changeAnotherImage($event.target)" style="left: 78vw;" class="cert_img_upd" src="../assets/slide2upd.png" alt="">
          </picture>
        </div>

        <div>
          <picture>
            <source srcset="../assets/slide3.webp" type="image/webp">  
            <img @click="changeImage($event.target)" src="../assets/slide3.png" alt="">
          </picture>
          <picture>
            <source srcset="../assets/slide3upd.webp" type="image/webp">
            <img @click="changeAnotherImage($event.target)" style="left: 156vw;" class="cert_img_upd" src="../assets/slide3upd.png" alt="">
          </picture>
        </div>

        <div>
          <picture>
            <source srcset="../assets/slide4.webp" type="image/webp">  
            <img @click="changeImage($event.target)" src="../assets/slide4.png" alt="">
          </picture>
          <picture>
            <source srcset="../assets/slide4upd.webp" type="image/webp">
            <img @click="changeAnotherImage($event.target)" style="left: 234vw;" class="cert_img_upd" src="../assets/slide4upd.png" alt="">
          </picture>
        </div>
      </div>

      <div class="cert_mobile_right">
        <p style="font-size: 12vw;color: grey;position:relative;left:0px;margin: 0;height: 7vw;"><img src="../assets/arrow_right.png" alt=""></p>
      </div>

    </div>

    <!-- <div class="sudna">
      <h1>Наши суда.</h1>
      <div class="sudna_item" style="width:15vw;">
        <img src="../assets/sudno1.png" alt="">
        <div><p>Нефтетакновый талкер</p></div>
      </div>

      <div class="sudna_item" style="width:24vw;">
        <img src="../assets/sudno2.png" alt="">
        <div><p>Судно-контейнеровоз</p></div>
      </div>

      <div class="sudna_item" style="width:24vw;">
        <img src="../assets/sudno3.png" alt="">
        <div><p>Плавучая гостиница</p></div>
      </div>

      <div class="sudna_item" style="width:15vw;">
        <img src="../assets/sudno4.png" alt="">
        <div><p>Судно для перевозки модулей</p></div>
      </div>
    </div> -->

    <div class="count">
      <h1 v-if="!loading" style="font-weight: 900 !important">Мы в цифрах.</h1>
      <div class="count_numb" ref="count">
        <span class="count_numb_1" id="a">{{ count_type }}</span>
        <span class="count_numb_2" id="b">{{ people_count }}</span>
      </div>
      <div class="count_text">
        <span class="count_text_1">Видов судов</span>
        <span class="count_text_2">Человек, штат компании</span>
      </div>
      <div style="background: #DEDEDE;height:6px;width:100vw;position:relative;top:20px;"></div>

      <span class="count_know">{{ nav_to_sudna }}</span>
      <a href="/Sudy" style="opacity:1;"><v-btn depressed color="primary" style="position: relative;top:-15px;left:65vw;width:22vw;height:86px;letter-spacing:0.01em;text-transform:initial;font-size:2.5vw;font-weight:bold;font-family: 'Montserrat', sans-serif;">Подробнее</v-btn></a>
    </div>

    <div class="count_mobile">
      <h1 v-if="!loading">Мы в цифрах.</h1>
      <div class="count_mobile_1">
        <span class="count_numb_1" id="c">{{ count_type }}</span>
        <p class="count_text_1" style="width:44vw;">Видов судов</p>
      </div>
      <img class="count_mobile_3" src="../assets/rock3.png" alt="">
      <picture>
        <source srcset="../assets/rock2.webp" type="image/webp">
        <img class="count_mobile_4" src="../assets/rock2.png" alt="">
      </picture>
      <span style="margin-top:6vw;display:inline-block" class="count_numb_2" id="d">{{ people_count }}</span>
      <p style="position:relative;top:-6vw;">Человек, штат компании</p>

      <div style="width: 100vw;height:2px;background: #DEDEDE;position:relative;left:-5vw;"></div>
      <h2>{{ nav_to_sudna }}</h2>
      <a href="/Sudy"><v-btn color="primary" style="font-size:3.4vw;width:50vw;margin-left:20vw;margin-top:26px;margin-bottom:14vw;letter-spacing:0.01em;text-transform:initial;font-size:3.4vw;font-weight:bold;font-family: 'Montserrat', sans-serif;">Подробнее</v-btn></a>
    </div>

    <div class="feedback">
      <div style="background-color: rgba(19, 19, 19, 0.8);width:100vw;height:40vw;">
      <div class="feedback_form">

        <h2 style="font-weight: 900 !important">Свяжитесь с нами</h2>
        <v-text-field
          label="Имя"
          v-model="name"
          hide-details
          style="background: rgba(255, 255, 255, 0.3) !important;border: 0.292639px solid #7C7C7C !important;box-sizing: border-box;backdrop-filter: blur(5.85278px) !important;margin-top:30px;padding-left: 10px;"
        ></v-text-field>
        <v-text-field
          label="Телефон"
          v-model="phone"
          hide-details
          style="background: rgba(255, 255, 255, 0.3) !important;border: 0.292639px solid #7C7C7C !important;box-sizing: border-box;backdrop-filter: blur(5.85278px) !important;margin-top:10px;padding-left: 10px;"
        ></v-text-field>
        <v-btn
        style="width:100%;height: 50px;margin-top: 50px;padding-left: 10px;letter-spacing:0.01em;text-transform:initial;font-size:1.3vw;font-weight:bold;font-family: 'Montserrat', sans-serif;"
              depressed
              color="primary"
              @click="send"
            >
          Отправить заявку
        </v-btn>
      </div>
      </div>
    </div>


    <div class="feedback_mobile">
      <img class="feedback_mobile_wave" src="../assets/wave2.png" alt="">
      <h1 style="width: 55vw;">Свяжитесь с нами</h1>
      <v-text-field
          label="Имя"
          v-model="name"
          hide-details
          color="white"
          style="background: rgba(255, 255, 255, 0.3) !important; color: white;border: 0.292639px solid #7C7C7C !important;backdrop-filter: blur(5.85278px) !important;margin-top:30px;padding-left: 10px;width:86vw;border: 0px;padding-top:1.4vw;"
        >
          <template v-slot:label style="color: white;border:0px;">
            <div style="color: white;border:0px;">
              Имя
            </div>
          </template>
        </v-text-field>
        <v-text-field
          label="Телефон"
          v-model="phone"
          hide-details
          color="white"
          style="background: rgba(255, 255, 255, 0.3) !important;border: 0.292639px solid #7C7C7C !important;backdrop-filter: blur(5.85278px) !important;margin-top:10px;padding-left: 10px;width:86vw;padding-top:1.4vw;"
        >
          <template v-slot:label style="color: white;border:0px;">
            <div style="color: white;border:0px;">
              Телефон
            </div>
          </template>
        </v-text-field>
        <v-btn
        style="width:49vw;height: 50px;margin-top: 8.5vw;margin-bottom: 7vw;padding-left: 10px;font-size: 3.4vw;letter-spacing:0.01em;text-transform:initial;font-size:3.4vw;font-weight:bold;font-family: 'Montserrat', sans-serif;"
              depressed
              color="primary"
              @click="send"
            >
          Оставить заявку
        </v-btn>
        <p>Трудоустройство казахстанских моряков на суда торгового флота</p>
    </div>
    <Footer id="footer"/>
    <v-dialog v-model="popup"
    width="600"
    >
      <v-card style="padding: 10px;">
          <h2>Свяжитесь с нами</h2>
          <v-row>
          <v-col cols="5">
            <v-text-field
              label="Имя"
              v-model="name"
              style="margin-top:10px;"
              hide-details
            ></v-text-field>
          </v-col>
          <v-col cols="1"></v-col>
          <v-col cols="5">
            <v-text-field
              label="Телефон"
              style="margin-top:10px;"
              v-model="phone"
              hide-details
            ></v-text-field>
          </v-col>
          </v-row>
          <v-btn
              style="margin-top:10px;margin-left: 200px;letter-spacing:0.01em;text-transform:initial;font-size:1.2vw;font-weight:bold;font-family: 'Montserrat', sans-serif;"
                depressed
                color="primary"
                @click="send"
              >
            Отправить заявку
          </v-btn>
      </v-card>
    </v-dialog>


    <v-dialog v-model="popupMobile" class="dialog_mobile"
    fullscreen
    style="position:absolute;z-index:1000;"
    >
      <v-card style="padding-left: 5vw !important;padding-top: 100px !important;position:relative;">
          <v-btn style="color: grey;font-size: 3vw;position:absolute;right: 10vw;top:40px;" @click="popupMobile = false">x</v-btn>
          <h2>Свяжитесь с нами</h2>
            <v-text-field
              label="Имя"
              v-model="name"
              style="margin-top:5vw; width: 85vw;"
              hide-details
            ></v-text-field>
            <v-text-field
              label="Телефон"
              style="margin-top:5vw;width: 85vw;"
              v-model="phone"
              hide-details
            ></v-text-field>
          <v-file-input
            show-size
            label="Загрузить анкету"
            style="width: 85vw;margin-top: 5vw;"
            truncate-length="50"
          ></v-file-input>
          <v-btn
              style="width: 85vw;margin-top: 5vw;font-size:3.2vw;letter-spacing:0.01em;text-transform:initial;font-size:3.4vw;font-weight:bold;font-family: 'Montserrat', sans-serif;"
                depressed
                color="primary"
                @click="send"
              >
            Отправить заявку
          </v-btn>
      </v-card>
    </v-dialog>
  </div>
</template>

<script>
import Loading from '@/pages/Loading.vue'
import Header from '@/components/Header.vue'
import Footer from '@/components/Footer.vue'
import {scroller} from 'vue-scrollto/src/scrollTo'

export default {
  name: 'Home',
  data(){
    return{
      about_1: '',
      about_2: '',
      about_3: '',
      about_4: '',
      education_1: '',
      education_2: '',
      count_type: '',
      people_count: '',
      nav_to_sudna: '',
      name: '',
      example: '',
      popup: false, 
      phone: '',
      loading: true,
      limit: 1,
      isMain: true,
      popupMobile: false, 
      speed: 10,
      workItems: [
        {
          name: 'Deputy Harbour Master – (IOW)',
          count: 2,
        },
        {
          name: 'Deputy Harbour Master – (IOW)',
          count: 2,
        },
        {
          name: 'Deputy Harbour Master – (IOW)',
          count: 2,
        },
        {
          name: 'Deputy Harbour Master – (IOW)',
          count: 2,
        },
      ],
      vacancies: [
      {
        name: "Капитан",
        count: 1,
        text: 'Deputy Harbour Master – Permanent – IOW – up to £40k plus benefits Cowes Harbour Commission (CHC) is working exclusively with Navis Consulting to appoint a new Deputy Harbour Master.',
        sudno: 'MCV Беркут',
        time: '4+1 месяца',
        cost: '2000 USD'
      },
      {
        name: "Старший механик",
        count: 3,
        text: 'Deputy Harbour Master – Permanent – IOW – up to £40k plus benefits Cowes Harbour Commission (CHC) is working exclusively with Navis Consulting to appoint a new Deputy Harbour Master.',
        sudno: 'MCV Беркут',
        time: '4+1 месяца',
        cost: '2000 USD'
      },
      ],
    }
  },
  created(){
    this.getVac();
    setTimeout(()=>{
      this.loading = false
      this.playVideo()
    }, 2500)

    setTimeout(()=>{
      let inputs = document.querySelectorAll(".v-input input")
      for(let item of inputs){
        item.style.maxHeight = '37px'
      }
    }, 1000)

    // document.querySelector("#video_1").play()
  },
  computed:{
    query(){
      return this.$route.query.id
    }
  },
  mounted(){
    this.getData()
    const firstScrollTo = scroller()
    if(this.query == 'about'){
      setTimeout(()=>{
        firstScrollTo('#about')
      }, 3000)
    }
    else if(this.query == 'education'){
      setTimeout(()=>{
        firstScrollTo('#education')
      }, 3000)
    }
    else if(this.query == 'vac'){
      setTimeout(()=>{
        firstScrollTo('#vac')
      }, 3000)
    }
    else if(this.query == 'cert'){
      setTimeout(()=>{
        firstScrollTo('#cert')
      }, 3000)
    }
    else if(this.query == 'footer'){
      setTimeout(()=>{
        firstScrollTo('#footer')
      }, 3000)
    }
    else{
      setTimeout(()=>{
        firstScrollTo('#home123')
      }, 3000)
    }
    const obj = document.querySelector("#b")
    const obj1 = document.querySelector("#a")
    const obj2 = document.querySelector("#c")
    const obj3 = document.querySelector("#d")
    setInterval(()=>{
        this.animateValue(obj, 0, this.people_count, 5000);
        this.animateValue(obj1, 0, this.count_type, 5000);
        this.animateValue(obj3, 0, this.people_count, 5000);
        this.animateValue(obj2, 0, this.count_type, 5000);
    },10000)
  },
  methods: {
    getData(){
            this.$axios.get("https://periodicals.abelsharman.kz/crewingData")
            .then((res)=>{
                this.about_1 = res.data[0].about_1
                this.about_2 = res.data[0].about_2
                this.about_3 = res.data[0].about_3
                this.about_4 = res.data[0].about_4
                this.education_1 = res.data[0].education_1
                this.education_2 = res.data[0].education_2
                this.count_type = res.data[0].count_type
                this.people_count = res.data[0].people_count
                this.nav_to_sudna = res.data[0].nav_to_sudna
            })
        },
    getVac(){
            this.$axios.get("https://periodicals.abelsharman.kz/crewings")
            .then((res)=>{
                this.vacancies = res.data
                // this.vacancies.splice(1, 8);
                console.log(this.vacancies)
            })
        },
    playVideo(){
      var autoPlayVideo = document.querySelector("#video_1")
      autoPlayVideo.oncanplaythrough = function() {
        autoPlayVideo.muted = true;
        autoPlayVideo.play();
        autoPlayVideo.pause();
        autoPlayVideo.play();
      }
    },
    send(){
      let name = this.name
      let phone = this.phone
      let example = this.example
      if(example.length > 0){
        this.$axios.post(`https://periodicals.abelsharman.kz/send?name=${name}&phone=${phone}&example=${example}`)
          .then((res)=>{
            console.log(res)
            if(res){
              this.popup = false
              this.name = ''
              this.phone = ''
              this.example = ''
              alert("Отправлено")
            }
          })
      }
      else{
        this.$axios.post(`https://periodicals.abelsharman.kz/send?name=${name}&phone=${phone}`)
        .then((res)=>{
          console.log(res)
          if(res){
            this.popup = false
            this.name = ''
            this.phone = ''
            this.example = ''
            alert("Отправлено")
          }
        })
      }
    },
    animateValue(obj, start, end, duration) {
      let startTimestamp = null;
      const step = (timestamp) => {
        if (!startTimestamp) startTimestamp = timestamp;
        const progress = Math.min((timestamp - startTimestamp) / duration, 1) / 10;
        obj.innerHTML = Math.floor(progress * (end + start) + start);
        if (progress < 1) {
          window.requestAnimationFrame(step);
        }
      };
      window.requestAnimationFrame(step);
    },
    changeImage(event){
      event.style.transform = 'rotateY(90deg)'
      event.parentNode.parentNode.childNodes[2].childNodes[2].style.transform = 'rotateY(0deg)'
    },
    changeAnotherImage(event){
      event.style.transform = 'rotateY(90deg)'
      event.parentNode.parentNode.childNodes[0].childNodes[2].style.transform = 'rotateY(0deg)'
    }
  },
  components: {
    Loading,
    Header,
    Footer
  },
}
</script>

<style lang="scss" scoped>
@keyframes leftRight {
  0%{
    left: 0px;
  }
  50%{
    left: 10vw;
  }
  100%{
    left: 0px;
  }
}
@media screen and (min-width: 490px) {
  .home_mobile, .about_mobile, .education_mobile, .vac_mobile, .cert_mobile, .count_mobile, .feedback_mobile{
    display: none;
  }
  .about{
    background: linear-gradient(264.1deg, #063661 0%, #0773D3 99.34%);
    width: 100vw;
    z-index: 1;
    height: 35vw;
    padding-top: 55px;
    top: -10px;
    position: relative;
    font-family: "Montserrat", sans-serif !important;
    .about_1{
      font-family: "Montserrat", sans-serif !important;
      position: absolute;
      top: 2%;
      right: -8vw;
      z-index: 4;
    }
    .about_info{
      margin-left: 51vw;
      font-family: "Montserrat", sans-serif !important;
      margin-top: 50px;
      .about_div{
        width: 95px;
        height: 4px;
        font-family: "Montserrat", sans-serif !important;
        background: #01DFFD;
      }
      h1{
        font-style: normal;
        font-weight: bold;
        font-family: "Montserrat", sans-serif !important;
        font-size: 5.19vw; //72px;
        line-height: 6.15vw; //88px;
        letter-spacing: -0.02em;
        color: #FFFFFF;
        margin: 0;
      }
      h2{
        font-style: normal;
        font-family: "Montserrat", sans-serif !important;
        font-weight: bold;
        font-size: 2.0vw; //30px;
        line-height: 2.592vw; //37px;
        letter-spacing: -0.02em;
        color: #32A3B2;
      }
    }
    .about_text{
      background: #FFFFFF;
      font-family: "Montserrat", sans-serif !important;
      box-shadow: 4px 8px 10px rgba(0, 0, 0, 0.5);
      border-radius: 20px;
      width: 85vw;
      margin-left: 7.5vw;
      margin-top: 25px;
      z-index: 2;
      height: 27vw;
      position: relative;
      .about_text_1{
        display: inline-block;
        font-family: "Montserrat", sans-serif !important;
        margin-left: 3%;
        margin-right: 3%;
        width: 34%;
        position: relative;
        height: max-content;
        border-radius: 15px;
        top: -22.5vw;
        z-index: 3;
        p{
          font-style: normal;
          font-weight: normal;
          font-family: "Montserrat", sans-serif !important;
          font-size: 1.1vw; //18px;
          line-height: 1.44vw; //21px;
          letter-spacing: -0.02em;
          width: 80%;
          margin-left: 2%;
          color: #C0C0C0;
        }
        img{
          width: 28vw; //388px;
          height: 35vw; //488px;
          object-fit: cover;
          font-family: "Montserrat", sans-serif !important;
          border-radius: 15px;
          border: 2px solid #FFFFFF;
        }
        strong{
          font-style: normal;
          font-family: "Montserrat", sans-serif !important;
          font-weight: bold;
          font-size: 1.73vw; //25px;
          line-height: 2.1vw; //30px;
          text-align: center;
          letter-spacing: -0.02em;
          color: #000000;
        }
        h2{
          font-style: normal;
          font-weight: bold;
          font-family: "Montserrat", sans-serif !important;
          font-size: 1.736vw; //25px;
          line-height: 2.1vw; //30px;
          text-align: right;
          letter-spacing: -0.02em;

          color: #494949;
        }
      }
      .about_text_2{
        display: inline-block;
        font-family: "Montserrat", sans-serif !important;
        width: 55%;
        vertical-align: top;
        margin: 36px 0 46px 0;
        p{
          font-style: normal;
          font-weight: normal;
          font-family: "Montserrat", sans-serif !important;
          font-size: 1.36vw; //20px;
          line-height: 1.7vw; //27px;

          color: #000000;
        }
      }
    }
  }
  .education{
    width: 100vw;
    font-family: "Montserrat", sans-serif !important;
    padding-top: 5vw;
    .education_info_img{
      img{
        width: 100%;
        position: relative;
        height: auto;
        top: -180px;
        margin-left: 40%;
      }
      position: absolute;
    }
    .education_info{
      display: inline-block;
      width: 74vw;
      font-family: "Montserrat", sans-serif !important;
      vertical-align: top;
      padding: 6% 0 0 8vw;
      position: relative;
      background: linear-gradient(264.1deg, #063661 0%, #078FD3 99.34%);
      height: 50vw;
      h1{
        font-style: normal;
        font-weight: bold;
        font-size: 4.8vw; //72px;
        font-family: "Montserrat", sans-serif !important;
        line-height: 6.4vw; //88px;
        letter-spacing: -0.02em;
        color: #FFFFFF;
        margin-top: 1%;
      }
      button{
        border-bottom-left-radius: 0px;
        border-bottom-right-radius: 20px;
        border-top-left-radius: 20px;
        border-top-right-radius: 0px;
        font-size: 0.9vw;
        font-style: normal;
        line-height: 15px;
        text-align: center;
        color: #FFFFFF;
        width: 17vw;
        height: 2.5vw;
      }
      .education_info_text{
        background: #FFFFFF;
        font-family: "Montserrat", sans-serif !important;
        box-shadow: 4px 8px 10px rgba(0, 0, 0, 0.5);
        border-radius: 20px;
        width: 68%;
        padding: 3%;
        margin-top: 3%;
        position: relative;
        p{
          font-style: normal;
          font-weight: normal;
          font-family: "Montserrat", sans-serif !important;
          font-size: 1.26vw; //20px;
          line-height: 1.78vw; //27px;

          color: #000000
        }
      }
    }
    img{
      display: inline-block;
      width: 25.6vw;
      height: 50vw;
    }
  }
  .work{
    width: 100vw;
    font-family: "Montserrat", sans-serif !important;
    padding-top: 5vw;
    padding-left: 8vw;
    h1{
      font-style: normal;
      font-weight: bold;
      font-family: "Montserrat", sans-serif !important;
      font-size: 4.89vw; //72px;
      line-height: 6.4vw; //88px;
      letter-spacing: -0.02em;
      color: #1A1A1A;
    }
    .work_item{
      background: #FFFFFF;
      border: 0.5px solid #848484;
      box-sizing: border-box;
      display: inline-block;
      box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25);
      border-radius: 15px;
      width: 40vw;
      font-family: "Montserrat", sans-serif !important;
      margin-right: 2vw;
      margin-top: 2vw;
      padding-top: 2vw;
      padding-left: 2vw;
      padding-bottom: 1.5vw;
      h2, h3{
        font-style: normal;
        font-weight: bold;
        font-family: "Montserrat", sans-serif !important;
        font-size: 1.91vw; //26px;
        line-height: 2.2vw; //30px;
        letter-spacing: -0.02em;
        color: #000000;
      }
      h3{
        color: grey;
      }
    }
  }
  .cert{
    width: 100vw;
    font-family: "Montserrat", sans-serif !important;
    padding-top: 5vw;
    padding-left: 8vw;
    position: relative;
    h1{
      font-style: normal;
      font-weight: bold;
      font-family: "Montserrat", sans-serif !important;
      font-size: 4.89vw; //72px;
      line-height: 6.4vw; //88px;
      letter-spacing: -0.02em;
      color: #1A1A1A;
    }
    .cert_1{
      position: absolute;
      left: 0%;
      font-family: "Montserrat", sans-serif !important;
      top: 60%;
    }
    .cert_2{
      position: absolute;
      left: 2%;
      font-family: "Montserrat", sans-serif !important;
      top: 60%;
    }
    .cert_3{
      position: absolute;
      right: 0%;
      top: 0%;
      font-family: "Montserrat", sans-serif !important;
    }
    .cert_img{
      margin-top: 5vw;
      font-family: "Montserrat", sans-serif !important;
      height: 30vw;
      div{
        position: relative;
        width: 22%;
        display: inline-block;
        height: 30vw;
      }
      img{
        width: 90%;
        margin: 10% 5%;
        cursor: pointer;
        transition: 0.5s all ease-in;
      }
      img:hover{
        width: 100%;
        margin: 0%;
      }
    }
    .cert_img_upd{
      position: absolute;
      transform:rotateY(90deg);
    }
  }
  .sudna{
    width: 100vw;
    font-family: "Montserrat", sans-serif !important;
    padding-top: 5vw;
    padding-left: 8vw;
    padding-bottom: 5vw;
    h1{
      font-style: normal;
      font-weight: bold;
      font-family: "Montserrat", sans-serif !important;
      font-size: 4.89vw; //72px;
      line-height: 6.4vw; //88px;
      letter-spacing: -0.02em;
      color: #1A1A1A;
    }
    .sudna_item{
      display: inline-block;
      margin-right: 1vw;
      font-family: "Montserrat", sans-serif !important;
      height: 300px;
      p{
        font-style: normal;
        font-family: "Montserrat", sans-serif !important;
        font-weight: bold;
        font-size: 1.06vw; //20px;
        text-align: center;
        letter-spacing: -0.02em;
        color: #FFFFFF;
        margin: 0;
        padding-top: 1vw;
      }
      div{
        background: linear-gradient(264.1deg, #063661 0%, #0773D3 99.34%);
        border-bottom-left-radius: 15px;
        border-bottom-right-radius: 15px;
        font-family: "Montserrat", sans-serif !important;
        margin: 0;
        position: relative;
        top: -10px;
        height: 5vw;
      }
      img{ 
        object-fit: contain;
        width: 100%;
        border-radius: 15px 15px 0px 0px;
      }
    }
  }
  .count{
    width: 100vw;
    font-family: "Montserrat", sans-serif !important;
    padding-top: 5vw;
    padding-bottom: 5vw;
    margin-bottom: 5vw;
    position: relative;
    h1{
      font-style: normal;
      font-weight: bold;
      font-size: 4.89vw; //72px;
      line-height: 6.4vw; //88px;
      letter-spacing: -0.02em;
      color: #FFFFFF;
      position: absolute;
      top: 20px;
      font-family: "Montserrat", sans-serif !important;
      z-index: 100;
      margin-left: 8vw;
    }
    .count_numb{
      background: linear-gradient(264.1deg, #063661 0%, #0773D3 99.34%);
      font-family: "Montserrat", sans-serif !important;
      width: 100vw;
      position: relative;
      top:60px;
      .count_numb_1, .count_numb_2{
        font-weight: bold;
        font-size: 229.661px;
        line-height: 280px;
        font-family: "Montserrat", sans-serif !important;
        text-align: center;
        letter-spacing: -0.02em;
        display: inline-block;
        color: #FFFFFF;
        
      }
      .count_numb_1{
        margin-left: 28vw;
      }
      .count_numb_2{
        margin-left: 16vw;
      }

    }
    .count_text{
      background: white;
      width: 100vw;
      height: 150px;
      position: relative;
      font-family: "Montserrat", sans-serif !important;
      top: 40px;
      padding-top: 50px;
      .count_text_1, .count_text_2{
        font-style: normal;
        font-weight: normal;
        font-size: 26px;
        line-height: 31px;
        font-family: "Montserrat", sans-serif !important;
        text-align: center;
        letter-spacing: -0.02em;

        color: #000000;
      }
      .count_text_1{
        margin-left: 27vw;
      }
      .count_text_2{
        margin-left: 15vw;
      }
    }
    .count_know{
      position: relative;
      top: 80px;
      font-style: normal;
      font-weight: bold;
      font-size: 35px;
      display: block;
      line-height: 43px;
      color: #000000;
      width: 36vw;
      margin-left: 13vw;
    }

  }
  .feedback{
    width: 100vw;
    height: 40vw;
    font-family: "Montserrat", sans-serif !important;
    background: url("../assets/shtur.png") no-repeat;
    background-color: rgba(19, 19, 19, 0.8);
    background-size: cover;
    font-family: "Montserrat", sans-serif !important;
    position: relative;
    .feedback_form{
      font-family: "Montserrat", sans-serif !important;
      width: 24vw;
      padding-top: 10vw;
      margin-left: 8vw;
      margin-bottom: 5vw;
    }
    h2{
      font-style: normal;
      font-weight: bold;
      font-family: "Montserrat", sans-serif !important;
      font-size: 2.49vw; //34px;
      line-height: 2.9vw; //40px;
      letter-spacing: -0.02em;
      width:50%;
      color: #FFFFFF;
    }
  }
  .vac{
    width: 100vw;
    font-family: "Montserrat", sans-serif !important;
    padding-top: 5vw;
    padding-left: 8vw;
    padding-bottom: 5vw;
    position: relative;
    h1{
      font-style: normal;
      font-weight: bold;
      font-family: "Montserrat", sans-serif !important;
      font-size: 4.89vw; //72px;
      line-height: 6.4vw; //88px;
      letter-spacing: -0.02em;
      color: #1A1A1A;
    }
    .vac_1{
      position: absolute;
      display: inline-block;
      top: -5%;
      left: 46%;
    }
    .vac_2{
      position: absolute;
      display: inline-block;
      top: 52%;
      right: 0%;
    }
    .vac_3{
      position: absolute;
      display: inline-block;
      top: 32%;
      left: 0%;
    }
  }
  .vac_list_item{
    position: relative;
    font-family: "Montserrat", sans-serif !important;
        margin-top: 44px;
        width: 100%;



        .vac_list_item_main{
          display: inline-block;
          width: 50%;
          font-family: "Montserrat", sans-serif !important;
          vertical-align: top;
          background: #FFFFFF;
          border: 0.5px solid #848484;
          box-sizing: border-box;
          box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25);
          border-radius: 15px;
          padding: 36px 2% 36px 2%;
          h1,h2{
            font-style: normal;
            font-weight: bold;
            font-size: 1.81vw;//26px;
            line-height: 2vw; //30px;
            letter-spacing: -0.02em;
            color: #000000;
            font-family: "Montserrat", sans-serif !important;
            margin: 0;
          }
          h2{
            font-size: 1.71vw;
            color: grey;

          }
          p{
            font-style: normal;
            font-weight: normal;
            font-size: 1.22vw; //18px;
            line-height: 1.62vw; //25px;
            margin-top: 24px;
            font-family: "Montserrat", sans-serif !important;
            color: #000000;
            width: 70%;
          }
          button{
            margin-top: 00px;
            height: 47px;
            margin-left: 70%;
            font-family: "Montserrat", sans-serif !important;
            width: 30%;
            font-size: 0.8vw;
          }
        }






        .vac_list_item_dop{
          display: inline-block;
          width: 23%;
          background: #FFFFFF;
          border: 0.5px solid #848484;
          box-sizing: border-box;
          font-family: "Montserrat", sans-serif !important;
          box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25);
          border-radius: 15px;
          margin-top: 10px;
          padding: 35px 5% 35px 3%;
          p{
            margin: 0;
            font-family: "Montserrat", sans-serif !important;
          }
          .vac_list_item_dop_1, .vac_list_item_dop_2{
            font-style: normal;
            font-weight: bold;
            font-family: "Montserrat", sans-serif !important;
            font-size: 1.02vw; //14.2963px;
            line-height: 1.18vw; //17px;
            margin: 12px 0;
            color: #000000;
          }
          .vac_list_item_dop_2{
            font-weight: 300;
            font-family: "Montserrat", sans-serif !important;
          }
        }
      
  }
  .home img{
    position: absolute;
    z-index: 5;
    width: 60vw;
    top: 7vw;
    left: 19vw;
    opacity: 0.8;
  }
  .home{
    position: relative;
    font-family: "Montserrat", sans-serif !important;
  }
  .home p, .home a{
    position: absolute;
    width: 7.7vw;
    height: 7.7vw;
    border-radius: 70px;
    font-family: "Montserrat", sans-serif !important;
    background-color: black;
    z-index: 8;
    opacity: 0;
    cursor: pointer;
  }
  .home .home_1{
    left: 45.3vw;
    top: 7vw;
  }
  .home .home_2{
    left: 54.2vw;
    top: 10.6vw;
  }
  .home_3{
    left: 58.2vw;
    top: 20.1vw;
  }
  .home .home_4{
    left: 54.1vw;
    top: 29.2vw;
  }
  .home .home_5{
    left: 45.3vw;
    top: 32.7vw;
  }
  .home .home_6{
    left: 36.2vw;
    top: 10.7vw;
  }
  .home .home_7{
    left: 32.3vw;
    top: 20vw;
  }
  .home .home_8{
    left: 36.2vw;
    top: 29.2vw;
  }
}

@media screen and (max-width: 490px){
  .main_page{
    position: relative;
  }
  .home, .about, .education, .vac, .cert, .count, .feedback{
    display: none;
  }
  .home_mobile{
    width: 100vw;
    background-repeat: no-repeat;
    background-image: url("../assets/mobile_background_home.png");
    background-color: rgba(19, 19, 19, 0.8) !important; 
    background-size: 100% 100%;
    position: relative;
    height: 79vh;
    padding-top: 93px;
    &:after {
      content: '';
      position: absolute;
      left: 0;
      right: 0;
      top: 0;
      bottom: 0;
      height: calc(79vh);
      background-color:rgba(19, 19, 19, 0.8); 
      z-index: 1;
    }
    p{
      font-style: normal;
      font-weight: bold;
      font-size: 8.5vw;
      line-height: 10vw;
      text-align: center;
      width: 90vw;
      margin-left: 5vw;
      margin-top: 20vw;
      letter-spacing: -0.02em;
      color: #FFFFFF;
      position: relative;
      z-index: 2;
      font-family: 'Montserrat', sans-serif;
    }
    button{
      width: 50vw;
      margin-left: 25vw;
      font-size: 3.4vw;
      line-height: 4.2vw;
      margin-top: 5vw;
      position: relative;
      z-index: 2;
      font-family: 'Montserrat', sans-serif;
    }
    .home_mobile_down{
      display: block;
      margin-top: 17vw;
      margin-left: 45vw;
      position: relative;
      z-index: 3;
    }
    .home_mobile_wave{
      position: absolute;
      bottom: 0px;
      z-index: 2;
      width: 100vw; 
    }
  }
  .about_mobile{
    width: 100vw;
    position: relative;
    background: #F1F1F1;
    height: 175vw;
    p{
      display: inline-block;
      font-style: normal;
      font-weight: bold;
      font-size: 8.5vw;
      line-height: 10vw;
      letter-spacing: -0.02em;
      color: #000000;
      margin-left: 5vw;
      margin-top: 24px;
      font-family: 'Montserrat', sans-serif;
    }
    img{
      display: inline-block;
      width: 47vw;
      position: absolute;
      right: -5vw;
      top: -60px;
      transform: rotate(-41.9deg);
    }
    .about_mobile_info{
      width: 90vw;
      margin-left: 5vw;
      background: #FFFFFF;
      border-radius: 0px 0px 10px 10px;
      margin-top: 4px;
      margin-bottom: 29px;
      font-family: 'Montserrat', sans-serif;
      img{
        display: block;
        position: relative;
        width: 100%;
        object-fit: cover;
        top: 0px;
        right: 0px;
        border-top-left-radius: 10px;
        transform: rotate(0deg);
        border-top-right-radius: 10px;
      }
      p{
        font-style: normal;
        font-weight: normal;
        font-size: 3.2vw;
        line-height: 4.2vw;
        margin-left: 4.5vw;
        margin-right: 8vw;
        font-family: 'Montserrat', sans-serif;
        color: #000000;
      }
    }
  }
  .education{
    width: 100vw;
    font-family: "Montserrat", sans-serif !important;
    padding-top: 5vw;
    .education_info_img{
      img{
        width: 100%;
        position: relative;
        height: auto;
        top: -180px;
        margin-left: 40%;
      }
      position: absolute;
    }
    .education_info{
      display: inline-block;
      width: 74vw;
      font-family: "Montserrat", sans-serif !important;
      vertical-align: top;
      padding: 6% 0 0 8vw;
      position: relative;
      background: linear-gradient(264.1deg, #063661 0%, #078FD3 99.34%);
      height: 50vw;
      h1{
        font-style: normal;
        font-weight: bold;
        font-size: 4.8vw; //72px;
        font-family: "Montserrat", sans-serif !important;
        line-height: 6.4vw; //88px;
        letter-spacing: -0.02em;
        color: #FFFFFF;
        margin-top: 1%;
      }
      button{
        border-bottom-left-radius: 0px;
        border-bottom-right-radius: 20px;
        border-top-left-radius: 20px;
        border-top-right-radius: 0px;
        font-size: 0.9vw;
        font-style: normal;
        line-height: 15px;
        text-align: center;
        color: #FFFFFF;
        width: 17vw;
        height: 2.5vw;
      }
      .education_info_text{
        background: #FFFFFF;
        font-family: "Montserrat", sans-serif !important;
        box-shadow: 4px 8px 10px rgba(0, 0, 0, 0.5);
        border-radius: 20px;
        width: 68%;
        padding: 3%;
        margin-top: 3%;
        position: relative;
        p{
          font-style: normal;
          font-weight: normal;
          font-family: "Montserrat", sans-serif !important;
          font-size: 1.26vw; //20px;
          line-height: 1.78vw; //27px;

          color: #000000
        }
      }
    }
    img{
      display: inline-block;
      width: 26vw;
      height: 50vw;
    }
  }
  .education_mobile{
    display: block;
    background-color: white;
    position: relative;
    padding-left: 5vw;
    width: 105vw;
    h1{
      font-style: normal;
      font-weight: bold;
      font-size: 8.5vw;
      line-height: 10vw;
      letter-spacing: -0.02em;
      color: #000000;
      font-family: 'Montserrat', sans-serif;
    }
    .education_mobile_img{
      width: 46vw;
      position: absolute;
      right: 5vw;
      top: 0;
    }
    .education_mobile_info{
      margin-top: 27px;
      background: #F1F1F1;
      border-radius: 10px;
      height: 105vw;
      font-family: 'Montserrat', sans-serif;
      .education_mobile_info_1{
        width: 45vw;
        display: inline-block;
        padding: 14px 20px 20px 13px;
        vertical-align: top;
        p{
          font-weight: normal;
          font-size: 3.2vw;
          line-height: 4.2vw;
          color: #000000;
          font-family: 'Montserrat', sans-serif;
        }
      }
      .education_mobile_info_2{
        display: inline-block;
        width: 45vw;
        img{
          object-fit: cover;
          height: 105vw;
          width: 100%;
          border-top-right-radius: 10px;
          border-bottom-right-radius: 10px;
        }
      }
    }
  }
  .work{
    width: 100vw;
    font-family: "Montserrat", sans-serif !important;
    padding-top: 5vw;
    padding-left: 8vw;
    h1{
      font-style: normal;
      font-weight: bold;
      font-family: "Montserrat", sans-serif !important;
      font-size: 4.89vw; //72px;
      line-height: 6.4vw; //88px;
      letter-spacing: -0.02em;
      color: #1A1A1A;
    }
    .work_item{
      background: #FFFFFF;
      border: 0.5px solid #848484;
      box-sizing: border-box;
      display: inline-block;
      box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25);
      border-radius: 15px;
      width: 40vw;
      font-family: "Montserrat", sans-serif !important;
      margin-right: 2vw;
      margin-top: 2vw;
      padding-top: 2vw;
      padding-left: 2vw;
      padding-bottom: 1.5vw;
      h2, h3{
        font-style: normal;
        font-weight: bold;
        font-family: "Montserrat", sans-serif !important;
        font-size: 1.91vw; //26px;
        line-height: 2.2vw; //30px;
        letter-spacing: -0.02em;
        color: #000000;
      }
      h3{
        color: grey;
      }
    }
  }
  .cert{
    width: 100vw;
    font-family: "Montserrat", sans-serif !important;
    padding-top: 5vw;
    padding-left: 8vw;
    position: relative;
    h1{
      font-style: normal;
      font-weight: bold;
      font-family: "Montserrat", sans-serif !important;
      font-size: 4.89vw; //72px;
      line-height: 6.4vw; //88px;
      letter-spacing: -0.02em;
      color: #1A1A1A;
    }
    .cert_1{
      position: absolute;
      left: 0%;
      font-family: "Montserrat", sans-serif !important;
      top: 60%;
    }
    .cert_2{
      position: absolute;
      left: 2%;
      font-family: "Montserrat", sans-serif !important;
      top: 60%;
    }
    .cert_3{
      position: absolute;
      right: 0%;
      top: 0%;
      font-family: "Montserrat", sans-serif !important;
    }
    .cert_img{
      margin-top: 5vw;
      font-family: "Montserrat", sans-serif !important;
      height: 30vw;
      div{
        position: relative;
        width: 22%;
        display: inline-block;
        height: 30vw;
      }
      img{
        width: 90%;
        margin: 10% 5%;
        cursor: pointer;
        transition: 0.5s all ease-in;
      }
      img:hover{
        width: 100%;
        margin: 0%;
      }
    }
    .cert_img_upd{
      position: absolute;
      transform:rotateY(90deg);
    }
  }
  .cert_mobile_right p{
    -webkit-animation: leftRight 2s infinite ease;
    -moz-animation: leftRight 2s infinite ease;
    -ms-animation: leftRight 2s infinite ease;
    -o-animation: leftRight 2s infinite ease;
    animation: leftRight 2s infinite ease;
    font-family: 'Montserrat', sans-serif;
  }
  .cert_mobile_right img{
    width: 15vw;
  }
  ::-webkit-scrollbar-thumb{
    background: #DADADA;
    border-radius: 20px;
  }
  .cert_mobile{
    display: block;
    padding-left: 5vw;
    width: 95vw;
    position: relative;
    margin-top: 10vw;
    h1{
      font-style: normal;
      font-weight: bold;
      font-size: 8.5vw;
      line-height: 10vw;
      letter-spacing: -0.02em;
      color: #000000;
      font-family: 'Montserrat', sans-serif;
    }
    .cert_mobile_img{
      animation: scrollLeft 0.5s ease;
    }
    .cert_img{
      overflow-x: scroll;
      position: relative;
      overflow-y: hidden;
      width: 95vw;
      height: 110vw;
      margin-top: 36px;
      font-family: 'Montserrat', sans-serif;
      white-space: nowrap;
      div{
        width: 70vw;
        display: inline-block;
        margin-right: 8vw;
        img{
          width: 100%;
          transition: 0.5s all ease-in;
        }
        .cert_img_upd{
          width: 70vw;
          position: absolute;
          transform:rotateY(90deg);
        }
      }
    }
  }
  .sudna{
    width: 100vw;
    font-family: "Montserrat", sans-serif !important;
    padding-top: 5vw;
    padding-left: 8vw;
    padding-bottom: 5vw;
    h1{
      font-style: normal;
      font-weight: bold;
      font-family: "Montserrat", sans-serif !important;
      font-size: 4.89vw; //72px;
      line-height: 6.4vw; //88px;
      letter-spacing: -0.02em;
      color: #1A1A1A;
    }
    .sudna_item{
      display: inline-block;
      margin-right: 1vw;
      font-family: "Montserrat", sans-serif !important;
      height: 300px;
      p{
        font-style: normal;
        font-family: "Montserrat", sans-serif !important;
        font-weight: bold;
        font-size: 1.06vw; //20px;
        text-align: center;
        letter-spacing: -0.02em;
        color: #FFFFFF;
        margin: 0;
        padding-top: 1vw;
      }
      div{
        background: linear-gradient(264.1deg, #063661 0%, #0773D3 99.34%);
        border-bottom-left-radius: 15px;
        border-bottom-right-radius: 15px;
        font-family: "Montserrat", sans-serif !important;
        margin: 0;
        position: relative;
        top: -10px;
        height: 5vw;
      }
      img{ 
        object-fit: contain;
        width: 100%;
        border-radius: 15px 15px 0px 0px;
      }
    }
  }
  .count{
    width: 100vw;
    font-family: "Montserrat", sans-serif !important;
    padding-top: 5vw;
    padding-bottom: 5vw;
    margin-bottom: 5vw;
    position: relative;
    h1{
      font-style: normal;
      font-weight: bold;
      font-size: 4.89vw; //72px;
      line-height: 6.4vw; //88px;
      letter-spacing: -0.02em;
      color: #FFFFFF;
      position: absolute;
      top: 20px;
      font-family: "Montserrat", sans-serif !important;
      z-index: 100;
      margin-left: 8vw;
    }
    .count_numb{
      background: linear-gradient(264.1deg, #063661 0%, #0773D3 99.34%);
      font-family: "Montserrat", sans-serif !important;
      width: 100vw;
      position: relative;
      top:60px;
      .count_numb_1, .count_numb_2{
        font-weight: bold;
        font-size: 229.661px;
        line-height: 280px;
        font-family: "Montserrat", sans-serif !important;
        text-align: center;
        letter-spacing: -0.02em;
        display: inline-block;
        color: #FFFFFF;
        
      }
      .count_numb_1{
        margin-left: 28vw;
      }
      .count_numb_2{
        margin-left: 16vw;
      }

    }
    .count_text{
      background: white;
      width: 100vw;
      height: 150px;
      position: relative;
      font-family: "Montserrat", sans-serif !important;
      top: 40px;
      padding-top: 50px;
      .count_text_1, .count_text_2{
        font-style: normal;
        font-weight: normal;
        font-size: 26px;
        line-height: 31px;
        font-family: "Montserrat", sans-serif !important;
        text-align: center;
        letter-spacing: -0.02em;

        color: #000000;
      }
      .count_text_1{
        margin-left: 27vw;
      }
      .count_text_2{
        margin-left: 15vw;
      }
    }
    .count_know{
      position: relative;
      top: 80px;
      font-style: normal;
      font-weight: bold;
      font-size: 35px;
      display: block;
      line-height: 43px;
      color: #000000;
      width: 36vw;
      margin-left: 13vw;
    }

  }
  .count_mobile{
    display: block;
    margin-top: 50px;
    padding-left: 5vw;
    h1{
      font-style: normal;
      font-weight: bold;
      font-size: 8.5vw;
      line-height: 10vw;
      letter-spacing: -0.02em;
      color: #000000;
      font-family: 'Montserrat', sans-serif;
    }
    h2{
      font-weight: bold;
      font-size: 6vw;
      line-height: 7.2vw;
      text-align: center;
      width: 85vw;
      position: relative;
      left: -5vw;
      margin-left: 5vw;
      color: #000000;
      font-family: 'Montserrat', sans-serif;
      margin-top: 11vw;
    }
    span{
      font-weight: bold;
      font-size: 26vw;
      line-height: 22vw;
      text-align: center;
      letter-spacing: -0.02em;
      color: #0773D3;
      font-family: 'Montserrat', sans-serif;
      vertical-align: top;
      margin-left: 5vw;
    }
    p{
      font-weight: 300;
      font-size: 5.8vw;
      font-family: 'Montserrat', sans-serif;
      line-height: 7.2vw;
      text-align: center;
      letter-spacing: -0.02em;
      color: #000000;
    }
    .count_mobile_1{
      display: inline-block;
      width: 38vw;
      vertical-align: top;
      font-family: 'Montserrat', sans-serif;
      padding-top: 15vw;
      padding-left: 4vw;
    }
    .count_mobile_3{
      display: inline-block;
      width: 55vw;
      font-family: 'Montserrat', sans-serif;
    }
    .count_mobile_4{
      width: 35vw;
      display: inline-block;
      font-family: 'Montserrat', sans-serif;
    }
  }
  .feedback{
    width: 100vw;
    height: 40vw;
    font-family: "Montserrat", sans-serif !important;
    background: url("../assets/shtur.png") no-repeat;
    background-color: rgba(19, 19, 19, 0.8);
    background-size: cover;
    font-family: "Montserrat", sans-serif !important;
    position: relative;
    .feedback_form{
      font-family: "Montserrat", sans-serif !important;
      width: 24vw;
      padding-top: 10vw;
      margin-left: 8vw;
      margin-bottom: 5vw;
    }
    h2{
      font-style: normal;
      font-weight: bold;
      font-family: "Montserrat", sans-serif !important;
      font-size: 2.49vw; //34px;
      line-height: 2.9vw; //40px;
      letter-spacing: -0.02em;
      width:50%;
      color: #FFFFFF;
    }
  }
  .v-text-field .v-label {
    color: white;
  }
  .theme--light.v-text-field--solo > .v-input__control > .v-input__slot{
    background-color: transparent;
  }
  .v-input__slot{
    background-color: transparent;
  }
  .feedback_mobile{
    display: block;
    padding-left: 5vw;
    position: relative;
    padding-top: 36vw;
    background: url("../assets/shtur.png") no-repeat;
    background-color: rgba(19, 19, 19, 0.8);
    background-size: cover;
    padding-bottom: 18vw;
    font-family: 'Montserrat', sans-serif;
    .feedback_mobile_wave{
      position: absolute;
      top: 0px;
      width: 100vw;
      left: 0px;
    }
    h1{
      font-style: normal;
      font-weight: bold;
      font-size: 8.5vw;
      line-height: 10vw;
      font-family: 'Montserrat', sans-serif;
      letter-spacing: -0.02em;
      color: #FFFFFF;
    }
    p{
      width: 55vw;
      font-weight: 300;
      font-size: 3.2vw;
      line-height: 4vw;
      letter-spacing: -0.02em;
      font-family: 'Montserrat', sans-serif;
      color: darkgrey;
      margin: 0;
    }
  }
  .vac{
    width: 100vw;
    font-family: "Montserrat", sans-serif !important;
    padding-top: 5vw;
    padding-left: 8vw;
    padding-bottom: 5vw;
    position: relative;
    h1{
      font-style: normal;
      font-weight: bold;
      font-family: "Montserrat", sans-serif !important;
      font-size: 4.89vw; //72px;
      line-height: 6.4vw; //88px;
      letter-spacing: -0.02em;
      color: #1A1A1A;
    }
    .vac_1{
      position: absolute;
      display: inline-block;
      top: -5%;
      left: 46%;
    }
    .vac_2{
      position: absolute;
      display: inline-block;
      top: 52%;
      right: 0%;
    }
    .vac_3{
      position: absolute;
      display: inline-block;
      top: 32%;
      left: 0%;
    }
  }
  .vac_mobile{
    display: block;
    padding-left: 5vw;
    background-color: white;
    margin-top: 41px;
    position: relative;
    font-family: 'Montserrat', sans-serif;
    margin-bottom: 30px;
    h1{
      font-weight: bold;
      font-size: 8.5vw;
      line-height: 10vw;
      font-family: 'Montserrat', sans-serif;
      letter-spacing: -0.02em;
      color: #000000; 
    }
    .vac_mobile_1{
      width: 41vw;
      position: absolute;
      font-family: 'Montserrat', sans-serif;
      right: 0px;
      top: -20vw;
    }
    .vac_mobile_2{
      width: 33vw;
      position: absolute;
      font-family: 'Montserrat', sans-serif;
      left: -10vw;
      top: 36vw;
      z-index: 2;
    }
    .vac_mobile_3{
      width: 29vw;
      font-family: 'Montserrat', sans-serif;
      position: absolute;
      right: 0px;
      transform: rotate(-30deg);
      top: 100vw;
    }
    .vac_mobile_card{
      margin-bottom: 30px;
      .vac_mobile_card_name{
        z-index: 3;
        position: relative;
        width: 89vw;
        background: #FFFFFF;
        border: 0.248762px solid lightgrey;
        box-shadow: 0px 1.99009px 1.99009px rgba(0, 0, 0, 0.25);
        border-radius: 7.46285px;
        padding: 18px 28px 21px 19px;
        margin-top: 19px;
        height: max-content;
        h1{
          font-style: normal;
          font-weight: bold;
          font-size: 4.8vw;
          line-height: 5.6vw;
          letter-spacing: -0.02em;
          color: #000000;
          span{
            color: rgb(7,115,211);
          }
        }
        p{
          font-style: normal;
          font-weight: normal;
          font-size: 3.6vw;
          line-height: 4.7vw;
          letter-spacing: -0.02em;
          color: #000000;
          margin: 0;
          margin-top: 7px;
        }
      }
      .vac_mobile_card_line{
        background: #C4C4C4;
        width: 2px;
        height: 14px;
        margin-left: 44vw;
      }
      .vac_mobile_card_dop{
        z-index: 3;
        position: relative;
        background: #FFFFFF;
        border: 0.22546px solid lightgrey;
        box-sizing: border-box;
        box-shadow: 0px 1.80368px 1.80368px rgba(0, 0, 0, 0.25);
        border-radius: 6.7638px;
        width: 89vw;
        height: max-content;
        h2, p, span{
          font-style: normal;
          font-size: 3.2vw;
          line-height: 4vw;
          color: #000000;
          margin: 0;
        }
        p{
          font-weight: 300;
          margin-bottom: 20px;
        }
        .vac_mobile_card_dop_1{
          display: inline-block;
          width: 50%;
          vertical-align: top;
          padding-left: 7vw;
          padding-top: 4vw;
          border-right: 2px solid #C4C4C4;
        }
        .vac_mobile_card_dop_2{
          display: inline-block;
          width: 48%;
          vertical-align: top;
          padding-left: 3.2vw;
          padding-top: 3.2vw;
        }
        .vac_mobile_card_dop_price{
          width: 100%;
          text-align: center;
          border-top: 2px solid #C4C4C4;
          padding: 10px 0;
          span{
            font-weight: 300;
          }
        }
      }
    }

  }
  .vac_list_item{
    position: relative;
    font-family: "Montserrat", sans-serif !important;
        margin-top: 44px;
        width: 100%;



        .vac_list_item_main{
          display: inline-block;
          width: 50%;
          font-family: "Montserrat", sans-serif !important;
          vertical-align: top;
          background: #FFFFFF;
        border: 0.5px solid #848484;
        box-sizing: border-box;
        box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25);
        border-radius: 15px;
        padding: 36px 2% 36px 2%;
          h1,h2{
            font-style: normal;
            font-weight: bold;
            font-size: 1.81vw;//26px;
            line-height: 2vw; //30px;
            letter-spacing: -0.02em;
            color: #000000;
            font-family: "Montserrat", sans-serif !important;
            margin: 0;
          }
          h2{
            font-size: 1.71vw;
            color: grey;

          }
          p{
            font-style: normal;
            font-weight: normal;
            font-size: 1.22vw; //18px;
            line-height: 1.62vw; //25px;
            margin-top: 24px;
            font-family: "Montserrat", sans-serif !important;
            color: #000000;
            width: 70%;
          }
          button{
            margin-top: 00px;
            height: 47px;
            margin-left: 70%;
            font-family: "Montserrat", sans-serif !important;
            width: 30%;
            font-size: 0.8vw;
          }
        }






        .vac_list_item_dop{
          display: inline-block;
          width: 23%;
          background: #FFFFFF;
          border: 0.5px solid #848484;
          box-sizing: border-box;
          font-family: "Montserrat", sans-serif !important;
          box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25);
          border-radius: 15px;
          margin-top: 10px;
          padding: 35px 5% 35px 3%;
          p{
            margin: 0;
            font-family: "Montserrat", sans-serif !important;
          }
          .vac_list_item_dop_1, .vac_list_item_dop_2{
            font-style: normal;
            font-weight: bold;
            font-family: "Montserrat", sans-serif !important;
            font-size: 1.02vw; //14.2963px;
            line-height: 1.18vw; //17px;
            margin: 12px 0;
            color: #000000;
          }
          .vac_list_item_dop_2{
            font-weight: 300;
            font-family: "Montserrat", sans-serif !important;
          }
        }
      
  }
}
@keyframes scrollLeft{
  0%{
    transform: rotate(0deg);
  }
  33%{
    transform: rotate(-15deg);
  }
  66%{
    transform: rotate(15deg);
  }
  100%{
    transform: rotate(0deg);
  }
}
.home_main_img{
  animation: scrollLeft 2s ease-in;
}
</style>
