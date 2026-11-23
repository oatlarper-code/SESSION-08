# 5.Yêu cầu đầu ra chi tiết
1. Bước 1.Thiết kế giải pháp(I/O)
- Input: Dữ liệu đầu vào định dạng biến (Cửa hàng:[TÊN_CỬA_HÀNG], Quy trình:[LOAI_QUY_TRINH] (Custom Instructions, Prompt Library, Prompt Injection), Nội dung:[NỘI_DUNG_ĐẦU_VÀO], Phản hồi:[NGỮ_CẢNH_BỔ_SUNG])
- Output: Trạng thái dữ liệu cảnh báo lỗi, tóm tắt nghiệp vụ, kết quả xử lý và hành động đề xuất. Các loại quy trình: Custom Instructions(Quy định chuẩn hóa của cửa hàng), Prompt Library(prompt mẫu hoàn chỉnh có biến), Prompt Injection(chỉ ra những đoạn nghi ngờ tấn công)
2. Bước 2. Viết prompt và chạy thử
- Prompt:
  - Bạn là chuyên viên quản trị viên AI cho cửa hàng. Nhiệm vụ xác định rõ các thông tin cần đưa vào và cấu trúc kết quả mong muốn.
  - Dữ liệu đầu vào:
    - Cửa hàng:[TÊN_CỬA_HÀNG]
    - Quy trình:[LOAI_QUY_TRINH] (Custom Instructions, Prompt Library, Prompt Injection)
    - Nội dung:[NỘI_DUNG_ĐẦU_VÀO]
    - Phản hồi:[NGỮ_CẢNH_BỔ_SUNG]
  - Quy tắc xử lý:
    - Nếu [LOAI_QUY_TRINH] bị trống thì không được chọn bừa mà phải để trạng thái là "INVALID"
    - Nếu [NỘI_DUNG_ĐẦU_VÀO] bị trống thì không được chọn bừa mà phải để trạng thái là "Empty"
    - Nếu [NGỮ_CẢNH_BỔ_SUNG] bị trống thì vẫn xử lý từng bước và để là chưa rõ ngữ cảnh bổ sung
  - Rằng buộc: Tạo ra một ví dụ về nội dung của cửa hàng và đưa ra các thông tin liên quan đến dữ liệu đầu vào
  - Đầu và mong muốn:
    1.Trạng thái dữ liệu cảnh báo lỗi
    - Trạng thái: ".."
    - Ghi chú kiểm tra: ".."
    2.Tóm tắt nghiệp vụ
    - ..
    3. Kết quả xử lý 
    - ..
    4. Đề xuất
    - ..
- Phản hồi của AI:
```
Dữ liệu đầu vào giả định (Ví dụ minh họa)
Cửa hàng: Tiệm Trà Sữa Mây Trắng

Quy trình: Prompt Library

Nội dung: Khách hàng nhắn tin phàn nàn: "Trà sữa giao tới bị đổ mất một nửa, trân châu thì cứng như đá. Làm ăn kiểu gì vậy?"

Phản hồi: (Để trống)

Kết quả thực thi theo cấu trúc
1. Trạng thái dữ liệu cảnh báo lỗi

Trạng thái: "Valid (Thiếu ngữ cảnh bổ sung)"

Ghi chú kiểm tra:

[LOAI_QUY_TRINH] hợp lệ (Prompt Library).

[NỘI_DUNG_ĐẦU_VÀO] có dữ liệu hợp lệ.

[NGỮ_CẢNH_BỔ_SUNG] bị trống — tiến hành xử lý theo quy tắc mặc định ở trạng thái chưa rõ ngữ cảnh bổ sung (chưa rõ đơn đặt qua ứng dụng giao hàng bên thứ ba hay shipper nội bộ, chưa có hình ảnh xác thực).

2. Tóm tắt nghiệp vụ

Phân loại tình huống: Xử lý khiếu nại khách hàng về chất lượng sản phẩm (trân châu cứng) và lỗi vận chuyển (đổ nước).

Mục tiêu: Xoa dịu cảm xúc tiêu cực của khách hàng ngay lập tức, xin lỗi chân thành, thu thập thông tin xác minh (ảnh chụp/mã đơn) và đưa ra phương án đền bù phù hợp để giữ chân khách.

3. Kết quả xử lý
Dựa trên quy trình Prompt Library, hệ thống trích xuất mẫu phản hồi tiêu chuẩn dành cho tình huống Khiếu nại chất lượng & Vận chuyển:

"Dạ Tiệm Trà Sữa Mây Trắng thành thật xin lỗi bạn vì trải nghiệm không trọn vẹn này ạ! Việc ly nước bị đổ và trân châu chưa đạt chuẩn là thiếu sót rất lớn của tiệm và đơn vị vận chuyển.

Để tiệm có thể hỗ trợ đổi lại ly mới hoặc hoàn tiền ngay cho mình, bạn vui lòng gửi giúp tiệm hình ảnh ly nước hiện tại kèm mã đơn hàng nhé. Tiệm sẽ xử lý cho bạn trong 5 phút ạ. Mong bạn thông cảm cho sự bất tiện này!"

4. Đề xuất

Bổ sung ngữ cảnh đầu vào: Cần cập nhật thêm dữ liệu ở trường [NGỮ_CẢNH_BỔ_SUNG] (ví dụ: Đơn đặt qua ShopeeFood/GrabFood hay đặt trực tiếp tại fanpage; chính sách hoàn tiền hiện hành của cửa hàng) để AI tự động điều hướng khách liên hệ đúng bộ phận CSKH của sàn hoặc điều shipper nội bộ đi đổi trả.

Tối ưu Prompt Library: Nên chia nhỏ mẫu phản hồi thành 2 nhánh riêng biệt: (1) Lỗi hoàn toàn do quán (trân châu cứng -> quán chịu 100% chi phí đổi mới) và (2) Lỗi do đối tác vận chuyển (đổ nước -> hướng dẫn khách bấm khiếu nại trên app để được hoàn tiền nhanh nhất).
```