# friendly-waddle
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Weather App</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">

  <style>
    body {
      font-family: Arial, sans-serif;
      background: linear-gradient(135deg, #4facfe, #00f2fe);
      color: #fff;
      text-align: center;
      padding: 50px;
    }

    .container {
      max-width: 400px;
      margin: auto;
      background: rgba(0,0,0,0.3);
      padding: 20px;
      border-radius: 15px;
    }

    input {
      padding: 10px;
      width: 70%;
      border: none;
      border-radius: 5px;
      margin-bottom: 10px;
    }

    button {
      padding: 10px;
      border: none;
      background: #ff9800;
      color: #fff;
      border-radius: 5px;
      cursor: pointer;
    }

    button:hover {
      background: #e68900;
    }

    .weather {
      margin-top: 20px;
    }

    h2 {
      margin-bottom: 10px;
    }
  </style>
</head>

<body>

  <div class="container">
    <h2>🌦️ Weather App</h2>

    <input type="text" id="city" placeholder="Enter city name">
    <br>
    <button onclick="getWeather()">Get Weather</button>

    <div class="weather" id="weather"></div>
  </div>

  <script>
    async function getWeather() {
      const city = document.getElementById("city").value;
      const apiKey = "YOUR_API_KEY";

      if (!city) {
        alert("Please enter a city name");
        return;
      }

      const url = `https://api.openweathermap.org/data/2.5/weather?q=${city}&units=metric&appid=${apiKey}`;

      try {
        const response = await fetch(url);
        const data = await response.json();

        if (data.cod !== 200) {
          document.getElementById("weather").innerHTML = `<p>${data.message}</p>`;
          return;
        }

        const weatherHTML = `
          <h3>${data.name}, ${data.sys.country}</h3>
          <p>🌡 Temperature: ${data.main.temp} °C</p>
          <p>🌥 Weather: ${data.weather[0].description}</p>
          <p>💧 Humidity: ${data.main.humidity}%</p>
          <p>🌬 Wind Speed: ${data.wind.speed} m/s</p>
        `;

        document.getElementById("weather").innerHTML = weatherHTML;

      } catch (error) {
        document.getElementById("weather").innerHTML = "<p>Error fetching data</p>";
      }
    }
  </script>

</body>
</html>
