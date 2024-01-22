<style>
input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
  -webkit-appearance: none;
  margin: 0;
}

input[type="number"] {
  -moz-appearance: textfield;
}
</style>




<template>
  <main class="min-h-screen bg-gray-300 flex justify-center items-center">
    <section
      class="w-[380px] h-[420px] lg:w-[750px] lg:h-[700px] flex flex-col rounded-br-[100px] lg:rounded-br-[200px] rounded-[25px] bg-white "
    >
      <div class="flex justify-start items-center gap-8 m-3 lg:m-10 ">
        <div class="flex flex-col">
          <span class="mb-3 font-bold text-gray-500">DAY</span>
          <input
            class="w-[100px] h-[50px] lg:w-[150px] lg:h-[70px] font rounded-[15px] border pl-3 placeholder:font-bold placeholder:text-[20px] placeholder:text-black"
            type="number"
            v-model="day"
            name=""
            id=""
            placeholder="DD"
          />
        </div>

        <div class="flex flex-col">
          <span class="mb-3 font-bold text-gray-500">MONTH</span>
          <input
            class="w-[100px] h-[50px] lg:w-[150px] lg:h-[70px] rounded-[15px] border pl-3 placeholder:font-bold placeholder:text-[17px] placeholder:text-black"
            type="number"
            v-model="month"
            name=""
            id=""
            placeholder="MM"
          />
        </div>

        <div class="flex flex-col">
          <span class="mb-3 font-bold text-gray-500">YEAR</span>
          <input
            class="w-[100px] h-[50px] lg:w-[150px] lg:h-[70px] rounded-[15px] border pl-3 placeholder:font-bold placeholder:text-[17px] placeholder:text-black"
            v-model="year"
            type="number"
            name=""
            id=""
            placeholder="YYYY"
          />
        </div>
      </div>

      <!-- ///////////////////////////icon//////////////// -->

      <div class="lg:pr-10 mt-6">
        <div class="flex justify-end items-center relative">
          <div class="h-[1px] w-full border-b border-gray-300"></div>
          <div
            class="w-20 h-20 lg:w-24 lg:h-24 border rounded-full flex justify-center items-center bg-[#8b5cf6] absolute bottom-1/2 left-1/2 -translate-x-1/2 translate-y-1/2 lg:left-[90%] lg:translate-x-0"
          >
            <img :src="img" alt="" @click="formYears" class="w-10 h-10" />
            
          </div>
          <!-- <div class="h-[1px] w-5/12 border-b border-gray-300 lg:hidden">

          </div> -->
        </div>
      </div>

        <!-- /////////////////////date//////////////// -->
      <div class="flex flex-col justify-center lg:ml-5 m-8">
        <!-- ////////////////////yyyy/////////////// -->
        <div class="flex">
          <h2 class="text-[40px] lg:text-[65px] font-bold pl-5 lg:pl-28 italic text-purple-800">
          {{ y ? y : "--" }}
        </h2>
          
        <span class="text-[40px] lg:text-[65px] font-bold pl-7 italic">YEAR</span>
        </div>


        <!-- /////////////////mmm///////////////// -->
        <div class="flex ">
          <h2 class="text-[40px] lg:text-[65px] font-bold pl-5 lg:pl-28 italic text-purple-800">
          {{ m ? m : "--" }}
        </h2>
          
        <span class="text-[40px] lg:text-[65px] font-bold pl-7 italic">MONTH</span>
        </div>

          <!-- ////////////////////dd////////////////////// -->

        <div class="flex">
          <h2 class="text-[40px] lg:text-[65px] font-bold pl-5 lg:pl-28 italic text-purple-800">
          {{ d ? d : "--" }}
        </h2>
          
        <span class="text-[40px] lg:text-[65px] font-bold pl-7 italic">DAY</span>
        </div>

      </div>
    </section>

    <!-- <div>
       <Header/> 
    </div> -->
  </main>
</template>






<script>
import Header from '../components/header/header.vue'
export default {
    components:{
        Header
        },
  data() {
    return {
      img: "/images/icon-arrow.svg",
      year: "",
      month: "",
      day: "",
      calcutage: "",
      d:'',
      m:'',
      y:'',
    }
  },
  watch: {
    year: function (newVal, oldvalue) {
      // console.log(newVal.length);
      if (newVal && newVal.toString().length > 4) {
        this.year = newVal.toString().slice(0, 4);
      }
    },

    month: function (newVal, oldvalue) {
      if ((newVal && newVal.toString().length > 2) || newVal > 12) {
        this.month = 12;
        // this.month = newVal.toString().slice(0,2)
        // alert('msg');
      }
    },

    day: function (newVal, oldvalue) {
      let limitValue = 31;
      if (this.month > 6) {
        limitValue = 30;
      }
      if ((newVal && newVal.toString().length > 2) || newVal > limitValue) {
        this.day = limitValue;
      }
    },
  },

  methods: {
    formYears() {
      // this.year
      // console.log(this.year);
      if (this.year === "" || this.year.toString().length != 4) {
        alert("adam bash year");
        this.year = "";
      } else {
        this.calculateAge();
      }
      //////////////
    },
    calculateAge() {

      // let nowTime = new Date(Date.now())
      // let yearsOffBrithy = new Date(this.year.toString()+'-'+this.month.toString()+'-'+this.day.toString())
      let nowTime = new Date()
      let d1 = nowTime.getDate()
      let m1 =1+ nowTime.getMonth()
      let y1 = nowTime.getFullYear()
      let allMonth= [31,28,31,30,31,30,31,31,30,31,30,31]
      if(this.day>d1){
        d1=d1+allMonth[m1-1]
        m1=m1-1
      }
      if(this.month>m1){
        m1=m1+12
        y1=y1-1
      }

      this.d =d1-this.day
      this.m = m1-this.month
      this.y = y1-this.year

      // let brithInems = yearsOffBrithy.getTime()
      // let x = yearsOffBrithy.getDate()
      // let y = yearsOffBrithy.getMonth()
      // let c = yearsOffBrithy.getFullYear()
      // let ageInms=new Date()-brithInems
      // let ageDate=new Date(ageInms)
      // let result= Math.abs(ageDate.getUTCFullYear()-1970)
      // console.log(result);
      // let carenYear = new Date(Date.now()).getFullYear();
    //   this.calcutage = carenYear - yearsOffBrithy;

    // new Date(this.year + '-' + this.month + '-' + this.day)
    //   console.log(yearsOffBrithy);
    
    },
  },
};
</script>