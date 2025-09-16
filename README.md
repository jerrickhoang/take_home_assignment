# Bài tập Take-Home: Hệ thống gợi ý bài tập tiếng Anh BeeTech

## 1. Bối cảnh & Mục tiêu

Nền tảng GlobalSpeak giúp học viên cải thiện **kỹ năng tiếng Anh** thông qua các bài tập thuộc 4 nhóm kỹ năng chính:  
- **Reading (Đọc hiểu)**  
- **Writing (Viết)**  
- **Listening (Nghe hiểu)**  
- **Speaking (Nói)**  

Mỗi bài tập có độ khó khác nhau (**easy, medium, hard**) và khi học viên hoàn thành, họ sẽ nhận được điểm số từ **0 đến 100**.  

Mục tiêu của hệ thống gợi ý là **dự đoán kết quả học viên sẽ đạt được với những bài tập chưa làm**. Từ đó, chúng ta có thể giới thiệu cho từng hta viên **bài tập phù hợp nhất** với trình độ và lịch sử học tập của họ.  

Bài tập này sẽ đánh giá khả năng của bạn trong việc:  
- Hiểu dữ liệu về tương tác học viên – bài tập.  
- Khai thác các mẫu dữ liệu để xây dựng mô hình gợi ý.  
- Dự đoán chính xác điểm số mà học viên có thể đạt được.  
- Trình bày tư duy mô hình hóa, so sánh phương pháp và phân tích kết quả.  

---

## 2. Dữ liệu cung cấp

Bạn sẽ nhận được 3 tệp CSV:

- **train.csv** – dữ liệu huấn luyện, bao gồm kết quả làm bài (có điểm số).  
- **test.csv** – dữ liệu kiểm tra, có cùng cấu trúc nhưng **không có điểm số** (bạn cần dự đoán).   

### Cấu trúc dữ liệu

- `learner_id` – mã học viên.  
- `exercise_id` – mã bài tập.  
- `exercise_type` – loại bài tập: `reading`, `writing`, `listening`, `speaking`.  
- `difficulty` – độ khó: `easy`, `medium`, `hard`.  
- `score` – điểm số (0–100), chỉ có trong **train.csv**.  
- `timestamp` – thời gian làm bài (UNIX time).  

**Ví dụ trong train.csv:**
```csv
learner_id,exercise_id,exercise_type,difficulty,score,timestamp
1,101,reading,easy,85,1693528102
1,102,reading,medium,60,1693529205
2,201,listening,easy,95,1693530205
2,103,writing,hard,40,1693531005
```

---

## 3. Nhiệm vụ cần thực hiện

1. **Xây dựng mô hình:**
   - Huấn luyện mô hình dự đoán điểm số trên tập `train.csv`.  
   - Bạn có thể lựa chọn và so sánh ít nhất **hai phương pháp**, ví dụ:  
     - Collaborative Filtering (User-User / Item-Item).  
     - Content-based Filtering (sử dụng thông tin `exercise_type`, `difficulty`).  
     - Matrix Factorization (SVD/ALS).  
     - Hoặc bất kỳ phương pháp gợi ý nào khác bạn thấy phù hợp.  

2. **Tạo file dự đoán:**
   - Sử dụng mô hình đã huấn luyện để dự đoán điểm số cho toàn bộ các dòng trong `test.csv`.  
   - Xuất ra file **submission.csv** với định dạng sau:  

   ```csv
   learner_id,exercise_id,predicted_score
   1,305,74.2
   1,401,65.0
   2,102,88.5
   ```

---

## 4. Tiêu chí đánh giá

Bài nộp sẽ được chấm dựa trên tập **test.csv ẩn (có điểm số thật)** với các thước đo sau:  

- **RMSE (Root Mean Squared Error):** đo độ chính xác khi dự đoán điểm số.  
- **Recall@5:** đánh giá khả năng gợi ý đúng các bài tập mà học viên có khả năng đạt điểm cao, trong nhóm 5 gợi ý hàng đầu.  

---

## 5. Yêu cầu nộp bài

Ứng viên cần nộp:  

1. **Notebook Jupyter (`.ipynb`) hoặc script Python (`.py`)** bao gồm:  
   - Mã nguồn đầy đủ.  
   - Giải thích chi tiết phương pháp, lý do lựa chọn mô hình.  
   - Bảng biểu hoặc biểu đồ phân tích dữ liệu (nếu có).  

2. **File CSV (`submission.csv`)** với dự đoán cho toàn bộ tập `test.csv`, đúng định dạng yêu cầu.  

---

## 6. Lưu ý

- Không có một lời giải duy nhất đúng. Điều quan trọng là **cách bạn phân tích, tiếp cận và giải thích kết quả**.  
- Cần chú ý tránh hiện tượng **overfitting** và giải thích rõ cách bạn xử lý vấn đề này.  
- Bài nộp có **cấu trúc rõ ràng, trình bày mạch lạc, phân tích sâu** sẽ được đánh giá cao.  
