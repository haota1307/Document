# REST

## REST là gì?

**REST** là viết tắt của **RE**presentational **S**tate **T**ransfer, là quy ước một số quy tắc ràng buộc khi thiết kế hệ thống mạng. REST cho phép máy khách (Clients) tương tác với dữ liệu được lưu trữ trên máy chủ (Servers) mà không cần phải có bất kỳ kiến thức trước nào về máy chủ hoặc những gì tồn tại trên đó.

REST có một số ràng buộc:

- **Uniform Interface** (Giao diện thông nhất)

- **Stateless** (Không trạng thái)

- **Cacheable** (Dữ liệu có thể lưu vào bộ nhớ cache)

- **Client-Server** (Máy khách - Máy chủ)

- **Layered System** (Hệ thống phân lớp)

- **Code on Demand** (Code theo yêu cầu)

## API là gì?

**API** là cơ chế cho phép 2 thành phần phần mềm giao tiếp với nhau bằng một tập hợp các định nghĩa và giao thức.

**Ví dụ**: hệ thống phần mềm của cơ quan thời tiết chứa dữ liệu về thời tiết hàng ngày. Ứng dụng thời tiết trên điện thoại của bạn sẽ “trò chuyện” với hệ thống này qua API và hiển thị thông tin cập nhật về thời tiết hàng ngày trên điện thoại của bạn.

## RESTful API là gì?

**RESTful API** là một API chuẩn REST. Chuẩn REST đọc khá là khó hiểu, học thuật vậy nên API của bạn chỉ cần áp dụng những kỹ thuật dưới đây thì có thể coi là chuẩn REST.

### Sử dụng các phương thức HTTP để request có ý nghĩa

- **GET**: Đọc một hoặc nhiều tài nguyên nào đó
- **PUT**: Cập nhật một hoặc nhiều tài nguyên nào đó
- **DELETE**: Xóa một tài nguyên nào đó
- **POST**: Tạo mới một tài nguyên nào đó

### Cung cấp tên tài nguyên hợp lý

Tạo ra một API tuyệt vời là 80% nghệ thuật và 20% khoa học.
Ví dụ:

- Sử dụng id định danh cho URL thay vì dùng query-string. Sử dụng URL query-string cho việc filter chứ không phải cho việc lấy một tài nguyên
  - **Good**: `/users/123`
  - **Poor**: `/api?type=user&id=23`
- Thiết kế cho người sử dụng chứ không phải thiết kế cho data của bạn
- Giữ cho URL ngắn và dễ đọc nhất cho client
- Sử dụng số nhiều trong URL để có tính nhất quán
  - **Nên dùng**: `/customers/33245/orders/8769/lineitems/1`
  - **Không nên**: `/customer/33245/order/8769/lineitem/1`

### Sử dụng các HTTP response code để xác định trạng thái API trả về

- **200 OK**: Thành công
- **201 CREATED**: Tạo thành công (có thể từ method POST hoặc PUT)
- **204 NO CONTENT**: Thành công nhưng không có gì trả về trong body cả, thường được dùng cho DELETE hoặc PUT
- **400 BAD REQUEST**: Lỗi, có thể nguyên nhân từ validate lỗi, thiếu data,...
- **401 UNAUTHORIZED**: Lỗi liên quan đến thiếu hoặc sai authentication token
- **403 FORBIDDEN**: Lỗi liên quan đến không có quyền truy cập
- **404 NOT FOUND**: Lỗi liên quan tài nguyên không tìm thấy
- **405 METHOD NOT ALLOWED**: Lỗi liên quan method không được chấp nhận. Ví dụ API chỉ cho phép sử dụng GET, PUT, DELETE nhưng bạn dùng POST thì sẽ trả về lỗi này.
- **500 INTERNAL SERVER ERROR**: Lỗi liên quan đến việc server bị lỗi khi xử lý một tác vụ nào đó (Server không cố ý trả về lỗi này cho bạn)

### Sử dụng định dạng JSON hoặc XML để giao tiếp client-server

**JSON** là kiểu dữ liệu tiện dụng cho server và client giao tiếp với nhau.

Có thể xử dụng **XML** nhưng phổ biến hơn cả vẫn là **JSON**

# Axios

## AJAX là gì

AJAX là chữ viết tắt của Asynchronous JavaScript and XML

Đừng quan tâm cái XML vì trong thực tế chúng ta dùng JSON để trao đổi data client-server

AJAX chỉ đơn giản là sự kết hợp của

- Trình duyệt được xây dựng với `XMLHttpRequest` object để nhận và gửi data từ server
- Javascript và HTML DOM để hiển thị data

AJAX giúp cho bạn:

- Cập nhật lại website mà không cần reload lại trang
- Yêu cầu dữ liệu từ server sau khi trang đã load
- Nhận dữ liệu từ server sau khi trang đã load
- Gửi data lên server ở chế độ ngầm

Các trình duyệt ngày nay cũng có thể dùng `FetchAPI` thay cho `XMLHttpRequest`, với `FetchAPI` thì chúng ta có thể tạo các HTTP request đến server một cách đơn giản hơn `XMLHttpRequest` rất nhiều.

Trong thực tế thì chúng ta thường dùng những thư viện như axios để tạo các HTTP request vì những thư viện này cho phép chúng ta tùy biến nhiều hơn.

## Axios

Một số tính năng nổi trội

- Chạy được ở cả trình duyệt (dùng `XMLHttpRequests`) và node.js (dùng `http`)
- Hỗ trợ Promise API
- Tạo được Interceptor request và response
- Cancel request
- Tự động chuyển JSON sang object
- Chống tấn công XSRF ở client

### Tạo interceptor

interceptor giống như là trung gian, trước khi gửi request lên server sẽ đi qua nó hoặc trước khi nhận nhận data thì cũng sẽ đi qua nó. Mục đích là để tiền xử lý các tác vụ.
