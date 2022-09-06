<script>
export default {
  name: "app",
  data() {
    return {
      api_key: "0633e5bec8a11c5d314f8116cc4239d9",
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
          .then((res) => {
            return res.json();
          })
          .then(this.setResults);
      }
    },
    setResults(results) {
      this.weather = results;
    },
    dateBuilder() {
      let d = new Date();
      let months = [
        "January",
        "February",
        "March",
        "April",
        "May",
        "June",
        "July",
        "August",
        "September",
        "October",
        "November",
        "December",
      ];
      let days = [
        "Sunday",
        "Monday",
        "Tuesday",
        "Wednesday",
        "Thursday",
        "Friday",
        "Saturday",
      ];
      let day = days[d.getDay()];
      let date = d.getDate();
      let month = months[d.getMonth()];
      let year = d.getFullYear();
      return `${day} ${date} ${month} ${year}`;
    },
  },
};
</script>

<template>
  <div id="app" :class="typeof weather.main != 'undefined' && weather.main.temp > 16 ? 'warm' : ''">
    <main>
      <div class="search-box">
        <input type="text" class="search-bar" placeholder="Search.." v-model="query" @keypress="fetchWeather" />
      </div>
      <div class="weather-info" v-if="typeof weather.main != 'undefined'">
        <div class="weather-info-1">
          <div class="location">
            {{ weather.name }} , {{ weather.sys.country }}
          </div>
          <div class="date">{{ dateBuilder() }}</div>
        </div>
        <div class="weather-info-2">
          <div class="temp">{{ Math.round(weather.main.temp) }} °C</div>
          <div class="weather">{{ weather.weather[0].main }}</div>
        </div>
      </div>
      <!-- <div class="mode">
        <img @click= "changeBg"  src="./assets/mode.png" alt="">
      </div> -->
    </main>
  </div>
</template>
0

<style>
@import url("https://fonts.googleapis.com/css2?family=Merienda&display=swap");

/* @media screen and (max-width: ;) */

* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}


#app.warm {
  background-image: url('./assets/warm.jpg');
}

#app {
  background-image: url("./assets/uwp1344596.jpg");
  background-size: cover;
  background-position: bottom;
  transition: all 0.4s ease-in-out;
  background-repeat: no-repeat;
  animation: Load4 10s ease-in-out infinite;
}

@keyframes Load4 {
  0% {
    filter: grayscale(0);
  }

  20% {
    filter: grayscale(0.2);
  }

  40% {
    filter: grayscale(0.4);
  }

  50% {
    filter: grayscale(0.6);
  }

  60% {
    filter: grayscale(0.4);
  }

  80% {
    filter: grayscale(0.2);
  }

  100% {
    filter: grayscale(0);
  }
}


@keyframes Load {
  0% {
    transform: translateY(-100%) scaleY(0);
  }

  20% {
    opacity: 0.2;
  }

  40% {
    opacity: 0.4;
  }

  60% {
    opacity: 0.6;
  }

  80% {
    opacity: 0.8;
  }

  100% {
    transform: translateY(0%) scaleY(1);
    opacity: 1;
  }
}

main {
  transition: all 0.4s ease-in-out;
  padding: 25px;
  min-height: 100vh;
  background: rgba(18, 11, 35, 0.437);
  animation: Load 1s ease-in-out;
}

.search-box {
  display: flex;
  align-items: center;
  justify-content: center;
  text-align: center;
  position: relative;
  top: 40px;
  /* transform: translateY(50%); */
}

::placeholder {
  text-align: center;
  color: black;
  opacity: 100% !important;
}

.search-bar {
  width: 25rem;
  height: 40px;
  border-radius: 0px 8px 0px 8px;
  opacity: 50%;
  box-shadow: 5px 0px 25px 4px rgba(0, 0, 0, 0.76);
  -webkit-box-shadow: 5px 0px 25px 4px rgba(0, 0, 0, 0.76);
  -moz-box-shadow: 5px 0px 25px 4px rgba(0, 0, 0, 0.76);
  border: none;
  outline: none;
  padding: 5px;
  transition: all 0.4s ease-in-out;
}

.weather-info {
  transition: all 0.4s ease-in-out;
  display: flex;
  flex-direction: column;
  position: relative;
  align-items: center;
  justify-content: center;
  margin-top: 5rem;
  padding: 20px;
  animation: Load3 0.4s ease-in-out;
  margin-right: 10px;
}

@keyframes Load3 {
  0% {
    opacity: 0;
  }

  100% {
    opacity: 0;
  }
}

.weather-info-1 .location {
  color: white;
  transition: all 0.4s ease-in-out;
  font-size: 50px;
  font-family: "Gill Sans", "Gill Sans MT", Calibri, "Trebuchet MS", sans-serif;
  /* font-style: italic; */
  text-shadow: 5px 2px 8px #100704;
}

/* 
.weather-info-1 .location:hover {
  transition: all .4s ease-in-out;
  text-shadow: 5px 2px 8px #100704;
  background-color: rgb(255, 255, 255, 0.35);
  border-radius: 10px;
  padding: 10px;
  box-shadow: 10px 10px 5px -2px rgba(0, 0, 0, 0.75);
  -webkit-box-shadow: 10px 10px 5px -2px rgba(0, 0, 0, 0.75);
  -moz-box-shadow: 10px 10px 5px -2px rgba(0, 0, 0, 0.75);
} */

.weather-info-1 .date {
  color: white;
  font-size: 20px;
  transition: all 0.4s ease-in-out;
  /* font-style: italic; */
  /* padding-left: 5rem; */
  font-family: "Gill Sans", "Gill Sans MT", Calibri, "Trebuchet MS", sans-serif;
  text-shadow: 5px 2px 8px #100704;
  opacity: 0.7;
  padding-top: 1rem;
  padding-bottom: 1rem;
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
}

/* .weather-info-1 .date:hover{
  transition: all .4s ease-in-out;
  text-shadow: 5px 2px 8px #100704;
  background-color: rgb(255, 255, 255, 0.35);
  border-radius: 10px;
  padding: 10px;
  box-shadow: 10px 10px 5px -2px rgba(0, 0, 0, 0.75);
  -webkit-box-shadow: 10px 10px 5px -2px rgba(0, 0, 0, 0.75);
  -moz-box-shadow: 10px 10px 5px -2px rgba(0, 0, 0, 0.75); 
  color: rgb(204, 42, 199);
}  */

.weather-info-2 .temp {
  transition: all 0.4s ease-in-out;
  color: white;
  font-size: 70px;
  font-family: "Gill Sans", "Gill Sans MT", Calibri, "Trebuchet MS", sans-serif;
  font-style: italic;
  padding: 2rem;
  margin: 1rem;
  text-shadow: 5px 2px 8px #100704;
  background-color: rgb(255, 255, 255, 0.35);
  border-radius: 20px;
  box-shadow: 10px 10px 5px -2px rgba(0, 0, 0, 0.75);
  -webkit-box-shadow: 10px 10px 5px -2px rgba(0, 0, 0, 0.75);
  -moz-box-shadow: 10px 10px 5px -2px rgba(0, 0, 0, 0.75);
}

.weather-info-2 .temp:hover {
  transition: all 0.4s ease-in-out;
  background-color: rgb(21, 14, 21);
}

.weather {
  display: flex;
  transition: all 0.4s ease-in-out;
  color: white;
  font-size: 50px;
  justify-content: center;
  align-items: center;
  text-transform: uppercase;
  /* font-style: italic; */
  font-weight: 590;
  padding-left: 20px;
  margin-right: 1.5rem;
  font-family: Impact, Haettenschweiler, "Arial Narrow Bold", sans-serif;
  padding-top: 1rem;
  letter-spacing: 2px;
  text-shadow: 5px 2px 8px #100704;
}

.search-bar:focus {
  opacity: 90%;
  box-shadow: 5px 0px 25px 4px rgba(0, 0, 0, 0.96);
  -webkit-box-shadow: 5px 0px 25px 4px rgba(0, 0, 0, 0.96);
  -moz-box-shadow: 5px 0px 25px 4px rgba(0, 0, 0, 0.96);
}
</style>
