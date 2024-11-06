# Etapa 1: Compilação da aplicação
FROM maven:3.8.5-openjdk-17 AS build
WORKDIR /app
COPY pom.xml .
COPY src ./src
RUN mvn clean package -DskipTests

# Etapa 2: Executar a aplicação
FROM openjdk:17-jdk-slim
WORKDIR /app
COPY --from=build /app/target/*.jar /app/app.jar

# Variável de ambiente para o PostgreSQL
ENV DB_URL=jdbc:postgresql://postgres:5432/mydatabase
ENV DB_USERNAME=postgres
ENV DB_PASSWORD=postgres

# Expor a porta usada pela aplicação
EXPOSE 8080

# Executar o jar gerado
ENTRYPOINT ["java", "-jar", "/app/app.jar"]