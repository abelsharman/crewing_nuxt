<template>
    <div class="header" style="position:relative;" :style="[isMain && width < 490 ? {'background-color': 'transparent'} : {}]">
       <a href="/" class="header_img"><img :class="{ header_logo_scroll : !isMain }" src="../assets/loading.png" alt=""></a>
        <div class="header_nav">
            <a href="/">Главная</a>

            <a href="/Sudy">Виды судов</a>
            <a v-if="!isMain" href="/?id=about">О нас</a>
            <a v-if="isMain" v-scroll-to="{el: '#about'}">О нас</a>

            <a v-if="!isMain" href="/?id=education">Обучение</a>
            <a v-if="isMain" v-scroll-to="{el: '#education'}">Обучение</a>

            <a href="/vacancies">Вакансии</a>

            <a v-if="!isMain" href="/?id=cert">Сертификаты</a>
            <a v-if="isMain" v-scroll-to="{el: '#cert'}">Сертификаты</a>

            <a v-if="!isMain" href="/?id=footer">Контакты</a>
            <a v-if="isMain" v-scroll-to="{el: '#footer'}">Контакты</a>
        </div>
        <a class="header_tel" :href="'tel:'+phone" v-if="phone.length > 0">{{ phone }}</a>

        <span id="header_123" style="position:absolute;bottom:-20px;left:50vw;opacity:0;">a</span>
        <v-app-bar
            :style="[!isMain ? {'background': 'white'} : {'background': 'transparent'}]"
            style="height: 93px;box-shadow:none"
            dark
            prominent
            class="header_mobile"
        >
            <a href="/"><img class="header_mobile_img" :class="{ header_logo_scroll : !isMain }" :src="getImgUrl()" alt=""></a>
            <p :style="[!isMain ? {color: '#173760'} : {color: '#173760'}]">Marine Personnel & Consulting</p>
            <v-app-bar-nav-icon large @click.stop="drawer = !drawer" style="margin-left: 30vw;margin-top:24px;" :style="[isMain ? {color: '#173760'} : {color: '#173760'}]"></v-app-bar-nav-icon>
        </v-app-bar>

        <v-navigation-drawer
            v-model="drawer"
            absolute
            left
            temporary
            style="background: linear-gradient(264.1deg, #063661 0%, #078FD3 99.34%);position: fixed;"
        >
            <v-list
                nav
                dense
            >
                <v-list-item-group
                    active-class="deep-purple--text text--accent-4"
                    style="margin-top: 30px;"
                    >
                    <v-list-item>
                        <v-list-item-title><a style="color: white;text-decoration: none;font-size: 4vw;" class="header_mobile_a" href="/">Главная</a></v-list-item-title>
                    </v-list-item>

                    <v-list-item>
                        <v-list-item-title><a style="color: white;text-decoration: none;font-size: 4vw;" class="header_mobile_a" href="/vacancies">Вакансии</a></v-list-item-title>
                    </v-list-item>

                    <v-list-item>
                        <v-list-item-title><a style="color: white;text-decoration: none;font-size: 4vw;" class="header_mobile_a" href="/Sudy">Виды судов</a></v-list-item-title>
                    </v-list-item>
                </v-list-item-group>
            </v-list>
        </v-navigation-drawer>

    </div>
</template>


<script>
export default {
    name: 'Header',
    data(){
        return {
            width: window.innerWidth,
            drawer: false,
            phone: '',
        }
    },
    mounted(){
        this.getData()
    },
    methods: {
        getImgUrl() {
            let pet = ''
            var images = require.context('../assets/', false, /\.png$/)
            if(this.isMain){
                pet = 'loading'
            }
            else{
                pet = 'new_logo'
            }
            return images('./' + pet + ".png")
        },
        getData(){
            this.$axios.get("https://periodicals.abelsharman.kz/crewingData")
            .then((res)=>{
                this.phone = res.data[0].phone
            })
        },
    },
    props: {
        isMain: Boolean
    },
}
</script>


<style lang="scss">
@media screen and (min-width: 490px) {
    .header{
        font-family: "Montserrat", sans-serif !important;
        height: 123px;
        width: 100vw;
        padding-left: 8vw;
        background: linear-gradient(264.1deg, #063661 0%, #078FD3 99.34%);
        img{
            height: 81%;
            position: relative;
            top: 11px;
            display: inline-block;
        }
        .header_mobile{
            display: none;
        }
        .header_nav{
            margin-left: 5vw;
            width: 63vw;
            display: inline-block;
            vertical-align: middle;
            position: relative;
            top: -35px;
            p, a{
                margin: 0 1.2vw;
                display: inline-block;
                font-family: "Montserrat", sans-serif !important;
                font-style: normal;
                font-weight: 350;
                font-size: 1.222vw; //18px;
                top: 0px;
                line-height: 24px;
                text-align: center;
                text-decoration: none;
                color: #FFFFFF !important;
                cursor: pointer;
            }
        }
        .header_tel{
            display: inline-block;
            width: max-content;
            text-decoration: none;
            font-family: "Montserrat", sans-serif !important;
            font-style: normal;
            font-weight: 350;
            font-size: 1.222vw; //18px;
            line-height: 24px;
            position: relative;
            margin-left:2vw;
            top: -35px;
            color: #fff !important;
            cursor: pointer;
        }

    }
}

@media screen and (max-width: 490px) {
    .header_img, .header_nav, .header_tel{
        display: none;
    }
    .header{
        background: transparent;
        height: 93px;
        position: absolute;
        width: 100vw;
        z-index: 999;
    }
    .header_mobile {
        img{
            width: 13vw;
            margin-top: 20px;
        }
        p{
            font-style: normal;
            font-weight: normal;
            font-size: 2.4vw;
            line-height: 12px;
            letter-spacing: 0.255em;
            text-transform: uppercase;
            color: white;
            margin-top: 36px;
            width: 33vw;
            margin-left: 8px;
        }
    }
}
@keyframes rotateBlock {
    0%{
        transform: rotate(0deg);
    }
    100%{
        transform: rotate(360deg);
    }
}
.header_logo_scroll{
    animation: infinite 10s rotateBlock ease-in-out;
}
</style>