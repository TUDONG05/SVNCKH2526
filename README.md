

#  **Đề tài:** Nghiên cứu một số kỹ thuật học máy định hướng phân cụm mờ cộng tác bán giám sát và ứng dụng trong phân loại ảnh

## 📌 Giới thiệu

Đề tài nghiên cứu các kỹ thuật **phân cụm mờ bán giám sát (Semi-Supervised Fuzzy Clustering)** và **phân cụm mờ cộng tác (Collaborative Fuzzy Clustering)** nhằm hỗ trợ bài toán phân loại ảnh trong điều kiện dữ liệu có nhãn hạn chế.

Nghiên cứu triển khai và đánh giá các thuật toán **FCM, SSFCM, S3FCM, ADSFCM, CFCM, S2CFC**, đồng thời đề xuất **ADS3FCM (Asymmetric Deviation Safe Semi-Supervised Fuzzy C-Means)** – kết hợp cơ chế bán giám sát an toàn của S3FCM với ràng buộc độ lệch bất đối xứng của ADSFCM.

Các thuật toán được kiểm chứng trên các bộ dữ liệu chuẩn UCI và ứng dụng vào hai bài toán thực tế:

- 🛰️ **Phân loại lớp phủ đất từ ảnh vệ tinh Landsat 8**
- 🧠 **Phân đoạn mô não từ ảnh MRI T1 BrainWeb**

---

## 🎯 Mục tiêu

- Nghiên cứu nền tảng **Fuzzy C-Means** và các phương pháp phân cụm mờ bán giám sát.
- Khảo sát cơ chế **phân cụm cộng tác** trên dữ liệu được chia thành nhiều site/view.
- Xây dựng và đánh giá thuật toán đề xuất **ADS3FCM**.
- Thực nghiệm trên dữ liệu chuẩn UCI, ảnh vệ tinh Landsat 8 và ảnh MRI BrainWeb.
- Đánh giá chất lượng phân cụm bằng cả chỉ số nội tại và ngoại tại.

---

## 🚀 Các thuật toán nghiên cứu

| Thuật toán | Tên đầy đủ | Vai trò |
|---|---|---|
| **FCM** | Fuzzy C-Means | Thuật toán phân cụm mờ nền tảng |
| **SSFCM** | Semi-Supervised Fuzzy C-Means | Mở rộng FCM với thông tin nhãn |
| **S3FCM** | Safe Semi-Supervised Fuzzy C-Means | Bổ sung cơ chế bán giám sát an toàn |
| **ADSFCM** | Asymmetric Deviation Semi-Supervised Fuzzy C-Means | Bổ sung ràng buộc độ lệch bất đối xứng |
| **ADS3FCM ⭐** | Asymmetric Deviation Safe Semi-Supervised Fuzzy C-Means | **Thuật toán đề xuất của đề tài** |
| **CFCM** | Collaborative Fuzzy C-Means | Phân cụm mờ cộng tác giữa nhiều site |
| **S2CFC** | Safe Semi-Supervised Collaborative Fuzzy Clustering | Kết hợp cộng tác và bán giám sát an toàn |

### ⭐ Thuật toán đề xuất — ADS3FCM

**ADS3FCM** kết hợp ưu điểm của **S3FCM** và **ADSFCM** trên nền tảng Fuzzy C-Means:

```text
                         ┌──────────────┐
                         │     FCM      │
                         │  Nền tảng    │
                         └──────┬───────┘
                                │
                   ┌────────────┴────────────┐
                   ▼                         ▼
            ┌─────────────┐           ┌─────────────┐
            │   S3FCM     │           │   ADSFCM    │
            │ Safe Semi-  │           │ Asymmetric  │
            │ Supervised  │           │  Deviation  │
            └──────┬──────┘           └──────┬──────┘
                   │                         │
                   └────────────┬────────────┘
                                ▼
                       ┌─────────────────┐
                       │    ADS3FCM ⭐   │
                       │   Đề xuất mới   │
                       └─────────────────┘
```

**Các thành phần chính:**

`FCM Objective` + `Safe Semi-Supervision` + `Asymmetric Deviation`

Ngoài ra, quá trình phân cụm được định hướng bằng **K-Means/K-Means++** để khởi tạo tâm cụm và sử dụng **ma trận thành viên FCM** làm thông tin tham chiếu.

> **Lưu ý:** CFCM và S2CFC được sử dụng để nghiên cứu và đối chứng hướng **phân cụm cộng tác**. Cơ chế cộng tác không được tích hợp trực tiếp vào hàm mục tiêu của ADS3FCM.

---

## 🌳 Phân cấp thuật toán

```text
FCM
├── SSFCM
│   ├── S3FCM
│   │   └── ADS3FCM
│   └── ADSFCM
│
├── CFCM
└── S2CFC
```

---

## 📊 Dữ liệu thực nghiệm

### UCI

Các bộ dữ liệu chuẩn được sử dụng để đánh giá khả năng phân cụm trên dữ liệu dạng bảng.

| Dataset | Số mẫu | Số đặc trưng | Số lớp |
|---|---:|---:|---:|
| Iris | 150 | 4 | 3 |
| Wine | 178 | 13 | 3 |
| Dry Bean | 13,611 | 16 | 7 |

Ngoài các bộ dữ liệu trên, báo cáo nghiên cứu còn thực nghiệm trên một số bộ dữ liệu UCI khác để đánh giá tính ổn định của thuật toán.

### Landsat 8

Dữ liệu ảnh viễn thám Landsat 8 sử dụng các kênh phổ:

- Blue — B2
- Green — B3
- Red — B4
- Near-Infrared — B5

Các khu vực thực nghiệm:

- **Tây Hồ – Hà Nội**
- **Lục Nam- Bắc Ninh**

Dữ liệu được tiền xử lý, chuẩn hóa và sử dụng để phân loại các vùng lớp phủ đất.

### MRI BrainWeb

Dữ liệu ảnh não mô phỏng **BrainWeb T1-weighted** được sử dụng để đánh giá khả năng phân đoạn các cấu trúc mô não.

Quy trình xử lý bao gồm:

- Cắt lát ảnh MRI 3D thành ảnh 2D.
- Chuẩn hóa cường độ.
- Lọc nhiễu.
- Phân lập vùng não.
- Trích xuất dữ liệu pixel.
- Phân cụm và so sánh với Ground Truth.

---

## 🖼️ Kết quả trực quan

Hình ảnh kết quả Landsat 8 và MRI BrainWeb được lưu trong kho dữ liệu
nội bộ, không phân phối qua repository công khai này.

---

## 📈 Chỉ số đánh giá

Nghiên cứu sử dụng cả **chỉ số nội tại** và **chỉ số ngoại tại** để đánh giá chất lượng phân cụm.

### Internal Metrics

| Chỉ số | Ý nghĩa | Hướng tốt |
|---|---|---|
| DI | Dunn Index | ↑ |
| DB | Davies-Bouldin Index | ↓ |
| PC | Partition Coefficient | ↑ |
| XB | Xie-Beni Index | ↓ |
| PE | Partition Entropy | ↓ |
| SI | Silhouette Index | ↑ |

### External Metrics

| Chỉ số | Ý nghĩa | Hướng tốt |
|---|---|---|
| AC | Accuracy | ↑ |
| F1 | F1-score | ↑ |
| NMI | Normalized Mutual Information | ↑ |
| ARI | Adjusted Rand Index | ↑ |
| PUR | Purity | ↑ |

---

## 📌 Kết quả nổi bật

ADS3FCM cho thấy khả năng cải thiện chất lượng phân loại so với FCM truyền thống trên các dữ liệu thực nghiệm.

Một số kết quả tiêu biểu:

- **Landsat 8 — Lục Nam:** AC đạt khoảng **0.778**.
- **MRI BrainWeb:** AC đạt khoảng **0.81**.
- Thuật toán cho kết quả tốt trên nhiều bộ dữ liệu UCI và dữ liệu ảnh thực tế khi lượng nhãn sử dụng bị hạn chế.

Bên cạnh đó, ADS3FCM có chi phí tính toán cao hơn ADSFCM và vẫn nhạy với dữ liệu mất cân bằng, đặc biệt khi một số cụm có kích thước quá nhỏ.

---

## 📁 Nội dung repository

```text
SVNCKH2526/
├── README.md
├── papers/
│   └── README.md                # Ghi chú về tài liệu tham khảo lưu cục bộ
```

Mã nguồn, dữ liệu thực nghiệm và các tài liệu PDF được lưu nội bộ,
không phân phối qua repository công khai này.

---

## 🛠️ Công nghệ sử dụng

| Công nghệ | Mục đích |
|---|---|
| Python | Ngôn ngữ triển khai chính |
| NumPy | Tính toán ma trận |
| SciPy | Đại số tuyến tính và tính toán khoa học |
| Pandas | Xử lý dữ liệu bảng |
| Scikit-learn | Tiền xử lý, K-Means và các chỉ số đánh giá |
| Rasterio | Đọc và xử lý ảnh GeoTIFF |
| Nibabel | Xử lý dữ liệu ảnh y tế |
| Scikit-image | Tiền xử lý và xử lý hình thái học |
| Matplotlib | Trực quan hóa dữ liệu và kết quả |

---

## ▶️ Chạy chương trình nội bộ

> Phần này dành cho thành viên đã được cung cấp mã nguồn và dữ liệu
> qua kênh nội bộ; repository công khai không bao gồm các tệp này.

### 1. Clone repository

```bash
git clone https://github.com/TUDONG05/SVNCKH2526 
```

### 2. Tạo môi trường ảo

```bash
python -m venv .venv
```

#### Windows

```bash
.venv\Scripts\activate
```

#### Linux / macOS

```bash
source .venv/bin/activate
```

### 3. Cài đặt thư viện

```bash
pip install numpy scipy pandas scikit-learn rasterio nibabel scikit-image matplotlib
```

### 4. Chạy thực nghiệm

Ví dụ:

```bash
python ads3fcm.py
```

Thực nghiệm Landsat 8:

```bash
python s2cfc_landsat.py
```

Thực nghiệm MRI:

```bash
python mri.py
```

> Một số script có thể yêu cầu điều chỉnh đường dẫn dữ liệu hoặc tham số thực nghiệm trước khi chạy.

---

## 🔬 Hướng phát triển

Một số hướng mở rộng được đề xuất:

- **Spatial ADS3FCM:** tích hợp thông tin không gian giữa các pixel lân cận.
- Mở rộng ADS3FCM sang **Kernel Fuzzy Clustering**.
- Phát triển phiên bản phân tán cho dữ liệu quy mô lớn.
- Cải thiện tốc độ hội tụ và chi phí tính toán.
- Nâng cao khả năng xử lý dữ liệu mất cân bằng và nhiễu.
- Mở rộng thực nghiệm trên các tập dữ liệu ảnh y tế và viễn thám lớn hơn.

---

## 👥 Nhóm nghiên cứu

**Trường Đại học Công nghiệp Hà Nội (HaUI)**  
**Năm học:** 2025–2026

### Giảng viên hướng dẫn

**ThS. Nguyễn Xuân Hoàng**

### Thành viên

- **Đồng Văn Tú** — Chủ nhiệm đề tài
- **Giang Lê Hoàng**
- **Lê Tiến Đạt**
- **Bùi Thùy Dương**

---

## 📚 Tài liệu tham khảo

Các bài báo và tài liệu nền tảng được lưu trong thư mục [`papers/`](./papers/), bao gồm:

- Fuzzy C-Means
- S3FCM
- ADSFCM
- S2CFC

Chi tiết lý thuyết, chứng minh và kết quả thực nghiệm được trình bày trong báo cáo tổng kết đề tài.

---

## 📄 License

Repository được xây dựng phục vụ mục đích **nghiên cứu và học thuật**.

Nếu sử dụng mã nguồn hoặc kết quả của đề tài cho nghiên cứu khác, vui lòng trích dẫn nguồn phù hợp.
