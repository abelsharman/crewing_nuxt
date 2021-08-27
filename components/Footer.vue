<template>
    <div class="footer">
      <a href="https://www.instagram.com/crewingkz/"><img class="footer_desktop" src="../assets/instagram.png" alt=""></a>
      <a href="https://t.me/crewingkz"><img class="footer_desktop" style="margin-left: 16px;" src="../assets/telegram.png" alt=""></a>

      <div
            style="box-shadow:none;background-color:linear-gradient(264.1deg, #063661 0%, #078FD3 99.34%);"
            dark
            prominent
            class="footer_mobile"
        >
            <a href="/"><img class="footer_mobile_2" src="../assets/loading.png" alt=""></a>
            <p>Marine Personal & Consulting</p>
            <img class="footer_mobile_1" style="margin-left:11vw" src="../assets/instagram.png" alt="">
            <img class="footer_mobile_1" style="margin-left: 6vw;" src="../assets/telegram.png" alt="">
        </div>
    </div>    
</template>


<script>
export default {
    name: 'Footer'
}
</script>


<style lang="scss" scoped>
@media screen and (min-width: 490px){
    .footer{
        background: linear-gradient(264.1deg, #063661 0%, #078FD3 99.34%);
        width: 100vw;
        height: 187px;
        padding-top: 52px;
        padding-left: 8vw;
        .footer_mobile{
            display: none;
        }
        .footer_desktop{
            display: inline-block
        }
    }
}
@media screen and (max-width: 490px){
    .footer{
        background: linear-gradient(264.1deg, #063661 0%, #078FD3 99.34%);
        width: 100vw;
        height: 18vw;
        padding-left:5vw;
        .footer_desktop{
            display: none;
        }
        .footer_mobile{
            display: block;
            .footer_mobile_2{
                width: 14vw;
                margin-top: 5px;
                margin-bottom: 9px;
            }
            p{
                width: 34vw;
                font-weight: 300;
                font-size: 2.4vw;;
                line-height: 3.2vw;
                letter-spacing: 0.255em;
                text-transform: uppercase;
                color: #FFFFFF;
                margin: 0;
                display:inline-block;
                position: relative;
                top: -29px;
                padding-left: 1vw;
            }
            .footer_mobile_1{
                width: 10vw;
                position: relative;
                top: -19px;
            }
        }
    }
}
</style>