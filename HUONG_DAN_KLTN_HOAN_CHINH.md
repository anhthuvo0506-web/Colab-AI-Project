# Notebook KLTN hoàn chỉnh

[Mở trực tiếp trên Google Colab](https://colab.research.google.com/github/anhthuvo0506-web/Colab-AI-Project/blob/main/KLTN_11-2026_HOAN_CHINH.ipynb)

File: `KLTN_11-2026_HOAN_CHINH.ipynb` (86 cell).

- Giữ nguyên 77 cell gốc; thêm một cell chuẩn bị biến trước 16F-R và phần đánh giá ở cuối.
- Bổ sung sinh RSSI tại tọa độ mới, so sánh với KNN/APMean trên cùng candidate, metrics/coverage, CI bootstrap theo cụm RP, chẩn đoán RSSI từng AP, bản đồ và xuất Excel/ZIP.
- Đã chạy toàn bộ pipeline trên DATASET_DLULIB.zip trong môi trường kiểm tra. Bản GitHub giữ nguyên mã nguồn, đã xóa toàn bộ output và execution count để chỉ đăng code. Chạy lại với dataset của bạn để tạo bảng, biểu đồ và file kết quả.

## Cách chạy

1. Mở bằng liên kết Colab phía trên; chọn GPU để chạy nhanh hơn.
2. Chạy notebook theo thứ tự và tải `DATASET_DLULIB.zip` khi được yêu cầu.
3. Nếu chỉ chạy nhanh phần bổ sung: chạy phần gốc đến Cell 7 (index 37), sau đó 17A, 17B và 17D/E. 17C cần chạy phần gốc đến Cell 16E trước.
4. Cell cuối xuất CSV, Excel, hình và ZIP kết quả để tải về máy.

Các file cũ trong repo được giữ nguyên. Dataset không được tải thêm lên repo trong lần cập nhật này.

## Đọc kết quả

Không mặc định CGAN tốt hơn ORIGINAL; kết luận theo bảng và khoảng tin cậy sau khi chạy. Đơn vị sai số là đơn vị tọa độ nguồn, chưa xác nhận là mét. VALIDATION đã được dùng chọn mô hình/k, chưa phải holdout cuối độc lập. Candidate trong convex hull TRAIN chưa đảm bảo vùng đi lại được khi chưa có polygon mặt bằng. Chưa chứng minh độ chính xác vật lý tại điểm hoàn toàn mới hoặc mức tiết kiệm chi phí thực địa.
