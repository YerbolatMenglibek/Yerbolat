import requests
import json


api_key = "7b5c4ce06c9fdbf952406d5c9aa04678"

def get_weather(city):
    base_url = "https://api.openweathermap.org/data/2.5/weather"

    params = {
        "q": city,
        "appid": api_key,
        "units": "metric"
    }

    try:
        response = requests.get(base_url, params=params)
        data = response.json()

        if data["cod"] == 200:
            temperature = data["main"]["temp"]
            wind_speed = data["wind"]["speed"]
            precipitation = data.get("rain", {}).get("1h", 0)
            humidity = data["main"]["humidity"]

            print(f"Weather in {city}:")
            print(f"Temperature: {temperature}°C")
            print(f"Wind Speed: {wind_speed} m/s")
            print(f"Precipitation (last hour): {precipitation} mm")
            print(f"Humidity: {humidity}%")
        else:
            print(f"Unable to fetch weather data for {city}.")
    except requests.exceptions.RequestException as e:
        print(f"An error occurred: {e}")

if __name__ == "__main__":
    city = input("Enter the city name: ")
    get_weather(city)
