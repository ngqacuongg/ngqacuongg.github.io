# CLAUDE.md

Repo này là **trang cá nhân (portfolio, digital CV)** của Nguyễn Quốc Anh Cường, phục vụ qua GitHub Pages ở gốc tên miền: https://ngqacuongg.github.io/

- Repo công khai `ngqacuongg/ngqacuongg.github.io`, nhánh `main`. Mọi file push lên đều công khai.
- Trước 20/11/2026 portfolio nằm trong repo thực hành `hoc-claude-code` (thư mục `portfolio/`). Địa chỉ cũ giờ chỉ còn trang chuyển hướng về đây.
- File `.nojekyll` để Pages phục vụ file y nguyên, không chạy Jekyll.
- `gh` ở `~/.local/bin/gh`.

## Cấu trúc và ghi chú

- Một file `index.html` duy nhất. Chạy bằng `open index.html`. Khi push lên nhánh `main` sẽ lên https://ngqacuongg.github.io/
- **Giao diện "sổ tay nghiên cứu nhiều lớp giấy"** (23/11/2026). Người dùng chê bản liệt kê là "dài, không ấn tượng, giống AI"; muốn giữ chất sổ tay nhưng nghệ thuật hơn, gọn hơn, dễ dùng. Giữ đúng tinh thần này khi sửa:
  - Mặt bàn ở dưới; mỗi mục là một trang giấy (`section.page`) có lỗ gáy, đường lề hồng, một tờ lấp ló phía sau. Thẻ chia mục giấy màu ở mép phải (`#tabs`, ẩn dưới 1180px).
  - Trang đầu là cuốn sổ mở hai trang (`header.spread`): polaroid "Hình 0" (`img/portrait.jpg`), con dấu, thẻ "hiện tại", ba giấy nhớ dẫn vào mục.
  - Các lớp dùng lại: thẻ ghi chú (`.icard`, `.jcard`), giấy nhớ (`.sticky`, `.q`), chồng polaroid (`.stack`), bìa hồ sơ (`.folder`), hoá đơn in nhiệt (`.receipt`), băng nhãn Dymo (`.dymo`, nét đứt = đang học), bưu thiếp (`.postcard`).
  - Chi tiết gói trong thẻ, bấm mới mở: chồng polaroid mở bộ xem ảnh (`openGallery`, phím mũi tên), thẻ K mở bảng tài liệu (`openK`), brochure mở sách lật.
  - Chữ: Newsreader (in), Patrick Hand (viết tay, có dấu tiếng Việt), mono của máy cho số. Hai màu mực `--blue`, `--rose`. Mặc định giấy sáng, nút "Tắt đèn".
  - **Không dùng**: emoji, gradient trang trí, nền chuyển động phát sáng, ô số liệu, nhãn viên thuốc, chữ khổng lồ in hoa.
- Nội dung lấy từ CV (`~/Downloads/[NTU Application]/NQACuong_CV.pdf`) và các artifact trên claude.ai. Toàn bộ nằm trong object `ME` ở đầu thẻ `<script>`; mỗi đoạn chữ viết dạng `["tiếng Việt", "English"]`. Thứ tự chương nằm trong `CHAPTERS`.
- Chương "Mình là ai" (`ME.bioLead`, `ME.story`, `ME.goal`) viết lại từ bản tự thuật `~/Downloads/[NTU Application]/NQACuong_Autobiography_and_Research_Plan.pdf`. Không nêu tên trường hay giáo sư đang nộp hồ sơ lên trang.
- Chương "Hành trình" là các trang nhật ký xếp dọc (`ME.journey`, hàm `journeyHTML`): học vấn, thực tập (BV Bệnh Nhiệt đới, ĐH Y Dược, Touching Soul Center 07–10/2026 với vai trò Undergraduate Psychology Intern; người dùng muốn mốc này đứng **trước** mốc RA BV Bệnh Nhiệt đới), Cuộc thi Sáng tạo Tế bào gốc 2025, và hai mốc trợ lý nghiên cứu đang làm song song: BV Bệnh Nhiệt đới (từ 06/2026, ngay sau thực tập ở ĐH Y Dược) và BV Quân y 175 (từ 08/2026). Mốc có `now: true` mở sẵn. **3 poster về vi khuẩn kháng carbapenem thuộc mốc RA BV Bệnh Nhiệt đới**, không phải đợt thực tập vi sinh 2025. Hoạt động ngoại khoá nằm ở `ME.alongside`.
  - Bấm một mốc mở ra sản phẩm của mốc đó (`items`): poster (`{ p: "poster", i }` trỏ vào `ME.posters`), brochure Dinh dưỡng (`{ p: "brochure" }`, mở sách lật), hoặc chứng nhận (`{ p: "cert", … }`). Người dùng muốn poster và dự án nằm trong timeline, nên chương Nghiên cứu không còn lưới "Dự án & poster" riêng.
  - Ảnh chứng nhận là `img/cert-<năm>-<nơi cấp>-<nội dung>.jpg` (ảnh lớn + `-sm`), dựng từ PDF bằng PDFKit. **Chứng nhận ĐH Y Dược đã che dòng ngày sinh**; chứng nhận mới phải soát ngày sinh, số giấy tờ tuỳ thân trước khi đưa lên.
  - Giải ở Cuộc thi Tế bào gốc: **Giải Khuyến khích – Top 18 thuộc đội TEISC (poster CAR-T)**, người dùng đã xác nhận. Poster hiPSC là poster cá nhân, không có giải. Tổng cộng 2 giải poster (thêm giải Bình chọn nhiều nhất).
- Chương "Nghiên cứu": 4 câu hỏi (`ME.interests`) và các nghiên cứu đang tham gia (`ME.studies`). Dữ liệu `ME.nutrition` và `ME.posters` dùng cho các hình trong timeline (hàm `itemFigure` → `figure`).
  - Brochure Dinh dưỡng mở cửa sổ sách lật (`openBook`, `bookHTML`, `flipBook`): hai ảnh mặt giấy được cắt bằng CSS thành 8 trang theo `ME.nutrition.pages`; lật quá trang cuối thì hiện cả hai mặt. Ảnh xuất từ Canva của người dùng; **không dán link `canva.link` lên trang vì đó là link chỉnh sửa**.
  - Poster CHRO và hiPSC lấy từ ảnh người dùng dán vào chat (1414 × 2000), vì Canva không cho xuất thiết kế của tài khoản khác.
- Chương "Dạy & chia sẻ" là tài liệu gia sư Sinh học lớp 10 cho một học sinh trường International German School (`ME.tutor`, hàm `tutorHTML`). Nguồn ở `~/Downloads/[TS]/Crystal - IGS/`; **không đưa tên học sinh lên trang** (tên thư mục và phiếu gốc có tên học sinh).
  - Xếp theo 13 stage K (Lernplan của trường), mỗi stage mở ra theo thứ tự Tương tác → Slides → Cheat sheet → Video → Phiếu bài tập. Tài liệu dùng chung nhiều stage ghi `ks: [từ, đến]`. Stage K có 3 phiếu: K1 = AB1–3 … K13 = AB37–39 (dòng "Topic block N" trong phiếu xác nhận điều này).
  - Mỗi K có một dòng "Tương tác" trỏ tới visual tương tác: `lessons/visual-genetics-k1-k4.html` và `visual-genetics-k5-k13.html`, là bản sao của hai artifact bài học trên claude.ai (Genetics Stage 1, Stage 2), mở thẳng phần `#kN`. Khi người dùng sửa artifact, đọc lại artifact rồi chép lại; bản sao đã được thêm link "← Portfolio", đoạn đồng bộ sáng/tối theo `portfolio-theme`, `scroll-margin-top` và đoạn cuộn tới `#kN` sau khi tải. **Bỏ khối "Kế hoạch … trước bài kiểm tra" có ngày cụ thể** (lịch riêng của học sinh) ở bản công khai.
  - 39 phiếu bài tập là bản người dùng dịch từ phiếu tiếng Đức của giáo viên, nên **chỉ hiện tên, không cho tải** (người dùng đã chọn vậy).
  - Slides, cheat sheet và video nằm trong `media/`: slides là PDF xuất từ .pptx bằng PowerPoint, cheat sheet là PDF xuất từ .docx bằng Word (cả hai qua `osascript`, nên đặt `with timeout of 300 seconds` vì app khởi động chậm). Mỗi bộ K1–K4, K5–K7, K8–K10, K11–K13 có một slides, hai cheat sheet (Anh–Việt, Anh–Đức) và một video `video-genetics-kX-kY.mp4` kèm ảnh bìa `-cover.jpg`. Video mở trong cửa sổ `#vidDlg`.
- Mục Liên hệ và CV chỉ dùng email công việc `cuong.nguyen.220214@alumni.fulbright.edu.vn` (`ME.emails`). **Không đưa email cá nhân lên**, người dùng đã yêu cầu bỏ.
- CV rút gọn công khai: chỉ có trang `cv/index.html` để xem. **Người dùng không cho tải CV**: không có file PDF trên trang, không có nút tải. Nếu cần xuất PDF để gửi riêng, dùng `cv/html2pdf.swift` và giữ file ngoài repo.
- Ngoại lệ duy nhất về thư viện ngoài: font Newsreader từ Google Fonts (đủ dấu tiếng Việt). Font hệ thống kiểu Iowan/Georgia hiện sai dấu chữ ư, ơ.
- Trang công khai: không đưa số điện thoại, GPA hay liên hệ người tham chiếu trong CV lên nếu người dùng chưa đồng ý. Link artifact claude.ai mặc định là riêng tư, người xem chỉ mở được khi người dùng đã bật chia sẻ.
- Chương "Học code" (`ME.school`, `ME.build`) gọi GitHub API công khai lúc mở trang (`loadGitHub`) để lấy thời gian push của từng repo và 6 commit mới nhất của repo này, nên push xong là trang tự mới. Kết quả lưu tạm 30 phút ở khoá `portfolio-gh` vì API giới hạn 60 lần/giờ cho mỗi người xem. Repo môn học hay dự án mới thì thêm tay vào `ME.school` / `ME.build`.
- `localStorage`: khoá `portfolio-theme` (`light` hoặc `dark`, mặc định sáng; hai trang `lessons/` cũng đọc khoá này), `portfolio-lang` (vi/en) và `portfolio-gh` (bộ đệm GitHub).

## Cách làm việc với người dùng

- Trả lời bằng **tiếng Việt**. Code, tên file và commit message có thể dùng tiếng Anh.
- Người dùng đang học, nên khi làm việc hãy giải thích ngắn gọn *vì sao* chọn cách làm đó, không chỉ đưa kết quả.
- Trước khi đưa tài liệu mới lên (chứng nhận, poster, video), soát thông tin riêng tư: ngày sinh, số điện thoại, tên học sinh, lịch học có ngày cụ thể.

## Quy ước đặt tên (người dùng rất coi trọng, phải giữ nhất quán)

- **File**: `<loại>-<năm hoặc chủ đề>-<nội dung>[-<biến thể>][-sm].<đuôi>`, chữ thường, gạch nối, không dấu. Loại đứng đầu để file cùng loại nằm cạnh nhau.
  - `img/poster-2026-ecoli-chro.jpg`, `img/cert-2025-ump-molbio.jpg`, `img/prizeboard-2025-stemcell.jpg`, `img/brochure-2026-nutrition-cover.jpg`
  - `media/slides-genetics-k1-k4.pdf`, `media/cheatsheet-genetics-k1-k4-en-vi.pdf`, `media/video-genetics-k1-k4.mp4` + `-cover.jpg`, `lessons/visual-genetics-k1-k4.html`
  - Ảnh thu nhỏ luôn là `-sm`. Đổi tên thì dùng `git mv` và sửa mọi tham chiếu (cả trang chuyển hướng trong repo `hoc-claude-code/portfolio/`).
- **Tên hiển thị**: `<Loại> <phạm vi> · <nội dung>`, cùng một từ cho cùng một loại ở mọi chỗ.
  - Dạy học: `Slides K1–K4`, `Cheat sheet K1–K4 · Anh–Việt`, `Video K1–K4 · <tựa>`, `Visual K1 · <công cụ>`.
  - Chứng nhận: `Chứng nhận · <nội dung>` / `Certificate · <nội dung>`; bảng giải: `Bảng giải · …` / `Prize board · …`.
  - Tự học (`ME.learn`): mỗi bài là `{ n, title, lesson, practice, video }`, hiện `Bài N · <tên> · bài giảng · thực hành · video`.
  - **Mỗi bài tự học có đủ ba phần: slides bài giảng (`lesson`), trang thực hành (`practice`) và video cơ chế (`video`). Khi thêm bài, phải tìm video, đừng bỏ sót.** Video thường là file mp4 trong trang thực hành (`Artifact list scope:"files"`), có khi nhúng base64 ngay trong `index.html` của trang thực hành, hoặc nằm trong kho asset của deck (`scope:"assets"`, slide `video`). Chép về `media/video-<chủ đề>-l<n>.mp4` (chủ đề: `gutbrain`, `network`, `dairy`, `wine`) kèm ảnh bìa `-cover.jpg` (lấy khung hình bằng AVFoundation). Bài 3 Hầm rượu hiện chưa có video.
  - Các artifact claude.ai đang ở chế độ riêng tư, nên video chép về repo là phần duy nhất người xem chắc chắn mở được. **Lesson thì gọi lesson hết, practice thì practice hết**, không trộn "quiz", "bài tập", "lab"…
