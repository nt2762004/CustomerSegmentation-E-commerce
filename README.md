# Phân khúc khách hàng E-commerce (Customer Segmentation)

Dự án này xây dựng một hệ thống phân tích hành vi khách hàng sử dụng mô hình **RFM (Recency, Frequency, Monetary)** kết hợp với thuật toán Machine Learning **K-Means Clustering**.

Hệ thống tập trung vào việc khai phá dữ liệu giao dịch, phân nhóm khách hàng thành các tập hợp có đặc điểm tương đồng (như VIP, Trung thành...) để hỗ trợ doanh nghiệp đưa ra các chiến lược Marketing cá nhân hóa hiệu quả.

**Link Dataset**: [Online Retail Dataset (UCI/Kaggle)](https://archive.ics.uci.edu/dataset/352/online+retail)

## Cấu trúc Thư mục

```
├── customer_segmentation.ipynb   # Notebook chính: Toàn bộ quy trình từ xử lý dữ liệu, RFM đến phân cụm và trực quan hóa
├── online+retail/                # Thư mục chứa dữ liệu
│   └── Online Retail.xlsx        # Dữ liệu giao dịch gốc (Transaction Data)
└── README.md                     # Tài liệu hướng dẫn dự án
```

### 1. `customer_segmentation.ipynb` (Phân tích và Phân cụm)
Notebook này thực hiện toàn bộ quy trình Data Science khép kín (End-to-End).

*   **Mục tiêu:** Chuyển đổi dữ liệu giao dịch thô thành các insight về phân khúc khách hàng có thể hành động được (Actionable Insights).
*   **Quy trình:**
    *   **Xử lý dữ liệu (Data Cleaning):**
        *   *Lọc bỏ nhiễu:* Loại bỏ các bản ghi thiếu `CustomerID` (khách vãng lai không định danh).
        *   *Xử lý đơn hàng hủy:* Loại bỏ các giao dịch có `InvoiceNo` bắt đầu bằng 'C' (Cancelled) để không làm sai lệch chỉ số doanh thu.
        *   *Làm sạch logic:* Loại bỏ các giá trị `Quantity` hoặc `UnitPrice` âm.
    *   **Feature Engineering (Tạo đặc trưng RFM):**
        *   **Recency (R):** Số ngày kể từ lần mua hàng cuối cùng (càng thấp càng tốt).
        *   **Frequency (F):** Tổng số lần mua hàng (càng cao càng tốt).
        *   **Monetary (M):** Tổng số tiền đã chi tiêu (càng cao càng tốt).
    *   **Chuẩn hóa dữ liệu (Normalization):**
        *   *Log Transformation:* Áp dụng hàm Log để xử lý độ lệch (skewness) của dữ liệu tài chính (nơi phần lớn khách hàng chi ít và một số ít chi rất nhiều).
        *   *StandardScaler:* Đưa 3 chỉ số R, F, M về cùng một thang đo (mean=0, std=1) để thuật toán K-Means không bị thiên vị bởi biến có giá trị lớn (như Monetary).
    *   **Modeling (K-Means Clustering):**
        *   *Elbow Method:* Sử dụng biểu đồ khuỷu tay để xác định số lượng cụm ($k$) tối ưu (cân bằng giữa độ nén của cụm và số lượng cụm).
        *   *Clustering:* Phân chia khách hàng vào $k$ nhóm dựa trên khoảng cách Euclide trong không gian RFM.
    *   **Trực quan hóa & Insight (Visualization):**
        *   *3D Scatter Plot:* Hình dung sự phân tách của các cụm trong không gian 3 chiều.
        *   *Snake Plot:* Biểu đồ đường so sánh giá trị chuẩn hóa giữa các nhóm, giúp dễ dàng nhận diện xu hướng.
    *   **Gán nhãn tự động (Auto-Labeling):**
        *   Tự động tính điểm xếp hạng cho từng cụm theo công thức: $Score = Frequency + Monetary - Recency$.
        *   Gán các nhãn kinh doanh như: **VIP (Kim cương)**, **Trung thành (Vàng)**, **Tiềm năng**, **Nguy cơ rời bỏ**... dựa trên điểm số.

## Yêu cầu cài đặt

Dự án yêu cầu các thư viện Python sau:

```bash
pip install pandas numpy matplotlib seaborn scikit-learn plotly openpyxl
```
