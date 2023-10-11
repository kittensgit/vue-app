<script>
import axios from 'axios';
export default {
    data() {
        return {
            city: '',
            error: '',
            info: null,
        };
    },
    computed: {
        cityName() {
            return '«' + this.city + '»';
        },
        showTemp() {
            return 'temperature: ' + this.info.main.temp;
        },
        showFeelsLike() {
            return 'feels like: ' + this.info.main.feels_like;
        },
        showMinTemp() {
            return 'min temperature: ' + this.info.main.temp_min;
        },
        showMaxTemp() {
            return 'max temperature: ' + this.info.main.temp_max;
        },
    },
    methods: {
        getWeather() {
            if (this.city.trim().length < 2) {
                this.error = 'Need more than one character name';
                return false;
            }

            this.error = '';

            axios
                .get(
                    `https://api.openweathermap.org/data/2.5/weather?q=${this.city}&units=metric&appid=cbf7feaaafe60e2be6038d48a828d9c9`
                )
                .then((res) => (this.info = res.data));
        },
    },
};
</script>

<template>
    <div class="wrapper">
        <h1>Weather app</h1>
        <p>
            Find out the weather in
            {{ city == '' ? 'your city' : cityName }}
        </p>
        <input type="text" v-model="city" placeholder="Enter city" />
        <!-- <button v-show="city !== ''">Get weather</button> -->
        <button v-if="city !== ''" @click="getWeather()">Get weather</button>
        <button v-else disabled>Enter the name city</button>
        <p class="error">{{ error }}</p>
        <div v-if="info !== null">
            <p>{{ showTemp }}</p>
            <p>{{ showFeelsLike }}</p>
            <p>{{ showMinTemp }}</p>
            <p>{{ showMaxTemp }}</p>
        </div>
    </div>
</template>

<style scoped>
.error {
    color: #d03939;
}
.wrapper {
    width: 900px;
    height: 500px;
    border-radius: 50px;
    background: #1f0f24;
    padding: 20px;
    text-align: center;
    color: white;
}

.wrapper h1 {
    margin-top: 20px;
}
.wrapper p {
    margin-top: 20px;
}
.wrapper input {
    margin-top: 30px;
    background: transparent;
    border: 0;
    border-bottom: 2px solid #110813;
    color: #fcfcfc;
    font-size: 14px;
    padding: 5px 8px;
    outline: none;
    transition: all 0.2s ease-in;
}
.wrapper input:focus {
    border-bottom-color: #6e2d7d;
}
.wrapper button {
    background: #e3bc4b;
    color: white;
    border-radius: 10px;
    border: 2px solid #b99935;
    padding: 10px 15px;
    margin-left: 20px;
    cursor: pointer;
    transition: transform 500ms ease;
}
.wrapper button:disabled {
    background: #746027;
    cursor: not-allowed;
}
.wrapper button:hover {
    transform: scale(1.1) translateY(-5px);
}
</style>
