<template>
  <div class="row">
    <!-- 1st column -->
    <div class="col-1">
      <div class="card mt-4 ms-2 p-1">
        <i class="fa-solid text-primary fa-wind border top fa-1x mt-3"></i>
        <i class="fa-solid fa-cloud-sun-rain weath text-center"></i>
        <h6 class="text-center">Weather</h6>
        <i class="fa-solid fa-bars text-center bar"></i>
        <h6 class="text-center">Cities</h6>
        <i class="fa-solid fa-map text-center map"></i>
        <h6 class="text-center">Map</h6>
        <i class="fa-solid fa-sliders text-center setting"></i>
        <h6 class="text-center bottom">Setting</h6>
      </div>
    </div>
    <!-- 2nd Column -->
    <div class="col-7">
      <div class="input-control">
        <input
          placeholder="search for cities"
          type="text"
          v-model="query"
          @keypress="fetchWeather"
        />
      </div>
      <div class="weather-wrap" v-if="typeof weather.main != 'undefined'">
        <div class="location-box">
          <div class="location">
            {{ weather.name }}, {{ weather.sys.country }}
          </div>
          <div class="date">{{ dateBuilder() }}</div>
        </div>
        <div class="weather-box d-flex">
          <div class="temp">{{ Math.round(weather.main.temp) }}°C</div>
          <div class="mx-auto">
            <img
              max-height="100"
              max-width="100"
              :src="`https://openweathermap.org/img/wn/${weather.weather[0].icon}@4x.png`"
            />
            
          </div>
        </div>
      </div>
      <div class="alert alert-dismissible alert-secondary">
        <h6>Hourly Forecast</h6>
        <div class="d-flex">
          <div>
            <h6 class="ms-3">{{ this.dt }}</h6>

            <img
              max-height="30"
              max-width="30"
              :src="`https://openweathermap.org/img/wn/${this.icon}@2x.png`"
            />
            <h6 class="ms-3">{{ this.temp }}°C</h6>
          </div>
          <div>
            <h6>{{ this.dt2 }}</h6>

            <img
              max-height="30"
              max-width="30"
              :src="`https://openweathermap.org/img/wn/${this.icon2}@2x.png`"
            />
            <h6>{{ this.temp2 }}°C</h6>
          </div>
          <div>
            <h6>{{ this.dt3 }}</h6>

            <img
              max-height="30"
              max-width="30"
              :src="`https://openweathermap.org/img/wn/${this.icon3}@2x.png`"
            />
            <h6>{{ this.temp3 }}°C</h6>
          </div>
          <div>
            <h6>{{ this.dt4 }}</h6>

            <img
              max-height="30"
              max-width="30"
              :src="`https://openweathermap.org/img/wn/${this.icon4}@2x.png`"
            />
            <h6>{{ this.temp4 }}°C</h6>
          </div>
          <div>
            <h6>{{ this.dt5 }}</h6>

            <img
              max-height="30"
              max-width="30"
              :src="`https://openweathermap.org/img/wn/${this.icon5}@2x.png`"
            />
            <h6>{{ this.temp5 }}°C</h6>
          </div>
          <div>
            <h6>{{ this.dt6 }}</h6>

            <img
              max-height="30"
              max-width="30"
              :src="`https://openweathermap.org/img/wn/${this.icon6}@2x.png`"
            />
            <h6>{{ this.temp6 }}°C</h6>
          </div>
          <div>
            <h6>{{ this.dt7 }}</h6>

            <img
              max-height="30"
              max-width="30"
              :src="`https://openweathermap.org/img/wn/${this.icon7}@2x.png`"
            />
            <h6>{{ this.temp7 }}°C</h6>
          </div>
        </div>
      </div>
    </div>
    <!-- 3rd column -->
    <div class="col-3">
      <div class="list-group last" v-if="typeof weather.main != 'undefined'">
        <a href="#" class="list-group-item list-group-item-action"
          >Feel like
          <p class="feels">{{ weather.main.feels_like }}°C</p></a
        >
        <a href="#" class="list-group-item list-group-item-action"
          >Description
          <p class="feels">{{ weather.weather[0].description }}</p></a
        >
        <a href="#" class="list-group-item list-group-item-action"
          >Speed
          <p class="feels">{{ weather.wind.speed }}km/h</p></a
        >
        <a href="#" class="list-group-item list-group-item-action"
          >Humidity
          <p class="feels">{{ weather.main.humidity }}%</p></a
        >
        <a href="#" class="list-group-item list-group-item-action"
          >Pressure
          <p class="feels">{{ weather.main.pressure }}hpa</p></a
        >
        <a href="#" class="list-group-item list-group-item-action"
          >Wind
          <p class="feels">1km/h</p></a
        >
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "weatherApp",
  data() {
    return {
      api_key: "6240187100620a16cd75dc11a45f81cb",
      url_base: "https://api.openweathermap.org/data/2.5/",
      query: "",
      weather: {},
      list: {},
      dt: "",
      temp: "",
      icon: "",
      dt2: "",
      temp2: "",
      icon2: "",
      dt3: "",
      temp3: "",
      icon3: "",
      dt4: "",
      temp4: "",
      icon4: "",
      dt5: "",
      temp5: "",
      icon5: "",
      dt6: "",
      temp6: "",
      icon6: "",
      dt7: "",
      temp7: "",
      icon7: "",
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

      if (e.key == "Enter") {
        fetch(
          `${this.url_base}forecast?q=${this.query}&units=metric&APPID=${this.api_key}`
        )
          .then((res) => {
            return res.json();
          })
          .then((data) => {
            console.log(data.list[1].weather[0].icon);
            // 1st data
            this.dt = data.list[0].dt_txt.slice(10);
            this.temp = data.list[0].main.temp;
            this.icon = data.list[0].weather[0].icon;
            // 2nd data
            this.dt2 = data.list[1].dt_txt.slice(10);
            this.temp2 = data.list[1].main.temp;
            this.icon2 = data.list[1].weather[0].icon;
            // 3rd data
            this.dt3 = data.list[2].dt_txt.slice(10);
            this.temp3 = data.list[2].main.temp;
            this.icon3 = data.list[2].weather[0].icon;
            // 4th data
            this.dt4 = data.list[3].dt_txt.slice(10);
            this.temp4 = data.list[3].main.temp;
            this.icon4 = data.list[3].weather[0].icon;
            // 5th data
            this.dt5 = data.list[4].dt_txt.slice(10);
            this.temp5 = data.list[4].main.temp;
            this.icon5 = data.list[4].weather[0].icon;
            // 6th data
            this.dt6 = data.list[5].dt_txt.slice(10);
            this.temp6 = data.list[5].main.temp;
            this.icon6 = data.list[5].weather[0].icon;
            // 7th data
            this.dt7 = data.list[6].dt_txt.slice(10);
            this.temp7 = data.list[6].main.temp;
            this.icon7 = data.list[6].weather[0].icon;
          });
      }
    },
    setResults(results) {
      this.weather = results;
    },
    setForecast(result) {
      this.list = result;
      console.log(this.list);
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
    // hourlyForecast(e){
    //     if (e.key =="Enter"){
    //         fetch(`${this.url_base}forecast?q=${this.query}&units=metric&APPID=${this.api_key}`)
    //         .then(res=>{
    //             return res.json();
    //         }).then((data)=>{
    //             console.log(data.list[0].main.temp)
    //             this.dt=data.list[0].dt_txt.slice(0,9)
    //             this.temp=data.list[0].main.temp
    //         })
    //     }
    // }
  },
};
</script>

<style>
.card {
  background-color: rgb(233, 231, 231);
}
.top {
  width: 30px;
  padding: 5px;
  margin-right: 5px;
  border-radius: 5px;
  margin-left: 19px;
  background-color: rgb(206, 206, 206);
}

.weath {
  margin-top: 70px;
}

.bar {
  margin-top: 30px;
}

.map {
  margin-top: 30px;
}

.setting {
  margin-top: 30px;
}

/* 2nd column */
.input-control {
  display: flex;
  flex-direction: column;
}

.input-control input {
  border: 2px solid rgb(233, 231, 231);
  border-radius: 6px;
  display: block;
  font-size: 12px;
  padding: 10px;
  width: 100%;
  background-color: rgb(233, 231, 231);
  color: black;
  margin-top: 20px;
}

.input-control input:focus {
  outline: 0;
}

.location-box .location {
  color: black;
  font-size: 32px;
  font-weight: 500;

  text-shadow: 1px 3px rgba(0, 0, 0, 0.25);
}

.location-box .date {
  color: black;
  font-size: 20px;
  font-weight: 300;
  font-style: italic;
}

.weather-box {
  text-align: center;
}

.weather-box .temp {
  display: inline-block;
  padding: 10px 25px;
  font-size: 102px;
  font-weight: 900;
  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);

  border-radius: 16px;
  margin: 30px 0px;
  box-shadow: rgba(143, 140, 140, 0.25);
}

.weather-box .weather {
  color: black;
  font-size: 48px;
  font-weight: 700;
  font-style: italic;
  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}

.feel {
  margin-top: 30px;
}

/* 3rd column */
.last {
  margin-top: 23px;
}

.feels {
  margin-left: 190px;
  margin-top: -20px;
}

.bottom {
  margin-bottom: 200px;
}
</style>
