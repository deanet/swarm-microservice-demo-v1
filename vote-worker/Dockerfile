FROM java:7
#FROM java:7

RUN apt-get update -qq && apt-get install -y maven && apt-get clean
#RUN apt-get update -y && apt-get install -y gnupg && apt-key adv --recv-keys --keyserver keyserver.ubuntu.com C2518248EEA14886 && apt-get install -y maven && apt-get clean


WORKDIR /code

ADD pom.xml /code/pom.xml
RUN ["mvn", "dependency:resolve","-Dhttps.protocols=TLSv1.2"]
#RUN ["mvn","-U","clean","install"]
#RUN ["mvn","dependency:resolve","-Dverbose=true"]
RUN ["mvn", "verify","-Dhttps.protocols=TLSv1.2"]

# Adding source, compile and package into a fat jar
ADD src /code/src
RUN ["mvn", "package"]

CMD ["/usr/lib/jvm/java-7-openjdk-amd64/bin/java", "-jar", "target/worker-jar-with-dependencies.jar"]
