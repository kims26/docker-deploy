# 사용할 베이스 이미지를 선택합니다. Java 11과 Maven을 사용합니다.
FROM maven:3.8.4-openjdk-11-slim AS builder

# 작업 디렉토리를 설정합니다.
WORKDIR /app

# 소스 코드 및 pom.xml을 복사합니다.
COPY pom.xml .
COPY src ./src

# 애플리케이션을 빌드합니다.
RUN mvn package -DskipTests

# 빌드된 JAR 파일을 복사합니다.
FROM openjdk:11-jre-slim
WORKDIR /app

# JAR 파일을 복사합니다.
COPY --from=builder /app/target/deploy-0.0.1-SNAPSHOT.jar ./app.jar

# 애플리케이션을 실행합니다.
CMD ["java", "-jar", "app.jar"]
