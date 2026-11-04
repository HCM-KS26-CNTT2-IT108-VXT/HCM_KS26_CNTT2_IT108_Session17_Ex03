# Bài 3: Xử lý lỗi bố cục giao diện hệ thống theo dõi xe

## Phần 1. Phân tích

### 1. Định vị phần tử bị lỗi

- Nhấn `F12` để mở DevTools.
- Chọn tab **Elements**.
- Dùng biểu tượng Inspect để chọn khung "Thông tin tài xế".
- Kiểm tra thẻ HTML trong DOM Tree để xác định phần tử gây chồng lấn.
- Chọn tab **Computed** để xem kích thước và các thông số CSS.

### 2. Sơ đồ CSS Box Model

Box Model gồm 4 lớp:

```text
+--------------------------+
|          Margin          |
|  +--------------------+  |
|  |       Border       |  |
|  |  +--------------+  |  |
|  |  |   Padding    |  |  |
|  |  | +----------+ |  |  |
|  |  | | Content  | |  |  |
|  |  | +----------+ |  |  |
|  |  +--------------+  |  |
|  +--------------------+  |
+--------------------------+
```

- **Content:** Chứa nội dung.
- **Padding:** Khoảng cách giữa nội dung và viền.
- **Border:** Đường viền phần tử.
- **Margin:** Khoảng cách bên ngoài phần tử.

## Phần 2. Triển khai

**Đề xuất CSS mới để sửa lỗi chồng lấn:**

```css
.driver-info {
    width: 100%;
    padding: 16px;
    border: 1px solid #ccc;
    margin-bottom: 20px;
    box-sizing: border-box;
}

.station-list {
    width: 100%;
    padding: 16px;
    border: 1px solid #ccc;
    margin-top: 20px;
    box-sizing: border-box;
}
```

**Cách thực hiện:**

1. Chọn phần tử bị lỗi trong tab Elements.
2. Mở tab Styles.
3. Thêm hoặc chỉnh sửa các thuộc tính CSS.
4. Quan sát kết quả trực tiếp trên giao diện.
5. Chỉ thay đổi trong DevTools, không sửa file mã nguồn gốc.

## Phần 3. Kiểm thử

Nếu thay đổi Margin nhưng phần tử vẫn không di chuyển, cần kiểm tra:

- `position: absolute`: Phần tử được định vị theo phần tử cha.
- `position: fixed`: Phần tử cố định theo màn hình.
- `transform`: Có thể làm thay đổi vị trí hiển thị.
- `!important`: Có thể khiến một quy tắc CSS khác được ưu tiên.
- Kiểm tra các quy tắc CSS khác đang ghi đè thuộc tính Margin trong tab Styles.

**Cách xử lý:** Kiểm tra thuộc tính đang có hiệu lực trong Computed và Styles, sau đó thử tắt quy tắc gây xung đột.

**Kết luận:** Dùng DevTools để xác định phần tử lỗi, điều chỉnh Box Model và kiểm tra lại giao diện mà không cần sửa mã nguồn gốc.
