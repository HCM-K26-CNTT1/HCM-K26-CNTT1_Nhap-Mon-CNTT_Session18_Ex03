# BÀI 3: XỬ LÝ LỖI BỐ CỤC GIAO DIỆN HỆ THỐNG THEO DÕI XE

## PHẦN 1. PHÂN TÍCH

### 1. Xác định phần tử bị lỗi

Sử dụng Inspect Element trong DevTools để chọn khung Thông tin tài xế và xác định thẻ HTML tương ứng trong DOM Tree.

Phần tử cần kiểm tra: `div.driver-info`.

Phần tử bị ảnh hưởng: `div.station-list`.

Nguyên nhân: Các thuộc tính CSS về kích thước, khoảng cách và định vị chưa hợp lý, khiến hai khung nội dung bị chồng lấn.

### 2. Phân tích CSS Box Model

CSS Box Model gồm 4 thành phần:

- Content: Vùng hiển thị nội dung.
- Padding: Khoảng cách giữa nội dung và đường viền.
- Border: Đường viền bao quanh phần tử.
- Margin: Khoảng cách bên ngoài phần tử.

Sơ đồ Box Model hiện tại (thông số giả định):

```text
        MARGIN: 0px
   +----------------------+
   | BORDER: 1px          |
   |  +----------------+  |
   |  | PADDING: 30px  |  |
   |  |  +----------+  |  |
   |  |  | CONTENT  |  |  |
   |  |  | 400x150  |  |  |
   |  |  +----------+  |  |
   |  +----------------+  |
   +----------------------+
```

Nhận xét: Margin bằng 0 khiến phần tử không có khoảng cách bên ngoài. Padding lớn làm tăng kích thước tổng thể của phần tử nếu không sử dụng `box-sizing: border-box`. Đây là những yếu tố có thể góp phần gây chồng lấn giao diện.

## PHẦN 2. TRIỂN KHAI

### 1. Thông số CSS mới

Đề xuất thay đổi trực tiếp trong tab Styles của DevTools:

```css
.driver-info {
    width: 400px;
    padding: 15px;
    border: 1px solid #ccc;
    margin-bottom: 20px;
    box-sizing: border-box;
    position: static;
}

.station-list {
    width: 400px;
    padding: 15px;
    border: 1px solid #ccc;
    margin-top: 20px;
    box-sizing: border-box;
}
```

### 2. Giải thích kết quả

- Giảm Padding xuống 15px để tránh khung quá lớn.
- Thêm Margin để tạo khoảng cách giữa hai khung.
- Sử dụng Box-sizing: border-box để kiểm soát kích thước.
- Sử dụng Position: static để phần tử trở về luồng bố cục thông thường.

Kết quả mong đợi: Khung Thông tin tài xế và Danh sách trạm không còn chồng lấn, bố cục rõ ràng và dễ quan sát hơn.

Các thay đổi chỉ được thực hiện trong tab Styles, không chỉnh sửa mã nguồn gốc.

## PHẦN 3. KIỂM THỬ

### 1. Tại sao thay đổi Margin nhưng phần tử vẫn không di chuyển?

Có thể do thuộc tính Position hoặc một quy tắc CSS khác đang ảnh hưởng đến phần tử.

Ví dụ:
- `position: absolute`: Phần tử được định vị theo phần tử cha phù hợp.
- `position: fixed`: Phần tử được cố định theo cửa sổ trình duyệt.
- `position: static`: Phần tử nằm trong luồng bố cục thông thường.

### 2. Kiểm tra thuộc tính ghi đè ở Browser Engine

Kiểm tra tab Styles để tìm thuộc tính Margin bị gạch ngang hoặc bị quy tắc CSS khác ghi đè.

Ví dụ:

```css
.driver-info {
    margin-bottom: 20px;
    margin: 0 !important;
}
```

Trong trường hợp này, `margin: 0 !important` ghi đè giá trị `margin-bottom: 20px`.

Cách xử lý:
- Kiểm tra các quy tắc CSS đang áp dụng.
- Tìm thuộc tính `!important`.
- Kiểm tra User Agent Stylesheet (CSS mặc định của trình duyệt).
- Thử bỏ chọn thuộc tính đang ghi đè trong DevTools để kiểm tra kết quả.

Kết luận: Browser Engine không tự động ghi đè mọi thay đổi Margin. Cần kiểm tra các quy tắc CSS có độ ưu tiên cao hơn và kiểu mặc định của trình duyệt.

## KẾT LUẬN

Qua bài thực hành, em đã biết cách sử dụng Inspect Element để xác định phần tử HTML trong DOM Tree, phân tích 4 thành phần CSS Box Model và điều chỉnh thuộc tính CSS thông qua tab Styles trong DevTools.

Việc điều chỉnh hợp lý các thuộc tính giúp khắc phục lỗi chồng lấn giao diện mà không cần chỉnh sửa file mã nguồn gốc.