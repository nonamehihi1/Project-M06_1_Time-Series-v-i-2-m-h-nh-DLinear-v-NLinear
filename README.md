# Project-M06_1_Time-Series-DLinear-v-NLinear
Dự đoán chính xác dạng time series với 2 mô hình

Dự báo chuỗi thời gian có nhiều thử thách không chỉ nằm ở việc đoán giá của ngày mai, mà là việc 'nhìn xa'. Ngoài ra dữ liệu cực kỳ nhiễu, phi tuyến và không có tính dừng. Khi nghe đến vấn đề phụ thuộc dài hạn, ta thường nghĩ đến các lớp mô hình tranformer, nhưng độ phức tạp của thuật toán sẽ trở nên không khả thi trong thời gian thật. Do đó ta sẽ sử dụng hướng đi LTSF-Linear

Câu hỏi: Chúng ta muốn dự đoán cái gì? 
-Khi nói về kiểu dự đoán, chúng ta có thể dự đoán 1 bước là giá trị ngay tiếp theo, hoặc dự đoán nhiều bước là một chuỗi giá trị trong tương lai
-Chiến lược phổ biến đầu tiên cho bài toán dự đoán nhiều bước(multi-step) là đệ quy, tức là mô hình đầu tiên dự đoán bước thời gian t+1, sau đó kết quả dự đoán này sẽ được làm đầu vào mới để mô hình tiếp tục dự đoán bước t+2. Mặc dù trực quan, phương pháp này có rủi ro lớn là nếu có lỗi nhỏ ở bước t+1 có thể bị khuếch đại và làm sai dự đoán ở các bước dự đoán t+H
-Chiến lược thứ 2 là trực tiếp, mô hình sẽ được huấn luyện để học ánh xạ thằng từ toàn bộ dữ liệu trong quá khứ để dự đoán đồng thời toàn bộ các bước tương lai chỉ 1 lần duy nhất 

Trong project này sẽ sử dụng chiến lược dự báo trực tiếp

I. Mô hình LTSF-Linear: Linear
- Cơ chế: Dùng 1 lớp biến đổi tuyến tính để ánh xạ trực tiếp từ quá khứ vào tương lai: y = Wx + b
- Cách hoạt động:
- <img width="715" height="254" alt="{94036B2E-536A-4E43-B59F-E2C20F40276E}" src="https://github.com/user-attachments/assets/03199c43-2977-470e-9af0-da0484866cc6" />
- Nhược điểm là không phù hợp với những dữ liệu có phi tuyến mạnh

II. Mô hình LTSF-Linear: NLinear
Trong thực tế, dữ liệu chuỗi thời gian thường bị hiện tượng Additive level shift.
Ví dụ: Giá cổ phiếu năm nay ở mức 100-110, nhưng năm sau có thể vọt lên mức 500-510.
Nếu dùng mô hình Linear thuần túy, nó sẽ bị "khớp" vì chưa bao giờ thấy mức giá 500 trong quá trình học. NLinear giải quyết việc này bằng kỹ thuật Re-centering (đưa về mốc 0).

- Cơ chế: sử dụng kỹ thuật re-centering
- Cách hoạt động :
<img width="860" height="318" alt="{E4100883-A9B3-4E81-A63B-00EA17879623}" src="https://github.com/user-attachments/assets/29cc18c4-8e2e-4fcf-9131-8050287da315" />


III. Mô hình LTSF-Linear: DLinear
- Cơ chế: mô hình này sẽ chia dữ liệu thành 2 phần là : xu hướng(thành phần thay đổi chậm theo thời gian, phản ánh xu hướng dài hạn của chuỗi) và Mùa vụ(phần còn lại khi bỏ xu hướng)

- Cách hoạt động:<img width="907" height="456" alt="{D3752539-52EE-4015-8B18-5DF4CD70D777}" src="https://github.com/user-attachments/assets/cbc30314-821c-40a4-bd38-880f6ef71050" />
