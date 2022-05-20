#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["AttendanceDockerWebAPI/AttendanceDockerWebAPI.csproj", "AttendanceDockerWebAPI/"]
RUN dotnet restore "AttendanceDockerWebAPI/AttendanceDockerWebAPI.csproj"
COPY . .
WORKDIR "/src/AttendanceDockerWebAPI"
RUN dotnet build "AttendanceDockerWebAPI.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "AttendanceDockerWebAPI.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "AttendanceDockerWebAPI.dll"]