<template>
  <div class="weather" id="weather">
    <h3>Just type the city name</h3>
    <p>You must spelling correctly</p>
    <form>
      <input type="text" placeholder="City" v-model="city" />
      <button id="click" type="button" @click="getWeather">Find</button>
    </form>
    <div v-if="info" class="city">
      <h4>{{ info.name }}, {{ info.sys.country }}</h4>
      <h5>{{ info.weather[0].main }}</h5>
      <h3>{{ temp }}°c</h3>
      <ul>
        <li>{{ temp_max }}°c</li>
        <li>{{ temp_min }}°c</li>
      </ul>
      <h5>{{ info.weather[0].description }}</h5>
    </div>
    <div v-if="error" class="error">
      <h3>{{ error }}</h3>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      city: "",
      info: undefined,
      error: undefined,
      ip: undefined
    };
  },
  methods: {
    getWeather: function() {
      axios
        .get(
          // the url of API
          "http://api.openweathermap.org/data/2.5/weather?q=" +
            this.city +
            "&APPID=7bf97b089ffac7ed14c8ece93eafa3a7"
        )
        .then(
          // Assign the response to info varible and empty the error
          response => ((this.info = response.data), (this.error = undefined))
        )
        .catch(
          () => (
            // Assign the invalid message to error varible and empty the info
            (this.info = undefined),
            (this.error = "please Enter valid city name")
          )
        );
    }
  },
  computed: {
    temp() {
      // convert kilvin to celsius for current tempreture
      return (this.info.main.temp - 273.15).toFixed(1);
    },
    temp_min() {
      // convert kilvin to celsius for min tempreture
      return (this.info.main.temp_min - 273.15).toFixed(1);
    },
    temp_max() {
      // convert kilvin to celsius for max tempreture
      return (this.info.main.temp_max - 273.15).toFixed(1);
    }
  },
  created() {
    axios
      // to get the IP Address
      .get("https://www.cloudflare.com/cdn-cgi/trace")
      .then(
        response => (this.ip = response.data.split("\n")[2].replace("ip=", ""))
      );
  },
  watch: {
    ip: function() {
      axios
        // to get the current city of user
        .get("https://ipinfo.io/" + this.ip + "/json?token=1682e6cc695f57")
        .then(response => (this.city = response.data.city));
      setTimeout(function() {
        document.getElementById("click").click();
      }, 500);
    }
  }
};
</script>

<style lang="scss" scoped>
.weather {
  background-color: darkblue;
  color: #eee;
  padding: 80px 0;
  text-align: center;

  h3 {
    font-size: 30px;
    margin-bottom: 15px;
  }

  p {
    color: #999;
  }

  form {
    margin: 20px 0;

    input {
      padding: 10px 20px;
      border: none;
      width: 40%;
    }

    button {
      padding: 10px 20px;
      border: none;
      background-color: darkorchid;
      color: #fff;
      width: 20%;
    }
  }

  .city {
    h4 {
      font-size: 30px;
      margin: 10px 0;
    }

    h3 {
      font-size: 36px;
      margin: 10px 0;
    }

    h5 {
      font-size: 24px;
      margin: 10px 0;
    }

    ul {
      list-style: none;

      li {
        display: inline-block;
        margin: 10px;
        font-size: 20px;
      }
    }
  }
}
</style>
