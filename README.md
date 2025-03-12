# Bank-Loans-Analyst
## Tổng quan dự án
### 1. Giới thiệu
Dự án phân tích dữ liệu khoản vay ngân hàng nhằm mục tiêu đánh giá rủi ro tín dụng, xác định các yếu tố ảnh hưởng đến khả năng hoàn trả của khách hàng và hỗ trợ quyết định phê duyệt khoản vay. Thông qua việc khai thác dữ liệu lịch sử, dự án sẽ cung cấp các thông tin quan trọng cũng như các xu hướng vốn vay giúp ngân hàng tối ưu hóa chiến lược cho vay và giảm thiểu rủi ro nợ xấu.

### 2. Mục tiêu
- **Phân tích xu hướng khoản vay:** Xác định các đặc điểm của khách hàng có khoản vay được duyệt hoặc bị từ chối.
- **Đánh giá rủi ro tín dụng:** Xác định các yếu tố ảnh hưởng đến khả năng có khoản nợ xấu.
- **Hỗ trợ cải thiện chính sách cho vay:** Đề xuất các biện pháp giảm rủi ro và tối ưu hóa lợi nhuận.

### 3. Dữ liệu
- **Nguồn dữ liệu:** Dữ liệu lịch sử khoản vay từ ngân hàng, bao gồm thông tin cá nhân, tình trạng tài chính, lịch sử tín dụng và thông tin khoản vay (**Nguồn**: Cá nhân)
- **Các trường dữ liệu chính:**
  - **Thông tin khách hàng:** Tuổi, thu nhập, tình trạng hôn nhân, nghề nghiệp.
  - **Lịch sử tín dụng:** Điểm tín dụng, số lượng tài khoản tín dụng, số lần chậm thanh toán.
  - **Thông tin khoản vay:** Số tiền vay, thời hạn vay, lãi suất, mục đích vay.
  - **Kết quả hoàn trả:** Đã trả đúng hạn, trễ hạn hoặc vỡ nợ.

### 4. Phương pháp phân tích
- **Thống kê mô tả:** Phân tích tổng quan về dữ liệu, kiểm tra phân phối và tìm hiểu các đặc điểm nổi bật.
- **Trực quan hóa dữ liệu:** Sử dụng biểu đồ để thể hiện xu hướng và mối quan hệ giữa các biến số.

### 5. Công cụ sử dụng
- **Ngôn ngữ lập trình:** Python (Pandas, NumPy, Scikit-learn, Matplotlib, Seaborn)
- **Trực quan hóa:** Tableau
- **Xử lý dữ liệu:**  Python, Pandas

## Quy trình thực hiện phân tích
### 1. Tiền xử lý dữ liệu 
<img width="1075" alt="Ảnh màn hình 2025-03-12 lúc 13 34 44" src="https://github.com/user-attachments/assets/b61ee82e-b2e8-4f7b-94dc-4004fd8e345e" />

- Đặt lại tên chuẩn cho các cột
- Xử lý null và duplicates bằng thế các giá trị mean, các cặp dữ liệu tương ứng
- Thiết lập lại dạng dữ liệu chuẩn cho các cột dữ liệu (number, object)
- Nhóm các cặp dữ liệu theo từng bộ thông tin (Thông tin khách hàng, thông tin khoản vay, lịch sử tín dụng)

#### Thông tin dữ liệu sau xử lý 
**Thông tin khoản vay & tín dụng**
- **application_date**: Ngày khách hàng đăng ký khoản vay
- **credit_score_v2**: Điểm tín dụng của khách hàng (đánh giá mức độ tin cậy trong vay vốn)
- **loan_id**: Mã định danh duy nhất của khoản vay
- **initial_loan_amount**: Số tiền vay ban đầu khách hàng đăng ký
- **disbursed_amount**: Số tiền thực tế được ngân hàng giải ngân
- **remaining_principal**: Số dư gốc còn lại của khoản vay
- **interest_payment_type**: Hình thức thanh toán lãi suất (trả góp theo kỳ, trả trước, trả sau...)
- **longest_overdue_days**: Số ngày trễ hạn dài nhất của khoản vay
- **number_of_loans**: Tổng số khoản vay khách hàng đã từng đăng ký
- **has_bad_debt**: Khách hàng có nợ xấu hay không (1: Có, 0: Không)
- **has_late_payment**: Khách hàng có từng trả chậm hay không (1: Có, 0: Không)

**Thông tin cá nhân khách hàng**
- **id**: Mã định danh duy nhất của khách hàng
- **full_name**: Họ và tên khách hàng
- **card_number**: Số thẻ căn cước hoặc chứng minh nhân dân
- **gender**: Giới tính của khách hàng
- **birthday**: Ngày sinh của khách hàng

**Thông tin liên hệ & nơi cư trú**
- **customer_phone_number**: Số điện thoại khách hàng
- **city_name**: Thành phố nơi khách hàng sinh sống
- **district_name**: Quận/huyện nơi khách hàng sinh sống
- **ward_name**: Phường/xã nơi khách hàng sinh sống
- **residence_type**: Loại hình nhà ở (thuê, sở hữu cá nhân, đồng sở hữu...)
- **residence_duration**: Số năm khách hàng đã sinh sống tại địa chỉ hiện tại
- **household_city_name**: Thành phố theo hộ khẩu thường trú
- **household_district_name**: Quận/huyện theo hộ khẩu thường trú
- **household_ward_name**: Phường/xã theo hộ khẩu thường trú

**Thông tin công việc & thu nhập**
- **job_title**: Nghề nghiệp hoặc chức danh công việc của khách hàng
- **company_name**: Tên công ty nơi khách hàng làm việc
- **company_address**: Địa chỉ công ty
- **company_city**: Thành phố nơi công ty đặt trụ sở
- **company_district**: Quận/huyện nơi công ty đặt trụ sở
- **salary**: Mức lương hàng tháng của khách hàng

**Thông tin về người thân & tham chiếu**
- **relative_family_name**: Mối quan hệ với người thân tham chiếu
- **family_full_name**: Họ và tên người thân tham chiếu

**Thông tin sản phẩm tài chính & kiểm tra tín dụng**
- **credit_product_name**: Tên gói vay hoặc sản phẩm tín dụng mà khách hàng đăng ký
- **check_time**: Thời gian kiểm tra hồ sơ vay của khách hàng

**Thời gian & trạng thái khoản vay**
- **from_date**: Ngày bắt đầu khoản vay
- **to_date**: Ngày kết thúc khoản vay
- **status**: Trạng thái khoản vay (đang hoạt động, đã tất toán, quá hạn...)

### 2. Phân tích Time Series
![image](https://github.com/user-attachments/assets/3ffbe0df-567e-4421-944d-a8c8df7d3b2a)

**(Phỏng đoán ban đầu)** Số lượng khoản vay trong các tháng đầu năm tương đối cao, tuy nhiên, tổng số tiền giải ngân chủ yếu tập trung vào các tháng cuối năm. Điều này có thể do ngân hàng đẩy mạnh giải ngân vào giai đoạn cuối năm nhằm đạt được các mục tiêu tài chính. Bên cạnh đó, đầu năm thường có nhiều dịp lễ, Tết, dẫn đến nhu cầu chi tiêu tăng cao, đặc biệt đối với các khoản vay nhỏ phục vụ mua sắm. Xu hướng này cũng phần nào thể hiện ở các tháng cuối năm.

Đi sâu hơn thì tìm hiểu đến tính chất của các khoản vay này (theo mục khoản vay, tình trạng và số tiền còn lại)

<img width="634" alt="Ảnh màn hình 2025-03-12 lúc 13 51 29" src="https://github.com/user-attachments/assets/999234bb-050d-40c7-b400-5aaa33177c79" />

Có thể thấy rằng các khoản vay lãi theo ngày xuất hiện trong hầu hết các tháng trong năm, chủ yếu dành cho các khoản vay ngắn hạn với chu kỳ thanh toán nhanh. Trong khi đó, vào thời điểm cuối năm, số lượng các khoản vay dài hạn có xu hướng gia tăng, thường liên quan đến nhu cầu đầu tư hoặc mua sắm tài sản cố định. Ngoài ra, các ngân hàng cũng thường tung ra các chương trình ưu đãi vay dài hạn vào cuối năm nhằm thu hút khách hàng và kích thích nhu cầu vay vốn.

<img width="1270" alt="Ảnh màn hình 2025-03-12 lúc 13 56 54" src="https://github.com/user-attachments/assets/8dcc2cbc-b444-4c34-a722-81609a1086a7" />

Từ dữ liệu trên, có thể thấy rằng hai khoản vay chủ yếu của khách hàng là "Cầm cố Điện thoại" và "Cầm cố Xe máy". Đặc biệt, trong hai năm 2017 và 2018, các khoản vay ngắn hạn như "Vay theo sim" và "Cầm cố Điện thoại" có mức giải ngân thấp, tập trung chủ yếu vào các tháng 2, 3, và 4. Trong khi đó, các khoản vay có giá trị lớn hơn như "Cầm cố Xe máy" và "Đăng ký Xe ô tô" lại có xu hướng tăng dần và dịch chuyển về gần cuối năm.

Ngoài ra, có thể quan sát thấy sự thay đổi trong xu hướng vay vốn của khách hàng, khi họ dần mở rộng sang sử dụng nhiều sản phẩm tài chính khác nhau thay vì chỉ tập trung vào một số hình thức vay nhất định.

Bên cạnh xu hướng vay vốn, việc theo dõi các chỉ số liên quan đến thu hồi nợ cũng đóng vai trò quan trọng trong quản lý tín dụng. Các yếu tố như tỷ lệ thu hồi nợ, số dư nợ còn lại, và hiệu suất thu hồi giúp đánh giá hiệu quả hoạt động của ngân hàng và rủi ro tín dụng.

Cụ thể, việc phân tích tỷ lệ thu hồi nợ theo từng sản phẩm vay có thể cho thấy sự khác biệt giữa các nhóm khoản vay ngắn hạn như “Vay theo sim”, “Cầm cố Điện thoại” so với các khoản vay dài hạn hơn như “Cầm cố Xe máy” hay “Đăng ký Xe ô tô”. Thông qua đó, ngân hàng có thể xác định được những sản phẩm có mức độ rủi ro cao và điều chỉnh chính sách cho vay phù hợp.

![image](https://github.com/user-attachments/assets/bf13f4e5-7915-45cb-b23f-30e7e9cd8b20)

Ngoài ra, số dư nợ còn lại theo từng thời điểm cũng là một chỉ số quan trọng, giúp đánh giá khả năng khách hàng hoàn trả khoản vay cũng như xác định thời điểm thích hợp để thực hiện các biện pháp thu hồi. Việc phát triển thêm các phân tích về tốc độ thu hồi nợ theo tháng/quý, xu hướng gia tăng vấn đề nợ xấu, hay tác động của chính sách ưu đãi đối với tỷ lệ thu hồi sẽ giúp ngân hàng có cái nhìn toàn diện hơn về chất lượng danh mục tín dụng của mình.

![image](https://github.com/user-attachments/assets/e603d1a0-23a5-4c80-9a3f-5571d8b50ab8)

### 3. Các yếu tố ảnh hưởng đến nợ xấu

Tỷ lệ nợ xấu của ngân hàng hiện vẫn ở mức khá cao, mặc dù đã có sự kiểm soát và cải thiện theo từng năm. Đặc biệt, vào Quý 1 và Quý 2, khi có nhiều khoản vay ngắn hạn với giá trị thấp, nguy cơ nợ xấu thường tăng lên, đòi hỏi các biện pháp quản lý chặt chẽ hơn để hạn chế rủi ro tín dụng.

Để có cái nhìn sâu hơn, cần thực hiện phân tích nhóm khách hàng có tỷ lệ nợ xấu cao nhằm tìm ra những điểm khác biệt so với các nhóm khách hàng còn lại. Một số yếu tố có thể được xem xét bao gồm:

- Đặc điểm nhân khẩu học: Có sự khác biệt nào về độ tuổi, nghề nghiệp, khu vực sinh sống so với nhóm khách hàng có tỷ lệ trả nợ tốt không?
- Khả năng chi trả: Thu nhập trung bình và mức độ ổn định tài chính của nhóm này.
- Sản phẩm vay phổ biến: Họ chủ yếu vay theo hình thức nào (ví dụ: vay theo sim, cầm cố tài sản…)?
- Lịch sử tín dụng: Tỷ lệ khách hàng có điểm tín dụng thấp hoặc có tiền sử nợ xấu trong quá khứ.

**Đặc điểm nhân khẩu học:** 
**Nhóm ngành nghề nghiệp**

<img width="526" alt="Ảnh màn hình 2025-03-12 lúc 14 15 55" src="https://github.com/user-attachments/assets/473e0d5a-11e9-4cbc-8a52-cafbe7a36329" />

Có thể thấy rằng nhóm ngành "Nhà nước, Công an, Quân đội" chiếm tỷ lệ cao nhất, tuy nhiên số lượng khoản vay thực tế lại ở mức thấp, dẫn đến việc nhóm này chưa thực sự mang tính đại diện.

Thay vào đó, các nhóm ngành "Nhân viên văn phòng" và "Tự doanh & Kinh doanh" có tỷ lệ vay vốn khá cao. Đặc biệt, việc chưa xác định rõ nghề nghiệp của người vay cũng là một yếu tố đáng chú ý, với nhóm "unknown" chiếm 9.13%. Điều này cho thấy có một phần khách hàng chưa được phân loại rõ ràng về nghề nghiệp, có thể do thiếu thông tin hoặc chưa cập nhật đầy đủ dữ liệu hồ sơ.

Việc xác định tính chất nghề nghiệp của người vay không chỉ dừng lại ở danh mục ngành nghề mà còn liên quan đến các yếu tố khác như nơi làm việc, loại hình doanh nghiệp. Tuy nhiên, trong phân tích trên, chưa có đủ dữ liệu và thông tin bên ngoài để xác định chính xác những yếu tố này. Vì vậy, tôi sẽ chuyển hướng sang phân tích tiếp về độ tuổi trung bình của nhóm khách hàng, nhằm tìm hiểu thêm về đặc điểm nhân khẩu học và xu hướng vay vốn theo độ tuổi.

![image](https://github.com/user-attachments/assets/869987e4-5a02-4596-870e-df64b195a9ea)

Ở phần này thì chưa có điểm gì qúa khác biệt số với những nhóm nợ khác 

![image](https://github.com/user-attachments/assets/808c62df-5caf-41cb-945f-4d35bd77f2ba)

Thời gian sinh sống cũng chưa có sự khác biệt về tỷ lệ giữa các nhóm, tỷ lệ nợ xấu được dàn đều ở mức 7% - 10% cho các nhóm nên nhận thấy được cơ cấu thu hồi nợ và phê duyệt khoản vay của ngân hàng thực hiện chưa thực sự tốt và tỷ lệ nợ xấu ngoài việc phân phối chủ yếu theo nhóm ngành thì đặc điểm dân cư chưa thực sự quá ảnh hưởng.

**Khả năng chi trả:**

![image](https://github.com/user-attachments/assets/62626a0c-3d9e-403e-ae1a-a5f6b02b0c9c)

Mức lương chỉ chênh lệch nhau 1 chút, chưa thể hiện rõ được đặc điểm của nhóm nợ xấu, không quá khác biệt so với các nhóm khác (Đặc điểm có thể nằm ở các nhóm ngành nghề) (Thông tin này cũng có thể là người vay tự khai nên chưa xác định được đúng)

**Lịch sử tín dụng**

**Phân phối điểm tín dụng**

![image](https://github.com/user-attachments/assets/8fe5f446-a4ad-48bd-9e46-2590db764aa2)

![image](https://github.com/user-attachments/assets/3acae28b-1612-4351-9a42-26e65708ccec)

Biểu đồ cho thấy nhóm Nợ xấu có điểm tín dụng trung bình 525.3, thấp hơn đáng kể so với nhóm Khác (595.8). Khách hàng thuộc nhóm Nợ xấu chủ yếu có điểm dưới 550, trong khi nhóm Khác tập trung nhiều từ 600-700. Điều này cho thấy nguy cơ vỡ nợ cao hơn ở những khách hàng có điểm tín dụng thấp.

Ngân hàng nên siết chặt điều kiện vay với khách có điểm dưới 500, đồng thời tăng cường kiểm soát rủi ro và hỗ trợ nâng cao điểm tín dụng. Theo dõi xu hướng này giúp điều chỉnh chính sách tín dụng phù hợp, đảm bảo tăng trưởng bền vững.

**Lịch sử tín dụng** 

<img width="388" alt="Ảnh màn hình 2025-03-12 lúc 14 39 59" src="https://github.com/user-attachments/assets/ed03acef-0d8a-4d7a-aad1-12f3b2cc4656" />

Bảng dữ liệu thể hiện tỷ lệ các trạng thái khoản vay theo biến has_late_payment (có từng trễ hạn thanh toán hay không).

- Khách hàng không có trễ hạn (0): Tỷ lệ Nợ xấu cao hơn (9.13%) so với nhóm có trễ hạn (5.65%), cho thấy nhiều khoản vay có thể rơi vào nợ xấu ngay cả khi không có lịch sử trễ hạn.
- Khách hàng có trễ hạn (1): Tỷ lệ Đang vay cao hơn (29.46%) so với nhóm không trễ hạn (23.98%), có thể do họ tiếp tục vay dù từng trễ hạn.

Điều này cho thấy cần xem xét thêm các yếu tố khác ngoài trễ hạn để đánh giá rủi ro tín dụng chính xác hơn.

<img width="369" alt="Ảnh màn hình 2025-03-12 lúc 14 42 04" src="https://github.com/user-attachments/assets/488f4958-0efc-4cbb-97fa-6202ca869b72" />

Bảng dữ liệu cho thấy sự khác biệt đáng kể giữa khách hàng có lịch sử nợ xấu và không có nợ xấu trước đó. Cụ thể, nhóm khách hàng từng có nợ xấu có tỷ lệ nợ xấu hiện tại lên đến 18.32%, cao gấp khoảng 2.5 lần so với nhóm không có nợ xấu trước đây (7.45%).

Điều này nhấn mạnh rằng lịch sử tín dụng đóng vai trò quan trọng trong việc đánh giá rủi ro và quyết định cấp tín dụng của ngân hàng, đồng thời phản ánh xu hướng cẩn trọng hơn trong quản lý danh mục cho vay.

## Hướng phát triển trong tương lai
- **Mở rộng tập dữ liệu:** Tích hợp thêm thông tin về thị trường và yếu tố kinh tế vĩ mô.
- **Triển khai ứng dụng thực tế:** Phát triển hệ thống đánh giá tín dụng tự động hỗ trợ ngân hàng ra quyết định nhanh chóng.
- Sử dụng thêm các model dự đoán về các khoản tin đáng tin cậy, không tin cậy dựa trên nhiều thông tin hơn trong tương lại

## Kết luận
Từ hai phân tích trên, có thể thấy rằng lịch sử tín dụng và thói quen thanh toán của khách hàng có ảnh hưởng rõ rệt đến trạng thái khoản vay hiện tại. Khách hàng có lịch sử trả chậm hoặc từng có nợ xấu không chỉ có tỷ lệ nợ xấu cao hơn mà còn gặp khó khăn hơn trong việc tiếp cận tín dụng mới. Điều này cho thấy tầm quan trọng của việc kiểm soát rủi ro tín dụng thông qua đánh giá lịch sử vay nợ, đồng thời nhấn mạnh nhu cầu về các chính sách quản lý tín dụng phù hợp nhằm giảm thiểu rủi ro và cải thiện chất lượng danh mục cho vay.
