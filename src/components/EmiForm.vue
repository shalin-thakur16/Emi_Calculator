<template>
  <div>
    <div class="w-full ">
      <div class=" bg-gray-200 text-2xl font-semibold px-6 py-4 uppercase w-full"> Emi calculator</div>
    </div>
        <h1 class="text-2xl font-bold mt-16 text-blue-500 px-10 ml-[39px]">Easy way to Calculate your EMI</h1>
        <div class="flex flex-col md:flex-row justify-around mx-5">
    <div class="flex " >
      <div class="p-6 bg-gray-200 w-full flex-col md:flex-row rounded-md my-4 flex" >
        <div class="flex flex-col">

<div class="flex justify-between mt-[8px] gap-2 flex-col">
  <div class="px-2  flex flex-col  items-start gap-1">
    <p class="text-lg px-2">Amount</p>
    <input type="number" class="px-2 py-1 rounded-md" v-model="amount" />
  </div>
  <div class="px-2 flex flex-col items-start gap-1">
    <p class="">Duration(Years)</p>
    <input type="number" class="px-2 py-1 rounded-md" v-model="duration" />
  </div>
  <!-- <div class="px-2">
    <p class="text-lg flex flex-col items-start gap-1">Total Interest</p>
    <input type="number" class="px-2 py-1 rounded-md" v-model="TotalInterest"/>
  </div> -->
</div>
<div class="flex justify-between flex-col">
  <div class="px-2 flex flex-col items-start gap-1">
    <p class="text-lg">Interest Rate %</p>
    <input type="number" class="px-2 py-1 rounded-md" v-model="InterestRate"/>
  </div>
</div>
<div class="my-4 flex">
  <div class="mx-4">
    <button type="Submit" class="bg-red-400 px-3 py-2 text-lg rounded-md text-white" v-on:click="calculate">
      Submit
    </button>
  </div>
  <div>
    <button  class="bg-white px-3 py-2 text-lg rounded-md" v-on:click="resetData">
      Reset
    </button>
  </div>
</div>
</div>

<!-- To the Right side! -->
<div class="flex gap-3 mt-[8px]  items-start flex-col">

  <div class="px-2">
    <p class="text-lg flex flex-col items-start gap-1">Calculated EMI</p>
    <input type="number" class="px-2 py-1 rounded-md" v-model="calculatedEmi"/>
  </div>
   <div class="px-2">
    <p class="text-lg flex flex-col items-start gap-1">Total Interest</p>
    <input type="number" class="px-2 py-1 rounded-md" v-model="TotalInterest"/>
  </div> 
</div>
<!-- end of the right -->
</div>
</div>
    

   <div class="w-[418px]">
    <BackgroundImage/>
   </div>
  </div>
  </div>
        
</template>
<script>
import BackgroundImage from './BackgroundImage.vue';
export default {
    data() {
        return {
            amount: 1000000,
            InterestRate: 2,
            duration: 1,
            calculatedEmi: 0,
            TotalInterest: 0,
        };
    },
    methods: {
        calculate(e) {
            e.preventDefault();
            var loanAmount = this.amount;
            var numberOfMonths = this.duration >= 1 ? this.duration * 12 : 0;
            var rateOfInterest = this.InterestRate;
            var monthlyInterestRatio = rateOfInterest / 100 / 12;
            var top = Math.pow(1 + monthlyInterestRatio, numberOfMonths);
            var bottom = top - 1;
            var sp = top / bottom;
            var emi = loanAmount * monthlyInterestRatio * sp;
            var full = numberOfMonths * emi;
            var interest = full - loanAmount;
            this.calculatedEmi = Math.round(emi);
            this.TotalInterest = Math.round(interest);
            return this.calculatedEmi, this.totalInterest;
        },
        resetData(e) {
            e.preventDefault();
            this.amount = 1000000;
            this.InterestRate = 2;
            this.duration = 1;
            this.calculatedEmi = 0;
            this.TotalInterest = 0;
        }
    },
    components: { BackgroundImage }
}
</script>