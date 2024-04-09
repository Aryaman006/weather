<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<style>
    *{
        margin: 0;
        padding: 0;
        box-sizing: border-box;
        font-family: 'Poppins',sans-serif;
    }
    .card{
        width: 90%;
        max-width: 470px;
        background: linear-gradient(135deg,#00feba,#5b548a);
        color: #fff;
        margin: 50px auto 0;
        border-radius: 20px;
        padding: 40px 35px;
        text-align: center;
    }
    .search{
        width: 100%;
        display: flex;
        align-items: center;
        justify-content: space-between;
    }
    .search input{
        border: 0;
        outline: 0;
        background: #ebfffc;
        color: #555;
        padding: 10px 25px;
        height: 60px;
        border-radius: 30px;
        flex: 1;
        margin-left: 16px;
        font-size: 18px;
    }
    .search button{
        border: 0;
        outline: 0;
        background: #ebfffc;
        border-radius: 50%;
        width: 60px;
        height: 60px;
        cursor: pointer;
        overflow: hidden;
    }
    body{
        background-color: #212121;
    }
    .search img{
        width: 20px;
    }
    .weather{
        /* width: 170px; */
        margin-top: 50px;
    }
    .weather h1{
        font-size: 80px;
        font-weight: 500;
        margin-bottom: 10px;
    }
    .weather h2{
        font-size: 40px;
        font-weight: 400;
        margin-top: -10px;
    }
    .details{
        display: flex;
        align-items: center;
        justify-content: space-between;
        padding: 0 20px;
        margin-top: 50px;
    }
    .col{
        display: flex;
        align-items: center;
        text-align: left;
    }
    .col img{
        width: 40px;
        margin-right: 10px;
    }
    .weather-icon{
        width: 200px;
    }
    .humidity .wind{
            font-size: 28px;
            /* margin-top: -6px; */
    }
</style>
<body>
    <div class="card">
        <div class="search">
            <input type="text" placeholder="enter city name" spellcheck="false">
            <button><img src="images/search.png" alt=""></button>
        </div>
        <div class="weather">
            <img src="images/rain.png" class="weather-icon" alt="">
            <h1 class="temp">27°C</h1>
            <h2 class="city">New York</h2>
            <div class="details">
                <div class="col">
                    <img src="images/humidity.png" alt="">
                    <div>
                        <p class="humidity">50%</p>
                    <p>Humidity</p>
                    </div>
                </div>
                <div class="col">
                    <img src="images/wind.png" alt="">
                    <div>
                        <p class="wind"> 15km/hr</p>
                    <p>Wind speed</p>
                    </div>
                </div>
            </div>
        </div>
    </div>
    <script>
        // &appid={apiKey}
        // https://api.openweathermap.org/data/2.5/weather?&unit=metric&q=kolkata

        const temp=document.querySelector(".temp");
        const apiKey="5c09eb6d1519084b60d2879f6586d021";
        const apiUrl="https://api.openweathermap.org/data/2.5/weather?&appid=5c09eb6d1519084b60d2879f6586d021&units=metric&q=";
        
        const searchBox=document.querySelector(".search input");
        const searchBtn=document.querySelector(".search button");
        const weatherIcon=document.querySelector(".weather-icon")
        async function checkWeather(city){
            const response=await fetch(apiUrl+city);
            const data=await response.json();
            document.querySelector(".city").innerHTML=data.name;
            document.querySelector(".temp").innerHTML=Math.round(data.main.temp) +"°C";
            document.querySelector(".humidity").innerHTML=data.main.humidity + "%";
            document.querySelector(".wind").innerHTML=data.wind.speed + "km/hr";
            console.log(data);
            if(data.weather[0].main == 'Clouds'){
                weatherIcon.src="images/clouds.png"
            }
            if(data.weather[0].main == "Rain"){
                weatherIcon.src="images/rain.png"
            }
            if(data.weather[0].main == "Clear"){
                weatherIcon.src="images/clear.png"
            }
            if(data.weather[0].main == "Drizzle"){
                weatherIcon.src="images/drizzle.png"
            }
            if(data.weather[0].main == "Mist"){
                weatherIcon.src="images/mist.png"
            }
            if(data.weather[0].main == "Snow"){
                weatherIcon.src="images/snow.png"
            }
            if(data.weather[0].main == "Haze"){
                weatherIcon.src="images/fog.png"
            }
            console.log("Weather main:", data.weather[0].main);
        }
        searchBtn.addEventListener("click",()=>{            
            checkWeather(searchBox.value);
        })
    </script>
</body>
</html>
