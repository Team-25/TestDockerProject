#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.
FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /build


RUN curl -sL https://deb.nodesource.com/setup_10.x |  bash -
RUN apt-get install -y nodejs

COPY *.sln .
COPY Mynd/*.csproj ./Mynd/
COPY Mynd.Data/*.csproj ./Mynd.Data/
COPY Mynd.Services/*.csproj ./Mynd.Services/

RUN dotnet restore 

COPY Mynd/. ./Mynd/
COPY Mynd.Data/. ./Mynd.Data/
COPY Mynd.Services/. ./Mynd.Services/

COPY . .
WORKDIR /build
RUN dotnet publish -c release -o published --no-cache

FROM mcr.microsoft.com/dotnet/aspnet:5.0
WORKDIR /app
COPY --from=build /build/published ./
ENTRYPOINT ["dotnet", "mynd.dll"]


