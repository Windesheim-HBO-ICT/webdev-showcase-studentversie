FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
WORKDIR /app
EXPOSE 80
ENV ASPNETCORE_URLS=http://+:80

FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY ["ShowcaseAPI.csproj", "."]
RUN dotnet restore "ShowcaseAPI.csproj"
COPY . .
RUN dotnet build "ShowcaseAPI.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "ShowcaseAPI.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "ShowcaseAPI.dll"]
