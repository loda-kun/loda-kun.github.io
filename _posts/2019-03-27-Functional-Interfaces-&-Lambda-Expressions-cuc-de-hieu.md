---
id: loda1553649037877
layout: post
title: '「Java 8」Functional Interfaces & Lambda Expressions cực dễ hiểu'
author: loda
categories: [ java, java 8 ]
image: assets/images/loda1553649037877/1.jpg
description: Giải thích ý nghĩa là lí do hình thành Functional Interfaces, hướng dẫn sử dụng Lambda Expressions
---

Khái niệm `Functional Interfaces` được `Java` đưa ra cùng với phiên bản `Java 8`. về cơ bản, có thể hiểu:

> `Functional Interfaces` là interface nhưng chỉ có một 1 abstract function duy nhất.

Ví dụ:

```java
interface Runable{
    public void run(); // Chỉ có duy nhất một abstract function.
}
```

Dễ hiểu phải hem các bạn :3 Tuy nhiên, vì sao lại đưa ra khái niệm này và nó giúp ích gì cho `developer` như chúng ta. 

#### Functional Programming

Trước khi đi vào chi tiết, chúng ta cùng tìm hiểu khái niệm `Lập trình hướng hàm`.

Cùng xem ví dụ dưới đây:

```java
public static void main(String[] args) {
    // Mình muốn xử lý dữ liệu trước khi ỉn ra màn hình.
    System.out.println(process("Hey Loda!!!"));
}

public static String process(String input){
    // Cho tất cả viết hoa lên.
    return input.toUpperCase();
}

// Output: 
HEY LODA!!!
```

Hẳn đây là ví dụ dễ nhất thế giới :))) 

Tuy nhiên bạn sẽ thấy cách làm này không `flexible`, vì các bạn chỉ có thể xử lý cho chữ thành `UPPER CASE`. Muốn làm gì đó khác, như `toLowerCase` chẳng hạn, mình sẽ phải viết một `function` mới.

Chúng ta giải quyết cách cách này bằng `Anonymous function (Hàm ẩn danh)`

Sửa code chút:
```java
public interface StringProcessor{
    public String process(String input);
}

public static String getStr(String input, StringProcessor processor){
    return processor.process(input);
}


public static void main(String[] args) {
    // In ra chữ hoa
    System.out.println(getStr("Hello Loda!", new StringProcessor() {
        @Override
        public String process(String input) {
            return input.toUpperCase();
        }
    }));


    // In ra chữ thường
    System.out.println(getStr("Hey Loda!", new StringProcessor() {
        @Override
        public String process(String input) {
            return input.toLowerCase();
        }
    }));
}
// Output:
// HELLO LODA!
// hey loda!
```

Đây chính là `Lập trình hướng hàm` các bạn ạ, mục đích của nó là chúng ta đưa `hành vi` vào `hàm`. Hay nói cách khác là đưa thêm các đoạn code vào hàm như là một parameter.

> `Lập trình hướng hàm` là đưa hành vi vào hàm.

Tuy nhiên có một nhược điểm trong khi áp dụng cách này đó là viết code rất dài 😭 Chỉ mỗi việc in ra màn hình cũng mất của chúng ta 6-7 dòng code.

Đây là lúc mà `Lambda Expressions` ra đời.

#### Lambda Expressions

Quay lại ví dụ ở trên, cùng phân tích:

Chúng ta thấy là `StringProcessor` chỉ có duy nhất một `function process(xx)` (liên tưởng gì chưa các bạn :3). Nên mọi đoạn code đều sẽ giống hệt nhau ở việc `implement function` này.

```java
new StringProcessor() {
    @Override
    public String process(String input) {
        // Do something here
        // Chỉ khác nhau đoạn code ở giữa
        return x;
    }
}
```
Thực ra cái chúng ta quan tâm là:

* đầu vào `input` (`String`)
* một hoặc nhiều thao tác xử lý `input`
* cho tôi đầu ra là `output` (`String`)

đúng chứ?

Có cách nào để rút ngắn `code` hơn, nhưng vẫn không làm nhập nhằng ý nghĩa của `code`?

`Java 8` thấu hiểu sự bất cập này và đưa ra khái niệm `Lambda Expression`:

```java
// (input) -> input.toUpperCase()
// đầu vào -> đầu ra
System.out.println(getStr("Hello Loda!", input -> input.toUpperCase()));
```

> `Lambda Expression` là một cách định nghĩa ngắn gọn khi `implement` một `Functional Interface` (interface chỉ có một function) 

Cấu trúc của một lambda như sau:
```java
parameter -> expression body
```
Trong đó: 

* `parameter` là những tham số đầu vào của hàm (một hoặc nhiều)

* `expression body` là phần xử lý `parameter`, bạn cần trả ra đúng kiểu dữ liệu đã khai báo trong `Functional Interface`

Nếu `code` bạn chỉ cần 1 thao tác, thì không cần `return` giống ví dụ ở trên. Còn nếu `code` yêu cầu xử lý nhiều, thì dạng đầy đủ của nó như sau:

```java
parameter -> {
    expression body
    [return] (không trả về nếu là void)
}
```

ví dụ:

```java
System.out.println(getStr("Hello Loda!", input -> {
    String temp =  input + " Đừng quên like fanpage nhé!!!";
    return temp.toLowerCase();
}));
```

#### `Functional Interface`

Tới đây, bạn đã hiểu ý nghĩa của việc cho ra đời khái niệm `Functional Interface`, nó là một quy định chung phải có để có thể viết code dưới dạng Lambda.

Một số điều cần lưu ý với `Functional Interface` như sau:

##### `@FunctionalInterface`

`Annotation` này chỉ để bổ sung, nó đánh dấu một `interface` là `Functional Interface`. Lúc này bạn khai báo 2 `abtract function` bên trong `interface` thì sẽ báo lỗi.

```java
@FunctionalInterface // Gắn cái này lên interface, nó đánh dấu interface chỉ được phép có 1 funtion thôi
public interface StringProcessor{
    public String process(String input);
    public String preProcess(String input); // lỗi
}
```

#### `default function` & `static funtion`

`Java 8` cải tiến cho phép `interface` được khai báo `code` bên trong nó, với điều kiện `code` phải nằm trong `default` hoặc `static`.

`default` và `static` không phá vỡ quy luật của `@FunctionInterfaces`

```java

@FunctionalInterface // Gắn cái này lên interface, nó đánh dấu interface chỉ được phép có 1 funtion thôi
public interface StringProcessor{
    public String process(String input);
    // Mọi class implement StringProcessor đều có thể gọi hàm này để sử dụng luôn
    public default void printf(Object t){
        System.out.println(t);
    }

    // Là hàm static, gọi từ class cũng được.         StringProcessor.concat(a,b)
    public static String concat(String a, String b){
        return a + b;
    }
}
```


#### Lời kết

Tới đây, bạn đã nắm trong tay những khái niệm được coi là mạnh mẽ nhất `Java 8` rồi :))) Cầm và quẩy trong tất cả các đoạn code sắp tới của mình nhé.

Chúc các bạn thành công và nhớ like và chia sẻ cho bạn biết nhé, ahoho!