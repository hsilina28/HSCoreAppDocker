FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 56362
EXPOSE 44356

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["HSCoreAppDocker/HSCoreAppDocker.csproj", "HSCoreAppDocker/"]
RUN dotnet restore "HSCoreAppDocker/HSCoreAppDocker.csproj"
COPY . .
WORKDIR "/src/HSCoreAppDocker"
RUN dotnet build "HSCoreAppDocker.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "HSCoreAppDocker.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "HSCoreAppDocker.dll"]