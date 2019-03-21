---
id: loda1553158182446
layout: post
title: '「Java basic #3」Hàm và câu lệnh điều kiện'
author: loda
categories: [ java, java basic, series 2 tuần ]
image: assets/images/loda1553158182446/1.jpg
description: Hướng dẫn sử dụng câu lệnh rẽ nhánh, điều kiện if else trong java
---

Helluuuuuu eveerybody, Lại là mình `loda` đây. Trong bài này chúng ta sẽ đi tìm hiểu các câu lệnh rẽ nhánh hay điều kiện trong `Java`, từ đó giúp chúng ta điều hướng được chương trình theo ý muốn của mình. Cùng vào bài luôn nhé.

#### if

Các bạn nhìn qua ví dụ này:

```java
 public static void main(String[] args){
    // khai bao so nguyen
    int a = 10;
    
    // Kiểm tra xem a có bằng 9 không
    if(a == 9){
        // nếu bằng 9, in ra màn hình "Hello"
        System.out.println("Hello");
    }
    // Kiểm tra xem a có bằng 9 không
    if(a == 10){
        // nếu bằng 10, in ra màn hình "World"
        System.out.println("World");
    }

// Kết quả trên màn hình: 
// World
}
```

Nếu các bạn chạy ví dụ ở trên thì sẽ thấy kết quả trên màn hình chỉ có chữ `World`. Lí do thì bạn biết rồi phải không 😗 Cái mình muốn các bạn để ý ở đây là cái dấu `==`. Sao lại `==` 🤔 mà không phải `=`

Thì các cần biết như sau, câu lệnh `if` là một câu lệnh điều kiện, và nhận vào là một điều kiện `true` hoặc `false`. Có cú pháp như sau:

```java
if ([điều kiện]){
    // Thực hiện đoạn code nếu [điều kiện] là `true`. Nếu `false` bỏ qa đi xuống dưới.
}
// Tiếp tục thực hiện đoạn code phía dưới
```

Lúc này nếu bạn viết `if(a = 5)` như Sách giáo khoa toán thì sẽ nhận về kết cục cay đắng 😢 vì trong [Bài #2][link-bai2] mình có nói, dấu `=` là phép gán. Tức là gán cho `a` giá trị bằng `5` chứ không phải ý nghĩa là `so sánh a với 5` để mà trả về là `true` hay `false` nữa.

Vậy đấy, nên để so sánh bạn cần dùng `toán tử quan hệ` mình liệt kê dưới đây:

* `==`: Kiểm tra 2 toán hạng có `bằng nhau` không? (`if(a==b)`)
* `!=`: Kiểm tra 2 toán hạng có `khác nhau` không? (`if(a!=b)`)
* `>`: Kiểm tra toàn hạng A có `lớn hơn` B không? (`if(a>b)`)
* `<`: Kiểm tra toàn hạng A có `nhỏ hơn` B không? (`if(a<b)`)
* `>=`: Kiểm tra toàn hạng A có `lớn hơn hoặc bằng` B không? (`if(a>=b)`)
* `<`: Kiểm tra toàn hạng A có `nhỏ hơn hoặc bằng` B không? (`if(a<=b)`)

Tất cả `toán tử logic` ở trên, khi thực hiện xong nó sẽ trả về là kiểu `boolean`, nên bạn có thể gán nó vào một biến bất kỳ, như lày:

```java
int a = 5;
int b = 6;

boolean result = a == b; // false

System.out.println("Result: " + result);

// Kết quả in ra trên màn hình: 
// "Result: false"

if(result){ // viết tắt của if(result == true)
    System.out.println("Result is true");
}


```

Đến đây, có thể nói câu lệnh `if` thực chất nhận vào một giá trị `boolean`.


#### else

Tiếp theo, chúng ta tới với dạng đầy đủ của `if` chính là cấu trúc `if else`.

```java
if ([điều kiện]){
    // Thực hiện đoạn code nếu [điều kiện] là `true`. 
}else{
    // Thực hiện đoạn code trong này nếu [điều kiện] là `false`
}
//Các đoạn code ở dưới thực hiện bình thường sau khi if hoặc else diễn ra
```

Ví dụ:

```java
int a = 5;
if ( (a + 2) == 7 ){
    System.out.println("Bằng 7");
    // Sử dụng biến `a` ở ngay trong scope {} của `if`,, như bài #2 mình có nói, biến được sử dụng trong các scope con hoặc bằng cấp
    System.out.println("Giá trị lúc này của a = " + a);
}else{
    System.out.println("Khác 7");
    System.out.println("Giá trị lúc này của a = " + a);
    int b = 7; // Tạo ra 1 biến b trong else
}

b = 50; // Lỗi, không biết b là gì, vì b ở scope nhỏ hơn, bên ngoài không hiểu.

```

Ví dụ trên mình vừa cho các bạn thấy cách sử dụng `if else` vừa củng cố lại kiến thức của [Bài #2][link-bai2] luôn.


#### Toán tử logic

Toán tử logic là những toán tử giúp chúng ta kết hợp nhiều [điều kiện] lại với nhau. 

Ví dụ mình nói: `"Nếu ab = 3 VÀ ac = 4 VÀ bc = 5 thì abc là tam giác vuông"`

Thì trong code cần viết chương trình như thế nào?

Cách 1: Sử dụng `if` thông thường.
```java
int ab = 3;
int ac = 4;
int bc = 5;

if(ab == 3){
    if(ac == 4){
        if(bc == 5){
            System.out.println("abc là tam giác cực vuông");
        }
    }
}
```

Ohhh loooo, my eyes 😱 tôi đang nhìn cái rì thế này. Một chương trình là có vài trăm cái điều kiện chắc chết.

Cách 2: Sử dụng `if` và `toán tử logic`
```java
int ab = 3;
int ac = 4;
int bc = 5;

// Nếu ab = 3 VÀ ac = 4 VÀ bc = 5
if(ab == 3 && ac == 4 && bc==5){ 
    // thì abc là tam giác vuông
    System.out.println("abc là tam giác cực vuông");
}
```

Rất gì và này nọ phải không :))) đọc sao viết code y xì vậy, qua hay, quá tuyệt vời. 😱😜

Các bạn nhìn ví dụ cũng đoán ra `&&` chính là `toán tử logic` đại diện cho khái niệm `AND`. Chúng ta có tất cả các loại `toán tử logic` như sau:

* `&&`: AND
* `||`: OR
* `!`: NOT

Mục tiêu của các `toán tử logic` là tác động lên các biểu thức `boolean` để cho ra một biến `boolean` mới.

#### Phép AND (&&)

Phép `&&` hoạt động theo nguyên tắc, `chỉ cần có 1 cái sai, thì tất cả đều sai` hay `Tất cả đều phải đúng, mới là đúng`

Nếu `"A đúng và B đúng và C sai thì kết quả vẫn là sai"`

```java
// Bạn chạy thử xem nó đi vào phần nào nhé
if(true && true && true && false){
    System.out.println("true");
}else{
    System.out.println("false");
}
```

#### Phép OR (||)

Phép `||` thì rất dễ dãi,  `Chỉ 1 cái đúng là đụ`

```java
// Bạn chạy thử xem nó đi vào phần nào nhé
if(false || false || true || false){
    System.out.println("true");
}else{
    System.out.println("false");
}
```

#### Phép NOT (!)

Phép `!` làm phủ định giá trị của biểu thức, nếu nó đang `true` thì biến nó thành `false` và ngược lại.

```java
int a = 7;
if(!(a == 7)){ // (a==7) => true gặp thằng ! lại bị chuyển thành false. => vào vế else
    System.out.println("Đáng nhẽ ra nên vào đây");
}else{
    System.out.println("But nope, nó lại vào đây");
}

```



Function trong java