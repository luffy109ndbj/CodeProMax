# Code ProMax

[English](README.md) · [Tiếng Việt](README.vi.md)

Code ProMax là ứng dụng desktop proprietary giúp kết nối quy trình làm việc Codex cục bộ với ChatGPT Web, đồng thời vẫn giữ task Codex, context dự án, vòng đời tool và workspace cục bộ trên máy của bạn.

> **Phần mềm bên thứ ba không chính thức.** Code ProMax không liên kết, không được chứng thực và không được tài trợ bởi OpenAI.

## Demo

<p align="center">
  <img src="media/demo.gif" alt="Demo Code ProMax" width="960">
</p>

## Tính năng chính

- **ChatGPT Web trong quy trình Codex** — sử dụng các model ChatGPT mà tài khoản của bạn đang có ngay trong luồng task Codex, thay vì phải quản lý một phiên model API riêng.
- **Đăng nhập ChatGPT ngay trong app** — quá trình xác thực diễn ra trong browser profile riêng do launcher quản lý.
- **Chat Long** — phiên làm việc dài, có nhận biết project, giữ lịch sử task và context dự án.
- **Work** — workspace Codex tập trung vào project, phù hợp cho các tác vụ code và nhiều bước phức tạp.
- **Quick Chat** — luồng chat nhẹ hơn cho các câu hỏi nhanh không cần quyền truy cập project.
- **Quản lý thư mục project** — có thể chuyển project sang folder mới mà vẫn giữ alias path lịch sử và các thread cũ.
- **Hình ảnh và context task phong phú** — ảnh và context Codex đã tổng hợp có thể đi cùng task đang hoạt động.
- **MCP / local tools** — trong cấu hình hỗ trợ, ChatGPT có thể kết nối ngược về tool harness Codex cục bộ của task hiện tại.
- **Hỗ trợ Secure MCP Tunnel** — Code ProMax có thể sử dụng luồng Secure MCP Tunnel của OpenAI để kết nối MCP private/local khi account hoặc workspace hỗ trợ.
- **Chẩn đoán cục bộ** — có kiểm tra runtime health, log, smoke test, điều khiển hủy task và lỗi rõ ràng khi thiếu capability cần thiết.
- **Nhiều cấp model** — launcher hiển thị các model/mode ChatGPT mà tài khoản đang đăng nhập thực sự có quyền sử dụng.

Phần MCP tunnel sử dụng mô hình Secure MCP Tunnel được OpenAI công bố tài liệu, trong đó tunnel client do người dùng vận hành duy trì kết nối outbound và MCP server private không cần mở public inbound port. Hãy tham khảo tài liệu chính thức của OpenAI `tunnel-client` để xem yêu cầu nền tảng và tình trạng hỗ trợ mới nhất.

## Cài đặt

### Windows

1. Khi có bản build production-signed, mở mục **Releases** của repository này.
2. Tải installer Windows production-signed mới nhất, tên file sẽ tương tự:

   ```text
   code-promax-<version>-win-x64.exe
   ```

3. Chạy installer.
4. Mở **Code ProMax**.
5. Đăng nhập ChatGPT trong browser tích hợp bằng chính tài khoản của bạn.
6. Chạy bước kiểm tra browser/runtime do app cung cấp.
7. Cài đặt hoặc bật tích hợp Codex khi app yêu cầu.
8. Nếu app yêu cầu, khởi động lại Codex rồi chọn model ChatGPT Web được Code ProMax cung cấp.

Nếu Windows SmartScreen hoặc phần mềm bảo mật chặn installer, hãy xác minh rằng file được tải từ trang Releases chính thức của repository này và kiểm tra chữ ký/file đã công bố trước khi tiếp tục. Không nên tải build từ nguồn mirror mà bạn không tin tưởng.

## Cách sử dụng cơ bản

1. Mở Code ProMax và xác nhận phiên ChatGPT của bạn đang đăng nhập.
2. Mở hoặc chọn project bạn muốn làm việc.
3. Chọn luồng phù hợp với tác vụ:
   - **Quick Chat** cho câu hỏi ngắn, không cần truy cập project.
   - **Chat Long** cho hội thoại dài, có context project và lịch sử liên tục.
   - **Work** cho các tác vụ code/research lớn dựa trên project đã chọn.
4. Chọn model/mode ChatGPT Web mà tài khoản hiện tại của bạn đang có quyền sử dụng.
5. Bắt đầu task từ Codex như bình thường. Code ProMax xử lý phần bridge browser/model và stream kết quả trở lại task Codex.

Các model khả dụng, giới hạn sử dụng, UI và capability connector phụ thuộc vào tài khoản/workspace ChatGPT mà bạn đăng nhập và có thể thay đổi khi OpenAI cập nhật sản phẩm.

## Tùy chọn: MCP / quyền truy cập local tools

Một số workflow có thể kết nối ChatGPT với tool harness Codex cục bộ đang hoạt động thông qua MCP. Code ProMax có hướng dẫn thiết lập trực quan cho luồng này.

<p align="center">
  <img src="media/mcp-create-tunnel.gif" alt="Tạo Secure MCP Tunnel" width="900">
</p>

<p align="center">
  <img src="media/mcp-connect-connector.gif" alt="Kết nối MCP connector" width="900">
</p>

OpenAI có tài liệu riêng cho Developer Mode / MCP apps và Secure MCP Tunnel client. Các tính năng nền tảng này, quyền account, policy workspace và UI có thể thay đổi độc lập với Code ProMax.

Tài liệu chính thức hữu ích:

- OpenAI Secure MCP Tunnel client: https://github.com/openai/tunnel-client
- ChatGPT Developer Mode và MCP apps: https://help.openai.com/en/articles/12584461-developer-mode-and-mcp-apps-in-chatgpt

## Rủi ro tài khoản và trách nhiệm sử dụng

Code ProMax tương tác với ChatGPT bằng chính tài khoản của bạn. **Không có bảo đảm rằng việc sử dụng bất kỳ automation hoặc integration bên thứ ba nào cũng hoàn toàn không có rủi ro đối với tài khoản.**

Theo trải nghiệm thực tế của developer, Code ProMax đã được sử dụng trong nhiều tháng, trên nhiều máy tính và với các tài khoản ChatGPT Plus mà không ghi nhận việc các tài khoản thử nghiệm đó bị vô hiệu hóa do quá trình sử dụng này. **Đây chỉ là kinh nghiệm thực tế của developer, không phải cam kết rằng mọi người dùng, mọi tài khoản, mọi cách sử dụng, mọi khu vực, mọi workspace hoặc mọi policy trong tương lai của OpenAI đều sẽ có kết quả giống nhau.**

Một tài khoản ChatGPT có thể gặp yêu cầu xác minh, giới hạn tạm thời, hạn chế tính năng, đình chỉ hoặc vấn đề khác vì rất nhiều nguyên nhân. Tùy tình huống, nguyên nhân có thể liên quan đến bảo mật tài khoản, thanh toán, thực thi policy, hoạt động bất thường, cách sử dụng, quy định workspace, thay đổi sản phẩm hoặc các yếu tố khác. Nếu một vấn đề tài khoản xảy ra trong thời gian bạn đang cài Code ProMax, chỉ riêng việc hai sự kiện xảy ra cùng lúc không đủ để kết luận Code ProMax là nguyên nhân.

Một số phần của Code ProMax tích hợp với các capability có tài liệu chính thức từ OpenAI, bao gồm các chức năng liên quan đến MCP và Secure MCP Tunnel khi khả dụng. Tuy nhiên, phần bridge với ChatGPT Web vẫn là **integration bên thứ ba không chính thức** và không phải là cam kết từ OpenAI về độ an toàn tài khoản hoặc khả năng tương thích lâu dài.

Khi sử dụng Code ProMax, bạn có trách nhiệm:

- tuân thủ điều khoản, policy và quy định workspace của OpenAI áp dụng cho tài khoản của mình;
- tự quyết định mức độ và tần suất automation phù hợp;
- kiểm tra quyền tool trước khi cho phép hành động ghi hoặc sửa file cục bộ;
- bảo vệ tài khoản và thông tin đăng nhập ChatGPT của mình;
- sao lưu các file project quan trọng trước khi cho phép tác vụ tự động sửa code; và
- tự đánh giá mức rủi ro vận hành/tài khoản có phù hợp với nhu cầu của mình hay không.

**Code ProMax và developer không chịu trách nhiệm cho việc tài khoản bị đình chỉ, hạn chế, mất quyền truy cập, rate limit, bị review, gặp vấn đề thanh toán hoặc các vấn đề tài khoản ChatGPT khác khi nguyên nhân có thể phụ thuộc vào hệ thống OpenAI, hành vi người dùng, trạng thái tài khoản, việc thực thi policy hoặc các yếu tố nằm ngoài khả năng kiểm soát của ứng dụng.** Nội dung này không loại trừ các quyền hoặc trách nhiệm pháp lý mà luật áp dụng không cho phép loại trừ.

## Ghi chú về quyền riêng tư và bảo mật

- Prompt gửi tới ChatGPT vẫn được OpenAI xử lý; Code ProMax không phải là hệ thống AI chạy hoàn toàn local.
- Không nên xem Temporary Chat hoặc browser session tích hợp như một hình thức ẩn danh.
- Giữ hệ điều hành và Code ProMax ở phiên bản mới phù hợp.
- Chỉ cài build từ repository/release chính thức mà bạn tin tưởng.
- Kiểm tra kỹ quyền MCP/tool trước khi bật các hành động ghi hoặc chỉnh sửa.
- Ứng dụng không yêu cầu bạn public source project riêng của mình lên repository GitHub này để có thể sử dụng app desktop.

## Xử lý sự cố

Nếu thiết lập không hoạt động:

1. Xác nhận ChatGPT mở được và đã đăng nhập bên trong Code ProMax.
2. Chạy kiểm tra runtime/browser hoặc doctor check trong app.
3. Khởi động lại Code ProMax và Codex sau khi thay đổi cấu hình integration.
4. Nếu dùng MCP, xác nhận tunnel/connector khả dụng trong cùng môi trường OpenAI/ChatGPT mà bạn đã cấu hình.
5. Kiểm tra log cục bộ để tìm lỗi rõ ràng về capability, permission, browser UI hoặc network trước khi thử lại liên tục.

Do UI web và capability nền tảng của ChatGPT có thể thay đổi, một bản cập nhật trong tương lai từ OpenAI có thể tạm thời làm browser automation hoặc connector không hoạt động ngay cả khi bản thân Code ProMax không thay đổi.

## Phát hành và cập nhật

Các binary production-signed được phân phối qua mục **Releases** của repository này khi có bản phát hành. Source code của Code ProMax không được public tại đây.

Trước khi cài bản cập nhật, nên ưu tiên installer đã được production-sign và thông tin checksum/chữ ký được cung cấp cùng release nếu có.

## Giấy phép

Code ProMax là phần mềm proprietary. Xem [LICENSE](LICENSE).

Ứng dụng có sử dụng các thành phần open-source bên thứ ba theo giấy phép riêng của từng dự án. Thông tin notice và attribution được cung cấp tại:

- [THIRD_PARTY_NOTICES.txt](THIRD_PARTY_NOTICES.txt)
- [Bun.md](Bun.md)

Các thành phần bên thứ ba vẫn giữ nguyên quyền theo giấy phép gốc của chúng và không bị đổi sang giấy phép proprietary của Code ProMax.

## Thông báo thương hiệu

Code ProMax là ứng dụng bên thứ ba độc lập, không liên kết, không được chứng thực và không được tài trợ bởi OpenAI. OpenAI, ChatGPT, GPT, Codex và các nhãn hiệu liên quan thuộc về chủ sở hữu tương ứng.
