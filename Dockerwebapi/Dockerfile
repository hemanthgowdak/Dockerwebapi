#Get base image (full .Net core SDK)
FROM mcr.microsoft.com/dotnet/sdk:5.0 as build-env
WORKDIR /app
#copy csproj and restore
COPY *.csproj ./
RUN dotnet restore
#copy everthing else and build
COPY . ./
RUN dotnet publish -c Release -o out
#generate runtime image
FROM mcr.microsoft.com/dotnet/aspnet:5.0
WORKDIR /app
EXPOSE 80
COPY --from=build-env /app/out .
ENTRYPOINT [ "dotnet", "Dockerwebapi.dll" ]