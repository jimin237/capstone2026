# 1단계: 빌드 스테이지 (Maven을 사용하여 JAR 파일 생성)
FROM maven:3.8.4-openjdk-17 AS builder
WORKDIR /app
# 프로젝트 소스 전체를 복사
COPY . .
# Maven 빌드 실행 (테스트는 건너뛰어 속도 향상)
RUN mvn clean package -DskipTests

# 2단계: 실행 스테이지 (최종 실행용 가벼운 이미지)
FROM eclipse-temurin:17-jdk-jammy
WORKDIR /app
# 1단계(builder)에서 생성된 JAR 파일만 가져옴
COPY --from=builder /app/target/*.jar app.jar
# 애플리케이션 실행
ENTRYPOINT ["java", "-jar", "app.jar"]