<template>
<div>
    <div class="">

        <div class="">
            <h6>SCREEN CONTROLLER Beta </h6>
        <h1>Vaccination Profiling:{{currentData[0].currentNumber}} </h1>
        <button class="button" style="margin-left: 10px; margin-right: 20px;" v-on:click="addVPS"> 
            next
                </button>
                <button v-if="currentData[0].currentNumber !== 1" class="button" style="margin-left: 10px; margin-right: 20px;" v-on:click="backVPS">
            back
                </button>
                <button v-if="currentData[0].currentNumber !== 1" class="button" style="margin-left: 10px; margin-right: 20px" v-on:click="resetVPS">
            reset
         </button>
        </div>
    
        <div class="">
        <h1>Medical Screening Station: {{currentData[1].currentNumber}} </h1>
            <button class="button" style="margin-left: 10px; margin-right: 20px;" v-on:click="addMSS"> 
            next
                </button>
                <button v-if="currentData[1].currentNumber !== 1" class="button" style="margin-left: 10px; margin-right: 20px;" v-on:click="backMSS">
            back
                </button>
                <button   v-if="currentData[1].currentNumber !== 1" class="button" style="margin-left: 10px; margin-right: 20px" v-on:click="resetMSS">
            reset
         </button>
        </div>
        <div class="">
        <h1>Post Vaccination Station: {{currentData[2].currentNumber}} </h1>
            <button class="button" style="margin-left: 10px; margin-right: 20px;" v-on:click="addPVOFD"> 
            next
                </button>
                <button v-if="currentData[2].currentNumber !== 1" class="button" style="margin-left: 10px; margin-right: 20px;" v-on:click="resetPVOFD">
            back
                </button>
                <button v-if="currentData[2].currentNumber !== 1" class="button" style="margin-left: 10px; margin-right: 20px" v-on:click="resetPVOFD">
            reset
         </button>
        </div>        
    </div>
</div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'
import axios from 'axios';

import data from '/currentDisplay.json'

var mytrack = new Audio('/airport.mp3')
var back = new Audio('/airport_sound.mp3')
var resetaudio = new Audio('/skribbl_success.mp3')


const baseUrl = "http://localhost:3000/queue"

const configUrl = "http://localhost:3000/config"

export default {
  name: 'About',
  components: {
    HelloWorld
  },
  data() {
    return {
      currentData:[],
      currentNumber: 1,
      Mssnumber: 1,
      PVOFDnumber: 1,
      vaccNum: 1,
      loading: false,
      serverEdit: true,
      serverNumber: 0

    }
  },
  mounted() {
 
  },
  methods: {
    // for VPS
    async addVPS(){
       setTimeout(function(){ back.play(); }, 2000);
      //  const res = await axios.put (baseUrl,{id:0, stationName:"Medical Screening  Station",currentNumber: this.currentNumber}); 
      const res = await axios.put ('http://localhost:3000/queue/0',{
        currentNumber:this.currentNumber + 1, stationName: 'NOW SERVING'
      });
       this.currentData = [...this.currentData, res.data];
   
      // this.$router.go(this.$router.currentRoute)
       this.refetch();
     
         
    },
     async backVPS(){
          setTimeout(function(){ back.play(); }, 2000);
        this.refetch();
      //  const res = await axios.put (baseUrl,{id:0, stationName:"Medical Screening  Station",currentNumber: this.currentNumber}); 
      const res = await axios.put ('http://localhost:3000/queue/0',{
        currentNumber:this.currentNumber - 1, stationName: 'NOW SERVING'
      });
       this.currentData = [...this.currentData, res.data];
       
      // this.$router.go(this.$router.currentRoute)
       this.refetch();
    },
    async resetVPS(){
          setTimeout(function(){ resetaudio.play(); }, 2000);
      //  const res = await axios.put (baseUrl,{id:0, stationName:"Medical Screening  Station",currentNumber: this.currentNumber}); 
      const res = await axios.put ('http://localhost:3000/queue/0',{
        currentNumber:1, stationName: 'NOW SERVING'
      });
       this.currentData = [...this.currentData, res.data];
       
      // this.$router.go(this.$router.currentRoute)
       this.refetch();
     
    },

    // for MSS

    async addMSS(){
         setTimeout(function(){ back.play(); }, 2000);
      //  const res = await axios.put (baseUrl,{id:0, stationName:"Medical Screening  Station",currentNumber: this.currentNumber}); 
      const res = await axios.put ('http://localhost:3000/queue/1',{
        currentNumber:this.Mssnumber + 1, stationName: 'NOW SERVING'
      });
       this.currentData = [...this.currentData, res.data];
   
      // this.$router.go(this.$router.currentRoute)
       this.refetch();
    },
    async resetMSS(){
          setTimeout(function(){ resetaudio.play(); }, 2000);
      //  const res = await axios.put (baseUrl,{id:0, stationName:"Medical Screening  Station",currentNumber: this.currentNumber}); 
      const res = await axios.put ('http://localhost:3000/queue/1',{
        currentNumber:1, stationName: 'NOW SERVING'
      });
       this.currentData = [...this.currentData, res.data];
       
      // this.$router.go(this.$router.currentRoute)
       this.refetch();
    },


    async backMSS(){
         setTimeout(function(){ back.play(); }, 2000);
        this.refetch();
      //  const res = await axios.put (baseUrl,{id:0, stationName:"Medical Screening  Station",currentNumber: this.currentNumber}); 
      const res = await axios.put ('http://localhost:3000/queue/1',{
        currentNumber:this.Mssnumber - 1, stationName: 'NOW SERVING'
      });
       this.currentData = [...this.currentData, res.data];
       
      // this.$router.go(this.$router.currentRoute)
       this.refetch();
    },




    
    async addPVOFD(){
         setTimeout(function(){ back.play(); }, 2000);
      //  const res = await axios.put (baseUrl,{id:0, stationName:"Medical Screening  Station",currentNumber: this.currentNumber}); 
      const res = await axios.put ('http://localhost:3000/queue/2',{
        currentNumber:this.PVOFDnumber + 1, stationName: 'NOW SERVING'
      });
       this.currentData = [...this.currentData, res.data];
       
      // this.$router.go(this.$router.currentRoute)
       this.refetch();
    },
    async resetPVOFD(){
          setTimeout(function(){ resetaudio.play(); }, 2000);
    const res = await axios.put ('http://localhost:3000/queue/2',{
        currentNumber:1, stationName: 'NOW SERVING'
      });
       this.currentData = [...this.currentData, res.data];
       
      // this.$router.go(this.$router.currentRoute)
       this.refetch();
    },
    async backPVOFD(){
         setTimeout(function(){ back.play(); }, 2000);
        this.refetch();
      //  const res = await axios.put (baseUrl,{id:0, stationName:"Medical Screening  Station",currentNumber: this.currentNumber}); 
      const res = await axios.put ('http://localhost:3000/queue/2',{
        currentNumber:this.PVOFDnumber - 1, stationName: 'NOW SERVING'
      });
       this.currentData = [...this.currentData, res.data];
       
      // this.$router.go(this.$router.currentRoute)
       this.refetch();
    },

    


    async addVACC(){
         //  const res = await axios.put (baseUrl,{id:0, stationName:"Medical Screening  Station",currentNumber: this.currentNumber}); 
      const res = await axios.put ('http://localhost:3000/queue/3',{
        currentNumber:this.vaccNum + 1, stationName: 'Vaccination'
      });
     
   
      // this.$router.go(this.$router.currentRoute)
       this.refetch();
    },

    async resetVACC(){
      //  const res = await axios.put (baseUrl,{id:0, stationName:"Medical Screening  Station",currentNumber: this.currentNumber}); 
      const res = await axios.put ('http://localhost:3000/queue/3',{
        currentNumber:1, stationName: 'Vaccination'
      });
       this.currentData = [...this.currentData, res.data];
       
      // this.$router.go(this.$router.currentRoute)
       this.refetch();
    },

   async refetch(){
    try{
          const res = await axios.get(baseUrl);
          const con = await axios.get(configUrl);
          this.currentData = res.data;
          console.log(this.currentdata);
          this.currentNumber = res.data[0].currentNumber
          this.Mssnumber = res.data[1].currentNumber
          this.PVOFDnumber = res.data[2].currentNumber
          this.vaccNum = res.data[3].currentNumber
          this.serverNumber = con.data[0].server;
        }catch(e){
          console.log(e);
        }
    },

    async setServer(){
      //  const res = await axios.put (baseUrl,{id:0, stationName:"Medical Screening  Station",currentNumber: this.currentNumber}); 
      const res = await axios.put ('http://localhost:3000/config/0',{
        server:this.serverNumber
      });
       this.currentData = [...this.currentData, res.data];
   
      // this.$router.go(this.$router.currentRoute)
       this.refetch();
       this.serverEdit = true
    },


    activateloading(){
     

    }
  },
  async created(){
    try{
      const res = await axios.get(baseUrl);
      const con = await axios.get(configUrl);
      this.currentData = res.data;
      console.log(this.currentdata);
      this.currentNumber = res.data[0].currentNumber
      this.Mssnumber = res.data[1].currentNumber
      this.PVOFDnumber = res.data[2].currentNumber
      this.vaccNum = res.data[3].currentNumber
      this.serverNumber = con.data[0].server;
    }catch(e){
      console.log(e);
    }
  }
}
</script>

<style>
      .button{
        width: 10vw;
        height: 10vh;
        font-size: 5vh;
        background-color: #4CAF50; /* Green */
        border: none;
        color: white;
        text-align: center;
        text-decoration: none;
        display: inline-block;
        margin: 4px 2px;
        cursor: pointer;
      }

      .input-custom{
        width: 20vw;
        height: 10vh;
        font-size: 5vh;
      }
           h1{
        font-weight: 10vh;
        padding: 20px;
        font-size: 5vh;
        text-align: center;
        color: yellow;
      }

      h6{
          font-size: 1vh;
          color: white;
      }
      </style>