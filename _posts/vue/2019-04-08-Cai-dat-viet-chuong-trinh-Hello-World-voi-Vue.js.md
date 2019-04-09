---
id: loda1554730312569
layout: post
title: '[Vue #1] Cài đặt, viết chương trình Hello World với Vue.js'
author: loda
categories: [ frontend, web, vue ]
image: assets/images/loda1554730312569/1.jpg
description: Hướng dẫn cài đặt và sử dụng vue.js
---

`Vue` (phát âm là /vjuː/, giống như **view** trong tiếng Anh). Vue.js là một framework giúp chúng ta xây dựng giao diện người dùng nhanh hơn và thuận tiện hơn.

Cứ ví dụ như bạn code một trang web bình thường khi chưa có `vue.js`. Thì sẽ có một số thao tác như sử dụng `Jquery` chọn đối tượng và lắng nghe sự kiện của đối tượng đó để thay đổi các giá trị khác. Nếu đối tượng này thay đổi chúng ta phải thay đổi đối tượng kia, các kiểu, các kiểu. Nói chung là **không khó** nhưng nó lâu và rườm rà.

Từ đó các framework frontend thi nhau ra đời, giảm thiểu thời gian cho những đoạn code quản lý thừa thãi và module hóa trang web của bạn, giúp bạn tập trung vào logic nhiều hơn, còn lại để framework lo. `Vue.js` là một trong số đó.

Điểm mạnh của `Vue.js` là nó rất nhanh, dễ học (dễ học nhất trong các loại frontend framework) và đơn giản hóa cho người sử dụng.

#### Cài đặt

Có 2 cách cài đặt:

#1. Sử dụng CDN:

```html
<!-- Bạn thêm một thư viện, nhưng nó cao cấp hơn Jquery thôi :v -->
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
```

#2. Sử dụng `NPM`:

Cái này sẽ dành cho các bạn đã có nền tảng về `npm` (có thể là `webpack` nữa)

```bash
npm install vue
```

Nếu bạn lần đầu đến với `Vue.js` nhưng đã có nền tảng từ trước thì hãy làm việc với `npm` cho đơn giản, dễ quản lý thư viện. 

Còn nếu đây là lần đầu bạn tới `frontend framework` và `Vue.js` thì trước tiên hãy sử dụng CDN cho đơn giản đã nhé. Khi nắm đc căn bản, thì chuyển qa xài `npm` và `vue-cli`


#### Chương trình đầu tiên

Bạn tạo ra một file `index.html` đơn giản:

```html
<!doctype html>
<html>
  <head>
    <title>Getting Started</title>
  </head>
  <body>
    <div id="app">
        <h2>{{msg}}</h2>
    </div>


    <!-- Thêm vue.js vào trang web của bạn -->
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>

    <script>
        new Vue({
            el: "#app",
            data: {
                msg: 'Hello Loda'
            }
        });
    </script>
  </body>
</html>
```
Mở file này trên trình duyệt web của bạn và đón nhận sự thành công cho trang web đầu tiên bằng `Vue.js` của mình :)))

<iframe width="100%" height="300" src="//jsfiddle.net/lodanamnh/0qsmb2ej/1/embedded/js,html,result/" allowfullscreen="allowfullscreen" allowpaymentrequest frameborder="0"></iframe>


#### Góc lý thuyết

Đầu tiên, khi mở trang `index.html` ở trên bạn sẽ thấy một dòng chữ "Hello Loda". Hẳn bạn cũng đoán ra là cái  {% raw %}{{msg}}{% endraw %} đã bị thay thế bằng dòng chữ này. Từ đây chúng ta đi xuống dưới.

Để tạo ra một đối tượng `Vue` (Một trang web có thể có nhiều đối tượng `Vue`). Chúng ta cần gắn đối tượng `Vue` này vào một `element` cụ thể. Ở đây, tôi gắn vào đối tượng `<div id="app"></div>`.

```js
new Vue({
    el: "#app" // el ám chỉ element. gắn tới id="app" ở trên
});
```

Tiếp đến, bây giờ mọi thứ trong `<div id="app"></div>` sẽ chịu sự quản lý của `Vue`. Và nếu tôi muốn gắn một giá trị vào bên trong `div` này, tôi sẽ sử dụng 2 dấu ngoặc kép `{% raw %}{{msg}}{% endraw %}`.

Giá trị này sẽ được khai báo trong trường `data`. 

```js
new Vue({
    el: "#app",
    data: {
        msg: 'Hello Loda'
    }
});
```

Vậy đóa, hết sức đươn giản. Một đối tượng `Vue` có thể có nhiều biến, như thế này:

```js
new Vue({
    el: "#app",
    data: {
        msg: 'Hello Loda',
        msg2: 'haha',
        isCompleted: true
    }
});
```

Ở trong phạm vi `#app` bạn đã trỏ tới, bạn có thể gọi các biến này ra bằng tên của biến.


Bài 1 kết thúc ở đây, chúc các bạn học tốt!

[Bài 2: Đối tượng Vue, thuộc tính và phương thức](https://loda.me/Doi-tuong-Vue-thuoc-tinh-va-phuong-thuc/)