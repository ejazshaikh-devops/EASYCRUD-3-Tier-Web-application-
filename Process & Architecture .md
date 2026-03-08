# EASYCRUD-3-Tier-Web-application- (Student Registration)
Pre-made Backend, Frontend and Docker deploying it on Ec2 by connecting the database (RDS MariaDB) with backendend and frontend with backend 

Process :

Architechture :

User Browser
     │
     │ HTTP Request
     ▼
Frontend (React / Vite)
Hosted on EC2
Port: 5173 or Apache Static
     │
     │ API Calls (REST)
     ▼
Backend (Spring Boot)
Running on EC2
Port: 8080
     │
     │ JDBC Connection
     ▼
AWS RDS (MariaDB)
Port: 3306
     │
     ▼
Database Storage

Infrastructure Layout :

                INTERNET
                    │
                    ▼
            AWS EC2 INSTANCE
        ┌─────────────────────┐
        │                     │
        │  React Frontend    │
        │  (Vite Dev Server) │
        │      Port 5173     │
        │                     │
        │  Spring Boot API   │
        │      Port 8080     │
        │                     │
        └─────────┬───────────┘
                  │
                  │ TCP 3306
                  ▼
          AWS RDS DATABASE
            MariaDB Engine

Request Flow :
1. User opens browser
2. frontend loads the UI
3. frontend react sends ab API call
   GET /students
   POST /attendance
   DELETE /students/{id}
4. Spring Boot processes request
5. Hibernate/JPA interacts with MariaDB
6. Database returns data
7. JSON response sent to frontend

Process of Deployment : (Ec2 instance Ubuntu)
before this enable port : 8080 (for backend) 3306 (for Database)

Backend :
1. system update
3. install jdk,maven
4. clone the data of git by git clone (https link)
5. navigate to resource directory in backend/src/
6. vim application.proparties
7. copy DB endpoint paste in spring.datasource.url 
8. below put username of DB and below that password save :x NOTE : Script present in pushed project resource 
9. IMPORTENT go back to backend directory and run command : mvn clean package
10. Now /target will get created /target :
    It compile the project's source code lovated in src/main/java places the resulting .class into target classes. and after testing process compiled code and resources packeges into distributable format such as JAR or WAR
ls target copy .jar line
Run this command java jar target/(paste the line here) this will start the backend and DB get connected with each other now keep in runnig leave tab open

Frontend :
enable port 5173 (for frontend) if usng host 
1. install nodejs -npm 
2. instakk npm 
3. In frontend .env file is presend 
vim .env 
4. delete $backend from line 1 and 2 and replace it with public ip of instance 
now here we can run a check wether website working or not by npm run dev -- --host what ever changes will happen in frontend it will directly shown in website page 
5. If the frontend is working and data is traveling from front end to backend then move to last phase
 6. npm run build run this command a new directory will appear which has index.html file 
7. Install apache2 or Inginx systemctl commands and  copy the content of dist directory and paste in service's html directory cp -rf ./* (location of the html directory) 
8. By this 3-tier web application will start working any change will first go to backend and through the backend it will registered in database.
