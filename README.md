# BÀI 3: XỬ LÝ LỖI BỐ CỤC GIAO DIỆN HỆ THỐNG THEO DÕI XE

## PHẦN 1. PHÂN TÍCH

### 1. Định vị phần tử bị lỗi

- Sử dụng F12 để mở DevTools.
- Chọn tab Elements và công cụ Inspect Element.
- Click vào khung nội dung cần kiểm tra để xác định thẻ HTML trong DOM Tree.
- Chọn tab Computed để kiểm tra kích thước và Box Model.

Website sử dụng để thực hành: https://adminlte.io/themes/v3/

### 2. Phân tích CSS Box Model

CSS Box Model gồm 4 thành phần:

- Content: Vùng chứa nội dung.
- Padding: Khoảng cách giữa nội dung và đường viền.
- Border: Đường viền của phần tử.
- Margin: Khoảng cách bên ngoài phần tử.

Nguyên nhân có thể gây chồng lấn là kích thước, khoảng cách hoặc thuộc tính định vị của các phần tử chưa phù hợp.

## PHẦN 2. TRIỂN KHAI

### 1. Thông số CSS đề xuất

Thực hiện thay đổi trực tiếp trong tab Styles của DevTools:

```css
padding: 30px;
content: 692*500.000
```

## PHẦN 3. KIỂM THỬ

### 1. Kiểm tra khi thay đổi Margin không có tác dụng

Nếu thay đổi Margin nhưng phần tử vẫn không di chuyển, cần kiểm tra các thuộc tính CSS khác trong tab Styles.

Một số nguyên nhân:

- Position: absolute hoặc fixed khiến phần tử nằm ngoài luồng bố cục thông thường.
- Thuộc tính CSS khác có độ ưu tiên cao hơn đang ghi đè.
- Có sử dụng !important để ưu tiên một quy tắc CSS khác.

### 2. Cách xử lý

- Kiểm tra thuộc tính bị gạch ngang trong tab Styles.
- Kiểm tra thuộc tính Position.
- Tìm quy tắc CSS đang ghi đè Margin.
- Thử bỏ thuộc tính gây xung đột trực tiếp trong DevTools.

### 3. Kết luận

Thông qua bài thực hành, em đã biết cách sử dụng Inspect Element để xác định phần tử HTML, kiểm tra CSS Box Model và điều chỉnh các thuộc tính CSS trong DevTools để khắc phục lỗi bố cục giao diện mà không cần sửa mã nguồn gốc.

## HÌNH ẢNH MINH CHỨNG

### Ảnh 1: Inspect Element

![Inspect Element](images/01-inspect-element.png)

### Ảnh 2: CSS Box Model

![CSS Box Model](images/02-box-model.png)

### Ảnh 3: Kết quả sau khi chỉnh CSS

![Fix Layout](images/03-fix-layout.png)