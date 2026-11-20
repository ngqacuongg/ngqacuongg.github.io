# CLAUDE.md

Repo này là **trang cá nhân (portfolio, digital CV)** của Nguyễn Quốc Anh Cường, phục vụ qua GitHub Pages ở gốc tên miền: https://ngqacuongg.github.io/

- Repo công khai `ngqacuongg/ngqacuongg.github.io`, nhánh `main`. Mọi file push lên đều công khai.
- Trước 20/11/2026 portfolio nằm trong repo thực hành `hoc-claude-code` (thư mục `portfolio/`). Địa chỉ cũ giờ chỉ còn trang chuyển hướng về đây.
- File `.nojekyll` để Pages phục vụ file y nguyên, không chạy Jekyll.
- `gh` ở `~/.local/bin/gh`.

## Cấu trúc và ghi chú

- Một file `index.html` duy nhất, cùng bảng màu với `todo/`. Chạy bằng `open index.html`. Khi push lên nhánh `main` sẽ lên https://ngqacuongg.github.io/
- Giao diện lấy cảm hứng bố cục (không chép chữ hay thương hiệu) từ phongtdt-portfolio.cloud mà người dùng thích: nền tối là mặc định (`portfolio-theme` trống thì dùng `dark`), lưới chấm mờ, tiêu đề mở đầu 3 dòng chữ in hoa đậm (`UI.mega`, dòng giữa màu nhấn), nhãn in hoa giãn chữ, ô số liệu (`ME.highlights`) và 3 thẻ vai trò (`ME.roles`). Màu nhấn xanh rêu và mạng nơ-ron là dấu ấn riêng, giữ nguyên.
- Nội dung lấy từ CV (`~/Downloads/[NTU Application]/NQACuong_CV.pdf`) và các artifact trên claude.ai. Toàn bộ nằm trong object `ME` ở đầu thẻ `<script>`; mỗi đoạn chữ viết dạng `["tiếng Việt", "English"]`. Thứ tự chương nằm trong `CHAPTERS`.
- Chương "Mình là ai" (`ME.bioLead`, `ME.story`, `ME.goal`) viết lại từ bản tự thuật `~/Downloads/[NTU Application]/NQACuong_Autobiography_and_Research_Plan.pdf`. Không nêu tên trường hay giáo sư đang nộp hồ sơ lên trang.
- Chương "Hành trình" là timeline **dọc** (`ME.journey`, hàm `journeyHTML`): học vấn, thực tập (BV Bệnh Nhiệt đới, ĐH Y Dược, Touching Soul Center 07–10/2026 với vai trò Undergraduate Psychology Intern), Cuộc thi Sáng tạo Tế bào gốc 2025, và hai mốc trợ lý nghiên cứu đang làm song song: BV Bệnh Nhiệt đới (từ 06/2026, ngay sau thực tập ở ĐH Y Dược) và BV Quân y 175 (từ 08/2026). Mốc có `now: true` mở sẵn. **3 poster về vi khuẩn kháng carbapenem thuộc mốc RA BV Bệnh Nhiệt đới**, không phải đợt thực tập vi sinh 2025. Hoạt động ngoại khoá nằm ở `ME.alongside`.
  - Bấm một mốc mở ra sản phẩm của mốc đó (`items`): poster (`{ p: "poster", i }` trỏ vào `ME.posters`), brochure Dinh dưỡng (`{ p: "brochure" }`, mở sách lật), hoặc chứng nhận (`{ p: "cert", … }`). Người dùng muốn poster và dự án nằm trong timeline, nên chương Nghiên cứu không còn lưới "Dự án & poster" riêng.
  - Ảnh chứng nhận ở `img/certs/` (ảnh lớn + `-sm`), dựng từ PDF bằng PDFKit. **Chứng nhận ĐH Y Dược đã che dòng ngày sinh**; chứng nhận mới phải soát ngày sinh, số giấy tờ tuỳ thân trước khi đưa lên.
  - Giải ở Cuộc thi Tế bào gốc: **Giải Khuyến khích – Top 18 thuộc đội TEISC (poster CAR-T)**, người dùng đã xác nhận. Poster hiPSC là poster cá nhân, không có giải. Tổng cộng 2 giải poster (thêm giải Bình chọn nhiều nhất).
- Chương "Nghiên cứu": 4 câu hỏi (`ME.interests`) và các nghiên cứu đang tham gia (`ME.studies`). Dữ liệu `ME.nutrition` và `ME.posters` vẫn dùng cho các thẻ trong timeline (hàm `projectCard`).
  - Brochure Dinh dưỡng mở cửa sổ sách lật (`openBook`, `bookHTML`, `flipBook`): hai ảnh mặt giấy được cắt bằng CSS thành 8 trang theo `ME.nutrition.pages`; lật quá trang cuối thì hiện cả hai mặt. Ảnh xuất từ Canva của người dùng; **không dán link `canva.link` lên trang vì đó là link chỉnh sửa**.
  - Poster CHRO và hiPSC lấy từ ảnh người dùng dán vào chat (1414 × 2000), vì Canva không cho xuất thiết kế của tài khoản khác.
- Chương "Dạy & chia sẻ" là tài liệu gia sư Sinh học lớp 10 cho một học sinh trường International German School (`ME.tutor`, hàm `tutorHTML`). Nguồn ở `~/Downloads/[TS]/Crystal - IGS/`; **không đưa tên học sinh lên trang** (tên thư mục và phiếu gốc có tên học sinh).
  - Xếp theo 13 stage K (Lernplan của trường), mỗi stage mở ra theo thứ tự Slides → Cheat sheet → Video → Phiếu bài tập. Tài liệu dùng chung nhiều stage ghi `ks: [từ, đến]`. Stage K có 3 phiếu: K1 = AB1–3 … K13 = AB37–39 (dòng "Topic block N" trong phiếu xác nhận điều này).
  - Mỗi K có một dòng "Tương tác" trỏ tới visual tương tác: `lessons/genetics-k1-k4.html` và `genetics-k5-k13.html`, là bản sao của hai artifact bài học trên claude.ai (Genetics Stage 1, Stage 2), mở thẳng phần `#kN`. Khi người dùng sửa artifact, đọc lại artifact rồi chép lại; bản sao đã được thêm link "← Portfolio", đoạn đồng bộ sáng/tối theo `portfolio-theme`, `scroll-margin-top` và đoạn cuộn tới `#kN` sau khi tải. **Bỏ khối "Kế hoạch … trước bài kiểm tra" có ngày cụ thể** (lịch riêng của học sinh) ở bản công khai.
  - 39 phiếu bài tập là bản người dùng dịch từ phiếu tiếng Đức của giáo viên, nên **chỉ hiện tên, không cho tải** (người dùng đã chọn vậy).
  - Slides, cheat sheet và video nằm trong `media/`: slides là PDF xuất từ .pptx bằng PowerPoint, cheat sheet là PDF xuất từ .docx bằng Word (cả hai qua `osascript`, nên đặt `with timeout of 300 seconds` vì app khởi động chậm). Mỗi bộ K1–K4, K5–K7, K8–K10, K11–K13 có một slides, hai cheat sheet (Anh–Việt, Anh–Đức) và một video `genetics-kX-kY.mp4` kèm ảnh `-poster.jpg`. Video mở trong cửa sổ `#vidDlg`.
- Mục Liên hệ và CV chỉ dùng email công việc `cuong.nguyen.220214@alumni.fulbright.edu.vn` (`ME.emails`). **Không đưa email cá nhân lên**, người dùng đã yêu cầu bỏ.
- CV rút gọn công khai: `cv/index.html` (tiếng Anh, khổ A4) và `cv/NguyenQuocAnhCuong_CV.pdf`, mở từ nút "Xem CV" trên thanh điều hướng và nút ở mục Liên hệ. Cố ý **không có số điện thoại, GPA, người tham chiếu**. Sửa CV thì sửa HTML rồi xuất lại PDF (máy không có Chrome, dùng WebKit):
  `swiftc -O -o /tmp/html2pdf cv/html2pdf.swift && /tmp/html2pdf "$PWD/cv/index.html" "$PWD/cv/NguyenQuocAnhCuong_CV.pdf"`
  Khi in, WebKit bỏ qua `break-after: avoid`, nên mục Poster được ép sang trang 2 bằng lớp `page-break`; bố cục điện thoại chỉ áp dụng cho `@media screen`. Xuất xong phải xem lại số trang (đang là 2).
- Ngoại lệ duy nhất về thư viện ngoài: font Lora và Be Vietnam Pro từ Google Fonts, vì font hệ thống kiểu Iowan/Georgia hiện sai dấu chữ ư, ơ.
- Trang công khai: không đưa số điện thoại, GPA hay liên hệ người tham chiếu trong CV lên nếu người dùng chưa đồng ý. Link artifact claude.ai mặc định là riêng tư, người xem chỉ mở được khi người dùng đã bật chia sẻ.
- Chương "Học code" (`ME.school`, `ME.build`) gọi GitHub API công khai lúc mở trang (`loadGitHub`) để lấy thời gian push của từng repo và 6 commit mới nhất của repo này, nên push xong là trang tự mới. Kết quả lưu tạm 30 phút ở khoá `portfolio-gh` vì API giới hạn 60 lần/giờ cho mỗi người xem. Repo môn học hay dự án mới thì thêm tay vào `ME.school` / `ME.build`.
- `localStorage`: khoá `portfolio-theme` (sáng/tối), `portfolio-lang` (vi/en) và `portfolio-gh` (bộ đệm GitHub).

## Cách làm việc với người dùng

- Trả lời bằng **tiếng Việt**. Code, tên file và commit message có thể dùng tiếng Anh.
- Người dùng đang học, nên khi làm việc hãy giải thích ngắn gọn *vì sao* chọn cách làm đó, không chỉ đưa kết quả.
- Trước khi đưa tài liệu mới lên (chứng nhận, poster, video), soát thông tin riêng tư: ngày sinh, số điện thoại, tên học sinh, lịch học có ngày cụ thể.
