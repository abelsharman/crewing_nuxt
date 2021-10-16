<template>
    <div class="sudy">
        <Header :isMain="isMain" v-if="!loading" />
        <Loading :loading="loading"/>
        <!-- <div class="sudy_list">
            <h1 style="font-weight: 900 !important">Виды судов.</h1>
            <div>
                <img src="../assets/kar4.png" alt="">
                <div style="background: #C4C4C4;height:3px;width:8vw;display:inline-block;position:relative;top:-20px;"></div>
                <p>Сухогрузы</p>
            </div>
            <div>
                <p style="border-radius: 0px 20px;">Плавучие гостиницы</p>
                <div style="background: #C4C4C4;height:3px;width:8vw;display:inline-block;position:relative;top:-20px;"></div>
                <img src="../assets/kar2.png" alt="">
            </div>
            <div>
                <img src="../assets/kar1.png" alt="">
                <div style="background: #C4C4C4;height:3px;width:8vw;display:inline-block;position:relative;top:-20px;"></div>
                <p>Танкера</p>
            </div>
            <div>
                <p style="border-radius: 0px 20px;">Специализированный флот</p>
                <div style="background: #C4C4C4;height:3px;width:8vw;display:inline-block;position:relative;top:-20px;"></div>
                <img src="../assets/kar3.png" alt="">
            </div>
        </div> -->

        <div class="sudy_list_mobile">
            <h1>Виды судов.</h1>

            <div class="sudy_list_mobile_item">
                <div class="sudy_list_mobile_item_left">
                    <img src="../assets/loading.png" alt="">
                </div>

                <div class="sudy_list_mobile_item_img">
                    <img src="../assets/kar13.png" alt="">
                </div>
                <p class="sudy_list_mobile_p_1">Сухогрузы</p>
            </div>


            <div class="sudy_list_mobile_item">
                <div class="sudy_list_mobile_item_right">
                    <img src="../assets/loading.png" alt="">
                </div>

                <div class="sudy_list_mobile_item_img">
                    <img src="../assets/kar23.png" alt="">
                </div>
                <p class="sudy_list_mobile_p_2">Танкера</p>
            </div>



            <div class="sudy_list_mobile_item">
                <div class="sudy_list_mobile_item_left">
                    <img src="../assets/loading.png" alt="">
                </div>

                <div class="sudy_list_mobile_item_img">
                    <img src="../assets/kar33.png" alt="">
                </div>
                <p class="sudy_list_mobile_p_1">Буксиры</p>
            </div>




            <div class="sudy_list_mobile_item">
                <div class="sudy_list_mobile_item_right">
                    <img src="../assets/loading.png" alt="">
                </div>

                <div class="sudy_list_mobile_item_img">
                    <img src="../assets/kar43.png" alt="">
                </div>
                <p class="sudy_list_mobile_p_2">Специализированный флот</p>
            </div>



            <div class="sudy_list_mobile_item">
                <div class="sudy_list_mobile_item_left">
                    <img src="../assets/loading.png" alt="">
                </div>

                <div class="sudy_list_mobile_item_img">
                    <img src="../assets/kar53.png" alt="">
                </div>
                <p class="sudy_list_mobile_p_1">Плавучие гостиницы</p>
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
                <template v-slot:label style="color: white;border:0px;position:absolute;top:4px;">
                    <div style="color: white;border:0px;position:relative;top:-4px;">
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
                    <div style="color: white;border:0px;position:relative;top:-4px;">
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
    <Footer />
    </div>
</template>


<script>
import Loading from '@/pages/Loading.vue'
import Header from '@/components/Header.vue'
import Footer from '@/components/Footer.vue'

export default {
    name: 'Sudy',
    data(){
        return{
            loading: true,
            isMain: false,
            name: '',
            phone: '',
        }
    },
    components: {
        Loading, 
        Header,
        Footer
    },
    methods: {
        send(){
            let name = this.name
            let phone = this.phone
            this.$axios.post(`https://periodicals.abelsharman.kz/send?name=${name}&phone=${phone}`)
            .then((res)=>{
                console.log(res)
                if(res){
                this.popup = false
                this.name = ''
                this.phone = ''
                alert("Отправлено")
                }
            })
        },
    },
    created(){
        setTimeout(()=>{
            this.loading = false
        }, 2500)
  } ,
}
</script>



<style lang="scss" scoped>
@media screen and (max-width: 490px) {
    .feedback, .sudy_list{
        display: none;
    }
    .feedback_mobile{
        display: block;
        padding-left: 5vw;
        padding-top: 36vw;
        margin-top: 10vw;
        background: url("../assets/shtur.png") no-repeat;
        background-color: rgba(19, 19, 19, 0.8);
        background-size: cover;
        padding-bottom: 18vw;
        position: relative;
        font-family: "Montserrat", sans-serif;
        h1{
        font-style: normal;
        font-weight: bold;
        font-size: 8.5vw;
        line-height: 10vw;
        letter-spacing: -0.02em;
        font-family: "Montserrat", sans-serif;
        color: #FFFFFF;
        }
        p{
        width: 55vw;
        font-family: "Montserrat", sans-serif;
        font-weight: 300;
        font-size: 3.2vw;
        line-height: 4vw;
        letter-spacing: -0.02em;
        color: #828282;
        margin: 0;
        }
        .feedback_mobile_wave{
            position: absolute;
            top: 0px;
            width: 100vw;
            font-family: "Montserrat", sans-serif;
            left: 0px;
        }
    }

    .sudy_list_mobile{
        display: block;
        padding-top: 103px;
        padding-left: 5vw;
        h1{
            font-weight: bold;
            font-size: 8.5vw;
            line-height: 10vw;
            letter-spacing: -0.02em;
            font-family: "Montserrat", sans-serif;
            color: #000000;
        }
        .sudy_list_mobile_item{
            filter: drop-shadow(4px 8px 10px rgba(0, 0, 0, 0.5));
            border-radius: 20px;
            position: relative;
            width: 89vw;
            margin-top: 6vw;
            margin-bottom: 6vw;
            height: 29vw;
            .sudy_list_mobile_item_img{
                border-radius: 20px;
                img{
                    width: 92.8vw;
                    border-radius: 20px;
                    height: 32.6vw;
                    object-fit: cover;
                }
            }
            .sudy_list_mobile_item_left{
                background: linear-gradient(264.1deg, #063661 0%, #078FD3 99.34%);
                border-radius: 20px 0px 0px 20px;
                position: absolute;
                left: 0px;
                top: 0px;
                height: 28.8vw;
                width: 12vw;
                img{
                    width: 8.5vw;
                    margin-top: 10vw;
                    margin-left: 1.6vw;
                }
            }
            .sudy_list_mobile_item_right{
                background: linear-gradient(264.1deg, #063661 0%, #078FD3 99.34%);
                border-radius: 0px 20px 20px 0px;
                position: absolute;
                right: 0px;
                top: 0px;
                height: 28.8vw;
                width: 12vw;
                img{
                    width: 8.5vw;
                    margin-top: 10vw;
                    margin-left: 1.6vw;
                }
            }
            .sudy_list_mobile_p_1{
                font-style: 300;
                font-weight: normal;
                font-size: 3.2vw;
                line-height: 6.2vw;
                text-align: center;
                color: #FFFFFF;
                width: max-content;
                position: absolute;
                bottom: 0px;
                font-family: "Montserrat", sans-serif;
                right: 0px;
                margin: 0;
                padding: 0 4vw;
                background: #0773D3;
                border-radius: 20px 0px;
            }
            .sudy_list_mobile_p_2{
                top: 0px;
                left: 1.5vw;
                font-style: 300;
                font-weight: normal;
                font-size: 3.2vw;
                line-height: 6.2vw;
                font-family: "Montserrat", sans-serif;
                text-align: center;
                color: #FFFFFF;
                width: max-content;
                position: absolute;
                margin: 0;
                padding: 0 4vw;
                background: #0773D3;
                border-radius: 20px 0px;
            }
        }
    }

}

@media screen and (min-width: 490px){
    .feedback_mobile{
        display: none;
    }
    .sudy_list_mobile{
        display: block;
        padding-top: 50px;
        padding-left: 5vw;
        h1{
            font-style: normal;
            font-weight: bold;
            font-size: 4.4vw;
            line-height: 88px;
            color: #000000;
            margin-top: 60px;
            margin-bottom: 94px;
        }
        .sudy_list_mobile_item{
            filter: drop-shadow(4px 8px 10px rgba(0, 0, 0, 0.5));
            border-radius: 20px;
            position: relative;
            width: 89vw;
            margin-top: 6vw;
            margin-bottom: 6vw;
            height: 29vw;
            padding-left: 8vw;
            .sudy_list_mobile_item_img{
                border-radius: 20px;
                img{
                    width: 72.8vw;
                    border-radius: 20px;
                    height: 32.6vw;
                    object-fit: cover;
                }
            }
            .sudy_list_mobile_item_left{
                background: linear-gradient(264.1deg, #063661 0%, #078FD3 99.34%);
                border-radius: 20px 0px 0px 20px;
                position: absolute;
                left: 8vw;
                top: 0.4vw;
                height: 27.8vw;
                width: 12vw;
                img{
                    width: 8.5vw;
                    margin-top: 10vw;
                    margin-left: 1.6vw;
                }
            }
            .sudy_list_mobile_item_right{
                background: linear-gradient(264.1deg, #063661 0%, #078FD3 99.34%);
                border-radius: 0px 20px 20px 0px;
                position: absolute;
                right: 8vw;
                top: 0.4vw;
                height: 27.8vw;
                width: 12vw;
                img{
                    width: 8.5vw;
                    margin-top: 10vw;
                    margin-left: 1.6vw;
                }
            }
            .sudy_list_mobile_p_1{
                font-style: 300;
                font-weight: normal;
                font-size: 3.2vw;
                line-height: 6.2vw;
                text-align: center;
                color: #FFFFFF;
                width: max-content;
                position: absolute;
                bottom: 0.8vw;
                font-family: "Montserrat", sans-serif;
                right: 8.2vw;
                margin: 0;
                padding: 0 4vw;
                background: #0773D3;
                border-radius: 20px 0px;
            }
            .sudy_list_mobile_p_2{
                top: 0px;
                left: 7.8vw;
                font-style: 300;
                font-weight: normal;
                font-size: 3.2vw;
                line-height: 6.2vw;
                font-family: "Montserrat", sans-serif;
                text-align: center;
                color: #FFFFFF;
                width: max-content;
                position: absolute;
                margin: 0;
                padding: 0 4vw;
                background: #0773D3;
                border-radius: 20px 0px;
            }
        }
    }
    .sudy_list{
    margin-left: 15vw;
    font-family: "Montserrat", sans-serif !important;
    h1{
        font-style: normal;
        font-weight: bold;
        font-size: 4.4vw;
        line-height: 88px;
        color: #000000;
        margin-top: 60px;
        margin-bottom: 94px;
    }
    div{
        margin-bottom: 122px;
        img{
            width: 34vw;
            display: inline-block;
        }
        p{
            display: inline-block;
            font-style: normal;
            font-weight: bold;
            font-size: 1.5vw;
            line-height: 2.4vw;
            width: 20vw;
            text-align: center;
            padding: 1.5vw 0.4vw;
            color: #FFFFFF;
            background: #0773D3;
            border-radius: 20px 0px;
            position: relative;
            top: -140px;
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
}   
</style>