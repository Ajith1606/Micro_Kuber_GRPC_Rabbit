# Use the .NET SDK to build the application
FROM mcr.microsoft.com/dotnet/sdk:10.0 AS build-env
WORKDIR /App

COPY *.csproj ./
RUN dotnet restore

COPY . ./ 
RUN dotnet publish -c Release -o out


# Use the ASP.NET Core runtime for the final image
FROM mcr.microsoft.com/dotnet/aspnet:10.0
WORKDIR /App
ENV ASPNETCORE_HTTP_PORTS=80
COPY --from=build-env /App/out .
ENTRYPOINT ["dotnet", "PlatformService.dll"]