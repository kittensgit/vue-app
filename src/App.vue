<script>
export default {
    data() {
        return {
            city: '',
        };
    },
};
</script>

<template>
    <div class="wrapper">
        <h1>Weather app</h1>
        <p>
            Find out the weather in
            {{ city == '' ? 'your city' : '«' + city + '»' }}
        </p>
        <input type="text" v-model="city" placeholder="Enter city" />
        <!-- <button v-show="city !== ''">Get weather</button> -->
        <button v-if="city !== ''">Get weather</button>
        <button v-else disabled>Enter the name city</button>
    </div>
</template>

<style scoped>
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
