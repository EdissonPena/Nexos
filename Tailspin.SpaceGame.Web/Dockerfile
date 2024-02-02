# #See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

# FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
# WORKDIR /app
# EXPOSE 80
# EXPOSE 443

# FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
# WORKDIR /src
# COPY ["Tailspin.SpaceGame.Web.csproj", "Tailspin.SpaceGame.Web/"]
# RUN dotnet restore "Tailspin.SpaceGame.Web/Tailspin.SpaceGame.Web.csproj"
# COPY . .
# WORKDIR "/src/Tailspin.SpaceGame.Web"
# RUN dotnet build "Tailspin.SpaceGame.Web.csproj" -c Release -o /app/build

# FROM build AS publish
# RUN dotnet publish "Tailspin.SpaceGame.Web.csproj" -c Release -o /app/publish

# FROM base AS final
# WORKDIR /app
# COPY --from=publish /app/publish .
# ENTRYPOINT ["dotnet", "Tailspin.SpaceGame.Web.dll"]

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build-env
WORKDIR /App
EXPOSE 80
EXPOSE 443

# Copy everything
COPY . ./
# Restore as distinct layers
RUN dotnet restore
# Build and publish a release
RUN dotnet publish -c Release -o out

# Build runtime image
FROM mcr.microsoft.com/dotnet/aspnet:6.0
WORKDIR /App
COPY --from=build-env /App/out .
ENTRYPOINT ["dotnet", "Tailspin.SpaceGame.Web.dll"]