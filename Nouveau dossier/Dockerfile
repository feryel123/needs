FROM maven:3.6.3-jdk-8-openj9 AS MAVEN_TOOL_CHAIN
COPY pom.xml /tmp/
COPY src /tmp/src/
WORKDIR /tmp/
RUN mvn clean install

FROM openjdk:8-jdk-alpine
COPY --from=MAVEN_TOOL_CHAIN /tmp/target/*.jar ginkaku.jar
COPY wait-for-it.sh wait-for-it.sh
RUN chmod +x wait-for-it.sh 
CMD ["./wait-for-it.sh", "db:3306", "--timeout=30", "--", "java", "-jar", "ginkaku.jar"]
