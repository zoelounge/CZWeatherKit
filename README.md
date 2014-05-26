![](https://raw.githubusercontent.com/comyarzaheri/CZWeatherKit/master/Meta/czweatherkit_header.png?token=3284227__eyJzY29wZSI6IlJhd0Jsb2I6Y29teWFyemFoZXJpL0NaV2VhdGhlcktpdC9tYXN0ZXIvTWV0YS9jendlYXRoZXJraXRfaGVhZGVyLnBuZyIsImV4cGlyZXMiOjE0MDE1MTM3NTF9--b8641653a8eef5f1c67badeda79aa443b1836006)

CZWeatherKit is an easy-to-use, extensible weather library for iOS and OS X that allows for painless downloading of weather data from multiple weather services. CZWeatherKit is lightweight and requires no external dependencies.

# Getting Started

### Cocoa Pods

Add the following to your Podfile:

```ruby
    platform :ios, '7.0'
    pod "CZWeatherKit"
```

and run `pod install'

### Requirements

CZWeatherKit has only been tested on iOS 7 and OS X 10.9, but the library avoids using newer Cocoa/Cocoa Touch API so it may work on older deployment targets. 

### Supported Weather Services

CZWeatherKit currently supports the following weather services:
  * [Weather Underground](http://www.wunderground.com/weather/api/)
  * [Open Weather Map](http://openweathermap.org/API)

Some services require an API key while others do not. Consult the documentation for the API you would like to use. Additional services can be added (somewhat) easily by adopting the CZWeatherService protocol. See the 'Adding Services' section of the Readme.


# Examples

## Wunderground

### Getting Current Conditions

```objective-c 
    CZWeatherRequest *request = [CZWeatherRequest requestWithType:CZCurrentConditionsRequestType];
    request.location[CZWeatherKitLocationName.StateCityName] = @"TX/Austin";
    request.service = [CZWundergroundService serviceWithKey:<API_KEY_HERE>];
    [request performRequestWithHandler:^(id data, NSError *error) {
        if (data) {
            CZWeatherCondition *current = (CZWeatherCondition *)data;
            // Do whatever you like with the data here
        }
    }];
```

### Getting Forecast

```objective-c 
    const CGFloat latitude  = 30.2500;
    const CGFloat longitude = -97.7500;
    CZWeatherRequest *request = [CZWeatherRequest requestWithType:CZForecastRequestType];
    request.location[CZWeatherKitLocationName.CoordinateName] = [NSValue valueWithCGPoint:CGPointMake(latitude, longitude)];
    request.service = [CZWundergroundService serviceWithKey:<API_KEY_HERE>];
    [request performRequestWithHandler:^(id data, NSError *error) {
        if (data) {
            NSArray *forecasts = (NSArray *)data;
            // Do whatever you like with the data here
        }
    }];
```

### Getting 10-day Forecast

```objective-c 
    const CGFloat latitude  = 30.2500;
    const CGFloat longitude = -97.7500;
    CZWeatherRequest *request = [CZWeatherRequest requestWithType:CZForecastRequestType];
    request.detailLevel = CZWeatherRequestFullDetail;
    request.location[CZWeatherKitLocationName.CountryCityName] = @"Australia/Sydney";
    request.service = [CZWundergroundService serviceWithKey:<API_KEY_HERE>];
    [request performRequestWithHandler:^(id data, NSError *error) {
        if (data) {
            NSArray *forecasts = (NSArray *)data;
            // Do whatever you like with the data here
        }
    }];
```


## Open Weather Map 

### Getting Current Conditions

```objective-c 
    const CGFloat latitude  = 30.2500;
    const CGFloat longitude = -97.7500;
    CZWeatherRequest *request = [CZWeatherRequest requestWithType:CZCurrentConditionsRequestType];
    request.location[CZWeatherKitLocationName.CoordinateName] = [NSValue valueWithCGPoint:CGPointMake(latitude, longitude)];
    request.service = [CZOpenWeatherMapService serviceWithKey:<API_KEY_HERE>];
    [request performRequestWithHandler:^(id data, NSError *error) {
        if (data) {
            CZWeatherCondition *current = (CZWeatherCondition *)data;
            // Do whatever you like with the data here
        }
    }];
```

### Getting Hourly Forecast

```objective-c
    CZWeatherRequest *request = [CZWeatherRequest requestWithType:CZForecastRequestType];
    request.location[CZWeatherKitLocationName.CountryCityName] = @"London,UK";
    request.service = [CZOpenWeatherMapService serviceWithKey:<API_KEY_HERE>];
    [request performRequestWithHandler:^(id data, NSError *error) {
        if (data) {
            NSArray *forecasts = (NSArray *)data;
            // Do whatever you like with the data here
        }
    }];
```

### Getting Daily Forecast

```objective-c
    CZWeatherRequest *request = [CZWeatherRequest requestWithType:CZForecastRequestType];
    request.location[CZWeatherKitLocationName.StateCityName] = @"Austin,TX";
    request.service = [CZOpenWeatherMapService serviceWithKey:<API_KEY_HERE>];
    request.detailLevel = CZWeatherRequestFullDetail;
    [request performRequestWithHandler:^(id data, NSError *error) {
        if (data) {
            NSArray *forecasts = (NSArray *)data;
            // Do whatever you like with the data here
        }
    }];
```


## Architecture

### Requests and Services

TODO

### Adding Services

TODO
