# Use the official .NET SDK image for build
FROM mcr.microsoft.com/dotnet/sdk:9.0 AS build
WORKDIR /src
COPY ["MarketingSite.Web.csproj", "./"]
RUN dotnet restore "MarketingSite.Web.csproj"
COPY . .
RUN dotnet publish "MarketingSite.Web.csproj" -c Release -o /app/publish

# Use the official ASP.NET runtime image for the final stage
FROM mcr.microsoft.com/dotnet/aspnet:9.0 AS final
WORKDIR /app
COPY --from=build /app/publish .
EXPOSE 5120
ENV ASPNETCORE_URLS=http://+:5120
ENTRYPOINT ["dotnet", "MarketingSite.Web.dll"]

