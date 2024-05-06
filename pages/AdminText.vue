<template>
  <div class="admintext">
    <Header
      :isMain="isMain"
      style="z-index: 1000000 !important; position: absolute"
    />
    <div v-if="!loading" style="padding-top: 20vh; padding-left: 4vw">
      <div style="display: inline-block; width: 45vw">
        <v-textarea
          label="Телефон"
          filled
          style="width: 40vw"
          v-model="phone"
        ></v-textarea>
        <v-textarea
          label="Первый текст в блоке 'О нас'"
          filled
          style="width: 40vw"
          v-model="about_1"
        ></v-textarea>
        <v-textarea
          label="Второй текст в блоке 'О нас'"
          filled
          style="width: 40vw"
          v-model="about_2"
        ></v-textarea>
        <v-textarea
          label="Цитата в блоке 'О нас'"
          filled
          style="width: 40vw"
          v-model="about_3"
        ></v-textarea>
        <v-textarea
          label="Текст над картинкой в блоке 'О нас'"
          filled
          style="width: 40vw"
          v-model="about_4"
        ></v-textarea>
        <v-textarea
          label="Первый текст в блоке 'Обучение'"
          filled
          style="width: 40vw"
          v-model="education_1"
        ></v-textarea>
        <v-textarea
          label="Второй текст в блоке 'Обучение'"
          filled
          style="width: 40vw"
          v-model="education_2"
        ></v-textarea>
        <v-textarea
          label="Количество типов судов"
          filled
          style="width: 40vw"
          v-model="count_type"
        ></v-textarea>
        <v-textarea
          label="Количество сотрудников"
          filled
          style="width: 40vw"
          v-model="people_count"
        ></v-textarea>
        <v-textarea
          label="Текст для навигаций на страницу Судна"
          filled
          style="width: 40vw"
          v-model="nav_to_sudna"
        ></v-textarea>
      </div>
      <div style="display: inline-block; width: 30vw; vertical-align: top">
        <v-btn @click="changeData">Изменить данные</v-btn>
      </div>
    </div>

    <v-overlay :value="loading" :opacity="1" class="">
      <div style="width: 100vw; height: 100vh; padding-top: 40vh">
        <div class="my-loading d-flex flex-column justify-center align-center">
          <h1>Подтвердите свои данные</h1>
          <v-text-field
            label="Имя"
            v-model="name"
            hide-details
            style="
              background: rgba(255, 255, 255, 0.3) !important;
              border: 0.292639px solid #7c7c7c !important;
              box-sizing: border-box;
              backdrop-filter: blur(5.85278px) !important;
              margin-top: 30px;
              padding-left: 10px;
            "
          >
          </v-text-field>
          <v-text-field
            label="Пароль"
            v-model="password"
            hide-details
            type="password"
            style="
              background: rgba(255, 255, 255, 0.3) !important;
              border: 0.292639px solid #7c7c7c !important;
              box-sizing: border-box;
              backdrop-filter: blur(5.85278px) !important;
              margin-top: 30px;
              padding-left: 10px;
            "
          >
          </v-text-field>

          <v-btn color="success" @click="submitAcc" style="margin-top: 5vh"
            >Подтвердите</v-btn
          >
        </div>
      </div>
    </v-overlay>
  </div>
</template>

<script>
import Header from "@/components/Header";
export default {
  name: "AdminText",
  components: {
    Header,
  },
  data() {
    return {
      isMain: false,
      loading: true,
      name: "",
      password: "",
      vacancies: [],
      limit: 1,
      phone: "",
      about_1: "",
      about_2: "",
      about_3: "",
      about_4: "",
      education_1: "",
      education_2: "",
      count_type: "",
      people_count: "",
      nav_to_sudna: "",
    };
  },
  methods: {
    send() {
      let name = this.name;
      let phone = this.phone;
      let example = this.example;
      if (example.length > 0) {
        this.$axios
          .post(
            `https://crewing.kz/send?name=${name}&phone=${phone}&example=${example}`
          )
          .then((res) => {
            console.log(res);
            if (res) {
              this.popup = false;
              this.name = "";
              this.phone = "";
              this.example = "";
              alert("Отправлено");
            }
          });
      } else {
        this.$axios
          .post(`https://crewing.kz/send?name=${name}&phone=${phone}`)
          .then((res) => {
            console.log(res);
            if (res) {
              this.popup = false;
              this.name = "";
              this.phone = "";
              this.example = "";
              alert("Отправлено");
            }
          });
      }
    },
    getVac() {
      this.$axios.get("https://crewing.kz/crewings").then((res) => {
        this.vacancies = res.data;
        // this.vacancies.splice(1, 8);
        console.log(this.vacancies);
      });
    },
    submitAcc() {
      if (this.name == "admin" && this.password == "something") {
        this.loading = false;
        alert("Вы успешно подтвердили свою личность");
      } else {
        alert("Неправильно введены данные");
      }
    },
    getData() {
      this.$axios.get("https://crewing.kz/crewingData").then((res) => {
        // this.vacancies.splice(1, 8);
        console.log(res.data[0]);
        this.phone = res.data[0].phone;
        this.about_1 = res.data[0].about_1;
        this.about_2 = res.data[0].about_2;
        this.about_3 = res.data[0].about_3;
        this.about_4 = res.data[0].about_4;
        this.education_1 = res.data[0].education_1;
        this.education_2 = res.data[0].education_2;
        this.count_type = res.data[0].count_type;
        this.people_count = res.data[0].people_count;
        this.nav_to_sudna = res.data[0].nav_to_sudna;
      });
    },
    changeData() {
      let obj = {
        phone: this.phone,
        about_1: this.about_1,
        about_2: this.about_2,
        about_3: this.about_3,
        about_4: this.about_4,
        education_1: this.education_1,
        education_2: this.education_2,
        count_type: this.count_type,
        people_count: this.people_count,
        nav_to_sudna: this.nav_to_sudna,
      };
      this.$axios.patch("https://crewing.kz/crewingData", obj).then((res) => {
        // this.vacancies.splice(1, 8);
        console.log(res);
      });
      alert("Изменен текст");
    },
  },
  created() {
    this.getVac();
    this.getData();
  },
};
</script>

<style lang="scss" scoped>
@keyframes leftRight {
  0% {
    left: 0px;
  }
  50% {
    left: 10vw;
  }
  100% {
    left: 0px;
  }
}
@media screen and (min-width: 490px) {
  .home_mobile,
  .about_mobile,
  .education_mobile,
  .vac_mobile,
  .cert_mobile,
  .count_mobile,
  .feedback_mobile {
    display: none;
  }
  .about {
    background: linear-gradient(264.1deg, #063661 0%, #0773d3 99.34%);
    width: 100vw;
    z-index: 1;
    height: 35vw;
    padding-top: 55px;
    top: -10px;
    position: relative;
    font-family: "Montserrat", sans-serif !important;
    .about_1 {
      font-family: "Montserrat", sans-serif !important;
      position: absolute;
      top: 2%;
      right: -8vw;
      z-index: 4;
    }
    .about_info {
      margin-left: 51vw;
      font-family: "Montserrat", sans-serif !important;
      margin-top: 50px;
      .about_div {
        width: 95px;
        height: 4px;
        font-family: "Montserrat", sans-serif !important;
        background: #01dffd;
      }
      h1 {
        font-style: normal;
        font-weight: bold;
        font-family: "Montserrat", sans-serif !important;
        font-size: 5.19vw; //72px;
        line-height: 6.15vw; //88px;
        letter-spacing: -0.02em;
        color: #ffffff;
        margin: 0;
      }
      h2 {
        font-style: normal;
        font-family: "Montserrat", sans-serif !important;
        font-weight: bold;
        font-size: 2vw; //30px;
        line-height: 2.592vw; //37px;
        letter-spacing: -0.02em;
        color: #32a3b2;
      }
    }
    .about_text {
      background: #ffffff;
      font-family: "Montserrat", sans-serif !important;
      box-shadow: 4px 8px 10px rgba(0, 0, 0, 0.5);
      border-radius: 20px;
      width: 85vw;
      margin-left: 7.5vw;
      margin-top: 25px;
      z-index: 2;
      height: 25vw;
      position: relative;
      .about_text_1 {
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
        p {
          font-style: normal;
          font-weight: normal;
          font-family: "Montserrat", sans-serif !important;
          font-size: 1.1vw; //18px;
          line-height: 1.44vw; //21px;
          letter-spacing: -0.02em;
          width: 80%;
          margin-left: 2%;
          color: #c0c0c0;
        }
        img {
          width: 28vw; //388px;
          height: 35vw; //488px;
          object-fit: cover;
          font-family: "Montserrat", sans-serif !important;
          border-radius: 15px;
          border: 2px solid #ffffff;
        }
        strong {
          font-style: normal;
          font-family: "Montserrat", sans-serif !important;
          font-weight: bold;
          font-size: 1.73vw; //25px;
          line-height: 2.1vw; //30px;
          text-align: center;
          letter-spacing: -0.02em;
          color: #000000;
        }
        h2 {
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
      .about_text_2 {
        display: inline-block;
        font-family: "Montserrat", sans-serif !important;
        width: 55%;
        vertical-align: top;
        margin: 36px 0 46px 0;
        p {
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
  .education {
    width: 100vw;
    font-family: "Montserrat", sans-serif !important;
    padding-top: 5vw;
    .education_info_img {
      img {
        width: 100%;
        position: relative;
        height: auto;
        top: -180px;
        margin-left: 40%;
      }
      position: absolute;
    }
    .education_info {
      display: inline-block;
      width: 74vw;
      font-family: "Montserrat", sans-serif !important;
      vertical-align: top;
      padding: 6% 0 0 8vw;
      position: relative;
      background: linear-gradient(264.1deg, #063661 0%, #078fd3 99.34%);
      height: 50vw;
      h1 {
        font-style: normal;
        font-weight: bold;
        font-size: 4.8vw; //72px;
        font-family: "Montserrat", sans-serif !important;
        line-height: 6.4vw; //88px;
        letter-spacing: -0.02em;
        color: #ffffff;
        margin-top: 1%;
      }
      button {
        border-bottom-left-radius: 0px;
        border-bottom-right-radius: 20px;
        border-top-left-radius: 20px;
        border-top-right-radius: 0px;
        font-size: 0.9vw;
        font-style: normal;
        line-height: 15px;
        text-align: center;
        color: #ffffff;
        width: 17vw;
        height: 2.5vw;
      }
      .education_info_text {
        background: #ffffff;
        font-family: "Montserrat", sans-serif !important;
        box-shadow: 4px 8px 10px rgba(0, 0, 0, 0.5);
        border-radius: 20px;
        width: 68%;
        padding: 3%;
        margin-top: 3%;
        position: relative;
        p {
          font-style: normal;
          font-weight: normal;
          font-family: "Montserrat", sans-serif !important;
          font-size: 1.26vw; //20px;
          line-height: 1.78vw; //27px;

          color: #000000;
        }
      }
    }
    img {
      display: inline-block;
      width: 25.6vw;
      height: 50vw;
    }
  }
  .work {
    width: 100vw;
    font-family: "Montserrat", sans-serif !important;
    padding-top: 5vw;
    padding-left: 8vw;
    h1 {
      font-style: normal;
      font-weight: bold;
      font-family: "Montserrat", sans-serif !important;
      font-size: 4.89vw; //72px;
      line-height: 6.4vw; //88px;
      letter-spacing: -0.02em;
      color: #1a1a1a;
    }
    .work_item {
      background: #ffffff;
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
      h2,
      h3 {
        font-style: normal;
        font-weight: bold;
        font-family: "Montserrat", sans-serif !important;
        font-size: 1.91vw; //26px;
        line-height: 2.2vw; //30px;
        letter-spacing: -0.02em;
        color: #000000;
      }
      h3 {
        color: grey;
      }
    }
  }
  .cert {
    width: 100vw;
    font-family: "Montserrat", sans-serif !important;
    padding-top: 5vw;
    padding-left: 8vw;
    position: relative;
    h1 {
      font-style: normal;
      font-weight: bold;
      font-family: "Montserrat", sans-serif !important;
      font-size: 4.89vw; //72px;
      line-height: 6.4vw; //88px;
      letter-spacing: -0.02em;
      color: #1a1a1a;
    }
    .cert_1 {
      position: absolute;
      left: 0%;
      font-family: "Montserrat", sans-serif !important;
      top: 60%;
    }
    .cert_2 {
      position: absolute;
      left: 2%;
      font-family: "Montserrat", sans-serif !important;
      top: 60%;
    }
    .cert_3 {
      position: absolute;
      right: 0%;
      top: 0%;
      font-family: "Montserrat", sans-serif !important;
    }
    .cert_img {
      margin-top: 5vw;
      font-family: "Montserrat", sans-serif !important;
      height: 30vw;
      div {
        position: relative;
        width: 22%;
        display: inline-block;
        height: 30vw;
      }
      img {
        width: 90%;
        margin: 10% 5%;
        cursor: pointer;
        transition: 0.5s all ease-in;
      }
      img:hover {
        width: 100%;
        margin: 0%;
      }
    }
    .cert_img_upd {
      position: absolute;
      transform: rotateY(90deg);
    }
  }
  .sudna {
    width: 100vw;
    font-family: "Montserrat", sans-serif !important;
    padding-top: 5vw;
    padding-left: 8vw;
    padding-bottom: 5vw;
    h1 {
      font-style: normal;
      font-weight: bold;
      font-family: "Montserrat", sans-serif !important;
      font-size: 4.89vw; //72px;
      line-height: 6.4vw; //88px;
      letter-spacing: -0.02em;
      color: #1a1a1a;
    }
    .sudna_item {
      display: inline-block;
      margin-right: 1vw;
      font-family: "Montserrat", sans-serif !important;
      height: 300px;
      p {
        font-style: normal;
        font-family: "Montserrat", sans-serif !important;
        font-weight: bold;
        font-size: 1.06vw; //20px;
        text-align: center;
        letter-spacing: -0.02em;
        color: #ffffff;
        margin: 0;
        padding-top: 1vw;
      }
      div {
        background: linear-gradient(264.1deg, #063661 0%, #0773d3 99.34%);
        border-bottom-left-radius: 15px;
        border-bottom-right-radius: 15px;
        font-family: "Montserrat", sans-serif !important;
        margin: 0;
        position: relative;
        top: -10px;
        height: 5vw;
      }
      img {
        object-fit: contain;
        width: 100%;
        border-radius: 15px 15px 0px 0px;
      }
    }
  }
  .count {
    width: 100vw;
    font-family: "Montserrat", sans-serif !important;
    padding-top: 5vw;
    padding-bottom: 5vw;
    margin-bottom: 5vw;
    position: relative;
    h1 {
      font-style: normal;
      font-weight: bold;
      font-size: 4.89vw; //72px;
      line-height: 6.4vw; //88px;
      letter-spacing: -0.02em;
      color: #ffffff;
      position: absolute;
      top: 20px;
      font-family: "Montserrat", sans-serif !important;
      z-index: 100;
      margin-left: 8vw;
    }
    .count_numb {
      background: linear-gradient(264.1deg, #063661 0%, #0773d3 99.34%);
      font-family: "Montserrat", sans-serif !important;
      width: 100vw;
      position: relative;
      top: 60px;
      .count_numb_1,
      .count_numb_2 {
        font-weight: bold;
        font-size: 229.661px;
        line-height: 280px;
        font-family: "Montserrat", sans-serif !important;
        text-align: center;
        letter-spacing: -0.02em;
        display: inline-block;
        color: #ffffff;
      }
      .count_numb_1 {
        margin-left: 28vw;
      }
      .count_numb_2 {
        margin-left: 16vw;
      }
    }
    .count_text {
      background: white;
      width: 100vw;
      height: 150px;
      position: relative;
      font-family: "Montserrat", sans-serif !important;
      top: 40px;
      padding-top: 50px;
      .count_text_1,
      .count_text_2 {
        font-style: normal;
        font-weight: normal;
        font-size: 26px;
        line-height: 31px;
        font-family: "Montserrat", sans-serif !important;
        text-align: center;
        letter-spacing: -0.02em;

        color: #000000;
      }
      .count_text_1 {
        margin-left: 27vw;
      }
      .count_text_2 {
        margin-left: 15vw;
      }
    }
    .count_know {
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
  .feedback {
    width: 100vw;
    height: 40vw;
    font-family: "Montserrat", sans-serif !important;
    background: url("../assets/shtur.png") no-repeat;
    background-color: rgba(19, 19, 19, 0.8);
    background-size: cover;
    font-family: "Montserrat", sans-serif !important;
    position: relative;
    .feedback_form {
      font-family: "Montserrat", sans-serif !important;
      width: 24vw;
      padding-top: 10vw;
      margin-left: 8vw;
      margin-bottom: 5vw;
    }
    h2 {
      font-style: normal;
      font-weight: bold;
      font-family: "Montserrat", sans-serif !important;
      font-size: 2.49vw; //34px;
      line-height: 2.9vw; //40px;
      letter-spacing: -0.02em;
      width: 50%;
      color: #ffffff;
    }
  }
  .vac {
    width: 100vw;
    font-family: "Montserrat", sans-serif !important;
    padding-top: 5vw;
    padding-left: 8vw;
    padding-bottom: 5vw;
    position: relative;
    h1 {
      font-style: normal;
      font-weight: bold;
      font-family: "Montserrat", sans-serif !important;
      font-size: 4.89vw; //72px;
      line-height: 6.4vw; //88px;
      letter-spacing: -0.02em;
      color: #1a1a1a;
    }
    .vac_1 {
      position: absolute;
      display: inline-block;
      top: -5%;
      left: 46%;
    }
    .vac_2 {
      position: absolute;
      display: inline-block;
      top: 52%;
      right: 0%;
    }
    .vac_3 {
      position: absolute;
      display: inline-block;
      top: 32%;
      left: 0%;
    }
  }
  .vac_list_item {
    position: relative;
    font-family: "Montserrat", sans-serif !important;
    margin-top: 44px;
    width: 100%;

    .vac_list_item_main {
      display: inline-block;
      width: 50%;
      font-family: "Montserrat", sans-serif !important;
      vertical-align: top;
      background: #ffffff;
      border: 0.5px solid #848484;
      box-sizing: border-box;
      box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25);
      border-radius: 15px;
      padding: 36px 2% 36px 2%;
      h1,
      h2 {
        font-style: normal;
        font-weight: bold;
        font-size: 1.81vw; //26px;
        line-height: 2vw; //30px;
        letter-spacing: -0.02em;
        color: #000000;
        font-family: "Montserrat", sans-serif !important;
        margin: 0;
      }
      h2 {
        font-size: 1.71vw;
        color: grey;
      }
      p {
        font-style: normal;
        font-weight: normal;
        font-size: 1.22vw; //18px;
        line-height: 1.62vw; //25px;
        margin-top: 24px;
        font-family: "Montserrat", sans-serif !important;
        color: #000000;
        width: 70%;
      }
      button {
        margin-top: 00px;
        height: 47px;
        margin-left: 70%;
        font-family: "Montserrat", sans-serif !important;
        width: 30%;
        font-size: 0.8vw;
      }
    }

    .vac_list_item_dop {
      display: inline-block;
      width: 23%;
      background: #ffffff;
      border: 0.5px solid #848484;
      box-sizing: border-box;
      font-family: "Montserrat", sans-serif !important;
      box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25);
      border-radius: 15px;
      margin-top: 10px;
      padding: 35px 5% 35px 3%;
      p {
        margin: 0;
        font-family: "Montserrat", sans-serif !important;
      }
      .vac_list_item_dop_1,
      .vac_list_item_dop_2 {
        font-style: normal;
        font-weight: bold;
        font-family: "Montserrat", sans-serif !important;
        font-size: 1.02vw; //14.2963px;
        line-height: 1.18vw; //17px;
        margin: 12px 0;
        color: #000000;
      }
      .vac_list_item_dop_2 {
        font-weight: 300;
        font-family: "Montserrat", sans-serif !important;
      }
    }
  }
  .home img {
    position: absolute;
    z-index: 5;
    width: 60vw;
    top: 10vw;
    left: 19vw;
    opacity: 0.8;
  }
  .home {
    position: relative;
    font-family: "Montserrat", sans-serif !important;
  }
  .home p,
  .home a {
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
  .home .home_1 {
    left: 45.3vw;
    top: 10vw;
  }
  .home .home_2 {
    left: 54.2vw;
    top: 13.6vw;
  }
  .home_3 {
    left: 58.2vw;
    top: 23.1vw;
  }
  .home .home_4 {
    left: 54.1vw;
    top: 32.2vw;
  }
  .home .home_5 {
    left: 45.3vw;
    top: 35.7vw;
  }
  .home .home_6 {
    left: 36.2vw;
    top: 13.7vw;
  }
  .home .home_7 {
    left: 32.3vw;
    top: 23vw;
  }
  .home .home_8 {
    left: 36.2vw;
    top: 32.2vw;
  }
}

@media screen and (max-width: 490px) {
  .main_page {
    position: relative;
  }
  .home,
  .about,
  .education,
  .vac,
  .cert,
  .count,
  .feedback {
    display: none;
  }
  .home_mobile {
    width: 100vw;
    background-repeat: no-repeat;
    background-image: url("../assets/mobile_background_home.png");
    background-color: rgba(19, 19, 19, 0.8) !important;
    background-size: 100% 100%;
    position: relative;
    height: 79vh;
    padding-top: 93px;
    &:after {
      content: "";
      position: absolute;
      left: 0;
      right: 0;
      top: 0;
      bottom: 0;
      height: calc(79vh);
      background-color: rgba(19, 19, 19, 0.8);
      z-index: 1;
    }
    p {
      font-style: normal;
      font-weight: bold;
      font-size: 8.5vw;
      line-height: 10vw;
      text-align: center;
      width: 90vw;
      margin-left: 5vw;
      margin-top: 20vw;
      letter-spacing: -0.02em;
      color: #ffffff;
      position: relative;
      z-index: 2;
      font-family: "Montserrat", sans-serif;
    }
    button {
      width: 50vw;
      margin-left: 25vw;
      font-size: 3.4vw;
      line-height: 4.2vw;
      margin-top: 5vw;
      position: relative;
      z-index: 2;
      font-family: "Montserrat", sans-serif;
    }
    .home_mobile_down {
      display: block;
      margin-top: 17vw;
      margin-left: 45vw;
      position: relative;
      z-index: 3;
    }
    .home_mobile_wave {
      position: absolute;
      bottom: 0px;
      z-index: 2;
      width: 100vw;
    }
  }
  .about_mobile {
    width: 100vw;
    position: relative;
    background: #f1f1f1;
    height: 155vw;
    p {
      display: inline-block;
      font-style: normal;
      font-weight: bold;
      font-size: 8.5vw;
      line-height: 10vw;
      letter-spacing: -0.02em;
      color: #000000;
      margin-left: 5vw;
      margin-top: 24px;
      font-family: "Montserrat", sans-serif;
    }
    img {
      display: inline-block;
      width: 47vw;
      position: absolute;
      right: -5vw;
      top: -60px;
      transform: rotate(-41.9deg);
    }
    .about_mobile_info {
      width: 90vw;
      margin-left: 5vw;
      background: #ffffff;
      border-radius: 0px 0px 10px 10px;
      margin-top: 4px;
      margin-bottom: 29px;
      font-family: "Montserrat", sans-serif;
      img {
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
      p {
        font-style: normal;
        font-weight: normal;
        font-size: 3.2vw;
        line-height: 4.2vw;
        margin-left: 4.5vw;
        margin-right: 8vw;
        font-family: "Montserrat", sans-serif;
        color: #000000;
      }
    }
  }
  .education {
    width: 100vw;
    font-family: "Montserrat", sans-serif !important;
    padding-top: 5vw;
    .education_info_img {
      img {
        width: 100%;
        position: relative;
        height: auto;
        top: -180px;
        margin-left: 40%;
      }
      position: absolute;
    }
    .education_info {
      display: inline-block;
      width: 74vw;
      font-family: "Montserrat", sans-serif !important;
      vertical-align: top;
      padding: 6% 0 0 8vw;
      position: relative;
      background: linear-gradient(264.1deg, #063661 0%, #078fd3 99.34%);
      height: 50vw;
      h1 {
        font-style: normal;
        font-weight: bold;
        font-size: 4.8vw; //72px;
        font-family: "Montserrat", sans-serif !important;
        line-height: 6.4vw; //88px;
        letter-spacing: -0.02em;
        color: #ffffff;
        margin-top: 1%;
      }
      button {
        border-bottom-left-radius: 0px;
        border-bottom-right-radius: 20px;
        border-top-left-radius: 20px;
        border-top-right-radius: 0px;
        font-size: 0.9vw;
        font-style: normal;
        line-height: 15px;
        text-align: center;
        color: #ffffff;
        width: 17vw;
        height: 2.5vw;
      }
      .education_info_text {
        background: #ffffff;
        font-family: "Montserrat", sans-serif !important;
        box-shadow: 4px 8px 10px rgba(0, 0, 0, 0.5);
        border-radius: 20px;
        width: 68%;
        padding: 3%;
        margin-top: 3%;
        position: relative;
        p {
          font-style: normal;
          font-weight: normal;
          font-family: "Montserrat", sans-serif !important;
          font-size: 1.26vw; //20px;
          line-height: 1.78vw; //27px;

          color: #000000;
        }
      }
    }
    img {
      display: inline-block;
      width: 26vw;
      height: 50vw;
    }
  }
  .education_mobile {
    display: block;
    background-color: white;
    position: relative;
    padding-left: 5vw;
    width: 105vw;
    h1 {
      font-style: normal;
      font-weight: bold;
      font-size: 8.5vw;
      line-height: 10vw;
      letter-spacing: -0.02em;
      color: #000000;
      font-family: "Montserrat", sans-serif;
    }
    .education_mobile_img {
      width: 46vw;
      position: absolute;
      right: 5vw;
      top: 0;
    }
    .education_mobile_info {
      margin-top: 27px;
      background: #f1f1f1;
      border-radius: 10px;
      height: 105vw;
      font-family: "Montserrat", sans-serif;
      .education_mobile_info_1 {
        width: 45vw;
        display: inline-block;
        padding: 14px 20px 20px 13px;
        vertical-align: top;
        p {
          font-weight: normal;
          font-size: 3.2vw;
          line-height: 4.2vw;
          color: #000000;
          font-family: "Montserrat", sans-serif;
        }
      }
      .education_mobile_info_2 {
        display: inline-block;
        width: 45vw;
        img {
          object-fit: cover;
          height: 105vw;
          width: 100%;
          border-top-right-radius: 10px;
          border-bottom-right-radius: 10px;
        }
      }
    }
  }
  .work {
    width: 100vw;
    font-family: "Montserrat", sans-serif !important;
    padding-top: 5vw;
    padding-left: 8vw;
    h1 {
      font-style: normal;
      font-weight: bold;
      font-family: "Montserrat", sans-serif !important;
      font-size: 4.89vw; //72px;
      line-height: 6.4vw; //88px;
      letter-spacing: -0.02em;
      color: #1a1a1a;
    }
    .work_item {
      background: #ffffff;
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
      h2,
      h3 {
        font-style: normal;
        font-weight: bold;
        font-family: "Montserrat", sans-serif !important;
        font-size: 1.91vw; //26px;
        line-height: 2.2vw; //30px;
        letter-spacing: -0.02em;
        color: #000000;
      }
      h3 {
        color: grey;
      }
    }
  }
  .cert {
    width: 100vw;
    font-family: "Montserrat", sans-serif !important;
    padding-top: 5vw;
    padding-left: 8vw;
    position: relative;
    h1 {
      font-style: normal;
      font-weight: bold;
      font-family: "Montserrat", sans-serif !important;
      font-size: 4.89vw; //72px;
      line-height: 6.4vw; //88px;
      letter-spacing: -0.02em;
      color: #1a1a1a;
    }
    .cert_1 {
      position: absolute;
      left: 0%;
      font-family: "Montserrat", sans-serif !important;
      top: 60%;
    }
    .cert_2 {
      position: absolute;
      left: 2%;
      font-family: "Montserrat", sans-serif !important;
      top: 60%;
    }
    .cert_3 {
      position: absolute;
      right: 0%;
      top: 0%;
      font-family: "Montserrat", sans-serif !important;
    }
    .cert_img {
      margin-top: 5vw;
      font-family: "Montserrat", sans-serif !important;
      height: 30vw;
      div {
        position: relative;
        width: 22%;
        display: inline-block;
        height: 30vw;
      }
      img {
        width: 90%;
        margin: 10% 5%;
        cursor: pointer;
        transition: 0.5s all ease-in;
      }
      img:hover {
        width: 100%;
        margin: 0%;
      }
    }
    .cert_img_upd {
      position: absolute;
      transform: rotateY(90deg);
    }
  }
  .cert_mobile_right p {
    -webkit-animation: leftRight 2s infinite ease;
    -moz-animation: leftRight 2s infinite ease;
    -ms-animation: leftRight 2s infinite ease;
    -o-animation: leftRight 2s infinite ease;
    animation: leftRight 2s infinite ease;
    font-family: "Montserrat", sans-serif;
  }
  .cert_mobile_right img {
    width: 15vw;
  }
  ::-webkit-scrollbar-thumb {
    background: #dadada;
    border-radius: 20px;
  }
  .cert_mobile {
    display: block;
    padding-left: 5vw;
    width: 95vw;
    position: relative;
    margin-top: 10vw;
    h1 {
      font-style: normal;
      font-weight: bold;
      font-size: 8.5vw;
      line-height: 10vw;
      letter-spacing: -0.02em;
      color: #000000;
      font-family: "Montserrat", sans-serif;
    }
    .cert_mobile_img {
      animation: scrollLeft 0.5s ease;
    }
    .cert_img {
      overflow-x: scroll;
      position: relative;
      overflow-y: hidden;
      width: 95vw;
      height: 110vw;
      margin-top: 36px;
      font-family: "Montserrat", sans-serif;
      white-space: nowrap;
      div {
        width: 70vw;
        display: inline-block;
        margin-right: 8vw;
        img {
          width: 100%;
          transition: 0.5s all ease-in;
        }
        .cert_img_upd {
          width: 70vw;
          position: absolute;
          transform: rotateY(90deg);
        }
      }
    }
  }
  .sudna {
    width: 100vw;
    font-family: "Montserrat", sans-serif !important;
    padding-top: 5vw;
    padding-left: 8vw;
    padding-bottom: 5vw;
    h1 {
      font-style: normal;
      font-weight: bold;
      font-family: "Montserrat", sans-serif !important;
      font-size: 4.89vw; //72px;
      line-height: 6.4vw; //88px;
      letter-spacing: -0.02em;
      color: #1a1a1a;
    }
    .sudna_item {
      display: inline-block;
      margin-right: 1vw;
      font-family: "Montserrat", sans-serif !important;
      height: 300px;
      p {
        font-style: normal;
        font-family: "Montserrat", sans-serif !important;
        font-weight: bold;
        font-size: 1.06vw; //20px;
        text-align: center;
        letter-spacing: -0.02em;
        color: #ffffff;
        margin: 0;
        padding-top: 1vw;
      }
      div {
        background: linear-gradient(264.1deg, #063661 0%, #0773d3 99.34%);
        border-bottom-left-radius: 15px;
        border-bottom-right-radius: 15px;
        font-family: "Montserrat", sans-serif !important;
        margin: 0;
        position: relative;
        top: -10px;
        height: 5vw;
      }
      img {
        object-fit: contain;
        width: 100%;
        border-radius: 15px 15px 0px 0px;
      }
    }
  }
  .count {
    width: 100vw;
    font-family: "Montserrat", sans-serif !important;
    padding-top: 5vw;
    padding-bottom: 5vw;
    margin-bottom: 5vw;
    position: relative;
    h1 {
      font-style: normal;
      font-weight: bold;
      font-size: 4.89vw; //72px;
      line-height: 6.4vw; //88px;
      letter-spacing: -0.02em;
      color: #ffffff;
      position: absolute;
      top: 20px;
      font-family: "Montserrat", sans-serif !important;
      z-index: 100;
      margin-left: 8vw;
    }
    .count_numb {
      background: linear-gradient(264.1deg, #063661 0%, #0773d3 99.34%);
      font-family: "Montserrat", sans-serif !important;
      width: 100vw;
      position: relative;
      top: 60px;
      .count_numb_1,
      .count_numb_2 {
        font-weight: bold;
        font-size: 229.661px;
        line-height: 280px;
        font-family: "Montserrat", sans-serif !important;
        text-align: center;
        letter-spacing: -0.02em;
        display: inline-block;
        color: #ffffff;
      }
      .count_numb_1 {
        margin-left: 28vw;
      }
      .count_numb_2 {
        margin-left: 16vw;
      }
    }
    .count_text {
      background: white;
      width: 100vw;
      height: 150px;
      position: relative;
      font-family: "Montserrat", sans-serif !important;
      top: 40px;
      padding-top: 50px;
      .count_text_1,
      .count_text_2 {
        font-style: normal;
        font-weight: normal;
        font-size: 26px;
        line-height: 31px;
        font-family: "Montserrat", sans-serif !important;
        text-align: center;
        letter-spacing: -0.02em;

        color: #000000;
      }
      .count_text_1 {
        margin-left: 27vw;
      }
      .count_text_2 {
        margin-left: 15vw;
      }
    }
    .count_know {
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
  .count_mobile {
    display: block;
    margin-top: 50px;
    padding-left: 5vw;
    h1 {
      font-style: normal;
      font-weight: bold;
      font-size: 8.5vw;
      line-height: 10vw;
      letter-spacing: -0.02em;
      color: #000000;
      font-family: "Montserrat", sans-serif;
    }
    h2 {
      font-weight: bold;
      font-size: 6vw;
      line-height: 7.2vw;
      text-align: center;
      width: 85vw;
      position: relative;
      left: -5vw;
      margin-left: 5vw;
      color: #000000;
      font-family: "Montserrat", sans-serif;
      margin-top: 11vw;
    }
    span {
      font-weight: bold;
      font-size: 26vw;
      line-height: 22vw;
      text-align: center;
      letter-spacing: -0.02em;
      color: #0773d3;
      font-family: "Montserrat", sans-serif;
      vertical-align: top;
      margin-left: 5vw;
    }
    p {
      font-weight: 300;
      font-size: 5.8vw;
      font-family: "Montserrat", sans-serif;
      line-height: 7.2vw;
      text-align: center;
      letter-spacing: -0.02em;
      color: #000000;
    }
    .count_mobile_1 {
      display: inline-block;
      width: 38vw;
      vertical-align: top;
      font-family: "Montserrat", sans-serif;
      padding-top: 15vw;
      padding-left: 4vw;
    }
    .count_mobile_3 {
      display: inline-block;
      width: 55vw;
      font-family: "Montserrat", sans-serif;
    }
    .count_mobile_4 {
      width: 35vw;
      display: inline-block;
      font-family: "Montserrat", sans-serif;
    }
  }
  .feedback {
    width: 100vw;
    height: 40vw;
    font-family: "Montserrat", sans-serif !important;
    background: url("../assets/shtur.png") no-repeat;
    background-color: rgba(19, 19, 19, 0.8);
    background-size: cover;
    font-family: "Montserrat", sans-serif !important;
    position: relative;
    .feedback_form {
      font-family: "Montserrat", sans-serif !important;
      width: 24vw;
      padding-top: 10vw;
      margin-left: 8vw;
      margin-bottom: 5vw;
    }
    h2 {
      font-style: normal;
      font-weight: bold;
      font-family: "Montserrat", sans-serif !important;
      font-size: 2.49vw; //34px;
      line-height: 2.9vw; //40px;
      letter-spacing: -0.02em;
      width: 50%;
      color: #ffffff;
    }
  }
  .v-text-field .v-label {
    color: white;
  }
  .theme--light.v-text-field--solo > .v-input__control > .v-input__slot {
    background-color: transparent;
  }
  .v-input__slot {
    background-color: transparent;
  }
  .feedback_mobile {
    display: block;
    padding-left: 5vw;
    position: relative;
    padding-top: 36vw;
    background: url("../assets/shtur.png") no-repeat;
    background-color: rgba(19, 19, 19, 0.8);
    background-size: cover;
    padding-bottom: 18vw;
    font-family: "Montserrat", sans-serif;
    .feedback_mobile_wave {
      position: absolute;
      top: 0px;
      width: 100vw;
      left: 0px;
    }
    h1 {
      font-style: normal;
      font-weight: bold;
      font-size: 8.5vw;
      line-height: 10vw;
      font-family: "Montserrat", sans-serif;
      letter-spacing: -0.02em;
      color: #ffffff;
    }
    p {
      width: 55vw;
      font-weight: 300;
      font-size: 3.2vw;
      line-height: 4vw;
      letter-spacing: -0.02em;
      font-family: "Montserrat", sans-serif;
      color: darkgrey;
      margin: 0;
    }
  }
  .vac {
    width: 100vw;
    font-family: "Montserrat", sans-serif !important;
    padding-top: 5vw;
    padding-left: 8vw;
    padding-bottom: 5vw;
    position: relative;
    h1 {
      font-style: normal;
      font-weight: bold;
      font-family: "Montserrat", sans-serif !important;
      font-size: 4.89vw; //72px;
      line-height: 6.4vw; //88px;
      letter-spacing: -0.02em;
      color: #1a1a1a;
    }
    .vac_1 {
      position: absolute;
      display: inline-block;
      top: -5%;
      left: 46%;
    }
    .vac_2 {
      position: absolute;
      display: inline-block;
      top: 52%;
      right: 0%;
    }
    .vac_3 {
      position: absolute;
      display: inline-block;
      top: 32%;
      left: 0%;
    }
  }
  .vac_mobile {
    display: block;
    padding-left: 5vw;
    background-color: white;
    margin-top: 41px;
    position: relative;
    font-family: "Montserrat", sans-serif;
    margin-bottom: 30px;
    h1 {
      font-weight: bold;
      font-size: 8.5vw;
      line-height: 10vw;
      font-family: "Montserrat", sans-serif;
      letter-spacing: -0.02em;
      color: #000000;
    }
    .vac_mobile_1 {
      width: 41vw;
      position: absolute;
      font-family: "Montserrat", sans-serif;
      right: 0px;
      top: -20vw;
    }
    .vac_mobile_2 {
      width: 33vw;
      position: absolute;
      font-family: "Montserrat", sans-serif;
      left: -10vw;
      top: 36vw;
      z-index: 2;
    }
    .vac_mobile_3 {
      width: 29vw;
      font-family: "Montserrat", sans-serif;
      position: absolute;
      right: 0px;
      transform: rotate(-30deg);
      top: 100vw;
    }
    .vac_mobile_card {
      margin-bottom: 30px;
      .vac_mobile_card_name {
        z-index: 3;
        position: relative;
        width: 89vw;
        background: #ffffff;
        border: 0.248762px solid lightgrey;
        box-shadow: 0px 1.99009px 1.99009px rgba(0, 0, 0, 0.25);
        border-radius: 7.46285px;
        padding: 18px 28px 21px 19px;
        margin-top: 19px;
        height: max-content;
        h1 {
          font-style: normal;
          font-weight: bold;
          font-size: 4.8vw;
          line-height: 5.6vw;
          letter-spacing: -0.02em;
          color: #000000;
          span {
            color: rgb(7, 115, 211);
          }
        }
        p {
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
      .vac_mobile_card_line {
        background: #c4c4c4;
        width: 2px;
        height: 14px;
        margin-left: 44vw;
      }
      .vac_mobile_card_dop {
        z-index: 3;
        position: relative;
        background: #ffffff;
        border: 0.22546px solid lightgrey;
        box-sizing: border-box;
        box-shadow: 0px 1.80368px 1.80368px rgba(0, 0, 0, 0.25);
        border-radius: 6.7638px;
        width: 89vw;
        height: max-content;
        h2,
        p,
        span {
          font-style: normal;
          font-size: 3.2vw;
          line-height: 4vw;
          color: #000000;
          margin: 0;
        }
        p {
          font-weight: 300;
          margin-bottom: 20px;
        }
        .vac_mobile_card_dop_1 {
          display: inline-block;
          width: 50%;
          vertical-align: top;
          padding-left: 7vw;
          padding-top: 4vw;
          border-right: 2px solid #c4c4c4;
        }
        .vac_mobile_card_dop_2 {
          display: inline-block;
          width: 48%;
          vertical-align: top;
          padding-left: 3.2vw;
          padding-top: 3.2vw;
        }
        .vac_mobile_card_dop_price {
          width: 100%;
          text-align: center;
          border-top: 2px solid #c4c4c4;
          padding: 10px 0;
          span {
            font-weight: 300;
          }
        }
      }
    }
  }
  .vac_list_item {
    position: relative;
    font-family: "Montserrat", sans-serif !important;
    margin-top: 44px;
    width: 100%;

    .vac_list_item_main {
      display: inline-block;
      width: 50%;
      font-family: "Montserrat", sans-serif !important;
      vertical-align: top;
      background: #ffffff;
      border: 0.5px solid #848484;
      box-sizing: border-box;
      box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25);
      border-radius: 15px;
      padding: 36px 2% 36px 2%;
      h1,
      h2 {
        font-style: normal;
        font-weight: bold;
        font-size: 1.81vw; //26px;
        line-height: 2vw; //30px;
        letter-spacing: -0.02em;
        color: #000000;
        font-family: "Montserrat", sans-serif !important;
        margin: 0;
      }
      h2 {
        font-size: 1.71vw;
        color: grey;
      }
      p {
        font-style: normal;
        font-weight: normal;
        font-size: 1.22vw; //18px;
        line-height: 1.62vw; //25px;
        margin-top: 24px;
        font-family: "Montserrat", sans-serif !important;
        color: #000000;
        width: 70%;
      }
      button {
        margin-top: 00px;
        height: 47px;
        margin-left: 70%;
        font-family: "Montserrat", sans-serif !important;
        width: 30%;
        font-size: 0.8vw;
      }
    }

    .vac_list_item_dop {
      display: inline-block;
      width: 23%;
      background: #ffffff;
      border: 0.5px solid #848484;
      box-sizing: border-box;
      font-family: "Montserrat", sans-serif !important;
      box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25);
      border-radius: 15px;
      margin-top: 10px;
      padding: 35px 5% 35px 3%;
      p {
        margin: 0;
        font-family: "Montserrat", sans-serif !important;
      }
      .vac_list_item_dop_1,
      .vac_list_item_dop_2 {
        font-style: normal;
        font-weight: bold;
        font-family: "Montserrat", sans-serif !important;
        font-size: 1.02vw; //14.2963px;
        line-height: 1.18vw; //17px;
        margin: 12px 0;
        color: #000000;
      }
      .vac_list_item_dop_2 {
        font-weight: 300;
        font-family: "Montserrat", sans-serif !important;
      }
    }
  }
}
@keyframes scrollLeft {
  0% {
    transform: rotate(0deg);
  }
  33% {
    transform: rotate(-15deg);
  }
  66% {
    transform: rotate(15deg);
  }
  100% {
    transform: rotate(0deg);
  }
}
.home_main_img {
  animation: scrollLeft 2s ease-in;
}
</style>
