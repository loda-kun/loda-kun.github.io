---
id: loda1554795977503
layout: post
title: 'Khái niệm Cross-Origin Resource Sharing (CORS) và cách fix'
author: loda
categories: [ frontend, web ]
image: assets/images/loda1554795977503/1.jpg
description: Khai niệm Cross-Origin Resource Sharing (CORS), Hướng dẫn cách fix lỗi CORS, Fix lôi No 'Access-Control-Allow-Origin'
---

Cross-Origin Resource Sharing (CORS) là một tiêu chuẩn về bảo mật có ở các web browser thế hệ mới. 

Từ trước năm 1995, thì không có cách nào để một trang web gửi request thông qua trình duyệt đến một domain khác. Đây gọi là **Same Origin Policy**. Để ngăn cản một đoạn `script` nào đó thể gửi request sang một domain khác (gọi là không cùng `origin`). Một domain có chung origin khi nó phải giống nhau về `protocol`, `port`, `host`.

Nghĩa là:

Website của bạn đang ở domain `loda.me`. Thì không có cách nào bạn gửi request ajax sang domain `loda.he` hay `loda.she` được. Vì nó khác `orgin`

Việc áp dụng **Same Origin Policy** giúp hạn chế các cuộc tấn công mạng hoặc ăn cắp thông tin từ các website khác và gửi về máy chủ của họ.

Tuy nhiên, với nhu cầu phát triển, chúng ta sẽ có lúc cần phải request sang một domain khác. Đặc biệt là các frontend framework. Vậy nên CORS ra đời.

#### CORS

![cors](/assets/images/loda1554795977503/3.png){:class="center-image"}


CORS là một cơ chế xác nhận thông qua Header của request. Cụ thể là trên Server sẽ nói với browser về quy định chấp nhận những request từ domain nào và phương thức ra sao (GET, POST, PUT, v.v..)

* **Access-Control-Allow-Origin**: Những `origin` mà server cho phép. (ví dụ server `loda.his` chỉ chấp nhận `loda.me` request lên)
* **Access-Control-Allow-Headers**: Những Header được server cho phép. (ví dụ `x-authorize`, `origin`, cái này do server bạn quy định)
* **Access-Control-Allow-Methods**: Những Method được servẻ cho phép (POST, GET, v.v..)

Vậy làm sao web browser biết được những thông tin ở trên?

Nó sẽ phải tự đi hỏi server đó bằng cách gửi lên một request tên là `Preflight request`. request này được tự động gửi bởi web browser qua phương thức OPTIONS để thăm dò một domain nào đó.

`Preflight request` bao gồm:

* **Origin**: domain hiện tại
* **Access-Control-Request-Method**: Gửi lên các method để kiểm tra xem server có accept không. (GET, POST, v.v..)
* **Access-Control-Request-Headers**: thăm dò xem một header nào đó có được chấp nhận không.

![cors](/assets/images/loda1554795977503/2.png){:class="center-image"}

Vậy thoai, đơn giản vậy đó, vậy là chúng ta chỉ có thể request sang một domain khác, nếu domain đó accept CORS.

Vậy nên nếu bạn đang gặp tình trạng bị chặn request thì cách giải quyết nhanh nhất đó là cấu hình server để chấp nhận origin của bạn. (`Access-Control-Allow-Origin`)

Còn nếu server không do bạn nắm quyền hoặc hoàn toàn không thể tác động đến. Thì có trick sau, tất nhiên là chỉ áp dụng được với bạn và thời điểm đó thôi:

Tắt chức năng bảo mật của trình duyệt:

```bash
chrome --disable-web-security --user-data-dir
```

=))) điều này giúp bạn giải quyết được khi lập trình hoặc muốn chạy tạm thời ở máy mình, nhưng kéo theo là cái web browser của bạn lúc này không có bảo mật gì cả.
