FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["Template.VueTL/Template.VueTL.csproj", "Template.VueTL/"]
RUN dotnet restore "Template.VueTL/Template.VueTL.csproj"
COPY . .
WORKDIR "/src/Template.VueTL"
RUN dotnet build "Template.VueTL.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "Template.VueTL.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Template.VueTL.dll"]
