<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Weather App</title>
  <link rel="stylesheet" href="styles.css">
</head>
<body>
  <div class="container">
    <h1>Weather App</h1>
    <div class="weather-info" id="weatherInfo">
      <!-- Weather information will be displayed here -->
    </div>
  </div>
  <script src="script.js"></script>
</body>
</html>

body {
  font-family: Arial, sans-serif;
}

.container {
  max-width: 600px;
  margin: 0 auto;
  text-align: center;
}

.weather-info {
  margin-top: 20px;
}
window.addEventListener('load', () => {
  const apiKey = 'YOUR_API_KEY'; // Replace with your API key
  const apiUrl = `https://api.openweathermap.org/data/2.5/weather?q=cityName&appid=${apiKey}&units=metric`; // Replace cityName with desired city

  fetch(apiUrl)
    .then(response => response.json())
    .then(data => {
      displayWeather(data);
    })
    .catch(error => {
      console.error('Error fetching weather data:', error);
    });

  function displayWeather(data) {
    const weatherInfoElement = document.getElementById('weatherInfo');
    const cityName = data.name;
    const temperature = data.main.temp;
    const description = data.weather[0].description;

    weatherInfoElement.innerHTML = `
      <h2>${cityName}</h2>
      <p>Temperature: ${temperature}°C</p>
      <p>Description: ${description}</p>
    `;
  }
});
