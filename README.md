A minimal example of using the [Stimulsoft](https://www.stimulsoft.com/en) web
viewer JSP component in a [Spring Boot](https://spring.io/projects/spring-boot)
project - highlighting an issue when using JDBC sessions.

This version is a minimal example that does not work properly unless you
comment out the line indicated in the `build.gradle` file.

I believe the problem is due to two factors:

1. Spring wraps the `HttpSession` object using the
   `org.springframework.session.web.http.SessionRepositoryFilter$SessionRepositoryRequestWrapper$HttpSessionWrapper`
   class, which does implement the `javax.servlet.http.HttpSession` interface, and:

2. Stimulsoft's code accessing the http session object via reflection.

In theory, it should work, I'm not sure why it doesn't.

---

To run, from the base folder run the following command for Linux/Mac:

```
./gradlew bootRun
```

or for Windows:

```
.\gradlew.bat bootRun
```

Then go to the URL `http://localhost:8080/`

You will see the report does not load. Ctrl-C to exit, then comment out the
indicated line in `build.gradle` and perform the `bootRun` command again.
Reload the web page and you should see the graphical report.
