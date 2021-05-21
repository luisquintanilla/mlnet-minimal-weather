# Weather forecast model

This is a sample application that shows how to use [.NET Interactive](https://github.com/dotnet/interactive) to train a weather forecasting model for maximum temperatures in Seattle, WA. Once trained, the model is exposed as a web service for predictions inside an ASP.NET Core Minimal Web API.

## Prerequisites

- Notebook
    - [.NET 5 SDK](https://dotnet.microsoft.com/download/dotnet/5.0)
    - [Visual Studio Code](https://code.visualstudio.com/)
    - [.NET Interactive Notebooks Visual Studio Code extension](https://marketplace.visualstudio.com/items?itemName=ms-dotnettools.dotnet-interactive-vscode)
- Web API
    - .NET 6 Preview 4

## About the data

The data used for this model is from [NOAA](https://www.noaa.gov/). It contains 10 years worth of weather data for the Seattle Boeing Field weather station in Seattle, WA. The data looks like the following.

|STATION|NAME|LATITUDE|LONGITUDE|ELEVATION|DATE|TMAX|TMIN|
|---|---|---|---|---|---|---|---|
|USW00024234|"SEATTLE BOEING FIELD| WA US"|47.53028|-122.30083|6.1|4/1/2010|51|41|
|USW00024234|"SEATTLE BOEING FIELD| WA US"|47.53028|-122.30083|6.1|4/2/2010|53|41|
|USW00024234|"SEATTLE BOEING FIELD| WA US"|47.53028|-122.30083|6.1|4/3/2010|50|39|

## Making predictions

Start the Web API project.

Using a REST API client of your choice, make an HTTP `GET` request to `http://localhost:5000/predict`.

The response should look similar like the following:

```json
{
    "forecastTemp": [
        80.7973,
        82.15604,
        83.125435,
        83.9756,
        84.39549
    ],
    "lowerBoundTemp": [
        72.84004,
        71.66275,
        70.07037,
        68.60337,
        66.69504
    ],
    "upperBoundTemp": [
        88.75456,
        92.64932,
        96.1805,
        99.34783,
        102.09595
    ]
}
```

In this case, a forecast of the maximum temperature for the next 5 days is generated and stored in the `forecastTemp` property. Since no forecast is 100% accurate, the upper and lower bounds provide a range by which the actual forecast may vary.

Note that this forecast is generated at a point in time when the model was trained. As you get new weather measurements for subsequent days, you want to update your model with the actual values observed to generate a more reliable forecast.