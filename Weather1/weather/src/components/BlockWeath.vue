<template>
  
  <div  class="block__item">
  <div class="block__time">{{ time }}</div>
  <div class="block__icon icon__02d" :class='"icon__" + icon' ></div>
  <div class="block__temperature"> {{ temp }} </div>
  </div>


</template>


<script>

export default {
  props: ['time', 'icon', 'temp'],

}
</script>


<style scoped>
.block__icon {
  width: 50px;
  height: 50px;

}

.block__item {
  text-align: center;

}

.block__icon,
.block__time {
  margin-bottom: 15px;
  font-size: 20px;
}

.block__temperature {
  font-size: 17px;
  font-weight: 500;
}

.icon__01d,
.icon__01n,
.icon__02d,
.icon__02n,
.icon__03d,
.icon__03n,
.icon__04d,
.icon__04n,
.icon__09d,
.icon__09n,
.icon__10d,
.icon__10n,
.icon__11n,
.icon__11n,
.icon__13d,
.icon__13n,
.icon__50d,
.icon__50n {
  background-size: 50px;
  background-repeat: no-repeat;
}

.icon__01d,
.icon__01n {
  background-image: url("../images/01d.png");
}

.icon__02d,
.icon__02n {
  background-image: url("../images/02d.png");
}

.icon__03d,
.icon__03n {
  background-image: url("../images/03d.png");
}

.icon__04d,
.icon__04n {
  background-image: url("../images/04d.png");
}

.icon__09d,
.icon__09n {
  background-image: url("../images/09d.png");
}

.icon__10d,
.icon__10n {
  background-image: url("../images/10d.png");
}

.icon__11n,
.icon__11n {
  background-image: url("../images/11d.png");
}

.icon__13d,
.icon__13n {
  background-image: url("../images/13d.png");
}

.icon__50d,
.icon__50n {
  background-image: url("../images/50d.png");
}
</style>