# weather-app2
App.css
.App {
  text-align: center;
}

.App-logo {
  height: 40vmin;
  pointer-events: none;
}

@media (prefers-reduced-motion: no-preference) {
  .App-logo {
    animation: App-logo-spin infinite 20s linear;
  }
}

.App-header {
  background-color: #282c34;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  font-size: calc(10px + 2vmin);
  color: white;
}

.App-link {
  color: #61dafb;
}

@keyframes App-logo-spin {
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(360deg);
  }
}

App.js
// src/App.js
import React from 'react';
import Weather from './Weather';
import './App.css'; // Optional: for styling

const App = () => {
    return (
        <div className="App">
            <Weather />
        </div>
    );
};
AppTest.js
import { render, screen } from '@testing-library/react';
import App from './App';

test('renders learn react link', () => {
  render(<App />);
  const linkElement = screen.getByText(/learn react/i);
  expect(linkElement).toBeInTheDocument();
});
index.css
body {
  margin: 0;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', 'Roboto', 'Oxygen',
    'Ubuntu', 'Cantarell', 'Fira Sans', 'Droid Sans', 'Helvetica Neue',
    sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

code {
  font-family: source-code-pro, Menlo, Monaco, Consolas, 'Courier New',
    monospace;
}
index.js
import React from 'react';
import ReactDOM from 'react-dom/client';
import './index.css';
import App from './App';
import reportWebVitals from './reportWebVitals';

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>
);

// If you want to start measuring performance in your app, pass a function
// to log results (for example: reportWebVitals(console.log))
// or send to an analytics endpoint. Learn more: https://bit.ly/CRA-vitals
reportWebVitals();
reportWebVitals.js
const reportWebVitals = onPerfEntry => {
  if (onPerfEntry && onPerfEntry instanceof Function) {
    import('web-vitals').then(({ getCLS, getFID, getFCP, getLCP, getTTFB }) => {
      getCLS(onPerfEntry);
      getFID(onPerfEntry);
      getFCP(onPerfEntry);
      getLCP(onPerfEntry);
      getTTFB(onPerfEntry);
    });
  }
};

export default reportWebVitals;
setupTests.js
// jest-dom adds custom jest matchers for asserting on DOM nodes.
// allows you to do things like:
// expect(element).toHaveTextContent(/react/i)
// learn more: https://github.com/testing-library/jest-dom
import '@testing-library/jest-dom';

Weather.css
/* src/Weather.css */
.weather-container {
    max-width: 400px;
    margin: 0 auto;
    padding: 20px;
    background: #f5f5f5;
    border-radius: 10px;
    box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
    text-align: center;
}

.weather-container h1 {
    margin-bottom: 20px;
}

.weather-container input {
    padding: 10px;
    width: 70%;
    border: 1px solid #ddd;
    border-radius: 5px;
}

.weather-container button {
    padding: 10px;
    background: #3b82f6;
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    margin-left: 10px;
}

.weather-container button:hover {
    background: #2563eb;
}

.weather-info {
    margin-top: 20px;
}

.error {
    color: #ef4444;
    margin-top: 10px;
}
Weather.js
// src/Weather.js
import React, { useState } from 'react';
import axios from 'axios';
import './Weather.css'; // Optional: for styling

const Weather = () => {
    const [city, setCity] = useState('');
    const [weatherData, setWeatherData] = useState(null);
    const [error, setError] = useState('');

    const API_KEY = '1994e52bdb3503754250ececf13d198e'; // Replace with your OpenWeatherMap API key

    const fetchWeather = async () => {
        try {
            const response = await axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${city}&appid=${API_KEY}&units=metric`);
            setWeatherData(response.data);
            setError('');
        } catch (err) {
            setError('City not found');
            setWeatherData(null);
        }
    };

    const handleSubmit = (e) => {
        e.preventDefault();
        fetchWeather();
    };

    return (
        <div className="weather-container">
            <h1>Weather App</h1>
            <form onSubmit={handleSubmit}>
                <input
                    type="text"
                    value={city}
                    onChange={(e) => setCity(e.target.value)}
                    placeholder="Enter city"
                />
                <button type="submit">Get Weather</button>
            </form>
            {error && <p className="error">{error}</p>}
            {weatherData && (
                <div className="weather-info">
                    <h2>{weatherData.name}</h2>
                    <p>Temperature: {weatherData.main.temp} °C</p>
                    <p>Weather: {weatherData.weather[0].description}</p>
                </div>
            )}
        </div>
    );
};

export default Weather;


export default App;

