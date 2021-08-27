<template>
  <div class="about">
    <Header :isMain="isMain" v-if="!loading" />
    <Loading :loading="loading" />
    <div class="vac">
      <h1 style="font-weight: 900 !important">Вакансии.</h1>
      <div class="vac_docs">
        <div class="vac_docs_download">
          <p>Скачайте образец анкеты для заполнения</p>
          <a href="https://marketbot.abelsharman.kz/anketa.doc" download><img src="../assets/download.png" alt=""></a>
          <span>Нажмите на кнопку</span>
        </div>
        <div class="vac_docs_upload">
          <div class="flex h-screen items-center justify-center text-center">
            <div class="p-12 bg-gray-100 border border-gray-300" @dragover="dragover" @dragleave="dragleave" @drop="drop">
              <input type="file" multiple name="fields[assetsFieldHandle][]" id="assetsFieldHandle" style="opacity: 0;"
                class="w-px h-px opacity-0 overflow-hidden absolute" @change="onChange" ref="file" accept=".pdf,.jpg,.jpeg,.png,.docs,.docx,.doc" />
              <img src="../assets/upload.png" alt="">
              <label for="assetsFieldHandle" class="block cursor-pointer">
                <v-divider></v-divider>
                <div>
                  <strong>Перетащите свою анкету</strong>
                  или <span class="underline"> загрузите с устройства</span>
                </div>
              </label>
              <ul class="mt-4" v-if="this.filelist.length" v-cloak>
                <p>Загружено <v-icon>mdi-cloud-upload</v-icon></p>
              </ul>
            </div>
          </div>

        </div>
      </div>




      <div class="vac_list">
        <div class="vac_list_sort">
          <v-row style="width:95%;margin-left:2.5%">
            <v-col cols="2">
              <p>Показать</p>
            </v-col>
            <v-col cols="4">
              <v-select
                :items="countItems"
                v-model="count"
                label="Количество вакансий на странице"
              ></v-select>
            </v-col>
            <v-col cols="2">
              <p>Сортировать</p>
            </v-col>
            <v-col cols="4">
              <v-select
                :items="sortItems"
                v-model="sort"
                label="Сортировать"
              ></v-select>
            </v-col>
          </v-row>
        </div>




        <div class="vac_list_item" v-for="(item, index) in vacancies" :key="index">
          <div class="vac_list_item_main">
            <h1>{{ item.nameVac }}</h1>
            <h2>{{ item.count }} позиция</h2>
            <p>{{ item.text }}</p>
            <v-btn
              depressed
              color="primary"
              @click="(popup=true),(example=item.nameVac)"
              style="letter-spacing:0.01em;text-transform:initial;padding: 0 2vw; font-size:1vw;font-weight:bold;font-family: 'Montserrat', sans-serif;"
            >
              Отправить анкету
            </v-btn>
          </div>
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

        <div class="vac_mobile_card" v-for="(item, index) in vacancies" :key="index">
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

          <a href="https://marketbot.abelsharman.kz/anketa.doc" style="text-decoration:none;" download><v-btn color="black" outlined style="text-decoration:none;font-weight:300;font-size:3.2vw;letter-spacing:0.03em;text-transform:initial;width:37vw;margin:8vw 0;">Скачать образец <img src="../assets/pdf.png" style="margin-left:0.8vw;width:3.4vw;margin-top:0.5vw;" alt=""></v-btn></a>
          <v-btn color="primary" @click="(popupMobile=true),(example=item.nameVac)" style="font-size:3.2vw;letter-spacing:0.03em;width:48vw;margin-left:2vw;margin-top:8vw;margin-bottom:8vw;letter-spacing:0.01em;text-transform:initial;font-size:3.4vw;font-weight:bold;font-family: 'Montserrat', sans-serif;">Отправить анкету</v-btn>
          <div style="width: 100%;height:1px;background-color: #C4C4C4"></div>
        </div>  
      </div>
    </div>

    <div class="feedback">
      <div style="background-color: rgba(19, 19, 19, 0.8);width:100vw;height:40vw;">
      <div class="feedback_form">

        <h2>Свяжитесь с нами</h2>
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
        style="width:100%;height: 50px;margin-top: 50px;padding-left: 10px;letter-spacing:0.01em;text-transform:initial;font-size:1.2vw;font-weight:bold;font-family: 'Montserrat', sans-serif;"
              depressed
              color="primary"
              @click="send"
            >
          Отправить заявку
        </v-btn>
      </div>
      </div>
    </div>

    <v-dialog v-model="popup" class="dialog_desktop"
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
              style="margin-top:10px;margin-left: 200px;letter-spacing:0.01em;text-transform:initial;font-size:1vw;font-weight:bold;font-family: 'Montserrat', sans-serif;"
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
    <Footer />
  </div>
</template>

<script>
import Loading from '@/pages/Loading.vue'
import Header from '@/components/Header.vue'
import Footer from '@/components/Footer.vue'
// import { SMTPClient } from 'emailjs';

// const client = new SMTPClient({
// 	user: 'abelsharman85@gmail.com',
// 	password: 'cvbn7456kjh',
// 	host: 'smtp.gmail.com',
// 	ssl: true,
// });

export default {
  name: 'Vacancy',
  data(){
    return{
      loading: true,
      isMain: false,
      popup: false, 
      popupMobile: false,
      selectedFile: '',
      name: '',
      phone: '',
      example: '',
      sort: 'Сначала новые',
      sortItems: ['Сначала новые', "Сначала старые"],
      count: '5 вакансий на странице',
      countItems: ['5 вакансий на странице', '10 вакансий на странице', '15 вакансий на странице', 'Все вакансии на странице'],
      filelist: [], // Store our uploaded files,
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
        name: "Старший помощник капитана",
        count: 2,
        text: 'Deputy Harbour Master – Permanent – IOW – up to £40k plus benefits Cowes Harbour Commission (CHC) is working exclusively with Navis Consulting to appoint a new Deputy Harbour Master.',
        sudno: 'MCV Беркут, Буксир Талас',
        time: '4+1 месяца',
        cost: '1200 USD'
      },
      {
        name: "Второй помощник капитана",
        count: 1,
        text: 'Deputy Harbour Master – Permanent – IOW – up to £40k plus benefits Cowes Harbour Commission (CHC) is working exclusively with Navis Consulting to appoint a new Deputy Harbour Master.',
        sudno: 'MCV Беркут, Буксир Талас',
        time: '4+1 месяца',
        cost: '1200 USD'
      },
      {
        name: "Третий помощник капитана",
        count: 1,
        text: 'Deputy Harbour Master – Permanent – IOW – up to £40k plus benefits Cowes Harbour Commission (CHC) is working exclusively with Navis Consulting to appoint a new Deputy Harbour Master.',
        sudno: 'MCV Беркут, Буксир Талас',
        time: '4+1 месяца',
        cost: '1200 USD'
      },
      {
        name: "Старший механик",
        count: 3,
        text: 'Deputy Harbour Master – Permanent – IOW – up to £40k plus benefits Cowes Harbour Commission (CHC) is working exclusively with Navis Consulting to appoint a new Deputy Harbour Master.',
        sudno: 'MCV Беркут, Буксир Талас',
        time: '4+1 месяца',
        cost: '1200 USD'
      },
      {
        name: "Второй механик",
        count: 1,
        text: 'Deputy Harbour Master – Permanent – IOW – up to £40k plus benefits Cowes Harbour Commission (CHC) is working exclusively with Navis Consulting to appoint a new Deputy Harbour Master.',
        sudno: 'MCV Беркут, Буксир Талас',
        time: '4+1 месяца',
        cost: '1200 USD'
      },
      {
        name: "Электромеханик",
        count: 1,
        text: 'Deputy Harbour Master – Permanent – IOW – up to £40k plus benefits Cowes Harbour Commission (CHC) is working exclusively with Navis Consulting to appoint a new Deputy Harbour Master.',
        sudno: 'MCV Беркут, Буксир Талас',
        time: '4+1 месяца',
        cost: '1200 USD'
      },
      {
        name: "Боцман",
        count: 1,
        text: 'Deputy Harbour Master – Permanent – IOW – up to £40k plus benefits Cowes Harbour Commission (CHC) is working exclusively with Navis Consulting to appoint a new Deputy Harbour Master.',
        sudno: 'MCV Беркут, Буксир Талас',
        time: '4+1 месяца',
        cost: '1200 USD'
      },
      {
        name: "Матрос",
        count: 1,
        text: 'Deputy Harbour Master – Permanent – IOW – up to £40k plus benefits Cowes Harbour Commission (CHC) is working exclusively with Navis Consulting to appoint a new Deputy Harbour Master.',
        sudno: 'MCV Беркут, Буксир Талас',
        time: '4+1 месяца',
        cost: '1200 USD'
      },
      {
        name: "Моторист",
        count: 1,
        text: 'Deputy Harbour Master – Permanent – IOW – up to £40k plus benefits Cowes Harbour Commission (CHC) is working exclusively with Navis Consulting to appoint a new Deputy Harbour Master.',
        sudno: 'MCV Беркут, Буксир Талас',
        time: '4+1 месяца',
        cost: '1200 USD'
      },
      ],
    }
  },
  created(){
    this.getVac();
    setTimeout(()=>{
      this.loading = false
    }, 2500)
  },
  components: {
    Loading,
    Header,
    Footer
  },
  delimiters: ['${', '}'], 
  methods: {
     getVac(){
            this.$axios.get("https://periodicals.abelsharman.kz/crewings")
            .then((res)=>{
                this.vacancies = res.data
            })
        },
    send(){
      let name = this.name
      let phone = this.phone
      let example = this.example
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

    },
    onChange() {
      this.filelist = [...this.$refs.file.files];
      this.selectedFile = this.filelist[0]
      const formData = new FormData();
      formData.append("file", this.selectedFile); 
      this.$axios
        .post("https://periodicals.abelsharman.kz/upload", formData)
        .then(res => {
          console.log(res);
        })
        .catch(err => {
          console.log(err);
        });
    },
    remove(i) {
      this.filelist.splice(i, 1);
    },
    dragover(event) {
      event.preventDefault();
      // Add some visual fluff to show the user can drop its files
      if (!event.currentTarget.classList.contains('bg-green-300')) {
        event.currentTarget.classList.remove('bg-gray-100');
        event.currentTarget.classList.add('bg-green-300');
      }
    },
    dragleave(event) {
      // Clean up
      event.currentTarget.classList.add('bg-gray-100');
      event.currentTarget.classList.remove('bg-green-300');
    },
    drop(event) {
      event.preventDefault();
      this.$refs.file.files = event.dataTransfer.files;
      this.onChange(); // Trigger the onChange event manually
      // Clean up
      event.currentTarget.classList.add('bg-gray-100');
      event.currentTarget.classList.remove('bg-green-300');
    }
  }
}
</script>

<style lang="scss" scoped>
@media screen and (max-width: 490px){
  .dialog_desktop{
    display: none;
  }
  .dialog_mobile{
    display: block;
  }
  .vac{
    font-family: "Montserrat", sans-serif !important;
    padding-bottom: 61px;
    padding-top: 100px;
    padding-left: 5vw;
    h1{
      font-weight: bold;
      font-size: 8.5vw;
      line-height: 10.4vw;
      letter-spacing: -0.02em;
      color: #000000;
      font-family: "Montserrat", sans-serif;
    }
    .vac_docs{
      display: none;
    }
    .vac_list{
      font-family: "Montserrat", sans-serif;
      display: inline-block;
      width: 57vw;
      vertical-align: top;
      margin-top: 10px;
      .col{
        height: 70px !important;
      }
      .vac_list_sort{
        display: none;
      }

      .vac_list_item{
        display: none;
      }
    }
    .vac_mobile_card{
      margin-bottom: 30px;
      width: 89vw;
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
          font-family: "Montserrat", sans-serif;
          line-height: 5.6vw;
          letter-spacing: -0.02em;
          color: #000000;
          span{
            color: rgb(7,115,211);
            font-family: "Montserrat", sans-serif;
          }
        }
        p{
          font-style: normal;
          font-weight: normal;
          font-size: 3.6vw;
          line-height: 4.7vw;
          font-family: "Montserrat", sans-serif;
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
        font-family: "Montserrat", sans-serif;
        margin-left: 44vw;
      }
      .vac_mobile_card_dop{
        z-index: 3;
        position: relative;
        background: #FFFFFF;
        font-family: "Montserrat", sans-serif;
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
          font-family: "Montserrat", sans-serif;
          color: #000000;
          margin: 0;
        }
        p{
          font-weight: 300;
          margin-bottom: 20px;
          font-family: "Montserrat", sans-serif;
        }
        .vac_mobile_card_dop_1{
          display: inline-block;
          width: 50%;
          vertical-align: top;
          font-family: "Montserrat", sans-serif;
          padding-left: 7vw;
          padding-top: 4vw;
          border-right: 2px solid #C4C4C4;
        }
        .vac_mobile_card_dop_2{
          display: inline-block;
          width: 48%;
          font-family: "Montserrat", sans-serif;
          vertical-align: top;
          padding-left: 3.2vw;
          padding-top: 3.2vw;
        }
        .vac_mobile_card_dop_price{
          width: 100%;
          text-align: center;
          font-family: "Montserrat", sans-serif;
          border-top: 2px solid #C4C4C4;
          padding: 10px 0;
          span{
            font-weight: 300;
            font-family: "Montserrat", sans-serif;
          }
        }
      }
    }


  }
  .feedback{
    display: none;
  }
}

@media screen and (min-width: 490px){
  .vac{
    font-family: "Montserrat", sans-serif !important;
    margin-left: 8vw;
    margin-top: 47px;
    padding-bottom: 61px;
    h1{
      font-style: normal;
      font-weight: bold;
      font-size: 72px;
      line-height: 88px;
      letter-spacing: -0.02em;
      color: #1A1A1A;
      margin-bottom: 23px;
    }
    .vac_docs{
      display: inline-block;
      width: 23vw;
      .vac_docs_download{
        background: #FFFFFF;
        border: 0.5px solid #848484;
        box-sizing: border-box;
        box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25);
        border-radius: 15px;
        width: 100%;
        padding: 27px 0 16px 0;
        p{
          width: 60%;
          margin-left: 20%;
          text-align: center;
          font-style: normal;
          font-weight: bold;
          font-size: 1.02865vw; //14.2963px;
          line-height: 17px;
          text-align: center;

          color: #000000;
        }
        a{
          margin-top: 23px;
          cursor: pointer;
          display: block;
          width: 34%;
          margin-left: 33%;
          img{
            width: 100%;
          }
        }
        span{
          margin-top: 17px;
          display: block;
          font-style: normal;
          font-weight: 300;
          font-size: 1.02865vw; //14.2963px;
          line-height: 17px;
          text-align: center;
          color: #000000;
        }
      }
      .vac_docs_upload{
        background: #FFFFFF;
        border: 0.5px solid #848484;
        box-sizing: border-box;
        box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25);
        border-radius: 15px;
        margin-top: 30px;
        font-size: 1.02865vw; //14.2963px;
        line-height: 1.32865vw; //vw17px;
        padding-bottom: 37px;
        img{
          background: #EDEDED;
          border: 0.5px dashed #7E7E7E;
          width: 72%;
          padding: 21px 21%;
          margin: 25px 0 40px 0;
        }
        strong{
          font-style: normal;
          font-weight: bold;
          font-size: 1.02865vw; //14.2963px;
          line-height: 1.32865vw; //17px;
          text-align: center;
          color: #000000;
          margin-top: 28px;
          display: block;
        }
        span{
          font-style: normal;
          font-weight: 300;
          text-decoration: underline;
          font-size: 1.02865vw; //14.2963px;
          line-height: 1.32865vw; //vw17px;
          text-align: center;
          cursor: pointer;
          color: #0773D3;
        }
      }

    }
    .vac_list{
      display: inline-block;
      width: 57vw;
      vertical-align: top;
      margin-left: 1.4vw;
      margin-top: 10px;
      .col{
        height: 70px !important;
      }
      .vac_list_sort{
        background: #E8E8E8;
        border-radius: 15px;
        width: 100%;
        p{
          font-style: normal;
          font-weight: bold;
          font-size: 1.0756vw; //16px;
          line-height: 1.3695vw; //20px;
          color: #000000;
          margin-top: 10px;
        }
      }

      .vac_list_item{
        margin-top: 44px;
        width: 100%;
        background: #FFFFFF;
        border: 0.5px solid #848484;
        box-sizing: border-box;
        box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25);
        border-radius: 15px;
        padding: 36px 0 36px 5%;



        .vac_list_item_main{
          display: inline-block;
          width: 50%;
          vertical-align: top;
          h1,h2{
            font-style: normal;
            font-weight: bold;
            font-size: 1.81vw;//26px;
            line-height: 2vw; //30px;
            letter-spacing: -0.02em;
            color: #000000;
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
            color: #000000;
          }
          button{
            margin-top: 70px;
            height: 47px;
          }
        }






        .vac_list_item_dop{
          display: inline-block;
          width: 34%;
          background: #FFFFFF;
          border: 0.5px solid #848484;
          box-sizing: border-box;
          box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25);
          border-radius: 15px;
          margin-left: 5%;
          margin-top: 60px;
          padding: 15px 5% 15px 3%;
          p{
            margin: 0;
          }
          .vac_list_item_dop_1, .vac_list_item_dop_2{
            font-style: normal;
            font-weight: bold;
            font-size: 1.02vw; //14.2963px;
            line-height: 1.18vw; //17px;
            margin: 9px 0;
            color: #000000;
          }
          .vac_list_item_dop_2{
            font-weight: 300;
          }
        }
      
      }
    }


  }
  .feedback{
    width: 100vw;
    height: 40vw;
    font-family: "Montserrat", sans-serif !important;
    background: url("../assets/shtur.png") no-repeat;
    background-color: rgba(19, 19, 19, 0.8);
    background-size: cover;
    position: relative;
    .feedback_form{
      width: 24vw;
      padding-top: 10vw;
      margin-left: 8vw;
      margin-bottom: 5vw;
    }
    h2{
      font-style: normal;
      font-weight: bold;
      font-size: 2.49vw; //34px;
      line-height: 2.9vw; //40px;
      letter-spacing: -0.02em;
      width:50%;
      color: #FFFFFF;
    }
  }
  .vac_mobile_card{
    display: none;
  }
}
[v-cloak] {
  display: none;
}
</style>
