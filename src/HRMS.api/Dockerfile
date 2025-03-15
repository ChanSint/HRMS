# Build Stage
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src

# Copy csproj file and restore dependencies
COPY ["HRMS.api.csproj", "./HRMS.api/"]
RUN dotnet restore "HRMS.api/HRMS.api.csproj"

# Copy remaining files and build
COPY . ./HRMS.api
WORKDIR /src/HRMS.api
# RUN dotnet publish "HRMS.api.csproj" -c Release -o /app/publish

# Final Runtime Stage
# FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS runtime
# WORKDIR /app
# COPY --from=build /app/publish .

# Set environment variable for ports
ENV ASPNETCORE_URLS="http://*:5000,https://*:5001" 
EXPOSE 5000

# Start the application
CMD ["dotnet", "watch", "run"]
