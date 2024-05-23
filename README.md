<html lang="en">
<head>
 <meta charset="UTF-8">
 <meta http-equiv="X-UA-Compatible" content="IE=edge">
 <meta name="viewport" content="width=device-width, initial-scale=1.0">
 <link rel="stylesheet" href="style.css">
 <title>Weather App</title>
</head>
<body>
 <div class="card">
  <div class="search">
   <input type="text" class="search-bar" placeholder="Search">
   <button><svg stroke="currentColor" fill="currentColor" stroke-width="0" viewBox="0 0 16 16" height="1.5em" width="1.5em" xmlns="http://www.w3.org/2000/svg"><path fill-rule="evenodd" d="M10.442 10.442a1 1 0 011.415 0l3.85 3.85a1 1 0 01-1.414 1.415l-3.85-3.85a1 1 0 010-1.415z" clip-rule="evenodd"></path><path fill-rule="evenodd" d="M6.5 12a5.5 5.5 0 100-11 5.5 5.5 0 000 11zM13 6.5a6.5 6.5 0 11-13 0 6.5 6.5 0 0113 0z" clip-rule="evenodd"></path></svg></button>
  </div>

  <div class="weather loading">
   <h1 class="city">Weather in Lagos</h1>
   <h1 class="temp">51°C</h1>
   <div class="flex">
    <img src="//cdn.weatherapi.com/weather/64x64/day/116.png" alt="" class="icon">
    <div class="description">Cloudy</div>
   </div>
   <div class="humidity">Humidity:60%</div>
   <div class="wind">Wind Speed:6.2 km/hr</div>
  </div>
 </div>
 <script src="script.js"></script>

</body>
</html>

body {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    background: darkgrey;
    margin: 0;
    font-size: 120%;
    background-image: url("https://source.unsplash.com/1600x900/?nature,landscape");
    font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
   } 
   
   .card {
    background-color: black;
    padding: 2em;
    color: white;
    border-radius: 30px;
    width: 100%;
    max-width: 420px;
    margin: 1em;
    box-shadow: 1px 3px 5px rgba(141, 138, 138, 0.1);
   }
   
   .search {
    display: flex;
    align-items: center;
    justify-content: center;
   }
   input.search-bar {
    border: none;
    outline: none;
    padding: 0.4em 1em;
    border-radius: 30px;
    background-color: #534b4b;
    color: white;
    font-size: 120%;
    width: calc(100% - 100px);
    font-family: 'Roboto';
    letter-spacing: 2px;
   }
   
   button {
    margin: 0.5em;
    border-radius: 50%;
    border: none;
    height: 3em;
    width: 3em;
    outline: none;
    background-color: #534b4b;
    color: white;
    cursor: pointer;
    transition: 0.3s ease-in-out;
   }
   
   button:hover {
    background-color: #9b7979;
   }
   
   .weather {
    font-weight: bold;
   }
   
   .weather.loading {
    visibility: hidden;
    max-height: 20px;
    position: relative;
   }
   .weather.loading::after {
    position: absolute;
    top: 0;
    color: white;
    visibility: visible;
    content: "Page Loading...";
    font-weight: bold;
    left: 30px;
   }
   
   h1.city {
    letter-spacing: 2px;
    text-transform: uppercase;
    font-size: 1.3em;
   }
   
   h1.temp {
    margin: 0;
    margin-bottom: 0.5em;
    font-size: 1.3em;
   }
   
   .flex {
    display: flex;
    align-items: center;
    margin-left: -10px;
    margin-bottom: 0.5em;
   }
   .flex .description {
    text-transform: capitalize;
    margin-left: 8px;
   }
   
   .humidity {
    font-size: 1.2em;
    margin-bottom: 0.5em;
   }
   
   @media screen and (max-width: 420px) {
    .card {
      border-radius: 35px;
      max-width: 320px;
     }
   
    input.search-bar {
     padding: 0.3em 0.8em;
     border-radius: 30px;
     background-color: #534b4b;
     color: white;
     width: calc(100% - 100px);
     letter-spacing: 1px;
    }
   }

   let cityEl = document.querySelector(".city");

let iconEl = document.querySelector(".icon");

let descriptionEl = document.querySelector(".description");

let temperatureEl = document.querySelector(".temp");

let humidityEl = document.querySelector(".humidity");

let windEl = document.querySelector(".wind");

let searchBar = document.querySelector(".search-bar");

let searchEl = document.querySelector(".search button");

let weatherEl = document.querySelector(".weather");

let weather = {
 "apikey": "fb9a4868fe4f28b232a7658ccaa97136",

 fetchWeather: function (city) {
  fetch("http://api.weatherapi.com/v1/current.json?key=a6f6fef1470f473cb0694459230605%20&q=" + city + "&aqi=no").then((response) => response.json()).then((data) => this.displayWeather(data));
 },

 displayWeather: function (data) {
  const { name } = data.location;
  const { icon, text } = data.current.condition;

  const { temp_c, humidity } = data.current;

  const { wind_kph } = data.current;

  cityEl.innerText = `Weather in ${name}`;

  iconEl.src = icon;

  descriptionEl.innerText = text;

  temperatureEl.innerText = `Temperature: ${temp_c}°C`;

  humidityEl.innerText = `Humidity: ${humidity}%`;

  windEl.innerText = `Wind Speed: ${wind_kph} km/hr`;

  weatherEl.classList.remove("loading");

  document.body.style.backgroundImage = "url('https://source.unsplash.com/1600x900/?" + name + "')";
 },

 search: function () {
  this.fetchWeather(searchBar.value);
 }
};

searchEl.addEventListener("click", () => {
 console.log("Clicked!");
 weather.search();
});

searchBar.addEventListener("keyup", (event) => {
 if (event.key === "Enter") {
  weather.search();
 }
});

weather.fetchWeather("Lagos");
