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

![image-title-here](/assets/images/loda1553005203072/4.jpg){:class="center-image"}

Bắt đầu từ một câu chuyện: 

> Tại một vương quốc nọ năm 19xx (TCN), có một anh lập trình viên, khi đang viết phần mềm cho `Windows 9x`, thì sếp yêu cầu anh viết thêm cho cả `Linux`, `OpenVMS`, `FreeBSD`, `IBM`, v.v.. Chàng thanh niên không nói gì, anh chững lại đôi chút, lấy điếu thuốc rít một hơi, mắt anh nhìn xa xăm, đôi mắt anh lúc đó hồn nhiên tới lạ, tôi nghĩ nó là đôi mắt biết nói, nó nói: "f**k 🙂"

Đấy, đấy là câu chuyện của mình, còn lịch sử `Java` các bạn đọc [ở đây][java-wiki] nhé 😆

 Mình tóm tắt giúp bạn là `Java` được ra đời với mục tiêu là `"viết một lần, chạy mọi nơi"` (`"write once, run anywhere"`). Vì bản thân các `OS` là khác nhau, các lập trình viên không muốn với mỗi một OS lại phải code lại từ đầu. Nên `Java` ra đời. Năm 1995. 
 
 Lấy người anh `C/C++` làm nền tảng học tập, `Java` tiếp thu, cải thiện hơn và áp dụng mô hình hướng đối tượng chuẩn mực và mạnh mẽ nhất thời bấy giờ.

Đấy ngắn gọn thế thôi, để não bộ tiếp thu tiếp.

#### Cài đặt môi trường

Môi trường là seo? hổng hiểu 😕

Các bạn cứ tưởng tượng bạn đang xem một bộ `Film` vậy, trên thế giới có film `Mỹ`, `Tàu`, `Jav`, v.v.. mỗi film một thứ tiếng, nà ní, nhưng sao bạn vẫn xem và hiểu? Vì nó có `Phụ đề`.

`Java` hoạt động như vậy, nó chỉ nói 1 ngôn ngữ duy nhất thôi, tuy nhiên nó có một thằng anh bá đạo, tên ông ý nôm na là `môi trường ảo` hay tên chuẩn là `Java virtual machine (JVM)`. Nhiệm vụ của `JVM` là nó `phụ đề` (`thuyết minh`) cho từng loại OS khác nhau rằng thằng `Java` đang làm gì, nói gì, làm gì.

![image-title-here](/assets/images/loda1553005203072/2.png){:class="center-image"}

Vì chúng ta là `developer` nên chúng ta không chỉ muốn cài `môi trường` mà còn muốn code trên nó nữa. nên chúng ta sẽ cài gói `JDK` (`Java Development Kit`) luôn. Nó chứa các công cụ giúp lập trình `Java` ngoài ra trong quá trình cài, nó sẽ hỏi ta muốn cài môi trường luôn không, tiện lợi.

Nếu các bạn xài `Windows` hoặc `MacOS` thì click [vào đây][link-jdk], nhớ chọn `Accept lincense agreement` trước khi download. Khi download xong, bạn mở file và làm theo hướng dẫn nhé. 

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

![image-title-here](/assets/images/loda1553005203072/5.png){:class="center-image"}

Download tại: [https://www.jetbrains.com/idea/download/](https://www.jetbrains.com/idea/download/)

Hiện `Intellij` có 2 phiền bản, `Ultimate` là mất phí nhưng bá đạo thôi rồi, còn `Community` là miễn phí (vẫn tốt nhé). Bình thường không có điều kiện thì các bạn xài `Community` được rồi. TUY NHIÊN...😗

MÌNH CÓ KEY BẢN QUYỀN [Ở ĐÂY][link-key]. nên các bạn cứ down `Ultimate` về mà xài nhé...

Cài đặt thì cũng giống với `JDK` là chọn `next` và `accept` mọi mục để hưởng dịch vụ tốt nhất.


#### Hellooo world~

