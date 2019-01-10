FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 53947
EXPOSE 44320

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["./SignalRChat.csproj", "SignalRChat/"]
RUN dotnet restore "SignalRChat/SignalRChat.csproj"
COPY . ./SignalRChat
WORKDIR "/src/SignalRChat"
RUN dotnet build "SignalRChat.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "SignalRChat.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "SignalRChat.dll"]