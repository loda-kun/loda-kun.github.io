---
id: loda1553919997213
layout: post
title: 'Hướng dẫn tạo Spring Boot với nhiều modules bằng Gradle'
author: loda
categories: [ Java, Spring boot, gradle ]
image: assets/images/loda1553919997213/1.jpg
description: Hướng dẫn sử dụng Gradle để tạo một project Spring Boot với nhiều module con.
---


`Gradle` là một open-source có nhiệm vụ tự động hóa quá trình đóng gói một dự án với ưu điểm chính khả năng tùy biến cao và cho hiệu năng tốt.

`Gradle` ra đời sau và cải thiện các phần còn yếu của `Maven` như cú pháp khai báo rườm rà, khó quản lý, tốc độ build và test còn chưa được tối ưu. 
 
Để tận dụng những lợi thế này, hôm nay chúng ta sẽ tạo ra một project `Spring boot` với nhiều `module` với `Gradle` thay vì là `Maven` như truyền thống.


#### Spring Initializr

Để tạo ra một project Spring, việc tạo bằng tay là hơi vất vả, vì thế chúng ta sẽ dùng `Spring Initializr` do Spring cung cấp.

Bạn truy cập vào: [https://start.spring.io](https://start.spring.io)

Và đặt tên cho project và chọn build bằng `Gradle` như hình:

![spring-gradle](/assets/images/loda1553919997213/2.jpg){:class="center-image"}

Tiếp đến, chọn các `dependencies` đi kèm, và `Generate Project`


![spring-gradle](/assets/images/loda1553919997213/3.jpg){:class="center-image"}

Tải project về, và mở bằng `Intellij IDEA`

![spring-gradle](/assets/images/loda1553919997213/4.jpg){:class="center-image"}

Lần đầu nó sẽ phải download `Gradle Wrapper` nên hơi lâu chút, bạn ráng chờ hah. Sau khi nó sync xong thì sẽ được một project như này.

![spring-gradle](/assets/images/loda1553919997213/5.jpg){:class="center-image"}

Okay, thế là xong phần khởi tạo 1 project rồi!


#### Tạo module

Để phục vụ cho các mục đích khác nhau, mình sẽ chia project này thành 2 module là:

* `common`: Mục đích là để chứa `model` dùng chung và `repository` của nó

* `service`: Xử lý mọi thử ở đây

bạn tạo module bằng cách: `Chuột phải` > `New` > `New Module`

![spring-gradle](/assets/images/loda1553919997213/6.jpg){:class="center-image"}

Sau đó chọn, module là `gradle` > `java` và nhập tên module:

![spring-gradle](/assets/images/loda1553919997213/7.jpg){:class="center-image"}

Như vậy là chúng ta có 2 cái module nho nhỏ như này:

![spring-gradle](/assets/images/loda1553919997213/8.jpg){:class="center-image"}


#### Config Build.gradle

Bây giờ chúng ta sẽ config lại `build.gradle` của từng module.

Các file `build.gradle` đều có sẵn thông tin trong đó, nhưng bạn xóa hết đi và thêm lại như mình hướng dẫn ở dưới

Tại `build.gradle` ở thư mục gốc. (`multiple-module-gradle/build.gradle`):

```gradle
// Tại build.gradle gốc, chúng ta config để các thằng module con có thể có chung cấu hình, kế thừa plugin và dependencies của thằng cha này luôn.

// Như vậy thì lúc sau các module không cần config gì nữa.

allprojects {
	group 'me.loda.springboot'
	version '1.0-SNAPSHOT'

	apply plugin: 'eclipse'
	apply plugin: 'idea'
}

buildscript {
	ext {
		springBootVersion = '2.0.5.RELEASE'
		springManagementVersion = '1.0.7.RELEASE'
		lombokVersion = '1.18.6'
	}
	repositories {
		mavenCentral()
		jcenter()
	}
	dependencies {
		classpath("org.springframework.boot:spring-boot-gradle-plugin:${springBootVersion}")
		classpath("io.spring.gradle:dependency-management-plugin:${springManagementVersion}")
	}

}
subprojects {

	apply plugin: 'java'
	apply plugin: 'eclipse'
	apply plugin: 'io.spring.dependency-management'
	apply plugin: 'org.springframework.boot'

	sourceCompatibility = 1.8
	targetCompatibility = 1.8

	repositories {
		mavenLocal()
		mavenCentral()
	}

	dependencies{
		// SPRING DEPENDENCIES
		implementation 'org.springframework.boot:spring-boot-starter-data-jpa'
		implementation 'com.h2database.h2'

		// Utilities
		compileOnly "org.projectlombok:lombok:${lombokVersion}"
		annotationProcessor "org.projectlombok:lombok:${lombokVersion}"

		// TEST
		testImplementation 'org.springframework.boot:spring-boot-starter-test'
	}
}

```

Tại `build.gradle` ở module `service`. (`multiple-module-gradle/service/build.gradle`):

```gradle
// Thằng service này là thằng chạy chính, nên chúng ta cho thêm cái dependency web vào. Ngoài ra nó còn sử dụng các class ở module common nữa
dependencies {
    compile project (':common')
    compile('org.springframework.boot:spring-boot-starter-web')
    compile('org.springframework.boot:spring-boot-devtools')
}

// Cả file chỉ có bấy nhiêu dòng :))
```


Tại `build.gradle` ở module `common`. (`multiple-module-gradle/common/build.gradle`):

```gradle
// Bỏ trống,
// nếu cần gì bổ sung sau

// Hiện tại nó kế thừa từ `build.gradle` gốc là đủ dependencies để dùng rồi
```


#### Viết chương trình demo

Chúng ta sẽ tạo ra một project đơn giản:

* `common`: Chưa thông tin model `User`.

* `service`: Tạo ra `User` và dùng tầng `common` để lưu nó


#### Common

Cấu trúc module `common`:

![spring-gradle](/assets/images/loda1553919997213/9.jpg){:class="center-image"}

```java
// User.java
import java.io.Serializable;

import javax.persistence.Entity;
import javax.persistence.GeneratedValue;
import javax.persistence.Id;
import lombok.Data;
import lombok.RequiredArgsConstructor;

@Entity
@Data
@RequiredArgsConstructor
public class User implements Serializable {

    @Id
    @GeneratedValue
    private Long id;

    private final String name;
}
```

```java
// UserRepository

import org.springframework.data.jpa.repository.JpaRepository;

public interface UserRepository extends JpaRepository<User, Long> {
}
```

Chúng ta chỉ làm demo để chứng minh là các `module` đã hoạt động thôi :))))

Ở đây mình sử dụng `H2 Database`, là một dạng database lưu trữ trên bộ nhớ, được autoconfig trong `Springboot` rồi, nên các bạn chỉ cần tạo lớp `User` như kia, rồi chạy chương trình là nó tự tạo `table` tương ứng

Còn Các `annotation` ngoại lai kia chính là của `Lombok`. Để hiểu nó có ý nghĩa gì và sức mạnh của `Lombok` bạn xem bài viết sau:

[Hướng dẫn sử dụng Lombok, giúp code Java nhanh hơn 69%](https://loda.me/Huong-dan-su-dung-Lombok-giup-code-Java-nhanh-hon-69/)

#### Service

Bên module `service` chúng ta sẽ lấy tầng `common` ra xài:

![spring-gradle](/assets/images/loda1553919997213/10.jpg){:class="center-image"}

```java
// Application.java

import javax.transaction.Transactional;

import org.springframework.boot.CommandLineRunner;
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

import lombok.RequiredArgsConstructor;

@SpringBootApplication
@RequiredArgsConstructor
public class Application implements CommandLineRunner {
    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }

// Không cần @Autowired, vì chúng ta có @RequiredArgsConstructor rồi
    private final UserRepository userRepository;

    @Override
    @Transactional
    public void run(String... args) throws Exception {
        User user = new User("loda");

        user = userRepository.save(user);
        System.out.println(user);
    }
}

```


Chạy chương trình:

```java
// Output
// User(id=1, name=loda)

// user được insert vào database là có id = 1.
// project chạy thành công!
```


#### Lời kết

Vậy là chúng ta đã tạo ra một project với nhiều module bằng `Gradle` và `Spring boot`. Có thể thấy `Gradle` cho phép chúng ta khai báo khá dễ đọc, và gọn gàng. Ngoài ra bản thân nó còn được cộng đồng open-source cung cấp nhiều `plugin` nên gần như chúng ta không cần làm gì nhiều, chỉ cần apply plugin là xong!

Chi tiết project mình để tại [Github](https://github.com/loda-kun/multiple-module-gradle).

Chúc các bạn thành công! chớ quên like or share ủng hộ mềnh nha ahoho!:3 

