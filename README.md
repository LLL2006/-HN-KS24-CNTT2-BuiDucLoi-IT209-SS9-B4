# Bài 4: Lưu trữ dữ liệu đơn giản với Docker Volume

## 1. Mục tiêu
Tạo một Named Volume (`easy-volume`) để lưu trữ dữ liệu bền vững (persistent data), đảm bảo dữ liệu không bị mất đi khi container kết thúc hoặc bị xóa.

## 2. Các bước thực hiện

### Bước 1: Tạo Named Volume
Tạo một volume mới có tên là `easy-volume`:
```bash
docker volume create easy-volume
```

*Kiểm tra danh sách volume hiện có:*
```bash
docker volume ls
```

---

### Bước 2: Ghi dữ liệu vào Volume với Container thứ nhất
Sử dụng container tạm thời chạy image `alpine` để gắn (mount) volume `easy-volume` vào thư mục `/data` và ghi nội dung vào tệp `test.txt`:
```bash
docker run --rm -v easy-volume:/data alpine sh -c "echo 'Luu tru du lieu Docker' > /data/test.txt"
```

> **Giải thích tham số:**
> - `--rm`: Tự động xóa container sau khi chạy xong.
> - `-v easy-volume:/data`: Gắn volume `easy-volume` vào thư mục `/data` bên trong container.
> - `sh -c "echo 'Luu tru du lieu Docker' > /data/test.txt"`: Lệnh ghi chuỗi văn bản vào tệp `/data/test.txt`.

Container này sẽ tự hủy ngay sau khi lệnh kết thúc.

---

### Bước 3: Đọc lại dữ liệu với Container thứ hai (Kiểm tra)
Khởi chạy một container `alpine` hoàn toàn mới và mount cùng volume `easy-volume` để đọc tệp:
```bash
docker run --rm -v easy-volume:/data alpine cat /data/test.txt
```

### Kết quả mong đợi:
Terminal in ra:
```
Luu tru du lieu Docker
```

---

## 3. Các lệnh hữu ích & Dọn dẹp

### Xem thông tin chi tiết về Volume:
```bash
docker volume inspect easy-volume
```

### Xóa Volume sau khi hoàn thành bài tập:
```bash
docker volume rm easy-volume
```
