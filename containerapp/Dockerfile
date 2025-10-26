FROM openjdk:17
WORKDIR /usrapp/bin
ENV PORT=33026
COPY /target/classes /usrapp/bin/classes
COPY /target/dependency /usrapp/bin/dependency
CMD ["java","-cp","./classes:./dependency/*","edu.escuelaing.aygo.container.RestServiceApplication"]