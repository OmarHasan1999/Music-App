<template>
    <div class="main">
        <h3>My Music</h3>
        <h4>{{ current.songTitle }}  -   <span>{{ current.songArtist }}</span></h4>
        <div class="theButtons">
        <button class="butOne" @click="prev">Prev</button>
        <button class="butTwo" v-show="showPlay" @click="playSong(current)">Play</button>
        <button class="butTwo" v-show="!showPlay" @click="pauseSong">Pause</button>
        <button class="butThree" @click="next">Next</button>
        </div>
        <p>The PlayList</p>
        <div class="songButtons">
            <button v-for="song in theSongs" :key="song.song" @click="playSong(song)">{{ song.songTitle }}</button>
            
        </div>
    </div>
</template>


<script setup>
import songOne from "../assets/WhatsApp Audio 2024-03-18 at 4.52.50 PM (1).mp3"
import songTwo from "../assets/WhatsApp Audio 2024-03-19 at 2.01.51 AM.mp3"
import songThree from "../assets/WhatsApp Audio 2024-03-18 at 4.52.50 PM (3).mp3"
import songFour from "../assets/WhatsApp Audio 2024-03-19 at 1.45.57 AM.mp3"
import songFive from "../assets/WhatsApp Audio 2024-03-19 at 2.21.06 AM.mp3"
import songSix from "../assets/WhatsApp Audio 2024-03-19 at 2.20.21 AM.mp3"
import songSeven from "../assets/WhatsApp Audio 2024-03-19 at 2.20.25 AM (1).mp3"
import songEight from "../assets/WhatsApp Audio 2024-03-19 at 2.20.25 AM.mp3"
import songNine from "../assets/WhatsApp Audio 2024-03-19 at 3.02.11 AM.mp3"
import songTen from  "../assets/WhatsApp Audio 2024-03-19 at 2.20.25 AM (2).mp3"
import songEleven from "../assets/WhatsApp Audio 2024-03-19 at 3.15.02 AM.mp3"
import { ref, onMounted } from 'vue';

const current = ref({})
const showPlay = ref(true)
const index = ref(0)
let player = new Audio()

const theSongs = ref([
                {
                    songTitle: "Hal Asmar El-Lon",
                    songArtist: "Lena Chamamyan",
                    song: songOne
                },
                {
                    songTitle: "Bali Ma'ak",
                    songArtist: "Lena Chamamyan",
                    song: songTwo
                },
                {
                    songTitle: "Ala Mowj El-Bahr",
                    songArtist: "Lena Chamamyan",
                    song: songThree
                },
                {
                    songTitle: "Lamma bada",
                    songArtist: "Lena Chamamyan",
                    song: songFour
                },
                {
                    songTitle: "Al Rozana",
                    songArtist: "Lena Chamamyan",
                    song: songFive
                },
                {
                    songTitle: "Washaa' Alhawa",
                    songArtist: "Lena Chamamyan",
                    song: songSix
                },
                {
                    songTitle: "Yakhi Ana Souriyeh",
                    songArtist: "Lena Chamamyan",
                    song: songSeven
                },
                {
                    songTitle: "Ya Mayela Al-Ghusoon",
                    songArtist: "Lena Chamamyan",
                    song: songEight
                },
                {
                    songTitle: "Yumma Lala",
                    songArtist: "Lena Chamamyan",
                    song: songNine
                },
                {
                    songTitle: "Ya Msafera",
                    songArtist: "Lena Chamamyan",
                    song: songTen
                },
                {
                    songTitle: "Awal Msafera",
                    songArtist: "Lena Chamamyan",
                    song: songEleven
                },
            ])

onMounted(() => {
        current.value = theSongs.value[index.value]
        player.src = current.value.song

})

const playSong = (song) => {
            current.value = song
            player.src = song.song
            player.play()
            showPlay.value = false
        }

const pauseSong = () => {
            showPlay.value = true
            player.pause()
        }
        
const next = () => {
            index.value++
            if(index.value > theSongs.value.length -1){
                index.value = 0
            }
            current.value = theSongs.value[index.value]
            player.src = current.value.song
            player.play()
        }
        
const prev = () => {
            index.value--
            if(index.value < 0){
                index.value = theSongs.value.length -1
            }
            current.value = theSongs.value[index.value]
            player.src = current.value.song
            player.play()
        }


</script>
<!-- 
<script>


export default {
    data() {
        return {
            current: {},
            showPlay: true,
            index:0,
            theSongs:[
                {
                    songTitle: "Hal Asmar El-Lon",
                    songArtist: "Lena Chamamyan",
                    song: songOne
                },
                {
                    songTitle: "Bali Ma'ak",
                    songArtist: "Lena Chamamyan",
                    song: songTwo
                },
                {
                    songTitle: "Ala Mowj El-Bahr",
                    songArtist: "Lena Chamamyan",
                    song: songThree
                },
                {
                    songTitle: "Lamma bada",
                    songArtist: "Lena Chamamyan",
                    song: songFour
                },
                {
                    songTitle: "Al Rozana",
                    songArtist: "Lena Chamamyan",
                    song: songFive
                },
                {
                    songTitle: "Washaa' Alhawa",
                    songArtist: "Lena Chamamyan",
                    song: songSix
                },
                {
                    songTitle: "Yakhi Ana Souriyeh",
                    songArtist: "Lena Chamamyan",
                    song: songSeven
                },
                {
                    songTitle: "Ya Mayela Al-Ghusoon",
                    songArtist: "Lena Chamamyan",
                    song: songEight
                },
                {
                    songTitle: "Yumma Lala",
                    songArtist: "Lena Chamamyan",
                    song: songNine
                },
                {
                    songTitle: "Ya Msafera",
                    songArtist: "Lena Chamamyan",
                    song: songTen
                },
                {
                    songTitle: "Awal Msafera",
                    songArtist: "Lena Chamamyan",
                    song: songEleven
                },
            ],
            player: new Audio()
        }
    },
    mounted() {
        this.current = this.theSongs[this.index]
        this.player.src = this.current.song
    },
    methods: {
        playSong(song){
            this.current = song
            this.player.src = song.song
            this.player.play()
            this.showPlay = false
        },
        pauseSong(){
            this.showPlay = true
            this.player.pause()
        },
        next(){
            this.index++
            if(this.index > this.theSongs.length -1){
                this.index = 0
            }
            this.current = this.theSongs[this.index]
            this.player.src = this.current.song
            this.player.play()
        },
        prev(){
            this.index--
            if(this.index < 0){
                this.index = this.theSongs.length -1
            }
            this.current = this.theSongs[this.index]
            this.player.src = this.current.song
            this.player.play()
        },
    },

}
</script> -->

<style lang="css">
    *{
        padding: 0%;
        margin: 0%;
        box-sizing: border-box;
        overflow-x: hidden;
    }
    body{
        width: 100%;
        min-height: 100vh;
        font-family:Arial, Helvetica, sans-serif;
    }
    .main{
        display: flex;
        justify-content: center;
        align-items: center;
        flex-direction: column;
    }
    .main h3{
        color: white;
        font-size: 40px;
        font-weight: 700;
        width: 100%;
        padding: 20px;
        text-align: center;
        background-color: rgba(0, 0, 0, 0.904);
    }
    .main h4{
        color: rgba(0, 0, 0, 0.926);
        margin-top: 10vh;
        font-size: 30px;
    }
    .main h4 span{
        color: rgba(0, 0, 0, 0.673);
        font-style: italic;
    }
    .theButtons{
        display: flex;
        justify-content: center;
        align-items: center;
        flex-direction: row;
        margin-top: 5vh;
        cursor: pointer;
    }
    .theButtons .butTwo{
      margin: 10px 40px;
      padding: 15px 25px;
      border-radius: 4px;
      color: aliceblue;
      background-color: rgba(255, 0, 0, 0.736);
      border-style: none;
      font-size: 20px;
      font-weight: 700;
      cursor: pointer;


    }
    .theButtons .butOne{
      padding: 8px 15px;
      border-radius: 4px;
      color: aliceblue;
      background-color: orangered;
      border-style: none;
      font-size: 15px;
        cursor: pointer;
        font-weight: 700;

    }
    .theButtons .butThree{
      padding: 8px 15px;
      border-radius: 4px;
      color: aliceblue;
      background-color: orangered;
      border-style: none;
      font-size: 15px;
        cursor: pointer;
      font-weight: 700;

    }
    .main p{
        color: rgba(0, 0, 0, 0.754);
        margin-top: 7vh;
        font-size: 30px;
        font-weight: 700;
    }
    .songButtons{
        display: flex;
        justify-content: center;
        align-items: center;
        flex-direction: column;
        margin-top: 5vh;
        cursor: pointer;
    }
    .songButtons button{
        color: antiquewhite;
        background-color: #f64611;
        border-style: none;
        padding: 10px 40px;
        border-radius: 3px;
        margin-bottom: 10px;
        cursor: pointer;
        font-weight: 900;
        font-size: 18px;
        transition: 0.2s ease;
        font-family:'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
    }
    .songButtons button:hover{
        background-color: #ed6809;
    }
    @media only screen and (max-width: 414px){
        .main h4{
        color: rgba(0, 0, 0, 0.926);
        margin-top: 10vh;
        font-size: 18px;
        font-weight: 700;
    }
    .main h3{
        font-size: 30px;
        font-weight: 700;
    }
    }
</style>