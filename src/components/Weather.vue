<template>
    <div class="bg-image">
        <div class="main" v-bind:class="{ warm: state_weather}">
            <div class="container py-5">
                <div class="row justify-content-center">
                    <div class="col-xl-4 col-lg-4 col-md-4 col-sm-10 ">
                        <div class="row header" v-if="data.weather">
                            <div class="col-12 mb-5">
                                <input class="search-btn" type="text" placeholder="Search City..." v-model="data.city" @keyup.enter="getApi()">
                            </div>
                            <div class="col-12 text-grey">
                                <h2 style="font-size: 30px;">
                                    <span>
                                        <i class="logo-loc bi bi-geo-alt-fill"></i>
                                    </span> 
                                    {{ data.weather.name }}
                                </h2>
                                <h6 class="mt-1">{{ new Date().toLocaleString() }}</h6>
                            </div>
                            <div class="col-12 temperature p-5 mt-5">
                                <div class="row">
                                    <div class="col-sm-12 col-md-6 col-lg-6 d-flex align-items-center justify-content-center">
                                        <h1>
                                            <i style="font-size: 90px; color: white;" class="bi bi-cloud-sun-fill"></i>
                                        </h1>
                                    </div>
                                    <div class="col">
                                        <h1 style="font-size: 60px;">{{ Math.round(data.weather.main.temp) }}&deg;C</h1>
                                        <h1 style="font-size: 24px;">{{ data.weather.weather[0].main }}</h1>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios'

export default {
    name: 'Weather',
    props: {
    },
    data() {
        return {
            data: {
                weather: null,
                city: '',
                api_key: '67022d645376218e49d880e9c0e0069a',
                current_day:'',
                state_weather: false,
            }
        }
    },
    mounted: async function(){
        this.getApi()
    },
    methods: {
        async getApi() {
            if (this.data.city === ''){
                this.data.city = 'jakarta'
            }
            const getWeather = await axios.get(
                `https://api.openweathermap.org/data/2.5/weather?units=metric&q=${ this.data.city }&appid=${ this.data.api_key}`
            )
            this.data.weather = getWeather.data
            this.data.city = ''
            if (this.data.weather.main.temp > 16){
                this.state_weather = true; 
            }else {
                this.state_weather = false;
            }
            console.log(this.data.weather);
        }
    },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.bg-image {
    background-image: url('https://mdbootstrap.com/img/Photos/Others/images/76.jpg');
    min-height: 100vh; 
    background-size: cover;
}

.search-btn {
    border-radius: 30px;
    width: 100%;
    padding: 16px 30px;
    background-color: #343434;
    border: none;
    appearance: none;
    outline: none;
    color: white;
    filter: drop-shadow(0px 4px 4px rgba(0, 0, 0, 0.25));
}

.logo-loc{
    color: #CE2828;
}

.text-grey {
    color: #343434;
}

.temperature {
    background: rgba(189, 189, 189, 0.45);
    box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25);
    border-radius: 30px;
}

.logo-state {
    color: #FFFFFF;
}
.temperature>.row>h1{
    font-size: 100px;
}
#app {
    /* background-image: url('@/assets/bg.jpg'); */
    background-size: cover;
    background-position: bottom;
    transition: 0.4s;
}

.main {
    min-height: 100vh;
    padding: 25px;
    background-image: linear-gradient(to bottom,rgba(169, 172, 204, 0.30), rgba(2,15,22,0.55));
}
.main.warm {
    min-height: 100vh;
    padding: 25px;
    background-image: linear-gradient(to bottom,rgba(0, 0, 0, 0.30), rgba(2,15,22,0.55));
}

.header {
    /* padding-top: 20px; */
    color: azure;
    box-shadow: rgba(3,3,3,0.3);
}

.temp {
    display: inline-block;
    /* padding: 10px, 25px; */
    color: white;
    font-size: 100px;
    font-weight: 900;
    text-shadow: 3px 6px rgba(0,0,0,0.25);

    background-color: rgba(255,255,255,0.25);
    border-radius: 16px;
    margin: 30px 0px;
    box-shadow: 3px 6px rgba(0,0,0,0.25);
}
.temp>h1 {
    font-size: 100px;
}
.state>h1{
    font-size: 20px;
    margin-top: -20px;
}
.state>i {
    font-size: 60px;
}
</style>
