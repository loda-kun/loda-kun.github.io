---
id: loda1553005203072
layout: post
title: '「Java basic #1」Giới thiệu Java, Cài đặt môi trường và Hellooo world~'
author: loda
categories: [java, java basic, series 2 tuần]
image: assets/images/loda1553005203072/1.jpg
description: Hướng dẫn cài đặt Java và chạy chương trình đầu tiên, cực dễ hiểu
---

Xin chào tất cả các bạn, chào mừng các bạn đến với bài đầu tiên trong khóa học **Thành thạo Java Basic trong 2 tuần.**. Mình là `loda` sẽ đồng hành cùng các bạn trên công đường làm chủ ngôn ngữ `jav` này 🤗

Bài đầu tiên trong series này là giới thiệu cực kì **ngắn gọn** với các bạn `Java` là gì, đủ ý dễ hiểu, tập trung vào việc cài đặt môi trường, cài đặt công cụ lập trình. 

Okayyy vào bài.

#### Java

![java-basic](/assets/images/loda1553005203072/4.jpg){:class="center-image"}

Bắt đầu từ một câu chuyện: 

> Tại một vương quốc nọ năm 19xx (TCN), có một anh lập trình viên, khi đang viết phần mềm cho `Windows 9x`, thì sếp yêu cầu anh viết thêm cho cả `Linux`, `OpenVMS`, `FreeBSD`, `IBM`, v.v.. Chàng thanh niên không nói gì, anh chững lại đôi chút, lấy điếu thuốc rít một hơi, mắt anh nhìn xa xăm, đôi mắt anh lúc đó hồn nhiên tới lạ, tôi nghĩ nó là đôi mắt biết nói, nó nói: "f**k 🙂"

Đấy, đấy là câu chuyện của mình, còn lịch sử `Java` các bạn đọc [ở đây][java-wiki] nhé 😆

 Mình tóm tắt giúp bạn là `Java` được ra đời với mục tiêu là `"viết một lần, chạy mọi nơi"` (`"write once, run anywhere"`). Vì bản thân các `OS` là khác nhau, các lập trình viên không muốn với mỗi một OS lại phải code lại từ đầu. Nên `Java` ra đời. Năm 1995. 
 
 Lấy người anh `C/C++` làm nền tảng học tập, `Java` tiếp thu, cải thiện hơn và áp dụng mô hình hướng đối tượng chuẩn mực hơn. Từ đó trở thành ngôn ngữ mạnh mẽ nhất thời bấy giờ.

Đấy ngắn gọn thế thôi, để não bộ tiếp thu tiếp.

#### Cài đặt môi trường

Môi trường là seo? hổng hiểu 😕

Các bạn cứ tưởng tượng bạn đang xem một bộ `Film` vậy, trên thế giới có film `Mỹ`, `Tàu`, `Jav`, v.v.. mỗi film một thứ tiếng, nà ní, nhưng sao bạn vẫn xem và hiểu? Vì nó có `Phụ đề`.

`Java` hoạt động như vậy, nó chỉ nói 1 ngôn ngữ duy nhất thôi, tuy nhiên nó có một thằng anh bá đạo, tên ông ý nôm na là `môi trường ảo` hay tên chuẩn là `Java virtual machine (JVM)`. Nhiệm vụ của `JVM` là nó `phụ đề` (`thuyết minh`) cho từng loại OS khác nhau rằng thằng `Java` đang làm gì, nói gì, làm gì.

![image-title-here](/assets/images/loda1553005203072/2.png){:class="center-image"}

Vì chúng ta là `Developer` nên chúng ta không chỉ muốn cài `môi trường` mà còn muốn code trên nó nữa. nên chúng ta sẽ cài gói `JDK` (`Java Development Kit`) luôn. Nó chứa các công cụ giúp lập trình `Java` ngoài ra trong quá trình cài, nó sẽ hỏi ta muốn cài môi trường luôn `JRE` (`Java Runtime Enviroment`, thằng này chứa cả thằng `JVM` ở trên), tiện lợi.

Nếu các bạn xài `Windows` hoặc `MacOS` thì click vào đây để download:
 [https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html][link-jdk], 
 
 Nhớ chọn `Accept lincense agreement` trước khi download. Khi download xong, bạn mở file và làm theo hướng dẫn nhé. 

Đây là trang "chính chủ" nên bạn không cần lo về `virus` hay gì cả, cứ chọn `next` và `accept` mọi gợi ý là tốt nhất, tránh phải làm thêm các thao tác phụ.

![image-title-here](/assets/images/loda1553005203072/3.jpg){:class="center-image"}

Còn `Unix` thì các bạn nên sử dụng `apt-get` tự động setup cho dễ, nếu đã xài `Unix` thì vụ này rành rồi hah, mình k hướng dẫn gõ lệnh đâu hê hê 😄:

```bash
sudo add-apt-repository ppa:webupd8team/java
sudo apt-get update
sudo apt-get install oracle-java8-installer
```

#### Cài đặt Intellij IDEA và kích hoạt bản quyền.

`Intellij IDEA` chỉ làm một "công cụ" lập trình, giúp các bạn viết code dễ dàng hơn, giúp cuộc sống của bạn bớt lo lắng về những vấn đề khác mà chỉ cần tập trung vào viết code thôi.

![intellij](/assets/images/loda1553005203072/5.png){:class="center-image"}

Download tại: [https://www.jetbrains.com/idea/download/](https://www.jetbrains.com/idea/download/)

Hiện `Intellij` có 2 phiền bản, `Ultimate` là mất phí nhưng bá đạo thôi rồi, còn `Community` là miễn phí (vẫn tốt nhé). Bình thường không có điều kiện thì các bạn xài `Community` được rồi. TUY NHIÊN...😗

MÌNH CÓ KEY BẢN QUYỀN Ở ĐÂY [loda.me/jetbrains][link-key]. nên các bạn cứ down `Ultimate` về mà xài nhé... Nhớ làm theo hướng dẫn trong link.

Cài đặt thì cũng giống với `JDK` là chọn `next` và `accept` mọi mục để hưởng dịch vụ tốt nhất.

#### Hellooo world~

Được roài, sau một loạt các bước cài đặt cần thiết, thì bạn bây giờ đã sẵn sàng để bắt đầu `Lập trình Java`. Mở `Intellij` lên nào, chọn `Create new project`

![intellij](/assets/images/loda1553005203072/5.jpg){:class="center-image"}

Nhập tên cho `Project` của bạn, chọn thư mục lưu trữ cho nó, rồi nhấn `OK`.

Bạn tạo xong chưa? xong rồi thì cùng nhìn vào cấu trúc của project nhé.
Bạn sẽ thấy có 3 thư mục:

![intellij](/assets/images/loda1553005203072/6.jpg){:class="center-image"}

* `.idea`: Thằng này là thư mục do `Intellij` tự tạo ra để chứa các file config của phần mềm này, bạn sẽ k cần quan tâm đến, để nó tự nhiên đê :D 

* `src`: Đây là thư mục chính bạn sẽ làm việc, tất cả `code` bạn để trong này

* `{project-name}.iml`: File này cũng do `Intellj` tạo ra và quản lý module, bạn không cần quan tâm nó.

Okay,, hiểu kiến trúc 1 project `Java` cơ bản rồi,, bắt tay vào code luôn thoai. :3 

Bạn vào thư mục `src` tạo 1 file cho mình tên là `Main.java` nhé.
Trong code bạn sẽ viết như này, mình sẽ giải thích sau khi bạn chạy được chương trình.

```java
public class Main {
    public static void main(String[] args) {
        System.out.println("Hellooo World~~~, I'm loda");
    }
}
```

Bạn `click` chuột phải vào file trên màn hình, chọn `Run Main.main()` để chạy chương trình nhé.


**_Note:_**

> Nếu là **lần đầu**, Bạn sẽ phải kiểm tra setting một chút, cho chắc, để nó biết `Intellij` đã biết thư mục `JDK` mà bạn cài ở bước 2 chưa.

![java co ban](/assets/images/loda1553005203072/6.png){:class="center-image"}

> Bạn vào `File` > `Project Structure...` > `Project SDK`
Nếu thấy như hình, nó nhận `1.8` là okie, k cần lo lắng gì nữa. Nếu chưa có, bạn chọn mũi tên xem nó có sẵn chưa, nếu chưa, chọn `New` và chỉ dẫn nó tới thư mục `JDK` bạn đã cài ở bước 2 (`C:/Program File/Java/jdk 1.8` cho `Windows` hoặc `/Library/Java/JavaVirtualMachines/jdk1.8.0_201.jdk/Contents/Home` cho `MacOs`).

Okie bạn đã thấy dòng chữ `Hellooo World~~~, I'm loda` in ra màn hình phải không. Thế là bạn đã chạy chương trình `Java` đầu tiên thành công rồi đấy hú hú :333

##### Góc Giải thích. 

Ví dụ này bạn sẽ dễ nhận thấy các điều cơ bản sau:

* Cơ bản thì file code sẽ nằm trong thư mục `src`
* File code sẽ có tên kết thúc bằng `.java`
* Tên file là `A` thì trong file đó sẽ mặc định là `public class A`

Thế cái `public class A` là cái gì? Cái này mình sẽ giải thich ở các bài sau bạn nhé. tạm thời bạn hãy cứ tạo file `A.java` và mặc định làm việc bên trong đoạn `public class A`. (cứ hiểu nó như là 1 thằng đánh dấu, rằng tao là `A`, không phải `B` cũng được kakaka).

Còn chương trình chính của bạn chỉ có thể này thôi:
```java
public static void main(String[] args) {
    System.out.println("Hellooo World~~~, I'm loda");
}
```

* `public static void main(String[] args)`: (Gọi tắt là `psvm` nhé) Cái thằng này sẽ là nơi `Java` tìm tới đầu tiên, và đọc toàn bộ các đoạn code trong cái thằng tên là `psvm` này. Dù nó ở bất cứ đâu, nó sẽ được tìm tới.

* 2 cái dấu `{` `}`: Đánh dấu đoạn bắt đầu và kết thúc của cái `public static void main(String[] args)` kia.

Vậy là thằng `Java` sẽ đi lùng tìm, xem cái thằng `psvm` xem nó ở đâu. Rồi đọc hết tất cả những thứ nằm trong cái 2 dấu `{` `}` của thằng này.

Vậy trong ví dụ của chúng ta, nó sẽ đọc cái gì? bạn thấy đấy, chi có 1 dòng duy nhất thôi :v

```java
System.out.println("Hellooo World~~~, I'm loda");
```
Nhìn dòng này chúng ta sẽ biết:
* Các dòng code của `Java` đều kết thúc bằng dấu `;` (Ngoại trừ cái thằng `{` `}` nhé)
* `System.out.println()`: là câu lệnh in ra màn hình.
* `"Hellooo World~~~, I'm loda"`: là thứ sẽ được in ra màn hình, dấu ngoặc kép `"` cho `Java` biết đây là một đoạn text, chứu không phải một con số, một con chim, hay một con mèo gì cả.

#### Kết

Okieeeee lahhh, Thế là xong bài đầu tiên,, chúc mừng các bạn đã bước 1 chân vào thế giới `Java` đầy huyền bí :3 Có gì thắc mắc bạn cứ tự nhiên comment ở bên dưới nhé!

Chớ quên like và share cho bạn bè,, ahihi!


[java-wiki]: https://vi.wikipedia.org/wiki/Java_(ngôn_ngữ_lập_trình)
[link-jdk]: https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html
[link-key]: https://loda.me/jetbrains