FROM maven:3.8.4-openjdk-11 AS build
WORKDIR /app
COPY pom.xml ./

RUN mvn dependency:go-offline
COPY src/ ./src/
RUN mvn clean package -DskipTests


FROM openjdk:11-jre-slim
WORKDIR /app
COPY --from=build /app/target/*.jar ./
RUN ls -la

USER 1000
EXPOSE 80
CMD ["sh", "-c", "java -jar $(ls *.jar)"] 