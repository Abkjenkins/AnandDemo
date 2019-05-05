#Depending on the operating system of the host machines(s) that will build or run the containers, the image specified in the FROM statement may need to be changed.
#For more information, please see https://aka.ms/containercompat

FROM microsoft/dotnet:2.1-aspnetcore-runtime-nanoserver-sac2016 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.1-sdk-nanoserver-sac2016 AS build
WORKDIR /src
COPY ["App1/App1.csproj", "App1/"]
RUN dotnet restore "App1/App1.csproj"
COPY . .
WORKDIR "/src/App1"
RUN dotnet build "App1.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "App1.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "App1.dll"]