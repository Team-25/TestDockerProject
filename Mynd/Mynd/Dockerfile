#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

#FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
#WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /build



RUN curl -sL https://deb.nodesource.com/setup_10.x |  bash -
RUN apt-get install -y nodejs

COPY . .
COPY ["Mynd/Mynd.csproj", "Mynd/"]
COPY ["Mynd.Data/Mynd.Data.csproj", "Mynd.Data/"]
COPY ["Mynd.Services/Mynd.Services.csproj", "Mynd.Services/"]
COPY ./*.csproj .
RUN dotnet restore "Mynd/Mynd.csproj"

#COPY . .
#COPY ["Mynd/Mynd.csproj", "Mynd/"]
#COPY ["Mynd.Data/Mynd.Data.csproj", "Mynd.Data/"].
#COPY ["Mynd.Services/Mynd.Services.csproj", "Mynd.Services/"]
#RUN dotnet restore "Mynd/Mynd.csproj"
#RUN dotnet publish -c Release -o /app
#

COPY . .
WORKDIR /build
RUN dotnet publish -c release -o published --no-cache

#FROM build AS publish
#RUN dotnet publish "Mynd.csproj" -c Release -o /app/publish
#
#FROM base AS final
#WORKDIR /app
#COPY --from=build /app .
#EXPOSE 5000
#ENTRYPOINT ["dotnet", "Mynd.dll"]

FROM mcr.microsoft.com/dotnet/aspnet:5.0
WORKDIR /app
COPY --from=build /build/published ./
ENTRYPOINT ["dotnet", "mynd.dll"]


