<template>
    <div class="main">
      <div class="container">
        <div class="main__data">
          <div class="main__block">
            <div class="info">
              <div class="info__city">{{ city }}</div>
              <div class="info__description"> {{ description }}</div>

            </div>

            <div class="block">
                <BlockWeath v-for='forecast in forecasts' :key="forecast" :time='forecast.time' :icon='forecast.icon'
                :temp='forecast.temp'>
              </BlockWeath>

            </div>
            <div class="details">
              <div class="details__row">
                <div class="details__item">
                  <div class="details__name">Ощущается как:</div>
                  <div class="details__value"> {{ feels_like }}° </div>
                </div>
                <div class="details__item">
                  <div class="details__name">Давление:</div>
                  <div class="details__value">{{pressure}} мм.рт.</div>
                </div>
              </div>
              <div class="details__row">
                <div class="details__item">
                  <div class="details__name">Влажность:</div>
                  <div class="details__value">{{ humidity }}%</div>
                </div>
                <div class="details__item">
                  <div class="details__name">Ветер:</div>
                  <div class="details__value">5м/с</div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
</template>

<script >
import BlockWeath from "./BlockWeath.vue"
export default{
  props:['lat' , 'lon'],
    data() {
        return {
            // urlWeather: "https://api.openweathermap.org/data/2.5/forecast?q=&appid=0d0ad9d5450fd92b19583dc4dd1801bc&lang=ru&units=metric",
            dataWeather: "",
            forecasts: [],
            temperatureUnit: "˚",
            errors: [],
            dt_txt: "",
            lat1: '50.584981',
            lon1: '30.235748',
            cyty2: "Kyiv",
            city: "",
            description: "",
            icon: "",
            feels_like: "",
            humidity: "",
            pressure: "",
        };
    },
    async mounted() {
        await this.getWeather();
        this.forecasts = await this.getRenderForecast();
    },
    methods: {
        latAdd(){
          this.lat1 = lat
          this.lon1 = lon
          console.log(lon)
        },
        async getWeather() {
            try {
                const response = await fetch("https://api.openweathermap.org/data/2.5/forecast?lat="+this.lat1+"&lon="+this.lon1+"&appid=0d0ad9d5450fd92b19583dc4dd1801bc&lang=ru&units=metric");
                this.dataWeather = await response.json();
                console.log(this.dataWeather)
                this.city = this.dataWeather.city.name;
                this.description = this.dataWeather.list["0"]["weather"]["0"]["description"];
                this.dt_txt = this.getHoursString(this.dataWeather.list["0"]["dt_txt"]);
                this.feels_like = Math.round(this.dataWeather.list["0"]["main"]["feels_like"]);
                this.humidity = this.dataWeather.list["0"]["main"]["humidity"];
                this.pressure = this.getConvertPressure(this.dataWeather.list[0].main.pressure);
                await this.getRenderForecast();
            }
            catch (error) {
                this.errors.push(error);
            }
        },
        async getRenderForecast() {
            let forecastsD = [];
            for (let i = 0; i < 6; i++) {
                let item = this.dataWeather.list[i];
                let icon = item.weather[0].icon;
                let temp = Math.round(item.main.temp);
                let time = (i == 0 ? "Сейчас" : this.getHoursString(item.dt_txt));
                forecastsD.push({
                    time: time,
                    icon: icon,
                    temp: temp
                });
            }
            return forecastsD;
        },
        getConvertPressure(value) {
            return (value / 1.33).toFixed();
        },
        getAddZero(num) {
            if (num >= 0 && num <= 9) {
                return "0" + num;
            }
            else {
                return num;
            }
        },
        getHoursString(dateTime) {
            let date = new Date(dateTime);
            let hours = this.getAddZero(date.getHours()) + "-" + this.getAddZero(date.getMinutes());
            return hours;
        },
    },
    components: { BlockWeath }
}

</script>

<style scoped>

.main {

  height: 500px;
  background-image: url("../images/noaa-kcvlb727mn8-unsplash.jpg");
  background-repeat: no-repeat;
  background-size: cover;
  padding-top: 15px;
}

.main__data {
  margin: 0 auto;
  padding: 10px;
  border-radius: 10px;
  width: 100%;
  background-color: rgb(247, 247, 247, 0.4);
}

.block {
  display: flex;
  justify-content: space-between;
  margin-bottom: 20px;
}

.info {
  text-align: center;
  margin-bottom: 20px;

}

.info__city {
  font-size: 35px;
}

.info__description {
  font-size: 17px;
}

.details__row {
  display: flex;
  justify-content: space-around;
  margin-bottom: 20px;
}

.details__item {
  flex: 1;
  display: flex;
}

.details__name {
  margin-bottom: 10px;
  font-size: 20px;

}

.details__value {
  font-size: 20px;
  padding-left: 15px;
}
</style>
