# 첫 번째 베이스 이미지
FROM maven:3.8.4-openjdk-11 AS build

# 이제부터 컨테이너 기본 경로는 /app
WORKDIR /app

# EC2 project -> maven image (MOST to Container)
# COPY <Host> <Container>
# pom.xml : EC2에 Dockerfile과 같은 곳에 있는 pom.xml

COPY pom.xml .

COPY src ./src

# pom.xml과 src를 이용해 빌드 수행
RUN mvn clean package && echo "app build complete!"



# 두 번쨰 베이스 
FROM tomcat:9.0-jdk11

# maven 컨테이너에 있는 project-1-0.0. war파일을 tomcat 컨테이너에 복사하기
COPY --from=build /app/target/*.war /usr/local/tomcat/webapps/project.war

# 포트
EXPOSE 8080