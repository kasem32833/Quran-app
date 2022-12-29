

<template>
  <div class="bg-gray-100 min-h-screen">
    <div class="container py-6">
      <div class="bg-white p-4 ">
        <div class="flex -mx-4 items-center mb-6">
          <div class="flex-1 px-4">
            <select @change="getSpecificSura" name="" id="" class="quran-input">
              <option value="">Select Sura</option>
              <option v-for="sura in suras" :value="sura.number">{{sura.name}}-{{sura.englishName}}</option>
            </select>
          </div>
          <div class="flex-1 px-4 text-center">
            <h3 class="font-bold text-lg mb-1" >The Holy Quran</h3>
            <p>{{ currentSura.englishName}}</p>
          </div>
          <div class="flex-1 px-4 quran-input mr-4 ">
            <h4 class="font-bold text-xl ">Name: {{ currentSura.name }}-{{ currentSura.englishName }}</h4>
            <p>Number Of Ayahs: {{ currentSura.numberOfAyahs }}</p>
            <p>Revelation Type: {{ currentSura.revelationType }}</p>
          </div>
        </div>
        <div class="  text-4xl border rounded border-gray-400 p-4">
          <p class="flex py-4 items-center" v-if="currentSura.hasOwnProperty('ayahs')" v-for="ayah in currentSura.ayahs">
            <span class=" text-2xl flex item-center justify-center w-10 h-10  items-center rounded-full border border-gray-700 ">{{ayah.numberInSurah}} 
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
    })
    this.querySpecificSura(1);
  },
  methods: {
    getSpecificSura(e){
      console.log(e.target.value)
      this.querySpecificSura(e.target.value);
    },

    querySpecificSura(suraNumber){
      axios.get('https://api.alquran.cloud/v1/surah/' + suraNumber).then(response =>{
      this.currentSura = response.data.data
      })
    }
  }
  }   
</script>


