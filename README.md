# GmOwl

Quiz platform with timed quizzes, an admin panel and ChatGPT-assisted question writing. Built with Java servlets and JSP.

## Features

**Users**
- Register, log in and manage a profile
- Browse quizzes by subject and difficulty
- Take timed quizzes
- English and Ukrainian interface

**Admins**
- Create, edit and delete quizzes and questions
- Block, unblock, edit and delete users
- Generate a draft question for a quiz with ChatGPT, then review and save it

## Tech stack

| Layer | Technology |
| --- | --- |
| Language | Java |
| Web | Jakarta Servlet 5, JSP, JSTL |
| Server | Tomcat 10 |
| Database | InterSystems IRIS (JDBC) |
| Migrations | Liquibase |
| Logging | Log4j 2 |
| AI | OpenAI API via OkHttp |
| Deployment | Docker |

## Architecture

- Front controller (`FrontController`) routes every request to a command.
- Each action is a separate command class under `commands/user` or `commands/admin`.
- Filters handle authentication, admin access and localization.
- DAO classes isolate database access from the commands.

## Running

Requires Docker.

This version uses InterSystems IRIS Cloud SQL. To run IRIS locally instead, use the [`local-irisdb` branch](https://github.com/andrimishko/quiz-app/tree/local-irisdb).

**Cloud SQL setup**

1. Create an InterSystems IRIS Cloud SQL deployment.
2. Download the X.509 certificate.
3. Create a keystore:
   ```
   keytool -importcert -file path-to-cert/cert-file.pem -keystore keystore.jks
   ```
4. Copy `keystore.jks` to the `certs/` folder.
5. Set the keystore password in `certs/SSLConfig.properties`.

**ChatGPT generation (optional)**

Set your OpenAI API key in `src/main/resources/chatgpt.properties`:

```
api-key=your-api-key
```

**Start**

```
docker-compose up
```

Open http://localhost:8080.

## Demo

ChatGPT question generation:

![ChatGPT example](https://github.com/andrimishko/quiz-app/assets/49749263/5ecdcf02-35c8-46e4-bb8b-4b2a0e98b429)

Video walkthrough: https://github.com/andrimishko/quiz-app/assets/49749263/dd3e8ace-808f-421d-8ffb-608f254ec909

## License

MIT
