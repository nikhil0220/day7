##See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.
#
#FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
#WORKDIR /app
#EXPOSE 80
#EXPOSE 443
#
#FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
#WORKDIR /src
#COPY ["WebApplicationDay7/WebApplicationDay7.csproj", "WebApplicationDay7/"]
#RUN dotnet restore "WebApplicationDay7/WebApplicationDay7.csproj"
#COPY . .
#WORKDIR "/src/WebApplicationDay7"
#RUN dotnet build "WebApplicationDay7.csproj" -c Release -o /app/build
#
#FROM build AS publish
#RUN dotnet publish "WebApplicationDay7.csproj" -c Release -o /app/publish
#
#FROM base AS final
#WORKDIR /app
#COPY --from=publish /app/publish .
#ENTRYPOINT ["dotnet", "WebApplicationDay7.dll"]
FROM mcr.microsoft.com/dotnet/core/sdk:3.1 AS build-env
WORKDIR /app
# Copy csproj and restore as distinct layers
COPY *.csproj ./
RUN dotnet restore
# Copy everything else and build
COPY . ./
RUN dotnet publish -c Release -o out

# Build runtime image
FROM mcr.microsoft.com/dotnet/core/aspnet:3.1
WORKDIR /app
COPY --from=build-env /app/out .
ENTRYPOINT ["dotnet", ".WebApplicationDay7.dll"]