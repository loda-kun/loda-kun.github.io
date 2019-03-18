---
id: loda1552901817707
layout: post
title: '「Spring-boot #1」Hướng dẫn sử dụng Spring Profiles'
author: loda
categories: [ spring-boot, spring, spring profiles, java ]
image: assets/images/loda1552901817707/1.jpeg
description: Hướng dẫn sử dụng Spring Profiles quản lý cấu hình ứng dụng trên các môi trường khác nhau
---

`Spring Profiles` là một core feature trong `Spring Framework`, cho phép chúng ta cấu hình ứng dụng, active/deactive bean tuy theo môi trường.

Một kịch bản thực tế:

> Mình có 1 ứng dụng `Spring Boot` dùng để đọc báo, tuy nhiên mình phải hosting nó trên `AWS`. Vấn đề lúc này là khi đang viết code ở local thì mình cần kết nối với `MySQL` tại máy tính của mình, khi đưa lên AWS thì cần kết nối tới `MySQL` của `AWS`. Ngoài ra, chưa kể mình muốn cấu hình các biến cục bộ khác cho phù hợp với môi trường như `log`, `redis`, `secret`, v.v.. đặc biệt là việc một số phần trong code có thể thay đổi theo môi trường nữa.

```yml
constants:
  service:
    phase: ALPHA
    debug: true

spring:
  redis:
    clusterUri: redis://abdheyj3847A@10.127.155.18:7000
  datasource:
    username: xxx
    password: none
    url: jdbc:mysql://10.127.233.12:2030/news?useSSL=false&characterEncoding=UTF-8

news:
  api:
    channel-id: 1510354028
    channel-secret: e17c94a02293b33a32629407b32b40a5
    official-account-mid:
    connection-timeout-secs: 20
    .
    .
    ..
```

rất rất nhiều config phải không :((((

Sớm nhận ra những khó khăn trong việc config khi xây dựng ứng dụng, nên `Spring` đã cho ra đời `Spring Profiles` để giải quyết các vấn đề này.

#### 1. Tạo file config
`Spring Profiles` có sẵn trong `Framework` rồi nên bạn không cần thêm bất kì thư viện nào khác. 

Để sử dụng, các bạn tạo file config tại thư mục `resources` trong project. Mặc định `Spring` sẽ nhận các file có tên như sau:
```java
application.properties
application.yml
application-{profile-name}.yml // .properties
```

ví dụ mình có 2 môi trường, mình sẽ tạo ra các file như thế này:

```java
application.yml
application-local.yml
application-aws.yml
application-common.yml
```

`application` là file config chính khai báo các enviroment.
`application-local` chỉ sử dụng khi chạy chương trình ở local
`application-aws` chỉ sử dụng khi chạy ở AWS
`application-common` là những config dùng chung, môi trường nào cũng cần.

Bây giờ, mình sẽ khai báo trong từng file như sau:

_application.yml_

```yml
#application.yml
---
spring.profiles: local
spring.profiles.include: common, local
---
spring.profiles: aws
spring.profiles.include: common, aws
---
```

_application-aws.yml_

```yml
spring:
  datasource:
    username: xxx
    password: xxx
    url: jdbc:mysql://10.127.24.12:2030/news?useSSL=false&characterEncoding=UTF-8
```

_application-local.yml_

```yml
spring:
  datasource:
    username: root
    password:
    url: jdbc:mysql://localhost:3306/news?useSSL=false&characterEncoding=UTF-8

logging:
  level:
    org:
      hibernate:
        SQL: debug
```

_application-common.yml_

```yml
spring:
  jpa:
    properties:
      hibernate:
        jdbc:
          batch_size: 50
          batch_versioned_data: true
    hibernate:
      ddl-auto: none
```

Tadaa, xong, mình giải thích chút. bạn để ý trong file `application.yml` mình có khai báo 2 môi trường là `local` và `aws`. Tại mỗi môi trường sẽ `include` (bao gồm) các file config như kia. Khi mình kích hoạt `aws` chẳng hạn, `Spring` sẽ load tất cả config có trong `application-common.yml` và `application-aws.yml`. Rất tiện phải không :3 

#### 2. Kích hoạt config

Để sử dụng một `Profiles` bạn có các cách sau:

**#1: Sử dụng `spring.profiles.active` trong file `application.properties` hoặc `application.yml`**
```yml
spring.profiles.active=aws
```

**#2: Active trong code, trước khi chạy chương trình.**

```java
@Configuration
public class ApplicationInitializer 
  implements WebApplicationInitializer {
 
    @Override
    public void onStartup(ServletContext servletContext) throws ServletException {
        servletContext.setInitParameter(
          "spring.profiles.active", "aws");
    }
}
```
hoặc
```java
@Autowired
private ConfigurableEnvironment env;
...
env.setActiveProfiles("aws");
```
hoặc
```java
SpringApplication application = new SpringApplication(SpringBootProfilesApplication.class);
ConfigurableEnvironment environment = new StandardEnvironment();
environment.setActiveProfiles("aws");
application.setEnvironment(environment);
application.run(args);
```
Mình không khuyến khích cả 3 cách này ==!

**#3: Sử dụng JVM System Parameter (nên dùng)**
```java
-Dspring.profiles.active=aws
```
**#4: Environment Variable (Unix) (nên dùng)**
```bash
export SPRING_PROFILES_ACTIVE=aws
```

Nếu ai sử dụng `Intellij IDEA` thì có thể config ngay trong IDE như thế này, mỗi lần chạy nó tự active cho mình.


#### 3. Sử dụng Profiles trong code

Khi đã có `Profile` rồi, bây giờ ở trong `code`, bạn có thể toàn quyền quyết định xem `Bean` hay class nào sẽ được quyền chạy ở môi trường nào. Bằng cách sử dụng annotation `@Profile`

```java
// Bean này chỉ Spring khởi tạo và quản lý khi môi trường là `local`
@Component
@Profile("local")
public class LocalDatasourceConfig
```
Ngoài ra bạn có thể sử dụng toàn tử logic ở đây, ví dụ:
```java
// Bean này chỉ Spring khởi tạo và quản lý khi môi trường là những môi trường không phải là `local`
@Component
@Profile("!local")
public class LocalDatasourceConfig
```

Okiee lahhh, thế là mình đã giới thiệu xong với các bạn `Spring Profiles`, Đây là một tính năng cực kì cực kì hữu ích, hi vọng các bạn hiểu và nắm được kiến thức, áp dụng vào sản phẩm của chính mình. Chúc các bạn thành công!

Đứng quên like và chia sẻ cho bạn bè cùng biết nhé, ahihi :3 