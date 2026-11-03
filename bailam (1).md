# **Yêu cầu đầu ra**

## **Phần 1. Phân tích**

-   So sánh sự khác biệt về lưu trữ trạng thái giữa Incognito Mode (tạm thời trên RAM) và Dedicated Profile (lâu dài trên ổ cứng).
    
| Tiêu chí | Incognito Mode (Chế độ ẩn danh) | Dedicated Profile (Hồ sơ riêng) |
| :--- | :--- | :--- |
| **Vị trí & Cơ chế lưu trữ** | **Tạm thời trên RAM**: Mọi dữ liệu (Cookie, Cache, Session) bị xóa sạch ngay khi đóng tất cả cửa sổ ẩn danh. | **Lâu dài trên ổ cứng (Disk Drive)**: Lưu trữ và phân tách riêng biệt cấu hình, Cookie, Session và Lịch sử duyệt web cho từng Profile. |
| **Độ bền dữ liệu (Persistence)** | **Không lâu dài**: Mỗi lần mở lại là một phiên mới hoàn toàn, phải đăng nhập lại từ đầu. | **Dài hạn**: Duy trì trạng thái đăng nhập (Keep Login) qua các lần đóng/mở trình duyệt hoặc khởi động lại máy. |
| **Số lượng phiên đồng thời** | **Giới hạn**: Tất cả các cửa sổ ẩn danh mở cùng lúc đều dùng chung 1 tập Cookie/Session. | **Không giới hạn**: Cho phép mở song song nhiều Profile cùng lúc, mỗi Profile có môi trường. |
| **Tính ứng dụng với Quản trị viên** | Phù hợp để kiểm thử nhanh, thao tác tạm thời hoặc đăng nhập tài khoản trên máy lạ. | Phù hợp để làm việc cố định hàng ngày với nhiều bộ tài khoản (Personal, Work, Sandbox) mà không bị xung đột phiên. |

## **Phần 2. Triển khai**

-   Mô tả quy trình tạo và đồng bộ hóa Cloud Sync để bảo vệ Bookmark khi đổi máy tính.
**Giai đoạn 1: Thiết lập & Đăng nhập Profile**

1.  Mở trình duyệt $\rightarrow$ Nhấp biểu tượng Avatar góc trên bên phải $\rightarrow$ Chọn Thêm Add).

2.  Chọn Đăng nhập (Sign in) bằng tài khoản Google/Microsoft tương ứng.

**Giai đoạn 2: Bật Cloud Sync**

1.  Khi có hộp thoại xác nhận hiện ra, chọn Đồng ý, tôi tham gia (Yes, I'm in).
    
2.  Vào cài đặt  $\rightarrow$  Đồng bộ hóa  $\rightarrow$  Quản lý nội dung đồng bộ  $\rightarrow$ Đảm bảo mục Dấu trang (Bookmarks) đang BẬT.

**Giai đoạn 3: Tổ chức Bookmark**

1.  Nhấn `Ctrl + Shift + B` để hiện thanh Bookmark.
        
    
2.  Nhấn `Ctrl + Shift + O` để tạo cây thư mục khoa học và lưu sẵn các trang quan trọng (GitHub, Canvas LMS, Portal).

    

**Giai đoạn 4: Khôi phục trên máy tính mới**

1.  Mở trình duyệt trên máy mới $\rightarrow$ Nhấp biểu tượng Avatar  $\rightarrow$ Chọn Đăng nhập.
      
2.  Đăng nhập đúng tài khoản trên và bấm Bật đồng bộ  $\rightarrow$ Toàn bộ Bookmark sẽ tự động tải về đầy đủ sau vài giây.

## **Phần 3. Kiểm thử**

-   Giả định làm việc trên máy tính công cộng, hãy đề xuất quy tắc sử dụng Guest Profile để bảo mật.

### Quy tắc an toàn khi sử dụng Guest Profile

1.  **Tuyệt đối không đăng nhập tài khoản trình duyệt (Browser Sync)**
    
    -   Guest Profile được thiết kế cho các phiên làm việc vãng lai. Chỉ đăng nhập vào các dịch vụ web cần thiết (Gmail, Portal...), không đăng nhập tài khoản Google/Microsoft vào trình duyệt để bật đồng bộ.
        
2.  **Không lưu thông tin xác thực và tài khoản**
    
    -   Nếu trình duyệt hiển thị hộp thoại "Lưu mật khẩu?" (Save Password?) hoặc Tự động điền (Autofill), chọn không bao giờ (Never).
        
    -   Không tích chọn vào ô _"Ghi nhớ đăng nhập"_ (Remember me / Keep me signed in) trên các trang web.
        
3.  **Không tải xuống hoặc lưu tài liệu nhạy cảm vào ổ cứng**
    
    -   Hạn chế tối đa việc tải file về thư mục `Downloads` hoặc `Desktop` của máy công cộng. Nếu bắt buộc phải tải, hãy xóa vĩnh viễn (`Shift + Delete`) ngay sau khi hoàn thành công việc.
        
4.  **Luôn thoát chủ động và đóng toàn bộ cửa sổ**
    
    -   Đăng xuất (Log out) khỏi tất cả các trang web dịch vụ trước khi kết thúc làm việc.
        
    -   Đóng toàn bộ cửa sổ Guest Profile để hệ thống tự động kích hoạt cơ chế xóa sạch Cookie, Cache và Lịch sử duyệt web.

