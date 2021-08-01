<template>
  <div id="app">
    <main>
      <div class="search-box">
        <input
          type="text"
          name=""
          id=""
          class="search-bar"
          placeholder="Search..."
          v-model="query"
          v-on:keypress="fetchWeather"
        />
      </div>
      <div class="weather-wrap" v-if="typeof weather.main != 'undefined'">
        <div class="location-box">
          <div class="location">
            {{ weather.name }},{{ weather.sys.country }}
          </div>
          <div class="date">sunday 31 july 2021</div>
        </div>
        <div class="weather-box">
          <div class="temperature">21°c</div>
          <div class="weather">Rain</div>
        </div>
      </div>
    </main>
  </div>
</template>

<script>
export default {
  name: "app",
  data() {
    return {
      api_key: "452c6ecd93ac4727195d01a0fd56a54a",
      url_base: "https://api.openweathermap.org/data/2.5/",
      query: "",
      weather: {},
    };
  },
  methods: {
    fetchWeather(e) {
      if (e.key == "Enter") {
        fetch(
          `${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`
        )
          .then((result) => {
            return result.json();
          })
          .then(this.setResults);
      }
    },
    setResults(results) {
      this.weather = results;
    },
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
:root {
  --duration: 0.4s;
}
body {
  font-family: fantasy;
  background-image: linear-gradient(
    to bottom,
    rgba(0, 0, 0, 0.89),
    rgba(0, 0, 0, 1)
  );
}
#app {
  background-image: url("./assets/cold-bg.jpg");
  background-repeat: no-repeat;
  background-position: center;
  background-size: contain;
  transition: 0.4s;
  -moz-animation: appEaseIn var(--duration) ease-in forwards;
  -webkit-animation: appEaseIn var(--duration) ease-in forwards;
  animation: appEaseIn var(--duration) ease-in forwards;
}
@keyframes appEaseIn {
  0% {
    opacity: 0;
  }
  10% {
    opacity: 0.001;
  }
  50% {
    opacity: 0.05;
  }
  70% {
    opacity: 0.1;
  }
  80% {
    opacity: 0.15;
  }
  90% {
    opacity: 0.2;
  }
  100% {
    opacity: 1;
  }
}

main {
  min-height: 100vh;
  padding: 1.5%;
  background-image: linear-gradient(
    to bottom,
    rgba(0, 0, 0, 0.1),
    rgba(0, 0, 0, 0.35)
  );
}

.search-box {
  width: 25%;
  margin-bottom: 2%;
}
.search-box .search-bar {
  display: block;
  width: 100%;
  padding: 1%;
  color: #313131;
  font-size: 20px;
  border: none;
  appearance: none;
  outline: none;
  background: none;
  box-shadow: 0px 0px 8px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.5);
  border-radius: 0px 16px 0px 16px;
  transition: 0.4s;
}
.search-box .search-bar:focus {
  box-shadow: 0px 0px 16px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.75);
  border-radius: 16px 0px 16px 0px;
}
.location-box .location {
  color: #fff;
  font-size: 6vh;
  font-weight: 500;
  text-align: center;
  text-shadow: 1px 3px rgba(0, 0, 0, 0.25);
}
.location-box .date {
  color: #fff;
  font-size: 2vh;
  font-weight: 300;
  text-align: center;
  font-style: italic;
}
.weather-box {
  text-align: center;
}
.weather-box .temperature {
  display: inline-block;
  padding: 10px 25px;
  color: #fff;
  font-size: 10vh;
  font-weight: 900;
  text-shadow: 3px 6px rgba(0, 0, 0, 0.45);
  background-color: rgba(255, 255, 255, 0.1);
  border-radius: 16px;
  margin: 2% 0;
  box-shadow: 3px 6px rgba(0, 0, 0, 0.45);
}
.weather-box .weather {
  color: #fff;
  font-size: 5vh;
  font-weight: 500;
  font-style: italic;
  text-shadow: 3px 6px rgba(0, 0, 0, 0.45);
  margin: -0.5% 0;
}
</style>
