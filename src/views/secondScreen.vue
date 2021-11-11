<template>
<div>
    <div class="grid-container">
      <div class="grid-item">
      {{currentData[1].stationName}}
        <div class="text_number">
           {{currentData[1].currentNumber}}
        </div>
          Medical Screening Station
      </div>
    </div>
</div>

</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'
import axios from 'axios';

const configUrl = "http://localhost:3000/config"

const baseUrl = "http://localhost:3000/queue"

export default {
  name: 'secondScreen',
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
      timer: '',
      serverNumber: 0

    }
  },
  mounted() {
     this.timer = setInterval(
       this.refetch
      , 2000);


      console.log("dasdasdasdasd",this.serverNumber)
  },


  methods: {
    // for VPS
    async addVPS(){
        this.refetch();
      //  const res = await axios.put (baseUrl,{id:0, stationName:"Medical Screening  Station",currentNumber: this.currentNumber}); 
      const res = await axios.put ('http://localhost:3000/queue/0}',{
        currentNumber:this.currentNumber + 1, stationName: 'NOW SERVING'
      });
       this.currentData = [...this.currentData, res.data];
       
      // this.$router.go(this.$router.currentRoute)
       this.refetch();
    },
     async backVPS(){
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
      //  const res = await axios.put (baseUrl,{id:0, stationName:"Medical Screening  Station",currentNumber: this.currentNumber}); 
      const res = await axios.put ('http://localhost:3000/queue/1',{
        currentNumber:this.Mssnumber + 1, stationName: 'Quezon Vaccination Site'
      });
       this.currentData = [...this.currentData, res.data];
   
      // this.$router.go(this.$router.currentRoute)
       this.refetch();
    },
    async resetMSS(){
      //  const res = await axios.put (baseUrl,{id:0, stationName:"Medical Screening  Station",currentNumber: this.currentNumber}); 
      const res = await axios.put ('http://localhost:3000/queue/1',{
        currentNumber:1, stationName: 'Screening  Station'
      });
       this.currentData = [...this.currentData, res.data];
       
      // this.$router.go(this.$router.currentRoute)
       this.refetch();
    },




    
    async addPVOFD(){
      //  const res = await axios.put (baseUrl,{id:0, stationName:"Medical Screening  Station",currentNumber: this.currentNumber}); 
      const res = await axios.put ('http://localhost:3000/queue/2',{
        currentNumber:this.PVOFDnumber + 1, stationName: 'Post Vaccination Observation'
      });
       this.currentData = [...this.currentData, res.data];
       
      // this.$router.go(this.$router.currentRoute)
       this.refetch();
    },
    async resetPVOFD(){
    const res = await axios.put ('http://localhost:3000/queue/2',{
        currentNumber:1, stationName: 'Post Vaccination Observation'
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
  .text_title{
    font-family: Impact, Charcoal, sans-serif;
    font-size: 40px;
    letter-spacing: -0.4px;
    word-spacing: 2.4px;
    color: yellow;
    font-weight: 700;
    text-decoration: none;
    font-style: normal;
    font-variant: normal;
    text-transform: uppercase;
  }

    .text_number{
    font-family: Impact, Charcoal, sans-serif;
    font-size: 50vh;
    letter-spacing: -0.4px;
    word-spacing: 2.4px;
    color: #ffffff;
    font-weight: 700;
    text-decoration: none;
    font-style: normal;
    font-variant: normal;
    text-transform: uppercase;
  }

    #overlay {
      position: fixed;
      display: block;
      width: 100%;
      height: 100%;
      top: 0;
      left: 0;
      right: 0;
      bottom: 0;
      background-color: rgba(0,0,0,0.5);
      z-index: 2;
      cursor: pointer;
    }

    .grid-container {
        display: grid;
        grid-template-columns: auto ;
        padding: 10px;
        width: 100%;
        height: 100vh;
       
      }
      .grid-item {
       font-weight: 700;
        padding: 20px;
        font-size: 12vh;
        text-align: center;
        color: yellow;
      }

      .button{
        width: 3vw;
        height: 3vh;
        font-size: 1.5vh;
        background-color: #4CAF50; /* Green */
        border: none;
        color: white;
        text-align: center;
        text-decoration: none;
        display: inline-block;
        margin: 4px 2px;
        cursor: pointer;
      }
</style>
