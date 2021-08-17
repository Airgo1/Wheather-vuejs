<template>
  <div id="app container">
    <div>
      Wheather App
    </div>

    <template class="form">
        <b-form-input type="text" v-model="queryCity" placeholder="Enter your name" class="input"></b-form-input>
        <b-button v-on:click="getCity" class="button" >Recherche</b-button>
        <b-button v-on:click="getCoord" class="button">Localisation</b-button>
    </template>
   
    <section class="app">
      <div>
        <Forecast v-bind:city="this.city" v-bind:geo="this.geo" class="WeatherApp" :class="period"></Forecast>
        <b-button  v-on:click="addFavoite" class="button">Ajouter au favoris</b-button>
      </div>
      <!-- <div>
        <div v-if='coord == null || cityFind == null' class="p-4">
          <b-icon icon="clock" animation="spin" font-scale="4" shift-v="8" class="wait"></b-icon>
        </div>
        <b-card v-else
          title="Carte postale"
          img-src="https://picsum.photos/600/300/?image=25"
          img-alt="Image"
          img-top
          tag="article"
          style="max-width: 20rem;"
          class="card">
          <b-card-text>
            Description de la région
          </b-card-text>

          <b-button  v-on:click="addFavoite" class="button">Ajouter au favoris</b-button>
        </b-card>
      </div> -->
    </section>

    <section class="app">
      <Forecast v-for="histoOne in cityHistory" v-bind:city="histoOne.city" v-bind:geo="histoOne.geo" v-bind:key="histoOne.city" class="WeatherApp"  :class="period" ></Forecast>
    </section>

    <section>
      <AppCredits :year="year"></AppCredits>
    </section>
  </div>
</template>

<script>
import Forecast from '@/components/weathercomponent/Forecast'
import AppCredits from '@/components/AppCredits'

export default {
  name: 'App',
  components: {
    Forecast,
    AppCredits
  },

  data () {
    return {
      date: new Date(),
      queryCity: "",
      geo: true,
      city: "caen",
      cityHistory: [],
      coord: null,
      cityFind: null
    }
  },

  computed: {
    year () {
      return this.date.getFullYear()
    },
    period () {
      let hour = this.date.getHours()

      return (hour > 5 && hour < 18) ? 'app--day' : 'app--night'
    },
  },
  methods: {
    getCity () {
      console.log(this.queryCity)
      if(this.queryCity != "") {
        this.geo = false
        this.city = this.queryCity
      } 
    },
    getCoord () {
      this.geo = true
      this.city = ""
    },
    addFavoite () {
      this.cityHistory.push(
        { 
          city: this.city,
          geo: this.geo
        }
      )
    }
  }
}
</script>

<style>
/** Global **/
@import url('https://fonts.googleapis.com/css?family=Open+Sans');

* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: 'Open Sans', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: rgba(255, 255, 255, 0.9);
}

a {
  text-decoration: none;
  color: inherit;
  transition: color .2s ease-in;
}

/** container **/
.container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100%;
}

/** App **/
.app {
  display: flex;
  justify-content: center;
  align-items: center;
}

/** Form **/
.form {
  margin: 10px;
}
.app--day {
  /*background: linear-gradient(to bottom right, #6CB9C8, #6CB9C8) no-repeat;*/
  background-color: #6CB9C8;
}

.app--night {
  /*background: linear-gradient(to bottom right, #484F60, #484F60) no-repeat;*/
  background-color: #484F60;
}

.app--day a:hover {
  color: rgba(46, 146, 167, 0.9);
}

.app--night a:hover {
  color: rgba(0, 0, 0, 0.5);
}

.WeatherApp {
  margin: 10px;
}

.button {
  margin: 10px;
}
.wait {
  margin-left: 50px;
}
</style>
