# Notebook KLTN hoàn chỉnh

[Mở trực tiếp trên Google Colab](https://colab.research.google.com/github/anhthuvo0506-web/Colab-AI-Project/blob/main/KLTN_11-2026_HOAN_CHINH.ipynb)

File: `KLTN_11-2026_HOAN_CHINH.ipynb` (92 cell).

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

## Phần 18: trước ẩn / sau ẩn / sinh bù đúng RP ẩn

- Giữ nguyên toàn bộ các cell đã có và kết quả của thí nghiệm cũ. Chỉ bổ sung 18A/18B/18C ở cuối.
- OBSERVED / VALIDATION / HIDDEN được chia theo cụm tọa độ, không chỉ theo ID; train/scaler từ OBSERVED, chọn checkpoint/k bằng VALIDATION, TEST tại HIDDEN không tham gia lựa chọn.
- Train CGAN riêng theo split mới; so sánh trước ẩn (có RSSI đo thật), sau ẩn ORIGINAL, sinh bù CGAN và sinh bù KNN K7 trên cùng query trong từng floor/seed.
- Có bảng, biểu đồ, chẩn đoán RSSI, CI theo cụm RP và báo cáo phân tích/kết luận tự động, không mặc định CGAN tốt hơn.
- Chạy nhanh phần 18: phần dữ liệu/WKNN gốc tới index 12 → 18A → 18B → 18C. Không cần chạy phần 17 hoặc multi-seed cũ. Cấu hình mặc định 5 seed, 3 tầng, tối đa 300 epoch, early stopping 35.
- File mới lưu riêng ở `OUT/18_HIDE_AND_RECOVER`; cell cuối xuất ZIP. Không xóa ORIGINAL/CGAN/KNN hoặc bảng theo tầng cũ.
- Mốc trước ẩn có ưu thế RSSI đo thật, được gắn nhãn rõ. Thí nghiệm vẫn là mô phỏng bỏ khảo sát trên dataset đã đo, chưa chứng minh tính đúng vật lý/chi phí ngoài thực địa.
- Đã chạy kiểm tra phần 18 trên dataset được cung cấp; không đưa dataset, output, checkpoint hoặc bảng số liệu thực nghiệm lên GitHub trong lần cập nhật này.
