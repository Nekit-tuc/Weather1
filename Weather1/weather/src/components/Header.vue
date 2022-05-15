
<template>
    <header class="header">
      <div class="container">
        <nav class="navbar ">
          <a href="#" class="navbar__logo">-_-</a>

            <Search/>

        </nav>
      </div>
    </header>
</template>

<script>
import Search from "./Search.vue"
export default{
      components: { Search }
}
</script>



<style scoped>
.header {
  background-color: rgb(245, 245, 245);
}

.navbar {
  display: flex;
  justify-content: space-between;
  min-height: 50px;
  align-items: center;

}

.card {
  margin-left: 10px;
}

.navbar__logo {
  font-size: 30px;
  font-weight: 700;
  color: rgb(53, 115, 151);
  text-transform: uppercase;
}
</style>