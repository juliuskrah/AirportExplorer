# Airport Explorer
To get started quickly, set environment to `Development`:

```posh
C:\> set ASPNETCORE_ENVIRONMENT=Development
C:\> dotnet restore
C:\> dotnet run
```

## Add Packages
To add a new package run the following command:

```posh
C:\> dotnet add package <package-name>
```

## Manage Secrets
External source: <https://docs.microsoft.com/en-us/aspnet/core/security/app-secrets?tabs=visual-studio-code>

## Deploy to Heroku
To deploy to Heroku you need the following:

[x] Docker  
[x] Heroku CLI
[x] Heroku account
[x] ASP.NET Core 2 Runtime

- Publish your app:

  ```posh
  C:\> dotnet publish -c Release
  ```

- Add a Dockerfile to the root of your project: In the root of your project, add a file called **Dockerfile**
  (no extensions) and place the following in it:

  ```
  FROM microsoft/aspnetcore
  WORKDIR /app
  COPY . .
  CMD ASPNETCORE_URLS=http://*:$PORT dotnet <AssemblyName>.dll
  ```

  > Be sure to replace **&lt;AssemblyName&gt;** with the name of your project assembly e.g. **AirportExplorer**

- Copy the Dockerfile to your publish directory
  Your publish directory should be:
  ```
  ${ROOT}/bin/release/netcoreapp2.0/publish
  ```

- Build the Docker Image
  
  ```posh
  C:\> docker build -t <image-name> ./bin/release/netcoreapp2.0/publish
  ```

  > Be sure to replace **&lt;image-name&gt;** with the name you intend to give the image e.g. 
    **airport-explorer**

- Create the app on Heroku using the dashboard
  1. Make sure you have a heroku.com account
  2. Login to the dashboard and create the app

- Be sure you are logged in to heroku and its container registry
  
  ```posh
  C:\> heroku login
  C:\> heroku container:login
  ```

- Tag the heroku target image
  
  ```posh
  C:\> docker tag <image-name> registry.heroku.com/<heroku-app-name>/web
  ```

  > Be sure to replace **&lt;heroku-app-name&gt;** with the name of your heroku app e.g. **sample-app**

- Push the docker image to heroku

  ```posh
  C:\> docker push registry.heroku.com/thrails/web
  ```

- Check that your app works
  
  ```posh
  C:\> heroku open -a <heroku-app-name>
  ```

