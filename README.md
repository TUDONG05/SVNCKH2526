# Nghiên cứu phân cụm mờ cộng tác bán giám sát và ứng dụng trong phân loại ảnh

## Giới thiệu

Đề tài nghiên cứu các kỹ thuật **phân cụm mờ bán giám sát**
(Semi-Supervised Fuzzy Clustering) và **phân cụm mờ cộng tác**
(Collaborative Fuzzy Clustering), hướng đến bài toán phân loại ảnh
trong điều kiện dữ liệu có nhãn hạn chế.

Nghiên cứu triển khai và đánh giá các thuật toán **FCM, SSFCM, S3FCM,
ADSFCM, CFCM và S2CFC**, đồng thời đề xuất **ADS3FCM (Asymmetric Deviation
Safe Semi-Supervised Fuzzy C-Means)**.

> Repository này chỉ công khai thông tin tổng quan của đề tài.
> Mã nguồn, dữ liệu thực nghiệm, hình ảnh kết quả và các bài báo PDF
> được lưu trữ nội bộ, không phân phối qua GitHub. Poster tổng hợp
> của đề tài được công khai bên dưới.

## Poster nghiên cứu

[Xem hoặc tải poster tổng hợp đề tài (PDF, khổ A1, 5,4 MB)](PTKH_DongVanTu.pdf)

Poster trình bày tóm tắt cơ sở lý thuyết, phương pháp nghiên cứu, thuật toán
đề xuất ADS3FCM, dữ liệu thực nghiệm, kết quả và hướng phát triển.

## Mục tiêu

- Nghiên cứu nền tảng Fuzzy C-Means và các phương pháp phân cụm mờ bán giám sát.
- Khảo sát cơ chế phân cụm cộng tác trên dữ liệu được chia thành nhiều site/view.
- Xây dựng và đánh giá thuật toán đề xuất ADS3FCM.
- Thực nghiệm trên dữ liệu UCI, ảnh vệ tinh Landsat 8 và ảnh MRI BrainWeb.
- Đánh giá chất lượng phân cụm bằng các chỉ số nội tại và ngoại tại.

## Các thuật toán nghiên cứu

| Thuật toán | Tên đầy đủ | Vai trò |
|---|---|---|
| **FCM** | Fuzzy C-Means | Thuật toán phân cụm mờ nền tảng |
| **SSFCM** | Semi-Supervised Fuzzy C-Means | Mở rộng FCM với thông tin nhãn |
| **S3FCM** | Safe Semi-Supervised Fuzzy C-Means | Bổ sung cơ chế bán giám sát an toàn |
| **ADSFCM** | Asymmetric Deviation Semi-Supervised Fuzzy C-Means | Bổ sung ràng buộc độ lệch bất đối xứng |
| **ADS3FCM** | Asymmetric Deviation Safe Semi-Supervised Fuzzy C-Means | Thuật toán đề xuất của đề tài |
| **CFCM** | Collaborative Fuzzy C-Means | Phân cụm mờ cộng tác giữa nhiều site |
| **S2CFC** | Safe Semi-Supervised Collaborative Fuzzy Clustering | Kết hợp cộng tác và bán giám sát an toàn |

### Thuật toán đề xuất ADS3FCM

ADS3FCM kết hợp cơ chế bán giám sát an toàn của S3FCM với ràng buộc
độ lệch bất đối xứng của ADSFCM trên nền tảng Fuzzy C-Means:

```text
FCM
├── S3FCM: Safe Semi-Supervision
├── ADSFCM: Asymmetric Deviation
└── ADS3FCM: Safe Semi-Supervision + Asymmetric Deviation
```

Quá trình phân cụm được định hướng bằng K-Means/K-Means++ để khởi tạo
tâm cụm và sử dụng ma trận thành viên FCM làm thông tin tham chiếu.

> CFCM và S2CFC được sử dụng để nghiên cứu, đối chứng hướng phân cụm
> cộng tác; cơ chế cộng tác không được tích hợp trực tiếp vào hàm mục tiêu
> của ADS3FCM.

## Dữ liệu và bài toán thực nghiệm

### Dữ liệu UCI

| Dataset | Số mẫu | Số đặc trưng | Số lớp |
|---|---:|---:|---:|
| Iris | 150 | 4 | 3 |
| Wine | 178 | 13 | 3 |
| Dry Bean | 13.611 | 16 | 7 |

### Landsat 8

Ảnh viễn thám Landsat 8 được khai thác trên các kênh phổ Blue, Green, Red
và Near-Infrared để phân loại lớp phủ đất tại Tây Hồ và Lục Nam.

### MRI BrainWeb

Dữ liệu MRI T1-weighted của BrainWeb được sử dụng để phân đoạn các cấu trúc
mô não và so sánh kết quả với ground truth.

## Chỉ số đánh giá

| Nhóm | Chỉ số | Hướng tốt |
|---|---|---|
| Nội tại | Dunn Index (DI) | Tăng |
| Nội tại | Davies-Bouldin Index (DB) | Giảm |
| Nội tại | Partition Coefficient (PC) | Tăng |
| Nội tại | Xie-Beni Index (XB) | Giảm |
| Nội tại | Partition Entropy (PE) | Giảm |
| Nội tại | Silhouette Index (SI) | Tăng |
| Ngoại tại | Accuracy (AC) | Tăng |
| Ngoại tại | F1-score | Tăng |
| Ngoại tại | Normalized Mutual Information (NMI) | Tăng |
| Ngoại tại | Adjusted Rand Index (ARI) | Tăng |
| Ngoại tại | Purity (PUR) | Tăng |

## Kết quả nổi bật

- ADS3FCM cải thiện chất lượng phân loại so với FCM truyền thống trên các
  dữ liệu thực nghiệm.
- Landsat 8 tại Lục Nam đạt Accuracy khoảng **0,778**.
- MRI BrainWeb đạt Accuracy khoảng **0,81**.
- Thuật toán có chi phí tính toán cao hơn ADSFCM và còn nhạy với dữ liệu
  mất cân bằng, đặc biệt khi một số cụm có kích thước quá nhỏ.

## Công nghệ sử dụng trong nghiên cứu

Python, NumPy, SciPy, Pandas, Scikit-learn, Rasterio, Nibabel, Scikit-image và
Matplotlib được sử dụng trong quá trình triển khai và thực nghiệm.

## Nội dung repository công khai

```text
SVNCKH2526/
├── .gitignore
├── README.md
├── PTKH_DongVanTu.pdf
└── papers/
    └── README.md
```

Thư mục `papers/` chỉ chứa ghi chú về tài liệu tham khảo. Các bản PDF
không được công khai trong repository.

## Hướng phát triển

- Tích hợp thông tin không gian giữa các pixel lân cận vào ADS3FCM.
- Mở rộng ADS3FCM sang Kernel Fuzzy Clustering.
- Phát triển phiên bản phân tán cho dữ liệu quy mô lớn.
- Cải thiện tốc độ hội tụ và chi phí tính toán.
- Nâng cao khả năng xử lý dữ liệu mất cân bằng và nhiễu.

## Nhóm nghiên cứu

**Trường Đại học Công nghiệp Hà Nội (HaUI)**  
**Năm học:** 2025–2026

**Giảng viên hướng dẫn:** ThS. Nguyễn Xuân Hoàng

**Thành viên:**

- Đồng Văn Tú — Chủ nhiệm đề tài
- Giang Lê Hoàng
- Lê Tiến Đạt
- Bùi Thùy Dương

## Tài liệu tham khảo

Các hướng tài liệu nền tảng gồm Fuzzy C-Means, S3FCM, ADSFCM và S2CFC.
Danh mục tài liệu được ghi chú tại [`papers/README.md`](papers/README.md); các tệp
PDF được lưu nội bộ.

## Sử dụng và trích dẫn

Repository được công khai nhằm giới thiệu đề tài nghiên cứu. Khi sử dụng
thông tin hoặc kết quả của đề tài, vui lòng trích dẫn nguồn phù hợp.
