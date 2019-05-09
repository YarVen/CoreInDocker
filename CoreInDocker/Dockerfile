FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 54334
EXPOSE 44395

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["CoreInDocker/CoreInDocker.csproj", "CoreInDocker/"]
RUN dotnet restore "CoreInDocker/CoreInDocker.csproj"
COPY . .
WORKDIR "/src/CoreInDocker"
RUN dotnet build "CoreInDocker.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "CoreInDocker.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "CoreInDocker.dll"]