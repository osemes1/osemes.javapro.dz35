# osemes.javapro.dz35

Я переробив деякі класи щоб покрити повний функціонал по задачі:
    Версія не свіжа, не критично, але бажано використовувати новішу версію Spring Boot, тому що ряд методів для security config deprecated.
    WebSecutityConfigurerAdapter також застарів
    Яким чином можна отримти доступ до ресурсів, якщо вони не надаються через REST API?
    Також бажано використовувати юзерів із бази даних

Для цього зроблено:
- додані нові версії у pom.xml для необхідних додатків;
- створені нові класи та перероблені існуючи, а саме:

1. Перероблений клас User -- в нього додана сутність (Entity) для таблиці користувачів dz35_users
2. Додані нові класи -- UserRepository та UserConfig -- в них додав сутності для доступу до бази даних через Spring Data JPA та для завантаження користувачів з бази даних
3. Створив нову таблицю у БД: dz35_users та додав користувача "admin" з паролем "admin" і роллю "ADMIN":
4. Для користувача створив запис:
INSERT INTO dz35_users (username, password, role)
VALUES ('admin', '{bcrypt}$2a$10$uBt1d4N20Lbj3eKaxifn6u56IaGSWT0pP32I9hv/6LYjRzBui.OuIy', 'ADMIN');
використував bcrypt для збереження хеша паролю "admin". Цей хеш було створено за допомогою BCryptPasswordEncoder 
5. Переробив клас SecurityConfiguration.java
6. Додав налаштування у application.properties

Зараз додаток компілюється без помилок

 :: Spring Boot ::                (v2.6.0)

08:05:32.491 [main] INFO  com.example.demo.DemoApplication - Starting DemoApplication using Java 16.0.2 on NW11-139 with PID 13488 (C:\osem\Projects\osemes.javapro.dz35\target\classes started by User303 in C:\osem\Projects\osemes.javapro.dz35)
08:05:32.503 [main] INFO  com.example.demo.DemoApplication - No active profile set, falling back to default profiles: default
08:05:33.050 [main] INFO  org.springframework.data.repository.config.RepositoryConfigurationDelegate - Bootstrapping Spring Data JPA repositories in DEFAULT mode.
08:05:33.107 [main] INFO  org.springframework.data.repository.config.RepositoryConfigurationDelegate - Finished Spring Data repository scanning in 45 ms. Found 2 JPA repository interfaces.
08:05:33.629 [main] INFO  org.springframework.boot.web.embedded.tomcat.TomcatWebServer - Tomcat initialized with port(s): 8080 (http)
08:05:33.638 [main] INFO  org.apache.coyote.http11.Http11NioProtocol - Initializing ProtocolHandler ["http-nio-8080"]
08:05:33.639 [main] INFO  org.apache.catalina.core.StandardService - Starting service [Tomcat]
08:05:33.639 [main] INFO  org.apache.catalina.core.StandardEngine - Starting Servlet engine: [Apache Tomcat/9.0.55]
08:05:33.725 [main] INFO  org.apache.catalina.core.ContainerBase.[Tomcat].[localhost].[/] - Initializing Spring embedded WebApplicationContext
08:05:33.725 [main] INFO  org.springframework.boot.web.servlet.context.ServletWebServerApplicationContext - Root WebApplicationContext: initialization completed in 1183 ms
08:05:33.892 [main] INFO  org.hibernate.jpa.internal.util.LogHelper - HHH000204: Processing PersistenceUnitInfo [name: default]
08:05:33.936 [main] INFO  org.hibernate.Version - HHH000412: Hibernate ORM core version 5.6.1.Final
08:05:34.062 [main] INFO  org.hibernate.annotations.common.Version - HCANN000001: Hibernate Commons Annotations {5.1.2.Final}
08:05:34.155 [main] INFO  com.zaxxer.hikari.HikariDataSource - HikariPool-1 - Starting...
08:05:34.434 [main] INFO  com.zaxxer.hikari.HikariDataSource - HikariPool-1 - Start completed.
08:05:34.444 [main] INFO  org.hibernate.dialect.Dialect - HHH000400: Using dialect: org.hibernate.dialect.MySQL8Dialect
08:05:34.934 [main] INFO  org.hibernate.engine.transaction.jta.platform.internal.JtaPlatformInitiator - HHH000490: Using JtaPlatform implementation: [org.hibernate.engine.transaction.jta.platform.internal.NoJtaPlatform]
08:05:34.940 [main] INFO  org.springframework.orm.jpa.LocalContainerEntityManagerFactoryBean - Initialized JPA EntityManagerFactory for persistence unit 'default'
08:05:34.981 [main] WARN  org.springframework.boot.autoconfigure.orm.jpa.JpaBaseConfiguration$JpaWebConfiguration - spring.jpa.open-in-view is enabled by default. Therefore, database queries may be performed during view rendering. Explicitly configure spring.jpa.open-in-view to disable this warning
08:05:35.414 [main] INFO  org.springframework.security.web.DefaultSecurityFilterChain - Will secure any request with [org.springframework.security.web.context.request.async.WebAsyncManagerIntegrationFilter@32c8d67, org.springframework.security.web.context.SecurityContextPersistenceFilter@453439e, org.springframework.security.web.header.HeaderWriterFilter@2aac87ab, org.springframework.security.web.csrf.CsrfFilter@12811f95, org.springframework.security.web.authentication.logout.LogoutFilter@7cc3a7f7, org.springframework.security.web.authentication.UsernamePasswordAuthenticationFilter@af007d6, org.springframework.security.web.savedrequest.RequestCacheAwareFilter@779ef5cb, org.springframework.security.web.servletapi.SecurityContextHolderAwareRequestFilter@446981a4, org.springframework.security.web.authentication.AnonymousAuthenticationFilter@281963c, org.springframework.security.web.session.SessionManagementFilter@72c5064f, org.springframework.security.web.access.ExceptionTranslationFilter@5b74bb75, org.springframework.security.web.access.intercept.FilterSecurityInterceptor@4b4228cf]
08:05:35.581 [main] INFO  org.springframework.boot.autoconfigure.web.servlet.WelcomePageHandlerMapping - Adding welcome page: class path resource [static/index.html]
08:05:35.678 [main] INFO  org.apache.coyote.http11.Http11NioProtocol - Starting ProtocolHandler ["http-nio-8080"]
08:05:35.696 [main] INFO  org.springframework.boot.web.embedded.tomcat.TomcatWebServer - Tomcat started on port(s): 8080 (http) with context path ''
08:05:35.705 [main] INFO  com.example.demo.DemoApplication - Started DemoApplication in 3.592 seconds (JVM running for 4.213)
08:06:08.234 [http-nio-8080-exec-1] INFO  org.apache.catalina.core.ContainerBase.[Tomcat].[localhost].[/] - Initializing Spring DispatcherServlet 'dispatcherServlet'
08:06:08.234 [http-nio-8080-exec-1] INFO  org.springframework.web.servlet.DispatcherServlet - Initializing Servlet 'dispatcherServlet'
08:06:08.235 [http-nio-8080-exec-1] INFO  org.springframework.web.servlet.DispatcherServlet - Completed initialization in 1 ms



 

Виконання ДЗ 35. Spring Security

1. Реалізувати клас Product. Цей клас зберігатиме значення: id, name, cost

2. Замовлення зберігатимуться у спеціалізованому класі-репозиторії ProductRepository.
2.1 Реалізувати метод отримання за id
2.2 Реалізувати метод отримання все
2.3 Реалізувати метод додавання
2.4 Реалізувати метод видалення

3. Реалізувати клас User. Цей клас зберігатиме значення: id, name, password, role

4. Реалізувати клас SecurityConfiguration.
4.1 Цей клас повинен забороняти доступ до програми для неавторизованих користувачів
4.2 Цей клас повинен відкрити можливість автентифікації за допомогою Basic Authentication. Вхідні дані порівнюються з даними в БД
4.3 Операції додавання, видалення замовлення повинні бути доступні тільки для користувача за участю Admin

5. Налаштувати Spring-додаток через application.yml

6.1 Додаток має бути доступний за URL: http://localhost:8080
6.2 Налаштувати підключення в БД
6.3 Налаштувати логування на рівні INFO для пакетів програми та пакету org.springframework.web 

Процес логування включає виведення в консоль і запис у файл

7. Реалізувати контролер Ping для перевірки того, що програма працює. Цей контролер має лише один спосіб і повертає повідомлення “ОК”.
7.1 Контролер доступний за URL: http://localhost:8080/ping
7.2 Цей контролер доступний всім користувачам

8. Реалізувати контролер для взаємодії з ресурсом Product.
8.1 Контролер доступний за URL: http://localhost:8080/products
8.2 Отримання конкретного продукту
8.3 Отримання всіх продуктів
8.4 Видалення продукту
8.5 Додавання продукту

ВАЖЛИВО: ProductRepository повертає дані з БД, для цього необхідно створити БД та відповідні таблиці

==========================

У процесі реалізації задачі створив нові класи та методи.

Якщо зайти на http://localhost:8080 -- підвантажується вікно авторизації, за кредами admin/admin отримуємо Welcome сторінку

http://localhost:8080/ping -- видає OK

http://localhost:8080/products -- доступний, підключення до бази створено, able to orders operation if needed
