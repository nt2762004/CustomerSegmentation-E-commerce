# E-commerce Customer Segmentation

This project builds a customer behavior analysis system using the **RFM model (Recency, Frequency, Monetary)** combined with the **K-Means Clustering** Machine Learning algorithm.

The system focuses on exploring transaction data, grouping customers into sets with similar characteristics (such as VIP, Loyal, Hibernating...) to help businesses make effective personalized Marketing strategies.

## Folder Structure

```
├── customer_segmentation.ipynb   # Main Notebook: Full process from data processing, RFM to clustering and visualization
├── online+retail/                # Data folder
│   └── Online Retail.xlsx        # Original transaction data
└── README.md                     # Project documentation
```

### 1. `customer_segmentation.ipynb` (Analysis and Clustering)
This notebook performs the entire End-to-End Data Science process.

*   **Goal:** Convert raw transaction data into actionable customer segmentation insights.
*   **Process:**
    *   **Data Cleaning:**
        *   *Filter noise:* Remove records missing `CustomerID` (unidentified customers).
        *   *Handle cancelled orders:* Remove transactions with `InvoiceNo` starting with 'C' (Cancelled) to avoid incorrect revenue figures.
        *   *Logic cleaning:* Remove negative `Quantity` or `UnitPrice` values.
    *   **Feature Engineering (Create RFM features):**
        *   **Recency (R):** Number of days since the last purchase (lower is better).
        *   **Frequency (F):** Total number of purchases (higher is better).
        *   **Monetary (M):** Total money spent (higher is better).
    *   **Normalization:**
        *   *Log Transformation:* Apply Log function to handle skewness of financial data (where most customers spend little and a few spend a lot).
        *   *StandardScaler:* Bring 3 indicators R, F, M to the same scale (mean=0, std=1) so the K-Means algorithm is not biased by variables with large values (like Monetary).
    *   **Modeling (K-Means Clustering):**
        *   *Elbow Method:* Use the elbow chart to determine the optimal number of clusters ($k$) (balancing between cluster compactness and number of clusters).
        *   *Clustering:* Divide customers into $k$ groups based on Euclidean distance in RFM space.
    *   **Visualization & Insight:**
        *   *3D Scatter Plot:* Visualize the separation of clusters in 3D space.
        *   *Snake Plot:* Line chart comparing normalized values between groups, helping to easily identify trends.
    *   **Auto-Labeling:**
        *   Automatically calculate ranking score for each cluster using the formula: $Score = Frequency + Monetary - Recency$.
        *   Assign business labels like: **VIP (Diamond)**, **Loyal (Gold)**, **Potential**, **At Risk**... based on the score.

## Installation Requirements

The project requires the following Python libraries:

```bash
pip install pandas numpy matplotlib seaborn scikit-learn plotly openpyxl
```

---

# Phân khúc khách hàng E-commerce (Customer Segmentation)

Dự án này xây dựng một hệ thống phân tích hành vi khách hàng sử dụng mô hình **RFM (Recency, Frequency, Monetary)** kết hợp với thuật toán Machine Learning **K-Means Clustering**.

Hệ thống tập trung vào việc khai phá dữ liệu giao dịch, phân nhóm khách hàng thành các tập hợp có đặc điểm tương đồng (như VIP, Trung thành, Ngủ đông...) để hỗ trợ doanh nghiệp đưa ra các chiến lược Marketing cá nhân hóa hiệu quả.

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
