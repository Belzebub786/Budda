# Этап 1: сборка
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src

# Копируем проект и восстанавливаем зависимости
COPY *.csproj ./
RUN dotnet restore

# Копируем весь код и собираем
COPY . ./
RUN dotnet publish -c Release -o /app/publish

# Этап 2: запуск (маленький образ)
FROM mcr.microsoft.com/dotnet/aspnet:8.0
WORKDIR /app
COPY --from=build /app/publish .

# Порт
EXPOSE 5000

# Запуск
ENTRYPOINT ["dotnet", "NorseApp.dll"]