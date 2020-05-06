<template>
  <div id="app">
    <Home :class="{ active: page == 'Home' }" />
    <Weather class="" />
    <div class="navbar">
      <ul>
        <li @click="selectPage('Home')">Home</li>
        <li @click="selectPage('Weather')">Weather</li>
      </ul>
    </div>
  </div>
</template>

<script>
import Home from "./components/Home";
import Weather from "./components/Weather";

export default {
  name: "App",
  data() {
    return {
      page: "Home"
    };
  },
  components: {
    Home,
    Weather
  },
  methods: {
    selectPage: function(el) {
      this.page = el;
    }
  }
};

window.onload = function() {
  var app = document.getElementById("app");
  var header = document.getElementById("header");
  var weather = document.getElementById("weather");
  var windowheight = window.innerHeight + "px";

  // to make the page equal to window height
  fullheight(app);
  // to make the home component equal to window height
  fullheight(header);
  // to make the weather component equal to window height
  fullheight(weather);
  function fullheight(element) {
    element.style.height = windowheight;
  }

  window.onresize = function() {
    fullheight(app);
    fullheight(header);
    fullheight(weather);
  };
};
</script>

<style lang="scss">
#app {
  overflow: hidden;
}

body {
  margin: 0;
  padding: 0;

  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: Bitter;
  }
}

.header {
  position: fixed;
  bottom: 100%;
  transition: 1s all ease;
  width: 100%;

  &.active {
    bottom: 0;
  }
}

.navbar {
  position: fixed;
  top: 130px;
  right: -65px;
  color: #fff;

  ul {
    list-style: none;
    transform: rotate(90deg);

    li {
      display: inline-block;
      cursor: pointer;
      margin: 20px;
    }
  }
}

@media (max-width: 600px) {
  .navbar {
    top: 200px;
  }
}

@font-face {
  font-family: Bitter;
  src: url(./assets/fonts/Bitter-Regular.ttf);
  src: url(./assets/fonts/Bitter-Bold.ttf);
}
</style>
