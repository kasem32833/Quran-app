

<template>
  <div class="bg-gray-100 min-h-screen">
    <div class="container py-6">
      <div class="bg-white p-4 ">
        <div class="flex -mx-4 items-center mb-6">
          <div class="flex-1 px-4">
            <select name="" id="" class="quran-input">
              <option value="">Select Sura</option>
              <option v-for="sura in suras" value="">{{sura.name}}-{{sura.englishName}}</option>
            </select>
          </div>
          <div class="flex-1 px-4 text-center">
            <h3 class="font-bold text-lg mb-1" >Al Baqara</h3>
            <p>The Cow</p>
          </div>
          <div class="flex-1 px-4">
            <select name="" id="" class="quran-input">
              <option value="">Select Ayah</option>
            </select>
          </div>
        </div>
        <div class=" font-bold text-4xl">
          <p class="flex py-4 items-center" v-if="currentSura.hasOwnProperty('ayahs')" v-for="ayah in currentSura.ayahs">
            <span class=" text-2xl flex item-center justify-center w-10 h-10  items-center rounded-full border border-gray-700 ">{{ayah.number}} 
          </span> - {{ ayah.text }}</p>
        </div>
      </div>
    </div>
  </div>
  
</template>


<script>
  import axios from 'axios'
  
  export default{
    name: 'App',
    data () {
      return{
        suras: [],
        currentSura: []
      }
     
    },
    mounted(){
      axios.get('https://api.alquran.cloud/v1/surah')
      .then(response =>{
      this.suras = response.data.data
    }
    )
      axios.get('https://api.alquran.cloud/v1/surah/1')
      .then(response =>{
        console.log(response.data.data)
      this.currentSura = response.data.data
    }
    )
  }
  }   
</script>


