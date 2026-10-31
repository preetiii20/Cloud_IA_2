
FROM eclipse-temurin:17-jdk

WORKDIR /app

COPY .mvn .mvn
COPY mvnw pom.xml ./
RUN chmod +x mvnw

COPY src ./src
RUN ./mvnw -DskipTests package

EXPOSE 8099

CMD ["sh", "-c", "java -jar target/*.jar"]
