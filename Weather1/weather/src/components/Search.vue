<template>
<div class="search">
                <input v-model="search" class="navbar__search"  placeholder="Поиск по городам">
                <button v-on:click="getSearchCity" class="navbar__btn" type="submit">искать</button>
</div>
</template>

<script>
export default{

  data(){
    return{
      urlCityName: '/src/components/json.city/ua-cities.json',
      cityNameArr: '',
      cityName: '',
      search: '',
    }
},

async mounted(){
  await this.getCit()
  // await this.getCitySearch()
  await this.getSearchCity()
      console.log(this.cityName)
},

methods: {
  async getCit(){
    const response = await fetch(this.urlCityName);
    this.cityNameArr = await response.json();
    console.log(this.cityNameArr)
  },
  // async getCitySearch(){
  //   this.cityName = this.cityNameArr.find(obj => obj.name === )
  //   console.log(this.cityName)
  // },
  async getSearchCity(){
    this.cityName = await this.cityNameArr.find(obj => obj.name === this.search)
    this.lat = await this.cityName.lat;
    this.lon = await this.cityName.lon
    console.log(this.cityName)
    console.log(this.lat)
    console.log(this.lon)

  },

}
// 
}

</script>

<style>

</style>