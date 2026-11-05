# Notebook KLTN hoàn chỉnh

[Mở trực tiếp trên Google Colab](https://colab.research.google.com/github/anhthuvo0506-web/Colab-AI-Project/blob/main/KLTN_11-2026_HOAN_CHINH.ipynb)

File: `KLTN_11-2026_HOAN_CHINH.ipynb` (94 cell).

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

## Sửa lỗi `KeyError: F1` ở 18B sau khi chạy bản đồ

Một số cell vẽ hình gốc dùng tên `data` làm biến tạm DataFrame, ghi đè dictionary dữ liệu theo tầng. Phần 18B đã chuyển sang nguồn riêng `EXT18_INPUT_DATA`, khôi phục từ `splits` gốc (ghép TRAIN+VALIDATION làm bảng nguồn, TEST giữ nguyên). Không dùng reference tăng cường để tái tạo dữ liệu nguồn. Có kiểm tra schema và thông báo rõ khi thiếu dữ liệu Phase 1.

Mở phiên bản notebook mới nhất và chạy lại 18A rồi 18B. Nếu session vẫn giữ `splits`, không cần chạy lại huấn luyện ở phần cũ. Nếu chưa nạp dữ liệu hoặc session đã reset, chạy phần dữ liệu/WKNN gốc tới index 12 trước.

Đã kiểm tra hồi quy với đúng phép gán biến `data` của cell bản đồ; dữ liệu khôi phục khớp nguồn Phase 1, xử lý nguồn thiếu/sai schema, và chạy lại thí nghiệm 5 seed trên 3 tầng. Bản GitHub vẫn chỉ chứa code; không đăng dữ liệu hoặc output.

## Hai cell cuối: dashboard tổng hợp và bản đồ tương tác

Notebook hiện có 94 cell. Hai cell code mới được nối cuối; toàn bộ 92 cell trước giữ nguyên.

- **Cell kế cuối — 19:** đọc kết quả đã xuất từ phần 18, hiển thị bảng tổng hợp theo tầng/phương pháp, kết quả từng seed và query thất bại, kiểm toán split/sinh bù, CI ghép cặp, chẩn đoán RSSI; có 6 biểu đồ tương tác. Xuất dashboard HTML và Excel.
- **Cell cuối — 20:** bản đồ tọa độ X/Y có bộ chọn tầng, seed, phương pháp; hiển thị OBSERVED, VALIDATION, RP ẩn, reference sinh bù và dự đoán trung bình. Rê chuột/bấm RP để xem tọa độ thật/dự đoán, sai số, query hợp lệ, trạng thái reference và RSSI reference nếu có. Có bảng RP và các chỉ số tổng hợp ngay trong map.
- Dùng một thang màu sai số chung cho mọi lựa chọn; vector nối tới vị trí dự đoán trung bình không được gọi là sai số trung bình query.
- Chạy 18B rồi 18C, sau đó hai cell cuối. Nếu file kết quả phần 18 đã có và `EXT18_DIR` vẫn trỏ đúng thư mục, chỉ cần chạy hai cell cuối, không train lại.
- Xuất riêng vào `OUT/19_FINAL_VIEW`: `19_DASHBOARD_TONG_HOP.html`, `19_BANG_TONG_HOP.xlsx`, `20_MAP_TONG_HOP_TOA_DO.html`, `20_TOA_DO_VA_SAI_SO_RP.csv`; cell cuối tải ZIP tổng hợp trên Colab. HTML nhúng Plotly để mở độc lập mà không tải thư viện từ CDN.
- Đã kiểm tra số liệu của mọi lựa chọn floor/seed/method khớp kết quả phần 18; thử trực tiếp các bộ chọn, click RP, lớp điểm/vector, bảng và iframe notebook bằng trình duyệt.
- GitHub chỉ chứa code; không đăng HTML/bảng tọa độ hoặc dữ liệu dẫn xuất. Các file hiển thị được tạo khi chạy notebook với dataset của bạn.

## Màu sắc các bảng ở cell 19

- CGAN tím, KNN xanh dương, sau ẩn ORIGINAL cam, trước ẩn xám; cột tầng có màu riêng cho F1/F2/F3.
- Ô sai số có thang xanh → vàng → đỏ từ thấp đến cao trong cùng tầng và seed (nếu có). Giá trị ngang nhau dùng trung tính. Đây là cách đọc số liệu, không tự khẳng định phương pháp tốt hơn có ý nghĩa thống kê.
- Coverage và tỷ lệ phục hồi càng cao càng xanh; query thất bại/overlap có màu đỏ khi khác 0. Delta dương xanh, âm đỏ; CI chứa 0 vàng, thiếu dữ liệu trung tính.
- Màu phương pháp là nhãn nhận diện, khác với màu đánh giá các ô chỉ số. Có chú thích ngay trước các bảng.
- Các bảng được render bằng HTML đã định dạng, hiển thị rõ trên nền sáng/tối. Dashboard HTML và workbook Excel cũng giữ màu; số liệu gốc không thay đổi.
- Chỉ cần cập nhật và chạy lại cell 19 để xem bảng màu, không huấn luyện lại. Chạy thêm cell 20 nếu muốn tải ZIP có bản HTML/Excel vừa cập nhật.
