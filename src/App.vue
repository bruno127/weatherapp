<template>
  <div id="app">
<main>
      <div class="search-box">
        <input 
        type="text" 
        class="search-bar" 
        placeholder="Search..."
        />
      </div>
      <div class="weather-wrap">
        <div class="location-box">
          <div class="location"> Mostar, BiH </div>
          <div class="date"> 25.08.2022. </div>
        </div>

        <div class="weather-box">
          <div class="temp">32 °C</div>
          <div class="weather"> Sunny </div>
        </div>
      </div>
    </main>
  </div>
</template>

<script>
export default {
  name: 'App',
}
</script>

<style>

</style>
