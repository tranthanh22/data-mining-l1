# CSC14004 - Data Mining - LAB 01 - Data Preprocessing
## Thông tin thành Viên

| Họ và tên | MSSV |
|----------|------|
| Võ Thành Đạt |23127345 |
| Huỳnh Minh Đoàn | 23127347 |
| Trần Ngọc Thành | 23127478 |

---

## Giới thiệu
Đây là đồ án Lab 01 môn **Data Mining and Its Applications**.  
Mục tiêu của đồ án là thực hiện tiền xử lý dữ liệu cho nhiều loại dữ liệu khác nhau bao gồm:

- Image Data
- Tabular Data
- Text Data / Temporal Data

Tất cả các bước tiền xử lý được thực hiện bằng Python trong Jupyter Notebook.

---


## Mô tả ngắn gọn bộ dữ liệu sử dụng

### 1. Image Dataset

Bộ dữ liệu được sử dụng là **New Plant Diseases Dataset**, một tập dữ liệu mở rộng dựa trên dự án PlantVillage, chuyên dùng để phát triển các mô hình học máy nhận diện bệnh lý cây trồng thông qua phân tích hình ảnh lá.

* **Nguồn dữ liệu**: [New Plant Diseases Dataset (Kaggle)](https://www.kaggle.com/datasets/vipoooool/new-plant-diseases-dataset)
* **Mô tả khái quát**: 
    Bộ dữ liệu cung cấp một cái nhìn toàn diện về sức khỏe cây trồng thông qua hình ảnh màu (RGB). Đây là một tập dữ liệu đã được dán nhãn cẩn thận, mô phỏng các vấn đề nông nghiệp thực tế. Dữ liệu bao gồm các mẫu lá ở trạng thái khỏe mạnh và các trạng thái nhiễm bệnh với nhiều mức độ khác nhau. Việc phân tích bộ dữ liệu này giúp giải quyết bài toán chẩn đoán sớm bệnh tật, giảm thiểu thiệt hại kinh tế trong nông nghiệp.
* **Đặc điểm & Quy mô**: 
    * Bao gồm khoảng **87,000 hình ảnh** chất lượng cao.
    * Ảnh được thu thập trong cả điều kiện kiểm soát (phòng thí nghiệm) và điều kiện thực địa, tạo ra sự đa dạng về nền (background) và độ phức tạp của ảnh.
* **Phân loại**: 
    * Được chia thành **38 lớp** (classes) riêng biệt.
    * Bao gồm **14 loài cây** phổ biến (như táo, việt quất, anh đào, ngô, nho, cam, đào, ớt chuông, khoai tây, mâm xôi, đậu nành, bí ngòi, dâu tây và cà chua).
    * Phân tách rõ rệt giữa lá khỏe mạnh và lá bị nhiễm **26 loại bệnh** khác nhau (do nấm, vi khuẩn, virus hoặc ve gây ra).



* **Mục tiêu tiền xử lý**: 
    Do ảnh gốc có kích thước không đồng nhất và điều kiện ánh sáng khác nhau, các bước tiền xử lý là bắt buộc để đảm bảo tính hội tụ của mô hình:
    * **Resizing**: Đưa tất cả ảnh về kích thước chuẩn $224 \times 224$ để phù hợp với các kiến trúc CNN hiện đại.
    * **Data Augmentation**: Sử dụng các phép xoay, lật và điều chỉnh độ sáng để làm phong phú dữ liệu, giúp mô hình chống lại hiện tượng quá khớp (overfitting).
    * **Normalization**: Áp dụng Z-score hoặc Min-Max scaling để đưa phân phối pixel về khoảng tối ưu, giúp tăng tốc độ huấn luyện.
    * **Edge Detection**: Trích xuất đặc trưng cạnh (Canny/Sobel) để hỗ trợ mô hình nhận diện các cấu trúc tổn thương đặc trưng trên bề mặt lá.

### 2. Tabular Dataset

Trong phần tiền xử lý dữ liệu dạng bảng (Tabular) này, bộ dữ liệu được sử dụng là **Credit Card Transactions Fraud Detection Dataset** của người dùng Kartik Shenoy, được sửa đổi và cập nhật lần cuối vào khoảng 6 năm trước trên nền tảng Kaggle.

* **Đường dẫn**: Credit Card Transactions Fraud Detection Dataset

* **Mô tả khái quát**: Bộ dữ liệu này là một tập dữ liệu mô phỏng các giao dịch thẻ tín dụng, được thu thập để phục vụ cho việc phát triển và đánh giá các thuật toán phát hiện gian lận trong giao dịch (fraud detection). Dữ liệu chứa cả giao dịch hợp lệ (legitimate) và gian lận (fraud) trong một khoảng thời gian xác định, với các đặc trưng mô tả liên quan đến giao dịch, khách hàng và người bán hàng.

### 3. Temporal Dataset
Ở phần này nhóm sử dụng bộ dữ liệu cổ phiếu của **Apple** có mã là AAPL có nguồn là **Stock Market Data (NASDAQ, NYSE, S&P500)** do **Paul Timothy Mooney** xây dựng và công bố trên nền tảng Kaggle. Bộ dữ liệu này cung cấp dữ liệu lịch sử giá cổ phiếu của nhiều công ty lớn trên thị trường chứng khoán Mỹ, được thu thập theo tần suất ngày (daily), phản ánh đầy đủ diễn biến giao dịch của từng cổ phiếu qua nhiều năm.

**Đường dẫn trên kaggle:** https://www.kaggle.com/datasets/paultimothymooney/stock-market-data

**Cấu trúc gồm 1 file AAPL.csv**

**Gồm 10590 dòng và 7 cột thuộc tính chính như sau:**

**OHLC (Open, High, Low, Close)**: Phản ánh đầy đủ biến động giá trong một ngày giao dịch.

**Adjusted Close**: Thường được sử dụng trong phân tích dài hạn và mô hình dự báo vì loại bỏ các yếu tố kỹ thuật như chia tách cổ phiếu.

**Volume**: Thể hiện mức độ quan tâm và thanh khoản của thị trường đối với cổ phiếu.	

--- 

## Cấu trúc file 
```
data-mining-l1/
│
├── README.md
├── requirements.txt
│
├── data/
│   ├── images/
│   ├── tabular/
│   └── temporal/
│
├── notebooks/
│   ├── 01_image_preprocessing.ipynb
│   ├── 02_tabular_preprocessing.ipynb
│   └── 04_temporal_preprocessing.ipynb
│
└── docs/
    └── Report.pdf
```

## Cách chạy chương trình

### Bước 1: Clone project
### Bước 2: Cài các môi trường cần thiết
Ở thư mục gốc

```bash
pip install -r requirements.txt
```
### Bước 3: Tải dataset
https://drive.google.com/drive/folders/1JiVZounRd6gtzrzboGj5AX1XL4Ei-D_q?usp=sharing

và để theo cấu trúc file như bên trên

### Bước 3: Mở Jupyter Notebook
### Bước 4: Chạy Notebook
Chạy các notebook theo thứ tự:
- 01_image_preprocessing.ipynb
- 02_tabular_preprocessing.ipynb
- 04_temporal_preprocessing.ipynb

Chạy các cell từ trên xuống dưới.

---

## Tài nguyên bên ngoài
Dataset:

Google Drive:

https://drive.google.com/drive/folders/1JiVZounRd6gtzrzboGj5AX1XL4Ei-D_q?usp=sharing

## Ghi chú

- Code được viết bằng Python
- Sử dụng Jupyter Notebook
- Mỗi bước tiền xử lý đều có giải thích bằng markdown
