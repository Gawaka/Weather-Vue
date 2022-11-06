<template>
  <div class="wrapper">
    <div class="wrapper__content">
    <div class="title">
      <h1>Weather App</h1>
      <span>
        check the weather in  
        {{ city == "" ? "your city" 
        :cityName }}
      </span>
    </div>
    <div class="nav">
      <input class="nav__input" 
        type="text" 
        placeholder="your city" 
        v-model="city">
      <my-button v-if="city != ''" 
        @click="getWeather()"
        type="submit"
      >
        Search
      </my-button>
      <my-button
        disabled
        v-else
      >
        Сhoose your city
      </my-button>
    </div>
    <p class="error">{{ error }}</p>
    <div class="nav__info">
      <div class="weather" v-if="info != null">
        <p>{{ showTemp }}</p>
        <p>{{ showFeelFike }}</p>
        <p>{{ showMinTemp }}</p>
        <p>{{ showMaxTemp }}</p>
        <p>{{ showHumidity }}</p>
      </div>
    </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import MyButton from "@/components/MyButton.vue";

export default {
  components: {
    MyButton,
  },
    data() {
      return {
        city: '',
        error: '',
        info: null,
      }
    },
    computed: {
      cityName() {
        return "«" + this.city + "»"
      },
      showTemp() {
        return "Temperature: " + this.info.main.temp + "°"
      },
      showFeelFike() {
        return "Feels like: " + this.info.main.feels_like + "°"
      },
      showMinTemp() {
        return "Min temperature: " +  this.info.main.temp_min + "°"
      },
      showMaxTemp() {
        return "Max temperature: " + this.info.main.temp_max + "°"
      },
      showHumidity() {
        return "Humidity: " + "   " + this.info.main.humidity + "%"
      },
    },
    methods: {
      getWeather() {
        if(this.city.trim().length < 2) {
          this.error = "too short name :("
          return false
        }
        this.error = "";
        axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${this.city}&units=metric&appid=fab4c5932e221273664ee40bf1704901`)
          .then(res => (this.info = res.data))
    }
  }
};
</script>

<style lang="scss" scoped>

.wrapper {
  padding: 20px;
  margin: auto;
  background: #525252;
  width: 370px;
  height: 400px;
  border-radius: 50px;
  opacity: 0.9;

  @media only screen and (min-width: 768px) {
    width: 600px;
  }

  @media only screen and (min-width: 1024px) {
    width: 900px;
  }
}

.title {
  color: wheat;
  padding-top: 20px;
  text-align: center;
  letter-spacing: 0.08em;

  span {
    padding-top: 15px;
    letter-spacing: 0.1em;
  }
}

.nav {
  padding-top: 20px;
  text-align: center;
  display: flex;
  justify-content: center;
  gap: 15px;

  &__input {
    width: 200px;
    height: 30px;
    background: rgb(168,233,255);
    border: none;
    outline: none;
    border-radius: 10px;
    text-align: center;
  }

  &__input::placeholder {
    text-align: center;
    opacity: 0.3;
    color: #1f1f1f;
  }

  &__input:focus::placeholder {
    color: transparent;
  }

  &__info {
    padding-top: 30px;
    display: flex;
    flex-direction: column;
    justify-content: center;
    text-align: center;
  }
}

.weather {
  margin: 0 auto;
  display: flex;
  flex-direction: column;
  align-items: flex-start;
}

.error {
  padding-top: 40px;
  font-size: 30px;
  color: red;
  text-align: center;
}
</style>
