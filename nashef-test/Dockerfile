#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["nashef-test/nashef-test.csproj", "nashef-test/"]
RUN dotnet restore "nashef-test/nashef-test.csproj"
COPY . .
WORKDIR "/src/nashef-test"
RUN dotnet build "nashef-test.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "nashef-test.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "nashef-test.dll"]