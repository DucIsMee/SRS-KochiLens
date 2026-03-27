# KOCHI LENS — SOFTWARE REQUIREMENTS SPECIFICATION (SRS)

# PHẦN 1: MÔ HÌNH HÓA QUY TRÌNH (BUSINESS FLOW)

## 1.1. Sơ đồ Use Case — Quản lý Sản phẩm (PIM)

Mô tả các Actor và trường hợp sử dụng liên quan đến phân hệ Quản lý Sản phẩm.

### 1.1.1. Danh sách Actor

| Actor | Vai trò | Mô tả |
|---|---|---|
| Admin | Quản trị viên | Quản lý toàn bộ danh mục, sản phẩm, biến thể, giá bán và tồn kho hệ thống. |
| Customer | Khách hàng (B2C/B2B/Guest) | Tìm kiếm, xem chi tiết sản phẩm, chọn biến thể và thêm vào giỏ hàng. |
| Warehouse Staff | Nhân viên kho | Cập nhật số lượng tồn kho sau nhập hàng hoặc sau khi giao hàng thành công. |

### 1.1.2. Use Case — Admin (Quản lý sản phẩm)

| STT | Use Case | Mô tả |
|---|---|---|
| UC-A01 | Thêm sản phẩm mới | Admin nhập thông tin sản phẩm: tên, mô tả, danh mục, hình ảnh, SKU, barcode, giá bán, thuế VAT. |
| UC-A02 | Quản lý biến thể sản phẩm | Admin tạo và gán biến thể (màu sắc, kích thước) cho từng sản phẩm; cấu hình giá và SKU riêng cho từng biến thể. |
| UC-A03 | Cập nhật thông tin sản phẩm | Admin chỉnh sửa mô tả, giá bán, hình ảnh, trạng thái hiển thị (Published / Draft / Archived). |
| UC-A04 | Quản lý danh mục | Admin tạo, sửa, xóa danh mục sản phẩm; gán sản phẩm vào một hoặc nhiều danh mục. |
| UC-A05 | Thiết lập giá và thuế | Admin cấu hình giá bán lẻ, giá bán sỉ (B2B), phần trăm thuế VAT áp dụng. |
| UC-A06 | Xem báo cáo tồn kho | Admin xem báo cáo tổng hợp tồn kho theo sản phẩm, biến thể, kho. |

### 1.1.3. Use Case — Customer (Xem và chọn sản phẩm)

| STT | Use Case | Mô tả |
|---|---|---|
| UC-C01 | Tìm kiếm sản phẩm | Khách hàng tìm kiếm theo từ khóa, lọc theo danh mục, khoảng giá, hãng sản xuất. |
| UC-C02 | Xem chi tiết sản phẩm | Khách hàng xem hình ảnh, mô tả kỹ thuật, giá bán, tình trạng tồn kho real-time. |
| UC-C03 | Chọn biến thể | Khách hàng chọn màu sắc, kích thước; hệ thống tự động cập nhật giá và kiểm tra tồn kho biến thể đó. |
| UC-C04 | Thêm vào giỏ hàng | Khách hàng thêm sản phẩm/biến thể vào giỏ hàng; cảnh báo nếu tồn kho không đủ. |
| UC-C05 | Xem sản phẩm liên quan | Hệ thống gợi ý sản phẩm tương tự hoặc thường được mua cùng. |

### 1.1.4. Use Case — Warehouse Staff (Quản lý tồn kho)

| STT | Use Case | Mô tả |
|---|---|---|
| UC-W01 | Cập nhật nhập kho | Nhân viên kho nhập số lượng hàng nhận được, hệ thống tự động tăng tồn kho. |
| UC-W02 | Kiểm kê định kỳ | Nhân viên kho thực hiện kiểm kê, điều chỉnh chênh lệch giữa tồn kho thực tế và hệ thống. |
| UC-W03 | Xem cảnh báo tồn kho thấp | Hệ thống hiển thị danh sách sản phẩm/biến thể dưới ngưỡng tồn kho tối thiểu. |

---

## 1.2. Sơ đồ Activity — Luồng đặt hàng (Chọn sản phẩm → Thanh toán thành công)

Mô tả chi tiết từng bước trong luồng đặt hàng của khách hàng trên website Kochi Lens.

| Bước | Hoạt động | Actor | Mô tả / Điều kiện |
|---|---|---|---|
| 1 | Tìm kiếm / Duyệt sản phẩm | Customer | Khách hàng truy cập website, sử dụng thanh tìm kiếm hoặc duyệt theo danh mục để tìm thiết bị ảnh phù hợp. |
| 2 | Xem chi tiết sản phẩm | Customer | Hệ thống hiển thị đầy đủ: tên, hình ảnh, thông số kỹ thuật, giá, tình trạng kho (real-time). |
| 3 | Chọn biến thể | Customer | Khách hàng chọn màu sắc / kích thước. Hệ thống kiểm tra tồn kho biến thể; nếu hết hàng → hiển thị "Hết hàng". |
| 4 | Thêm vào giỏ hàng | Customer + System | Hệ thống giữ tạm số lượng trong giỏ. Nếu số lượng yêu cầu > tồn kho → cảnh báo và giới hạn số lượng tối đa. |
| 5 | Xem lại giỏ hàng | Customer | Khách hàng kiểm tra danh sách sản phẩm, số lượng, tạm tính; có thể tăng/giảm/xóa sản phẩm. |
| 6 | Nhập thông tin giao hàng | Customer | Khách hàng điền tên, số điện thoại, địa chỉ giao hàng (Guest) hoặc chọn địa chỉ đã lưu (Member). |
| 7 | Chọn phương thức vận chuyển | Customer + System | Hệ thống tính phí ship theo địa chỉ giao hàng và trọng lượng đơn hàng. |
| 8 | Áp dụng mã giảm giá (tùy chọn) | Customer | Khách hàng nhập coupon code; hệ thống kiểm tra tính hợp lệ và áp dụng chiết khấu. |
| 9 | Xem tóm tắt đơn hàng | Customer + System | Hệ thống hiển thị tổng cộng: sản phẩm + phí ship + thuế VAT - giảm giá = Tổng thanh toán. |
| 10 | Chọn phương thức thanh toán | Customer | Khách hàng chọn VNPay / Momo / COD / Chuyển khoản. |
| 11 | Xác nhận đặt hàng | Customer | Khách hàng nhấn "Đặt hàng". Hệ thống tạo Draft Order, trừ tạm tồn kho. |
| 12 | Thực hiện thanh toán online | Customer + Payment Gateway | Khách hàng được chuyển sang cổng thanh toán (VNPay/Momo). Nhập OTP và xác nhận. |
| 13 | Xử lý kết quả thanh toán | System | **[Thành công]** → Xác nhận đơn hàng (Sale Order), trừ tồn kho chính thức, gửi email xác nhận. **[Thất bại]** → Hoàn tồn kho tạm, thông báo lỗi, cho phép thử lại. |
| 14 | Gửi thông báo xác nhận | System | Hệ thống gửi email / SMS chứa mã đơn hàng, danh sách sản phẩm, tổng tiền, thời gian giao hàng dự kiến. |

---

# PHẦN 2: ĐẶC TẢ CHỨC NĂNG (FUNCTIONAL REQUIREMENTS)

Các yêu cầu chức năng được viết theo chuẩn User Story: _"Là một [actor], tôi muốn [hành động] để [mục tiêu/lợi ích]."_

---

## 2.1. Nhóm chức năng: Quản lý Danh mục & Sản phẩm (Admin)

### US-001: Thêm sản phẩm mới

| | |
|---|---|
| **User Story** | Là một Admin, tôi muốn thêm sản phẩm mới vào hệ thống để khách hàng có thể xem và đặt mua sản phẩm trên website. |
| **Tiêu chí chấp nhận** | (1) Admin điền đầy đủ: tên sản phẩm, mô tả, danh mục, SKU, barcode, giá bán, % VAT và ít nhất 1 hình ảnh. (2) Hệ thống kiểm tra SKU không trùng lặp. (3) Sản phẩm lưu thành công với trạng thái `DRAFT` trước khi published. (4) Admin có thể publish hoặc giữ draft. |
| **Độ ưu tiên** | 🔴 Must Have |

### US-002: Quản lý biến thể sản phẩm

| | |
|---|---|
| **User Story** | Là một Admin, tôi muốn tạo biến thể (màu sắc, kích thước) cho từng sản phẩm để mỗi biến thể có SKU, giá và tồn kho riêng biệt. |
| **Tiêu chí chấp nhận** | (1) Admin có thể tạo các thuộc tính biến thể (màu, size). (2) Hệ thống tự động gợi ý tổ hợp hoặc cho phép tạo thủ công. (3) Mỗi tổ hợp biến thể có SKU độc lập, giá riêng (tùy chọn), số tồn kho riêng. (4) Hình ảnh có thể gán riêng theo màu sắc. |
| **Độ ưu tiên** | 🔴 Must Have |

### US-003: Cập nhật giá và thuế VAT

| | |
|---|---|
| **User Story** | Là một Admin, tôi muốn thiết lập giá bán lẻ, giá B2B và tỷ lệ thuế VAT cho từng sản phẩm để hệ thống tính toán đúng tổng thanh toán khi khách đặt hàng. |
| **Tiêu chí chấp nhận** | (1) Admin nhập giá bán chưa VAT và chọn mức thuế (0%, 5%, 10%). (2) Hệ thống tự động tính giá có VAT để hiển thị. (3) Có thể thiết lập giá B2B riêng cho khách thành viên doanh nghiệp. (4) Lịch sử thay đổi giá được lưu lại với timestamp. |
| **Độ ưu tiên** | 🔴 Must Have |

---

## 2.2. Nhóm chức năng: Tồn kho Real-time

### US-004: Hiển thị tồn kho real-time cho khách hàng

| | |
|---|---|
| **User Story** | Là một Khách hàng, tôi muốn thấy ngay tình trạng tồn kho khi chọn biến thể sản phẩm để tôi biết sản phẩm có sẵn để mua hay không. |
| **Tiêu chí chấp nhận** | (1) Trang chi tiết sản phẩm hiển thị trạng thái: "Còn hàng", "Sắp hết" (< 5 đơn vị), "Hết hàng". (2) Khi chọn biến thể, tồn kho cập nhật ngay không cần tải lại trang. (3) Nếu hết hàng, nút "Thêm vào giỏ" bị vô hiệu hóa. (4) Dữ liệu đồng bộ trong vòng 5 giây sau mỗi đơn hàng được xác nhận. |
| **Độ ưu tiên** | 🔴 Must Have |

### US-005: Cảnh báo tồn kho thấp cho Warehouse Staff

| | |
|---|---|
| **User Story** | Là một Nhân viên kho, tôi muốn nhận thông báo khi một sản phẩm/biến thể đạt ngưỡng tồn kho tối thiểu để tôi có thể đặt hàng nhập kịp thời. |
| **Tiêu chí chấp nhận** | (1) Admin có thể thiết lập ngưỡng tồn kho tối thiểu cho từng SKU. (2) Khi tồn kho chạm ngưỡng, hệ thống gửi email/notification đến Warehouse Staff. (3) Dashboard kho hiển thị danh sách sản phẩm cần nhập hàng. (4) Cảnh báo tự động xóa khi tồn kho được cập nhật vượt ngưỡng. |
| **Độ ưu tiên** | 🟡 Should Have |

---

## 2.3. Nhóm chức năng: Trải nghiệm khách hàng

### US-006: Tìm kiếm và lọc sản phẩm

| | |
|---|---|
| **User Story** | Là một Khách hàng, tôi muốn tìm kiếm sản phẩm theo từ khóa và lọc theo danh mục, khoảng giá, hãng sản xuất để nhanh chóng tìm được thiết bị phù hợp nhu cầu. |
| **Tiêu chí chấp nhận** | (1) Thanh tìm kiếm hỗ trợ full-text search theo tên, mô tả, SKU. (2) Bộ lọc gồm: danh mục, khoảng giá (slider), hãng sản xuất, tình trạng kho. (3) Kết quả trả về trong < 2 giây với phân trang (20 sản phẩm/trang). (4) Có thể sắp xếp theo: giá tăng/giảm, mới nhất, bán chạy nhất. |
| **Độ ưu tiên** | 🔴 Must Have |

### US-007: Email xác nhận đặt hàng

| | |
|---|---|
| **User Story** | Là một Khách hàng, tôi muốn nhận được email xác nhận đơn hàng ngay sau khi thanh toán thành công để tôi an tâm về giao dịch và theo dõi đơn hàng. |
| **Tiêu chí chấp nhận** | (1) Email gửi trong vòng 2 phút sau khi thanh toán thành công. (2) Email chứa: mã đơn hàng, danh sách sản phẩm, số lượng, đơn giá, tổng tiền, địa chỉ giao hàng, thời gian giao hàng dự kiến. (3) Email có link theo dõi trạng thái đơn hàng. (4) Hỗ trợ cả Guest (dùng email nhập khi đặt hàng) và Member. |
| **Độ ưu tiên** | 🔴 Must Have |

---

# PHẦN 3: ĐẶC TẢ DỮ LIỆU (DATA SCHEMA)

## 3.1. Partner (Khách hàng)

Bảng lưu trữ thông tin tất cả các loại khách hàng: Khách vãng lai (Guest), Khách B2C và Khách B2B.

| Tên trường | Kiểu dữ liệu | Bắt buộc | Mô tả |
|---|---|---|---|
| `partner_id` | UUID / INT | ✅ | Khóa chính, định danh duy nhất cho mỗi khách hàng. |
| `partner_type` | ENUM | ✅ | Loại khách hàng: `GUEST` \| `B2C` \| `B2B`. |
| `full_name` | VARCHAR(255) | ✅ | Tên đầy đủ cá nhân hoặc tên người liên hệ (B2B). |
| `company_name` | VARCHAR(255) | — | Tên công ty (bắt buộc nếu `partner_type = B2B`). |
| `tax_code` (MST) | VARCHAR(20) | — | Mã số thuế doanh nghiệp (bắt buộc nếu xuất hóa đơn VAT B2B). |
| `email` | VARCHAR(255) | ✅ | Địa chỉ email, dùng để gửi xác nhận đơn hàng. |
| `phone` | VARCHAR(20) | ✅ | Số điện thoại liên lạc. |
| `password_hash` | VARCHAR(512) | — | Mật khẩu đã băm (NULL nếu là Guest). |
| `loyalty_tier` | ENUM | — | Hạng thành viên: `STANDARD` \| `SILVER` \| `GOLD` \| `PLATINUM`. |
| `created_at` | TIMESTAMP | ✅ | Thời điểm tạo tài khoản. |
| `is_active` | BOOLEAN | ✅ | Trạng thái tài khoản: TRUE = hoạt động, FALSE = bị khóa. |

### 3.1.1. PartnerAddress (Địa chỉ giao hàng)

| Tên trường | Kiểu dữ liệu | Bắt buộc | Mô tả |
|---|---|---|---|
| `address_id` | UUID / INT | ✅ | Khóa chính. |
| `partner_id` | UUID / INT | ✅ | Khóa ngoại tham chiếu bảng Partner. |
| `label` | VARCHAR(100) | — | Nhãn địa chỉ: Nhà riêng, Văn phòng, v.v. |
| `recipient_name` | VARCHAR(255) | ✅ | Tên người nhận tại địa chỉ này. |
| `phone` | VARCHAR(20) | ✅ | Số điện thoại liên lạc khi giao hàng. |
| `address_line1` | VARCHAR(500) | ✅ | Số nhà, tên đường, tòa nhà. |
| `address_line2` | VARCHAR(500) | — | Tầng, căn hộ (nếu có). |
| `ward` | VARCHAR(100) | ✅ | Phường / Xã. |
| `district` | VARCHAR(100) | ✅ | Quận / Huyện. |
| `province` | VARCHAR(100) | ✅ | Tỉnh / Thành phố. |
| `is_default` | BOOLEAN | ✅ | TRUE nếu là địa chỉ giao hàng mặc định. |

---

## 3.2. Product (Sản phẩm)

Bảng lưu thông tin sản phẩm cha (template). Mỗi sản phẩm có thể có nhiều biến thể (ProductVariant).

| Tên trường | Kiểu dữ liệu | Bắt buộc | Mô tả |
|---|---|---|---|
| `product_id` | UUID / INT | ✅ | Khóa chính định danh sản phẩm. |
| `product_name` | VARCHAR(500) | ✅ | Tên sản phẩm hiển thị trên website. |
| `slug` | VARCHAR(500) | ✅ | URL-friendly name, dùng cho SEO (unique). |
| `category_id` | INT | ✅ | Khóa ngoại tham chiếu bảng Category. |
| `brand_id` | INT | — | Khóa ngoại tham chiếu bảng Brand (hãng sản xuất). |
| `description` | TEXT | — | Mô tả chi tiết sản phẩm (hỗ trợ HTML/rich text). |
| `base_price` | DECIMAL(18,2) | ✅ | Giá bán lẻ chưa VAT (đơn vị: VND). |
| `b2b_price` | DECIMAL(18,2) | — | Giá bán sỉ cho khách B2B (nếu khác giá lẻ). |
| `vat_rate` | DECIMAL(5,2) | ✅ | Tỷ lệ thuế VAT áp dụng: 0, 5, hoặc 10 (%). |
| `status` | ENUM | ✅ | Trạng thái sản phẩm: `DRAFT` \| `PUBLISHED` \| `ARCHIVED`. |
| `is_featured` | BOOLEAN | ✅ | TRUE nếu sản phẩm được hiển thị nổi bật trang chủ. |
| `meta_title` | VARCHAR(255) | — | Tiêu đề SEO meta tag. |
| `meta_description` | VARCHAR(500) | — | Mô tả SEO meta description. |
| `created_at` | TIMESTAMP | ✅ | Thời điểm tạo sản phẩm. |
| `updated_at` | TIMESTAMP | ✅ | Thời điểm cập nhật gần nhất. |
| `created_by` | INT | ✅ | Khóa ngoại tham chiếu Admin đã tạo sản phẩm. |

### 3.2.1. ProductVariant (Biến thể sản phẩm)

| Tên trường | Kiểu dữ liệu | Bắt buộc | Mô tả |
|---|---|---|---|
| `variant_id` | UUID / INT | ✅ | Khóa chính biến thể. |
| `product_id` | UUID / INT | ✅ | Khóa ngoại tham chiếu bảng Product. |
| `sku` | VARCHAR(100) | ✅ | Mã SKU định danh duy nhất toàn hệ thống (UNIQUE). |
| `barcode` | VARCHAR(100) | — | Mã barcode / EAN-13 / QR Code. |
| `color` | VARCHAR(100) | — | Giá trị thuộc tính màu sắc (ví dụ: Đen, Trắng, Bạc). |
| `size` | VARCHAR(100) | — | Giá trị thuộc tính kích thước (ví dụ: S, M, L, XL). |
| `price_override` | DECIMAL(18,2) | — | Giá bán riêng của biến thể (NULL = dùng `base_price` của Product). |
| `stock_quantity` | INT | ✅ | Số lượng tồn kho hiện tại (>= 0). |
| `min_stock_threshold` | INT | — | Ngưỡng tồn kho tối thiểu để kích hoạt cảnh báo. |
| `weight_gram` | INT | — | Trọng lượng (gram), dùng để tính phí ship. |
| `image_url` | VARCHAR(500) | — | URL hình ảnh đặc trưng cho biến thể này. |
| `is_active` | BOOLEAN | ✅ | TRUE nếu biến thể này đang được bán. |

---

## 3.3. Order (Đơn hàng)

Bảng lưu trữ toàn bộ thông tin đơn hàng từ lúc khởi tạo đến khi hoàn tất.

| Tên trường | Kiểu dữ liệu | Bắt buộc | Mô tả |
|---|---|---|---|
| `order_id` | UUID / INT | ✅ | Khóa chính định danh đơn hàng. |
| `order_number` | VARCHAR(50) | ✅ | Số đơn hàng hiển thị (ví dụ: KL-2026-00001). UNIQUE. |
| `partner_id` | UUID / INT | — | Khóa ngoại đến Partner (NULL nếu là Guest). |
| `guest_email` | VARCHAR(255) | — | Email khách vãng lai (bắt buộc nếu `partner_id = NULL`). |
| `status` | ENUM | ✅ | Trạng thái: `DRAFT` \| `CONFIRMED` \| `PROCESSING` \| `SHIPPED` \| `DELIVERED` \| `CANCELLED` \| `REFUNDED`. |
| `payment_status` | ENUM | ✅ | Trạng thái thanh toán: `PENDING` \| `PAID` \| `FAILED` \| `REFUNDED`. |
| `payment_method` | ENUM | ✅ | Phương thức: `VNPAY` \| `MOMO` \| `COD` \| `BANK_TRANSFER`. |
| `payment_transaction_id` | VARCHAR(255) | — | Mã giao dịch từ cổng thanh toán (VNPay/Momo). |
| `shipping_address_id` | INT | — | Khóa ngoại đến PartnerAddress (nếu là Member). |
| `shipping_address_snapshot` | JSONB / TEXT | ✅ | Snapshot địa chỉ giao hàng tại thời điểm đặt hàng. |
| `subtotal` | DECIMAL(18,2) | ✅ | Tổng tiền hàng chưa VAT, chưa phí ship. |
| `shipping_fee` | DECIMAL(18,2) | ✅ | Phí vận chuyển. |
| `discount_amount` | DECIMAL(18,2) | ✅ | Tổng giảm giá áp dụng (default: 0). |
| `tax_amount` | DECIMAL(18,2) | ✅ | Tổng tiền thuế VAT. |
| `total_amount` | DECIMAL(18,2) | ✅ | Tổng thanh toán = subtotal + shipping_fee + tax_amount - discount_amount. |
| `note` | TEXT | — | Ghi chú từ khách hàng. |
| `created_at` | TIMESTAMP | ✅ | Thời điểm tạo đơn hàng. |
| `confirmed_at` | TIMESTAMP | — | Thời điểm đơn hàng được xác nhận. |
| `cancelled_at` | TIMESTAMP | — | Thời điểm đơn hàng bị hủy. |
| `cancelled_reason` | TEXT | — | Lý do hủy đơn hàng. |

### 3.3.1. Luồng trạng thái đơn hàng (Order Status Flow)

| Trạng thái | Điều kiện chuyển sang | Hành động hệ thống |
|---|---|---|
| `DRAFT` | Khách đặt hàng, chưa thanh toán | Tạm giữ tồn kho, chờ thanh toán. |
| `CONFIRMED` | Thanh toán thành công | Trừ tồn kho chính thức, gửi email xác nhận, đẩy đơn sang OMS. |
| `PROCESSING` | Kho bắt đầu xử lý | Warehouse Staff nhận đơn, bắt đầu đóng gói. |
| `SHIPPED` | Đã bàn giao cho đơn vị vận chuyển | Cập nhật mã tracking, gửi thông báo cho khách. |
| `DELIVERED` | Khách hàng đã nhận hàng | Kế toán xuất hóa đơn VAT (nếu có yêu cầu). |
| `CANCELLED` | Hủy bởi khách hoặc Admin | Hoàn tồn kho, hoàn tiền (nếu đã thanh toán). |
| `REFUNDED` | Hoàn tiền thành công | Ghi nhận refund transaction, cập nhật kế toán. |

---

## 3.4. Quan hệ giữa các bảng (Entity Relationship Summary)

| Bảng nguồn | Quan hệ | Bảng đích | Mô tả |
|---|---|---|---|
| Partner | 1 — N | PartnerAddress | Một khách hàng có nhiều địa chỉ giao hàng. |
| Partner | 1 — N | Order | Một khách hàng có thể có nhiều đơn hàng. |
| Product | 1 — N | ProductVariant | Một sản phẩm cha có nhiều biến thể. |
| ProductVariant | N — N | OrderLine | Nhiều biến thể xuất hiện trong nhiều đơn hàng (qua bảng OrderLine). |
| Order | 1 — N | OrderLine | Một đơn hàng chứa nhiều dòng sản phẩm. |
| Order | 1 — 1 | Invoice | Mỗi đơn hàng DELIVERED tương ứng 1 hóa đơn xuất VAT. |
