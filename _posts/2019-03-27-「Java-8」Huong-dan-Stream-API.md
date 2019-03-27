---
id: loda1553677531692
layout: post
title: '「Java 8」Hướng dẫn Stream API'
author: loda
categories: [ java, java 8 ]
image: assets/images/loda1553677531692/1.jpg
description: Hướng dẫn và giải thích nguyên lý làm việc của Stream trong Java 8
---

`Stream` là một trong những concept được coi là đem sự thay đổi lớn nhất trong `Java 8`. Để có thể hiểu được nội dung này trọn vẹn, mình đề nghị các bạn đọc trước các khái niệm sau:

[Functional Interfaces & Lambda Expressions][link-functional]

[Optional][link-optional]

#### Khái quát

`Stream` là một abtract layer cho phép bạn xử lý một dòng dữ liệu dựa trên các thao tác đã định nghĩa trước.

Bạn có thể tạo `Stream` từ các nguồn dữ liệu như `Collections`, `Arrays` hoặc `I/O resources`.

```java
Collection<String> collection = Arrays.asList("hello", "loda", "kaka");
Stream<String> streamOfCollection = collection.stream(); // Tạo ra một stream từ collection
```

Mặc định các lớp kế thừa của `Collection` đều có hàm `.stream()`:

```java
List<String> list = new ArrayList<>();
Stream<String> stream = list.stream(); // tạo ra 1 luồng
Stream<String> parallelStream = list.parallelStream(); // luồng dữ liệu song song (xử lý trên nhiều thread cùng lúc)
```

#### Cách sử dụng

Chức năng của `Stream` là cực kì đa dạng giúp bạn thao tác dữ liệu dễ dàng hơn.

#### forEach

Duyệt qua toàn bộ dữ liệu của bạn

```java
list.stream().forEach(s -> System.out.println(s));
```

#### map

Tạo ra các giá trị mới từ dữ liệu hiện có

```java

Arrays.asList(3, 5, 7)
    .stream() // tạo ra Stream từ List<Integer>
    .map(i -> "loda-"+i) // biến đổi từng phần tử thành String 
    .map(String::toUpperCase) // biến đổi từng phần tử thành Upper case
    .forEach(System.out::println); // in ra xem thử
```

#### filter

`filter()` gíup chúng ta thao tác với những dữ liệu mong muốn

```java
Arrays.asList(2, 3, 5, 7)
    .stream()
    .filter(i -> i % 2 != 0)
    .map(i -> "loda-" + i)
    .map(String::toUpperCase)
    .forEach(System.out::println);
```

#### limit

Giới hạn số lượng dữ liệu cần xử lý

```java
IntStream.range(1, 1000).boxed() // Tạo ra Stream có dữ liệu từ 1->999
            .filter(i -> i % 2 != 0)
            .map(i -> "loda-" + i)
            .map(String::toUpperCase)
            .limit(10)
            .forEach(System.out::println);
```

#### sorted

sắp xếp `Stream`

```java
IntStream.range(1, 1000).boxed() // Tạo ra Stream có dữ liệu từ 1->999
            .filter(i -> i % 2 != 0)
            .map(i -> "loda-" + i)
            .map(String::toUpperCase)
            .limit(10)
            .forEach(System.out::println);
// OUTPUT: 
/*
LODA-1
LODA-11
LODA-13
LODA-15
*/
// đây là vì dữ liệu là String, nó đang sort StringString
```

Bạn có thể tự định nghĩa cách sort bằng cách thêm Comparator vào

```java
.sorted((o1, o2) -> o1.compareTo(o2))
```

#### collect

`collect` giúp chúng ta lấy toàn bộ dữ liệu đã biến đổi trong `Stream` thành đối tượng mình mong muốn

```java

List<String> result = IntStream.range(1, 1000).boxed()
                                .filter(i -> i % 2 != 0)
                                .map(i -> "loda-" + i)
                                .map(String::toUpperCase)
                                .limit(10)
                                .sorted(Comparator.naturalOrder()) // một cách khác để sort
                                .collect(Collectors.toList());

```

#### Xử lý song song

```java

List<String> result = IntStream.range(1, 1000).boxed()
                                .parallel() // tạo một Stream xử lý dữ liệu song song, tương đương với parallelStream()
                                .filter(i -> i % 2 != 0)
                                .map(i -> "loda-" + i)
                                .map(String::toUpperCase)
                                .limit(10)
                                .sorted(Comparator.naturalOrder()) // một cách khác để sort
                                .collect(Collectors.toList());

```

#### Bản chất của Stream

Bạn hãy chạy chương trình này nhé

```java
List<String> result = Stream.of("bạn", "hãy", "like", "Fanpage", "loda","dể","cập","nhật","nhiều","hơn")
                            .filter(s -> {
                                System.out.println("[filtering] " + s);
                                return s.length()>=4;
                            })
                            .map(s -> {
                                System.out.println("[mapping] " + s);
                                return s.toUpperCase();
                            })
                            .limit(3)
                            .collect(Collectors.toList());
System.out.println("----------------------");
System.out.println("Result:");
result.forEach(System.out::println);
```

Kết quả:

```java
[filtering] bạn // không thoả mãn
[filtering] hãy // tiếp tục tìm, cũng k thoả mãn
[filtering] like // thoả mãn
[mapping] like // mapping nó luôn
[filtering] Fanpage // lại quay lại filter tìm tiếp, thoả mãn
[mapping] Fanpage // mapping
[filtering] loda // thoả mãn
[mapping] loda // mapping
// Đủ 3 trường hợp thoả mãn, dừng.
----------------------
Result:
LIKE
FANPAGE
LODA
```

Bạn sẽ thấy rằng chương trình chỉ xử lý dữ liệu vừa đủ thoả mãn điều kiện `limit(3)` mà thôi, còn lại nó sẽ bỏ qua để tối ưu hoá performance.

Chứng tỏ `Stream` là `Lazy evaluation`. Hiểu đơn giản là nó sẽ không xử lý dữ liệu trực tiếp qua từng bước, mà chờ bạn khai báo xong tất cả các thao tác như `map`, `filter`,v.v.. rồi thực hiện toàn bộ trong một vòng lặp duy nhất.

Một lưu ý khi sử dụng là **Stream không được tái sử dụng**.
Ví dụ:

```java

Stream<String> stream = 
  Stream.of("loda", ".", "me","like").filter(element -> element.contains("e"));
Optional<String> anyElement = stream.findAny(); //Lấy ra một phần tử bất kỳ trong Stream, nó sẽ trả ra Optional 

// Thực hiện dòng lệnh tiếp theo sẽ bắn ra IllegalStateException
Optional<String> firstElement = stream.findFirst();
```

Vì `Stream` được tạo ra để **xử lý** dữ liệu chứ không phải để **lưu trữ**!

Nên muốn sử dụng, mỗi lần bạn sẽ cần tạo ra 1 `Stream` mới.


#### Lời kết

Tới đây là bạn đã có thể sử dụng `Stream` để giúp code của mình bá đạo hơn bao giờ hết rồi đấy!

Chúc bạn thành công, và chớ quên chia sẻ cho bạn bè nhé, ohoho :3

[link-functional]: localhost.com
[link-optional]: localhost.com