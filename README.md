# Auth Web Client

A Blazor WebAssembly (.NET 8) front end with login, registration and role-protected pages. It talks to the [identity-auth-api](https://github.com/jvishwa06/identity-auth-api) backend.

## Features

- **Account pages**: `Login`, `Register` and `Logout` components under `Component/Account`.
- **Custom authentication**: `CustomAuthenticationStateProvider` plus `CutomHttpHandler`, which attach the user's token to API calls. Tokens are kept in browser local storage (`Blazored.LocalStorage`).
- **Weather page** (`/weather`): restricted to users in the `admin` role. It looks up a city's weather from the OpenWeatherMap API (temperature and humidity) and lists the results. It also calls the backend routes `api/weather/add` and `api/weather/favorites` to save data and favourite cities.
- **Other pages**: Home and Counter.
- **PWA files**: `manifest.webmanifest` and a service worker.

## Project layout

```
Component/Account/   Login, Register, Logout
Layout/              MainLayout, NavMenu
Model/               FormResult, TokenInfo, UserInfo
Pages/               Home, Counter, Weather
Sevices/             Authentication, HTTP handler, WeatherService
Program.cs           Service registration
Dockerfile           Builds with the .NET SDK and serves with nginx
```

## Configuration

- `BackendUrl` sets the API address (read from configuration in `Program.cs`, with a built-in fallback).
- `WeatherService` needs an OpenWeatherMap API key. Set your own in `Sevices/WeatherService.cs`.

## Run

```bash
dotnet run
```

With Docker (builds the app and serves it from nginx on port 80):

```bash
docker build -t auth-web-client .
docker run -p 8080:80 auth-web-client
```
