# JSON Web Token (JWT): Nền Tảng Xác Thực và Ủy Quyền Trong Kỷ Nguyên Microservices

Chào bạn, với vai trò là một người hướng dẫn về lập trình và công nghệ, tôi rất vui được cùng bạn khám phá sâu hơn về JSON Web Token (JWT) – một công nghệ cốt lõi trong việc xây dựng các ứng dụng hiện đại, đặc biệt là trong môi trường microservices. Tài liệu này sẽ cung cấp cho bạn cái nhìn toàn diện về JWT, từ khái niệm cơ bản đến cách triển khai thực tế và các thực tiễn tốt nhất.

## Giới Thiệu về JWT: Nền Tảng Xác Thực Hiện Đại

Trong bối cảnh phát triển ứng dụng ngày nay, việc xác thực và ủy quyền người dùng một cách an toàn và hiệu quả là vô cùng quan trọng. JSON Web Token (JWT) đã nổi lên như một giải pháp tiêu chuẩn cho thách thức này.

### JWT là gì và tại sao nó lại quan trọng trong thế giới ứng dụng ngày nay?

**Định nghĩa**: JSON Web Token (JWT) là một tiêu chuẩn mở (RFC 7519) được thiết kế để tạo ra các đối tượng dữ liệu nhỏ gọn, an toàn và tự chứa, với khả năng được ký điện tử và/hoặc mã hóa. Cốt lõi của một JWT là một đối tượng JSON chứa các "claims" – những khẳng định về một thực thể (thường là người dùng) hoặc các dữ liệu bổ sung khác. Mục đích chính của JWT là truyền tải thông tin một cách đáng tin cậy giữa hai bên, bởi vì thông tin này được ký số, đảm bảo tính toàn vẹn và xác thực của nó.

**Tính chất quan trọng**:

- **Compact và Self-contained (Gọn nhẹ và Tự chứa)**: JWT có kích thước rất nhỏ gọn và mang theo tất cả thông tin cần thiết về người dùng cùng với các quyền hạn của họ ngay trong token. Điều này giúp giảm đáng kể số lượng truy vấn cần thiết đến cơ sở dữ liệu hoặc các dịch vụ khác để lấy thông tin người dùng, từ đó tối ưu hóa hiệu suất truyền tải dữ liệu.
- **Stateless (Phi trạng thái)**: Đây là một trong những ưu điểm lớn nhất của JWT. Khác với các phương pháp xác thực truyền thống dựa trên phiên (session-based authentication), máy chủ không cần lưu trữ bất kỳ thông tin phiên nào của người dùng sau khi token được cấp. Mỗi yêu cầu từ client đều mang theo token và mọi thông tin cần thiết để xác thực đều nằm trong token đó. Đặc tính phi trạng thái này là yếu tố then chốt giúp ứng dụng dễ dàng mở rộng (scalability), đặc biệt trong các hệ thống phân tán.
- **Secure (An toàn)**: Khi được triển khai đúng cách, JWT cung cấp một phương pháp an toàn để xử lý xác thực và ủy quyền. Chữ ký mã hóa của token đảm bảo rằng nội dung của nó không bị giả mạo hoặc thay đổi trong quá trình truyền tải, giúp các bên nhận token có thể tin cậy vào thông tin mà nó mang lại.

### Vai trò của JWT trong REST API và kiến trúc microservices

**REST API**: JWT là một lựa chọn lý tưởng cho bất kỳ ứng dụng giao diện người dùng (UI) nào cần xác thực người dùng, cũng như cho các cuộc gọi API yêu cầu ủy quyền. Nó cung cấp cơ chế xác thực và ủy quyền ở phạm vi người dùng, điều này khác biệt so với việc sử dụng API Key thường chỉ cung cấp quyền hạn ở phạm vi dự án. Khi một người dùng được xác thực, họ nhận được một JWT, sau đó token này được sử dụng để truy cập các tài nguyên được bảo vệ, đảm bảo rằng chỉ người dùng có quyền mới có thể thực hiện các hành động nhất định.

**Microservices**: Trong kiến trúc microservices, nơi các ứng dụng được chia thành nhiều dịch vụ nhỏ, độc lập và phân tán, JWT đã trở thành phương pháp xác thực và ủy quyền được ưa chuộng.

**Lợi ích chính trong Microservices**:

- **Statelessness**: Tính tự chứa của JWT hoàn toàn phù hợp với bản chất phân tán của microservices. Mỗi microservice có thể độc lập xác thực token mà không cần giao tiếp với một dịch vụ xác thực trung tâm. Điều này loại bỏ sự phụ thuộc vào trạng thái phiên trên máy chủ, giảm tải và điểm nghẽn tiềm năng.
- **Scalability**: Vì các dịch vụ không cần duy trì trạng thái phiên, việc mở rộng hệ thống theo chiều ngang trở nên dễ dàng hơn rất nhiều. Bạn có thể thêm hoặc bớt các instance của microservice mà không cần lo lắng về việc đồng bộ hóa trạng thái phiên.
- **Cross-Domain/SSO (Đa miền/Đăng nhập một lần)**: JWT rất phù hợp cho các giải pháp Single Sign-On (SSO) và xác thực đa miền. Người dùng có thể xác thực trên một dịch vụ và sử dụng cùng một token để truy cập các dịch vụ khác trên các miền khác nhau mà không cần đăng nhập lại.
- **Performance (Hiệu suất)**: Bằng cách giảm thiểu các truy vấn cơ sở dữ liệu để kiểm tra trạng thái phiên trên mỗi yêu cầu, JWT có thể tăng tốc đáng kể hiệu suất của ứng dụng của bạn, mang lại trải nghiệm người dùng mượt mà hơn.

### Liên hệ với hệ thống đặt món ăn: Tại sao một ứng dụng như vậy cần JWT?

Hãy hình dung một hệ thống đặt món ăn hiện đại. Nó thường được xây dựng dựa trên kiến trúc microservices, với các dịch vụ chuyên biệt như **User Service** (quản lý người dùng), **Restaurant Service** (quản lý nhà hàng), **Order Service** (xử lý đơn hàng), và **Payment Service** (xử lý thanh toán).

JWT là lựa chọn lý tưởng để đảm bảo an toàn API trong hệ thống phức tạp này. Khi một người dùng đăng nhập vào **User Service**, họ nhận được một JWT. Sau đó, khi họ muốn thực hiện các hành động như đặt món ăn thông qua **Order Service** hoặc xem chi tiết một nhà hàng từ **Restaurant Service**, họ sẽ gửi kèm JWT đó trong mỗi yêu cầu. Mỗi dịch vụ này có khả năng tự xác minh JWT để biết ai đang gửi yêu cầu và liệu họ có quyền thực hiện hành động đó hay không, mà không cần phải gọi lại **User Service** để kiểm tra cho mỗi yêu cầu. Điều này giúp hệ thống hoạt động mượt mà, hiệu quả hơn và giảm tải đáng kể cho **User Service**.

### Bạn nghĩ tại sao JWT lại được ưa chuộng hơn session-based authentication trong microservices?

Để trả lời câu hỏi này, chúng ta cần xem xét sự khác biệt cơ bản giữa hai phương pháp:

- **Session-based Authentication**: Phương pháp này yêu cầu máy chủ lưu trữ trạng thái phiên của người dùng. Khi người dùng đăng nhập, máy chủ tạo một phiên và lưu trữ dữ liệu phiên (ví dụ: ID người dùng, quyền hạn) trên máy chủ (thường là trong bộ nhớ hoặc cơ sở dữ liệu phiên). Client chỉ nhận được một định danh phiên (session ID), thường được lưu trong cookie, và gửi nó với mỗi yêu cầu. Để xác thực mỗi yêu cầu, máy chủ phải truy vấn kho lưu trữ phiên để lấy thông tin người dùng.
- **JWT Authentication**: Như đã thảo luận, JWT là phi trạng thái. Toàn bộ thông tin xác thực và ủy quyền được gói gọn trong token và được gửi từ client với mỗi yêu cầu. Máy chủ không cần lưu trữ bất kỳ trạng thái phiên nào.

Trong kiến trúc microservices, sự khác biệt này tạo ra những tác động lớn:

**Khả năng mở rộng (Scalability)**:

- **Session-based**: Trong môi trường microservices phân tán, việc quản lý trạng thái phiên trên máy chủ trở nên phức tạp. Nếu bạn có nhiều instance của cùng một dịch vụ hoặc nhiều dịch vụ khác nhau cần truy cập thông tin phiên, bạn sẽ cần một cơ chế để chia sẻ phiên (ví dụ: sticky sessions hoặc một kho lưu trữ phiên tập trung như Redis). Điều này có thể dẫn đến các vấn đề về đồng bộ hóa, độ trễ và trở thành điểm nghẽn tiềm năng khi hệ thống mở rộng.
- **JWT**: Với JWT, mỗi microservice có thể độc lập xác minh token mà không cần liên lạc với bất kỳ dịch vụ xác thực trung tâm nào hoặc truy vấn cơ sở dữ liệu phiên. Điều này giúp các dịch vụ có thể mở rộng độc lập và dễ dàng hơn, vì chúng không cần duy trì trạng thái phiên chung.

**Hiệu suất**:

- **Session-based**: Mỗi yêu cầu cần xác thực sẽ yêu cầu một truy vấn đến kho lưu trữ phiên (thường là cơ sở dữ liệu hoặc Redis). Điều này có thể tạo ra độ trễ, đặc biệt nếu kho lưu trữ phiên nằm trên một máy chủ khác hoặc nếu có lượng truy cập lớn.
- **JWT**: Việc xác minh JWT chủ yếu là một phép toán cục bộ (kiểm tra chữ ký và các claims). Điều này nhanh hơn nhiều so với việc truy vấn cơ sở dữ liệu cho mỗi yêu cầu, giúp cải thiện hiệu suất tổng thể của ứng dụng.

**Tính linh hoạt và Đa nền tảng**:

- **Session-based**: Thường phụ thuộc vào cookie, điều này có thể gây khó khăn khi làm việc với các ứng dụng di động hoặc các client không phải trình duyệt.
- **JWT**: Là một token tự chứa, có thể được gửi qua header HTTP (Authorization: Bearer <token>). Điều này làm cho nó linh hoạt hơn và phù hợp với nhiều loại client khác nhau, bao gồm ứng dụng web (SPA), ứng dụng di động và các dịch vụ backend khác.

Tuy nhiên, điều quan trọng cần lưu ý là JWT không phải là giải pháp hoàn hảo cho mọi trường hợp. Một nhược điểm của JWT là khó thu hồi ngay lập tức một token đã được cấp trước khi nó hết hạn, do tính chất phi trạng thái của nó. Trong khi đó, với session-based authentication, việc vô hiệu hóa một phiên có thể được thực hiện dễ dàng bằng cách xóa bản ghi phiên trên máy chủ. Mặc dù vậy, với các chiến lược quản lý token hiệu quả (như sử dụng refresh token và thời gian sống ngắn cho access token), JWT vẫn là lựa chọn ưu việt cho hầu hết các kiến trúc microservices hiện đại.

## Cấu Trúc Cốt Lõi của JWT

Một JSON Web Token (JWT) được cấu tạo từ ba phần chính, mỗi phần được mã hóa Base64Url và phân tách bằng dấu chấm (.) :

**Header.Payload.Signature**

### Các thành phần chính

**Header (Tiêu đề)**:

Phần này thường chứa hai thông tin chính: loại token (luôn là "JWT") và thuật toán mã hóa được sử dụng để ký token (ví dụ: HMAC SHA256 - HS256 hoặc RSA SHA256 - RS256).

Ví dụ về Header đã được giải mã: `{"alg": "HS256", "typ": "JWT"}`.

Header được mã hóa Base64Url để tạo thành phần đầu tiên của JWT.

**Payload (Nội dung)**:

Payload chứa các "claims" – các khẳng định hoặc thông tin về một thực thể (thường là người dùng) và các dữ liệu bổ sung khác.

Payload cũng được mã hóa Base64Url để tạo thành phần thứ hai của JWT.

**Claims**: Có ba loại claims chính:

- **Registered Claims (Các claims đã đăng ký)**: Đây là một tập hợp các claims được định nghĩa trước, không bắt buộc nhưng được khuyến nghị sử dụng để cung cấp một bộ thông tin hữu ích và có khả năng tương tác. Ví dụ phổ biến bao gồm:
  - **iss (issuer)**: Tổ chức phát hành JWT.
  - **sub (subject)**: Chủ thể của JWT (thường là ID người dùng).
  - **aud (audience)**: Đối tượng mà JWT hướng đến.
  - **exp (expiration time)**: Thời gian token hết hạn. Đây là một claim quan trọng để giới hạn thời gian sống của token.
  - **iat (issued at time)**: Thời gian token được cấp.
  - **jti (JWT ID)**: Một định danh duy nhất cho JWT, có thể được dùng để ngăn chặn việc sử dụng lại token.
- **Public Claims (Các claims công khai)**: Đây là các claims tùy chỉnh không được định nghĩa bởi đặc tả JWT nhưng được sử dụng rộng rãi và có thể được các bên khác nhau đồng ý về ý nghĩa của chúng. Chúng thường được đăng ký trong IANA JSON Web Token Claims Registry để tránh xung đột tên.
- **Private/Custom Claims (Các claims riêng tư/tùy chỉnh)**: Đây là các claims do nhà phát triển tự định nghĩa, dành riêng cho một ứng dụng hoặc trường hợp sử dụng cụ thể. Ví dụ, bạn có thể thêm `user_role` để chỉ định vai trò của người dùng.

**Signature (Chữ ký)**:

Chữ ký là một phần quan trọng đảm bảo tính toàn vẹn và xác thực của token. Nó được tạo ra bằng cách kết hợp Header đã mã hóa Base64Url, Payload đã mã hóa Base64Url, một khóa bí mật (secret key) hoặc khóa riêng tư (private key), và thuật toán mã hóa được chỉ định trong Header.

Mục đích của chữ ký là để xác minh rằng token được phát hành bởi bên mà nó tuyên bố và đảm bảo rằng thông tin trong token không bị thay đổi trên đường truyền.

**Có hai loại thuật toán ký chính**:

- **Symmetric (Đối xứng)**: Sử dụng cùng một khóa bí mật để ký và xác minh (ví dụ: HS256). Khóa này phải được giữ bí mật tuyệt đối và chỉ được biết bởi bên phát hành và bên xác minh token.
- **Asymmetric (Bất đối xứng)**: Sử dụng một cặp khóa: khóa riêng tư (private key) để ký và khóa công khai (public key) để xác minh (ví dụ: RS256). Khóa riêng tư được giữ bí mật bởi bên phát hành, trong khi khóa công khai có thể được chia sẻ rộng rãi để bất kỳ ai cũng có thể xác minh chữ ký mà không cần biết khóa riêng tư.

**Signing Key (Khóa ký)**:

Đây là khóa bí mật (cho thuật toán đối xứng) hoặc khóa riêng tư (cho thuật toán bất đối xứng) được sử dụng để tạo chữ ký của JWT. Khóa này là yếu tố quan trọng nhất để đảm bảo an toàn cho JWT. Nếu chuyển tất cả nội dung dưới đây thành 1 file markdown, không tự ý thay đổi nội dung:

---

# JSON Web Token (JWT): Nền Tảng Xác Thực và Ủy Quyền Trong Kỷ Nguyên Microservices

Chào bạn, với vai trò là một người hướng dẫn về lập trình và công nghệ, tôi rất vui được cùng bạn khám phá sâu hơn về JSON Web Token (JWT) – một công nghệ cốt lõi trong việc xây dựng các ứng dụng hiện đại, đặc biệt là trong môi trường microservices. Tài liệu này sẽ cung cấp cho bạn cái nhìn toàn diện về JWT, từ khái niệm cơ bản đến cách triển khai thực tế và các thực tiễn tốt nhất.

## Giới Thiệu về JWT: Nền Tảng Xác Thực Hiện Đại

Trong bối cảnh phát triển ứng dụng ngày nay, việc xác thực và ủy quyền người dùng một cách an toàn và hiệu quả là vô cùng quan trọng. JSON Web Token (JWT) đã nổi lên như một giải pháp tiêu chuẩn cho thách thức này.

### JWT là gì và tại sao nó lại quan trọng trong thế giới ứng dụng ngày nay?

**Định nghĩa**: JSON Web Token (JWT) là một tiêu chuẩn mở (RFC 7519) được thiết kế để tạo ra các đối tượng dữ liệu nhỏ gọn, an toàn và tự chứa, với khả năng được ký điện tử và/hoặc mã hóa. Cốt lõi của một JWT là một đối tượng JSON chứa các "claims" – những khẳng định về một thực thể (thường là người dùng) hoặc các dữ liệu bổ sung khác. Mục đích chính của JWT là truyền tải thông tin một cách đáng tin cậy giữa hai bên, bởi vì thông tin này được ký số, đảm bảo tính toàn vẹn và xác thực của nó.

**Tính chất quan trọng**:

- **Compact và Self-contained (Gọn nhẹ và Tự Chứa)**: JWT có kích thước rất nhỏ gọn và mang theo tất cả thông tin cần thiết về người dùng cùng với các quyền hạn của họ ngay trong token. Điều này giúp giảm đáng kể số lượng truy vấn cần thiết đến cơ sở dữ liệu hoặc các dịch vụ khác để lấy thông tin người dùng, từ đó tối ưu hóa hiệu suất truyền tải dữ liệu.
- **Stateless (Phi trạng thái)**: Đây là một trong những ưu điểm lớn nhất của JWT. Khác với các phương pháp xác thực truyền thống dựa trên phiên (session-based authentication), máy chủ không cần lưu trữ bất kỳ thông tin phiên nào của người dùng sau khi token được cấp. Mỗi yêu cầu từ client đều mang theo token và mọi informants cần thiết để xác thực đều nằm trong token đó. Đặc tính phi trạng thái này là yếu tố then chốt giúp ứng dụng dễ dàng mở rộng (scalability), đặc biệt trong các hệ thống phân tán.
- **Secure (An toàn)**: Khi được triển khai đúng cách, JWT cung cấp một phương pháp an toàn để xử lý xác thực và ủy quyền. Chữ ký mã hóa của token đảm bảo rằng nội dung của nó không bị giả mạo hoặc thay đổi trong quá trình truyền tải, giúp các bên nhận token có thể tin cậy vào thông tin mà nó mang lại.

### Vai trò của JWT trong REST API và kiến trúc microservices

**REST API**: JWT là một lựa chọn lý tưởng cho bất kỳ ứng dụng giao diện người dùng (UI) nào cần xác thực người dùng, cũng như cho các cuộc gọi API yêu cầu ủy quyền. Nó cung cấp cơ chế xác thực và ủy quyền ở phạm vi người dùng, điều này khác biệt so với việc sử dụng API Key thường chỉ cung cấp quyền hạn ở phạm vi dự án. Khi một người dùng được xác thực, họ nhận được một JWT, sau đó token này được sử dụng để truy cập các tài nguyên được bảo vệ, đảm bảo rằng chỉ người dùng có quyền mới có thể thực hiện các hành động nhất định.

**Microservices**: Trong kiến trúc microservices, nơi các ứng dụng được chia thành nhiều dịch vụ nhỏ, độc lập và phân tán, JWT đã trở thành phương pháp xác thực và ủy quyền được ưa chuộng.

**Lợi ích chính trong Microservices**:

- **Statelessness**: Tính tự chứa của JWT hoàn toàn phù hợp với bản chất phân tán của microservices. Mỗi microservice có thể độc lập xác thực token mà không cần giao tiếp với một dịch vụ xác thực trung tâm. Điều này loại bỏ sự phụ thuộc vào trạng thái phiên trên máy chủ, giảm tải và điểm nghẽn tiềm năng.
- **Scalability**: Vì các dịch vụ không cần duy trì trạng thái phiên, việc mở rộng hệ thống theo chiều ngang trở nên dễ dàng hơn rất nhiều. Bạn có thể thêm hoặc bớt các instance của microservice mà không cần lo lắng về việc đồng bộ hóa trạng thái phiên.
- **Cross-Domain/SSO (Đa miền/Đăng nhập một lần)**: JWT rất phù hợp cho các giải pháp Single Sign-On (SSO) và xác thực đa miền. Người dùng có thể xác thực trên một dịch vụ và sử dụng cùng một token để truy cập các dịch vụ khác trên các miền khác nhau mà không cần đăng nhập lại.
- **Performance (Hiệu suất)**: Bằng cách giảm thiểu các truy vấn cơ sở dữ liệu để kiểm tra trạng thái phiên trên mỗi yêu cầu, JWT có thể tăng tốc đáng kể hiệu suất của ứng dụng của bạn, mang lại trải nghiệm người dùng mượt mà hơn.

### Liên hệ với hệ thống đặt món ăn: Tại sao một ứng dụng như vậy cần JWT?

Hãy hình dung một hệ thống đặt món ăn hiện đại. Nó thường được xây dựng dựa trên kiến trúc mi croservices, với các dịch vụ chuyên biệt như **User Service** (quản lý người dùng), **Restaurant Service** (quản lý nhà hàng), **Order Service** (xử lý đơn hàng), và **Payment Service** (xử lý thanh toán).

JWT là lựa chọn lý tưởng để đảm bảo an toàn API trong hệ thống phức tạp này. Khi một người dùng đăng nhập vào **User Service**, họ nhận được một JWT. Sau đó, khi họ muốn thực hiện các hành động như đặt món ăn thông qua **Order Service** hoặc xem chi tiết một nhà hàng từ **Restaurant Service**, họ sẽ gửi kèm JWT đó trong mỗi yêu cầu. Mỗi dịch vụ này có khả năng tự xác minh JWT để biết ai đang gửi yêu cầu và liệu họ có quyền thực hiện hành động đó hay không, mà không cần phải gọi lại **User Service** để kiểmhalation cho mỗi yêu cầu. Điều này giúp hệ thống hoạt động mượt mà, hiệu quả hơn và giảm tải đáng kể cho **User Service**.

### Bạn nghĩ tại sao JWT lại được ưa chuộng hơn session-based authentication trong microservices?

Để trả lời câu hỏi này, chúng ta cần xem xét sự khác biệt cơ bản giữa hai phương pháp:

- **Session-based Authentication**: Phương pháp này yêu cầu máy chủ lưu trữ trạng thái phiên của người dùng. Khi người dùng đăng nhập, máy chủ tạo một phiên và lưu trữ dữ liệu phiên (ví dụ: ID người dùng, quyền hạn) trên máy chủ (thường là trong bộ nhớ hoặc cơ sở dữ liệu phiên). Client chỉ nhận được một định danh phiên (session ID), thường được lưu trong cookie, và gửi nó với mỗi yêu cầu. Để xác thực mỗi yêu cầu, máy chủ phải truy vấn kho lưu trữ phiên để lấy thông tin người dùng.
- **JWT Authentication**: Như đã thảo luận, JWT là phi trạng thái. Toàn bộ thông tin xác thực và ủy quyền được gói gọn trong token và được gửi từ client với mỗi yêu cầu. Máy chủ không cần lưu trữ bất kỳ trạng thái phiên nào.

Trong kiến trúc microservices, sự khác biệt này tạo ra những tác động lớn:

**Khả năng mở rộng (Scalability)**:

- **Session-based**: Trong môi trường microservices phân tán, việc quản lý trạng thái phiên trên máy chủ trở nên phức tạp. Nếu bạn có nhiều instance của cùng một dịch vụ hoặc nhiều dịch vụ khác nhau cần truy cập thông tin phiên, bạn sẽ cần một cơ chế để chia sẻ phiên (ví dụ: sticky sessions hoặc một kho lưu trữ phiên tập trung như Redis). Điều này có thể dẫn đến các vấn đề về đồng bộ hóa, độ trễ và trở thành điểm nghẽn tiềm năng khi hệ thống mở rộng.
- **JWT**: Với JWT, mỗi microservice có thể độc lập xác minh token mà không cần liên lạc với bất kỳ dịch vụ xác thực trung tâm nào hoặc truy vấn cơ sở dữ liệu phiên. Điều này giúp các dịch vụ có thể mở rộng độc lập và dễ dàng hơn, vì chúng không cần duy trì trạng thái phiên chung.

**Hiệu suất**:

- **Session-based**: Mỗi yêu cầu cần xác thực sẽ yêu cầu một truy vấn đến kho lưu trữ phiên (thường là cơ sở dữ liệu hoặc Redis). Điều này có thể tạo ra độ trễ, đặc biệt nếu kho lưu trữ phiên nằm trên một máy chủ khác hoặc nếu có lượng truy cập lớn.
- **JWT**: Việc xác minh JWT chủ yếu là một phép toán cục bộ (kiểm tra chữ ký và các claims). Điều này nhanh hơn nhiều so với việc truy vấn cơ sở dữ liệu cho mỗi yêu cầu, giúp cải thiện hiệu suất tổng thể của ứng dụng.

**Tính linh hoạt và Đa nền tảng**:

- **Session-based**: Thường phụ thuộc vào cookie, điều này có thể gây khó khăn khi làm việc với các ứng dụng di động hoặc các client không phải trình duyệt.
- **JWT**: Là một token tự chứa, có thể được gửi qua header HTTP (Authorization: Bearer <token>). Điều này làm cho nó linh hoạt hơn và phù hợp với nhiều loại client khác nhau, bao gồm ứng dụng web (SPA), ứng dụng di động và các dịch vụ backend khác.

Tuy nhiên, điều quan trọng cần lưu ý là JWT không phải là giải pháp hoàn hảo cho mọi trường hợp. Một nhược điểm của JWT là khó thu hồi ngay lập tức một token đã được cấp trước khi nó hết hạn, do tính chất phi trạng thái của nó. Trong khi đó, với session-based authentication, việc vô hiệu hóa một phiên có thể được thực hiện dễ dàng bằng cách xóa bản ghi phiên trên máy chủ. Mặc dù vậy, với các chiến lược quản lý token hiệu quả (như sử dụng refresh token và thời gian sống ngắn cho access token), JWT vẫn là lựa chọn ưu việt cho hầu hết các kiến trúc microservices hiện đại.

## Cấu Trúc Cốt Lõi của JWT

Một JSON Web Token (JWT) được cấu tạo từ ba phần chính, mỗi phần được mã hóa Base64Url và phân tách bằng dấu chấm (.) :

**Header.Payload.Signature**

### Các thành phần chính

**Header (Tiêu đề)**:

Phần này thường chứa hai thông tin chính: loại token (luôn là "JWT") và thuật toán mã hóa được sử dụng để ký token (ví dụ: HMAC SHA256 - HS256 hoặc RSA SHA256 - RS256).

Ví dụ về Header đã được giải mã: `{"alg": "HS256", "typ": "JWT"}`.

Header được mã hóa Base64Url để tạo thành phần đầu tiên của JWT.

**Payload (Nội dung)**:

Payload chứa các "claims" – các khẳng định hoặc thông tin về một thực thể (thường là người dùng) và các dữ liệu bổ sung khác.

Payload cũng được mã hóa Base64Url để tạo thành phần thứ hai của JWT.

**Claims**: Có ba loại claims chính:

- **Registered Claims (Các claims đã đăng ký)**: Đây là một tập hợp các claims được định nghĩa trước, không bắt buộc nhưng được khuyến nghị sử dụng để cung cấp một bộ thông tin hữu ích và có khả năng tương tác. Ví dụ phổ biến bao gồm:
  - **iss (issuer)**: Tổ chức phát hành JWT.
  - **sub (subject)**: Chủ thể của JWT (thường là ID người dùng).
  - **aud (audience)**: Đối tượng mà JWT hướng đến.
  - **exp (expiration time)**: Thời gian token hết hạn. Đây là một claim quan trọng để giới hạn thời gian sống của token.
  - **iat (issued at time)**: Thời gian token được cấp.
  - **jti (JWT ID)**: Một định danh duy nhất cho JWT, có thể được dùng để ngăn chặn việc sử dụng lại token.
- **Public Claims (Các claims công khai)**: Đây là các claims tùy chỉnh không được định nghĩa bởi đặc tả JWT nhưng được sử dụng rộng rãi và có thể được các bên khác nhau đồng ý về ý nghĩa của chúng. Chúng thường được đăng ký trong IANA JSON Web Token Claims Registry để tránh xung đột tên.
- **Private/Custom Claims (Các claims riêng tư/tùy chỉnh)**: Đây là các claims do nhà phát triển tự định nghĩa, dành riêng cho một ứng dụng hoặc trường hợp sử dụng cụ thể. Ví dụ, bạn có thể thêm `user_role` để chỉ định vai trò của người dùng.

**Signature (Chữ ký)**:

Chữ ký là một phần quan trọng đảm bảo tính toàn vẹn và xác thực của token. Nó được tạo ra bằng cách kết hợp Header đã mã hóa Base64Url, Payload đã mã hóa Base64Url, một khóa bí mật (secret key) hoặc khóa riêng tư (private key), và thuật toán mã hóa được chỉ định trong Header.

Mục đích của chữ ký là để xác minh rằng token được phát hành bởi bên mà nó tuyên bố và đảm bảo rằng thông tin trong token không bị thay đổi trên đường truyền.

**Có hai loại thuật toán ký chính**:

- **Symmetric (Đối xứng)**: Sử dụng cùng một khóa bí mật để ký và xác minh (ví dụ: HS256). Khóa này phải được giữ bí mật tuyệt đối và chỉ được biết bởi bên phát hành và bên xác minh token.
- **Asymmetric (Bất đối xứng)**: Sử dụng một cặp khóa: khóa riêng tư (private key) để ký và khóa công khai (public key) để xác minh (ví dụ: RS256). Khóa riêng tư được giữ bí mật bởi bên phát hành, trong khi khóa công khai có thể được chia sẻ rộng rãi để bất kỳ ai cũng có thể xác minh chữ ký mà không cần biết khóa riêng tư.

**Signing Key (Khóa ký)**:

Đây là khóa bí mật (cho thuật toán đối xứng) hoặc khóa riêng tư (cho thuật toán bất đối xứng) được sử dụng để tạo chữ ký của JWT. Khóa này là yếu tố quan trọng nhất để đảm bảo an toàn cho JWT. Nếu khóa này bị lộ, kẻ tấn công có thể tạo ra các token giả mạo hợp lệ.

### Cách các thành phần này phối hợp để đảm bảo xác thực an toàn

Quy trình xác thực JWT diễn ra như sau:

1. **Tạo Token**: Khi người dùng xác thực thành công (ví dụ: đăng nhập bằng tên người dùng và mật khẩu), máy chủ xác thực sẽ tạo một JWT. Token này bao gồm **Header** (chứa loại token và thuật toán ký), **Payload** (chứa các claims về người dùng như ID, vai trò, thời gian hết hạn) và **Signature** (được tạo bằng cách ký Header và Payload đã mã hóa bằng khóa bí mật/riêng tư của máy chủ).
2. **Ph公式 hành Token**: Máy chủ gửi JWT này về cho client.
3. **Lưu trữ Token**: Client lưu trữ token này (thường là trong bộ nhớ cục bộ, session storage hoặc cookie HttpOnly).
4. **Sử dụng Token**: Với mỗi yêu cầu tiếp theo đến các tài nguyên được bảo vệ, client sẽ đính kèm JWT vào header Authorization (ví dụ: `Authorization: Bearer <token>`).
5. **Xác minh Token**: Khi máy chủ (hoặc một microservice) nhận được yêu cầu, nó sẽ thực hiện các bước sau để xác minh JWT:
   - **Giải mã Header và Payload**: Máy chủ giải mã phần Header và Payload từ Base64Url. Điều này không yêu cầu khóa bí mật và có thể được thực hiện bởi bất kỳ ai. Tuy nhiên, việc giải mã này chỉ cho phép đọc thông tin, không đảm bảo tính toàn vẹn của dữ liệu.
   - **Xác minh chữ ký**: Máy chủ sử dụng thuật toán được chỉ định trong Header và khóa bí mật/công khai tương ứng để tính toán lại chữ ký. Nếu chữ ký được tính toán lại khớp với chữ ký trong token, điều đó xác nhận rằng token không bị giả mạo và được phát hành bởi bên đáng tin cậy.
   - **Kiểm tra Claims**: Sau khi chữ ký được xác minh, máy chủ sẽ kiểm tra các claims trong Payload, đặc biệt là `exp` (thời gian hết hạn) để đảm bảo token vẫn còn hiệu lực, `iss` (bên phát hành) và `aud` (đối tượng) để đảm bảo token được sử dụng đúng mục đích.
6. **Cấp quyền truy cập**: Nếu token hợp lệ và các claims đáp ứng yêu cầu ủy quyền, máy chủ sẽ xử lý yêu cầu và cấp quyền truy cập tài nguyên.

### Gợi ý: "Bạn nghĩ claims trong Payload có thể được dùng như thế nào trong hệ thống đặtMons ăn?"

Trong một hệ thống đặt món ăn, các claims trong Payload của JWT đóng vai trò cực kỳ quan trọng trong việc xác định danh tính và quyền hạn của người dùng mà không cần phải truy vấn cơ sở dữ liệu cho mỗi yêu cầu. Điều này giúp hệ thống phản hồi nhanh chóng và hiệu quả hơn.

Dưới đây là một số cách claims có thể được sử dụng:

- **sub (subject)**: Chứa ID duy nhất của người dùng (ví dụ: `user_id: "12345"`). Khi một microservice như **Order Service** nhận được yêu cầu tạo đơn hàng, nó có thể trích xuất `user_id` từ token để biết ai đang tạo đơn, liên kết đơn hàng với người dùng đó mà không cần phải gọi **User Service** để lấy thông tin cơ bản về ID người dùng.
- **roles (custom claim)**: Chứa danh sách các vai trò của người dùng (ví dụ: `roles: ["CUSTOMER"]`).
  - **Order Service** có thể kiểm tra vai trò `"CUSTOMER"` để đảm bảo chỉ khách hàng mới được phép đặt món.
  - **Restaurant Service** có thể kiểm tra vai trò `"RESTAURANT_OWNER"` để cho phép chủ nhà hàng quản lý menu của họ.
  - **Admin Service** có thể kiểm tra vai trò `"ADMIN"` để cấp quyền truy cập vào các chức năng quản trị hệ thống.
- **loyalty_points (custom claim)**: Chứa số điểm khách hàng thân thiết hiện có (ví dụ: `loyalty_points: 500`). **Payment Service** có thể sử dụng thông tin này để áp dụng giảm giá hoặc khuyến mãi mà không cần truy vấn database điểm thưởng.
- **preferred_language (custom claim)**: Chứa ngôn ngữ ưu tiên của người dùng (ví dụ: `preferred_language: "vi"`). UI Gateway hoặc các microservice có thể sử dụng claim này để cá nhân hóa nội dung hoặc thông báo cho người dùng.
- **last_order_timestamp (custom claim)**: Chứa thời gian đơn hàng gần nhất của người dùng (ví dụ: `last_order_timestamp: 1678886400`). **Order Service** có thể sử dụng để kiểm tra tần suất đặt hàng hoặc áp dụng các chính sách khuyến mãi dựa trên lịch sử.

Việc nhúng các claims này vào Payload giúp giảm thiểu đáng kể số lượng truy vấn cơ sở dữ liệu trên mỗi yêu cầu, vì thông tin cần thiết đã có sẵn trong token. Điều này đặc biệt hữu ích trong kiến trúc microservices, nơi mỗi dịch vụ có thể tự đưa ra quyết định ủy quyền dựa trên thông tin trong token mà không cần giao tiếp liên tục với dịch vụ xác thực trung tâm.

## Triển Khai JWT với Java Spring Boot

Việc tích hợp JWT vào ứng dụng Spring Boot là một quy trình có cấu trúc, tậnПП dụng sức mạnh của Spring Security để bảo vệ các API của bạn. Dưới đây là hướng dẫn từng bước về tư duy và cách thực hiện.

### Hướng dẫn từng bước cách tích Seafood JWT vào ứng dụng Spring Boot

**Tư duy chung**: Khi triển khai JWT trong Spring Boot, mục tiêu là tạo ra một luồng xác thực phi trạng thái. Điều này có nghĩa là sau khi người dùng đăng nhập và nhận được JWT, mọi yêu cầu tiếp theo sẽ được xác thực bằng cách kiểm tra token đó, không cần lưu trữ bất kỳ thông tin phiên nào trên máy chủ. Spring Security sẽ được cấu hình để nhận biết và xử lý các JWT này.

#### Bước 1: Thêm Dependencies cần thiết

Để làm việc với JWT và Spring Security, bạn cần thêm các dependency sau vào file `pom.xml` của dự án Maven (hoặc `build.gradle` nếu dùng Gradle):

- `spring-boot-starter-security`: Cung cấp các tính năng bảo mật cốt lõi của Spring Security.
- `spring-boot-starter-web`: Cần thiết cho việc xây dựng ứng dụng web và RESTful API.
- `spring-boot-starter-data-jpa`: Để tương tác với cơ sở dữ liệu (ví dụ: MSSQL) để lưu trữ thông tin người dùng.
- **Driver JDBC cho MSSQL**: `mssql-jdbc`.
- **Thư viện JWT**: `io.jsonwebtoken:jjwt-api`, `io.jsonwebtoken:jjwt-impl`, `io.jsonwebtoken:jjwt-jackson`.

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-security</artifactId>
    </dependency>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-data-jpa</artifactId>
    </dependency>
    <dependency>
        <groupId>com.microsoft.sqlserver</groupId>
        <artifactId>mssql-jdbc</artifactId>
        <scope>runtime</scope>
    </dependency>
    <dependency>
        <groupId>io.jsonwebtoken</groupId>
        <artifactId>jjwt-api</artifactId>
        <version>0.11.5</version>
    </dependency>
    <dependency>
        <groupId>io.jsonwebtoken</groupId>
        <artifactId>jjwt-impl</artifactId>
        <version>0.11.5</version>
        <scope>runtime</scope>
    </dependency>
    <dependency>
        <groupId>io.jsonwebtoken</groupId>
        <artifactId>jjwt-jackson</artifactId>
        <version>0.11.5</version>
        <scope>runtime</scope>
    </dependency>
</dependencies>
```

#### Bước 2: Cấu hình Spring Security (SecurityConfig)

Đây là trái tim của việc bảo mật ứng dụng. Bạn sẽ tạo một lớp cấu hình (ví dụ: `SecurityConfig`) mở rộng `WebSecurityConfigurerAdapter` (hoặc sử dụng cấu hình dựa trên `SecurityFilterChain` cho Spring Security 6+).

- **Vô hiệu hóa CSRF**: Vì JWT là phi trạng thái và không dựa vào cookie phiên, các cuộc tấn công CSRF (Cross-Site Request Forgery) truyền thống ít có khả năng xảy ra. Do đó, bạn có thể vô hiệu hóa bảo vệ CSRF.
- **Cấu hình Session Management là STATELESS**: Đây là điểm mấu chốt để Spring Security không tạo hoặc sử dụng các phiên HTTP. Điều này đảm bảo ứng dụng của bạn hoàn toàn phi trạng thái.
- **Định nghĩa các Endpoint công khai và được bảo vệ**: Bạn sẽ chỉ định những URL nào được phép truy cập công khai (ví dụ: `/auth/login`, `/auth/signup`) và những URL nào yêu cầu xác thực JWT hợp lệ.
- **Cấu hình AuthenticationProvider**: Kết nối `UserDetailsService` tùy chỉnh (để tải thông tin người dùng từ cơ sở dữ liệu) và `PasswordEncoder` (để mã hóa và so sánh mật khẩu).
- **Thêm JwtAuthFilter**: Bạn sẽ tạo một Filter tùy chỉnh để chặn mọi yêu cầu đến, trích xuất JWT từ header, xác thực nó và thiết lập ngữ cảnh bảo mật cho Spring Security. Filter này cần được thêm vào chuỗi filter của Spring Security trước `UsernamePasswordAuthenticationFilter` mặc định.

#### Bước 3: Tạo JwtService để quản lý Token

**JwtService** là một lớp tiện ích chịu trách nhiệm tạo, giải mã và xác thực JWT.

- **generateToken(UserDetails userDetails)**: Phương thức này sẽ lấy thông tin UserDetails của người dùng đã xác thực, sử dụng một khóa bí mật (secret key) được cấu hình (thường trong `application.properties`), và đặt các claims như subject (tên người dùng), issuer, expiration time vào Payload. Sau đó, nó sẽ ký token và trả về chuỗi JWT.
- **extractUsername(String token)**: Phương thức này sẽ giải mã token và trích xuất tên người dùng từ claim subject.
- **validateToken(String token, UserDetails userDetails)**: Đây là phương thức quan trọng để xác thực token. Nó sẽ sử dụng khóa bí mật đểMunicipal xác minh chữ ký của token. Sau đó, nó sẽ kiểm tra xem tên người dùng trong token có khớp với UserDetails được cung cấp hay không và quan trọng nhất là kiểm tra xem token đã hết hạn chưa (`exp` claim).

#### Bước 4: User Entity và Repository (Kết nối với MSSQL)

Bạn sẽ cần một **User entity** để ánh xạ tới bảng người dùng trong MSSQL. Entity này nên triển khai giao diện `UserDetails` của Spring Security để cung cấp thông tin chi tiết về người dùng (tên người dùng, mật khẩu, quyền hạn, trạng thái tài khoản, v.v.).

**UserRepository** là một interface mở rộng `JPA repository` để thực hiện các thao tác CRUD (Create, Read, Update, Delete) với bảng người dùng trong MSSznac. Ví dụ, bạn sẽ có phương thức `findByUsername(String username)` để tải thông tin người dùng khi họ đăng nhập.

**Kết nối với MSSQL**:
Thông tin người dùng (tên người dùng, mật khẩu đã mã hóa, vai trò) sẽ được lưu trữ trong cơ sở dữ liệu MSSQL của bạn. Spring Data JPA sẽ tự động ánh xạ các entity Java của bạn tới các bảng trong database. Bạn cần cấu hình thông tin kết nối MSSQL trong file `application.properties` (hoặc `application.yml`):

```properties
# application.properties
spring.datasource.url=jdbc:sqlserver://localhost:1433;databaseName=your_db_name;encrypt=true;trustServerCertificate=true;
spring.datasource.username=your_username
spring.datasource.password=your_password
spring.jpa.hibernate.ddl-auto=update # hoặc none, create, create-drop tùy môi trường
spring.jpa.show-sql=true

# Cấu hình JWT
security.jwt.secret-key=your_super_secret_key_for_jwt_signing_256_bits
security.jwt.expiration-time=3600000 # 1 giờ (milliseconds)
```

Lưu ý rằng, mặc dù thông tin người dùng được lưu trong MSSQL, bản thân JWT là phi trạng thái. MSSQL được sử dụng để xác thực người dùng ban đầu và lấy thông tin chi tiết của họ, chứ không phải để quản lý phiên sau khi JWT đã được cấp. Các thư viện JDBC hiện tại của MSSQL không hỗ trợ xác thực trực tiếp bằng JWT để kết nối với cơ sở dữ liệu.

#### Bước 5: Controller cho Authentication

Bạn sẽ có một **AuthController** với các endpoint để xử lý đăng ký và đăng nhập:

- **POST /auth/signup**: Nhận thông tin đăng ký người dùng mới, mã hóa mật khẩu bằng `PasswordEncoder`, lưu vào MSSQL thông qua `UserRepository`.
- **POST /auth/login**: Nhận tên người dùng và mật khẩu. Sử dụng `AuthenticationManager` của Spring Security để xác thực. Nếu xác thực thành công, gọi `JwtService` để tạo JWT và trả về cho client.

### Gợi ý: "Bạn sẽ cấu hình Spring Security với JWT như thế nào để bảo vệ API đặt món?"

Để bảo vệ API đặt món ăn bằng JWT trong Spring Boot, cấu hình `SecurityFilterChain` là nơi bạn định hình toàn bộ cơ chế bảo mật.

**Vô hiệu hóa CSRF và thiết lập Stateless Session**:

```java
@Configuration
@EnableWebSecurity
public class SecurityConfig {

    //... các bean khác như UserDetailsService, PasswordEncoder, JwtAuthFilter...

    @Bean
    public SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {
        http
           .csrf(csrf -> csrf.disable()) // Vô hiệu hóa CSRF cho API stateless
           .authorizeHttpRequests(auth -> auth
               .requestMatchers("/api/auth/**").permitAll() // Cho phép truy cập công khai các endpoint đăng ký/đăng nhập
               .anyRequest().authenticated() // Mọi yêu cầu khác đều phải được xác thực
            )
           .sessionManagement(session -> session.sessionCreationPolicy(SessionCreationPolicy.STATELESS)) // Đảm bảo ứng dụng là stateless
            //.authenticationProvider(authenticationProvider()) // Cấu hình AuthenticationProvider
           .addFilterBefore(jwtAuthFilter, UsernamePasswordAuthenticationFilter.class); // Thêm JwtAuthFilter trước filter mặc định
        return http.build();
    }

    //... các bean khác...
}
```

Trong đoạn mã trên, `csrf.disable()` là cần thiết vì JWT không dựa vào cookie phiên, làm cho các cuộc tấn công CSRF truyền thống không hiệu quả.

`sessionCreationPolicy(SessionCreationPolicy.STATELESS)` là cực kỳ quan trọng, nó báo cho Spring Security không tạo hoặc sử dụng bất kỳ phiên HTTP nào, phù hợp với bản chất phi trạng thái của JWT.

**Định nghĩa quyền truy cập Endpoint**:

- `requestMatchers("/api/auth/**").permitAll()`: Các endpoint liên quan đến xác thực (ví dụ: `/api/auth/login`, `/api/auth/signup`) sẽ được phép truy cập mà không cần xác thực.
(percent)

- **anyRequest().authenticated()**: Tất cả các endpoint còn lại (ví dụ: `/api/orders`, `/api/restaurants`) sẽ yêu cầu người dùng phải được xác thực bằng JWT hợp lệ.

**Tích hợp JwtAuthFilter**:
- `addFilterBefore(jwtAuthFilter, UsernamePasswordAuthenticationFilter.class)`: Đây là bước then chốt. **JwtAuthFilter** tùy chỉnh của bạn sẽ được thực thi trước filter xác thực mặc định của Spring Security. **JwtAuthFilter** này sẽ:
  - Trích xuất JWT từ header Authorization của yêu cầu.
  - Sử dụng **JwtService** để xác thực token (kiểm tra chữ ký, thời gian hết hạn, v.v.).
  - Nếu token hợp lệ, nó sẽ tải **UserDetails** của người dùng và thiết lập đối tượng **Authentication** vào **SecurityContextHolder** của Spring. Điều này cho phép các lớp xử lý API tiếp theo (Controller, Service) biết được người dùng hiện tại là ai và có những quyền hạn gì mà không cần phải tự xác thực lại.

Bằng cách này, mỗi yêu cầu đến API đặt món ăn sẽ đi qua **JwtAuthFilter**. Nếu token hợp lệ, yêu cầu sẽ được tiếp tục xử lý; nếu không, Spring Security sẽ tự động chặn yêu cầu đó và trả về lỗi **401 Unauthorized**. Điều này đảm bảo rằng chỉ những người dùng có token hợp lệ mới có thể truy cập các chức năng quan trọng của hệ thống đặt món ăn.

## Thực Tiễn Tốt Nhất (Best Practices) khi sử dụng JWT

Để tận dụng tối đa lợi ích của JWT và đảm bảo an toàn cho ứng dụng, việc tuân thủ các thực tiễn tốt nhất là điều cần thiết.

### Quản lý thời gian sống của Token

Việc thiết lập thời gian sống (**TTL - Time To Live**) phù hợp cho token là rất quan trọng để cân bằng giữa bảo mật và trải nghiệm người dùng.

- **Access Token (Token truy cập)**: Nên có thời gian sống ngắn (ví dụ: từ 15 phút đến 1 giờ). Mục đích là để giảm thiểu rủi ro nếu token bị đánh cắp. Nếu một access token bị lộ, kẻ tấn công chỉ có một khoảng thời gian giới hạn để sử dụng nó.
- **Refresh Token (Token làm mới)**: Nên có thời gian sống dài hơn (ví dụ: từ 1 ngày đến 2 tuần, hoặc thậm chí lâu hơn tùy theo yêu cầu bảo mật và trải nghiệm người dùng). Refresh token được sử dụng để lấy một access token mới khi access token hiện tại hết hạn, mà không yêu cầu người dùng phải đăng nhập lại. Refresh token thường là một token mờ (opaque token) và nên được lưu trữ an toàn hơn (ví dụ: trong database và chỉ được sử dụng một lần hoặc có cơ chế xoay vòng).

Luồng sử dụng access token và refresh token giúp cân bằng giữa bảo mật (access token ngắn hạn) và trải nghiệm người dùng (không cần đăng nhập lại thường xuyên nhờ refresh token).

### Bảo vệ chống tấn công (XSS, CSRF)

JWT bản thân nó không tự động ngăn chặn tất cả các loại tấn công web. Cần có các biện pháp bổ sung để bảo vệ ứng dụng.

**XSS (Cross-Site Scripting)**:

- **Tránh lưu trữ JWT trong localStorage hoặc sessionStorage**: Mặc dù tiện lợi, nhưng localStorage và sessionStorage dễ bị tấn công XSS. Nếu một script độc hại được tiêm vào trang web, nó có thể dễ dàng truy cập và đánh cắp token từ các vị trí này.
- **Ưu tiên sử dụng HttpOnly cookies**: Khi JWT được lưu trữ trong cookie với flag **HttpOnly** được bật, JavaScript chạy trên trình duyệt sẽ không thể truy cập được cookie đó. Điều này ngăn chặn các script XSS đánh cắp token.
- **Làm sạch dữ liệu đầu vào và triển khai Content Security Policy (CSP)**: Luôn xác thực và làm sạch mọi dữ liệu đầu vào từ người dùng để ngăn chặn việc tiêm script độc hại. CSP là một lớp bảo mật bổ sung giúp kiểm soát các nguồn tài nguyên mà trình duyệt được phép tải và thực thi, giảm thiểu rủi ro XSS.

**CSRF (Cross-Site Request Forgery)**:

- **JWTs alone do not prevent CSRF attacks**: JWT chỉ xác thực người dùng, không xác thực tính hợp lệ của yêu cầu.
- **Sử dụng thuộc tính SameSite cho cookie**: Đặt thuộc tính **SameSite** của cookie JWT thành **Lax** hoặc **Strict**. Điều này hướng dẫn trình duyệt không gửi cookie với các yêu cầu chéo nguồn (cross-origin requests), làm giảm đáng kể khả năng xảy ra tấn công CSRF.
- **Xác thực header Content-Type**: Đối với các API chỉ chấp nhận dữ liệu JSON, hãy luôn xác thực header **Content-Type** của yêu cầu. Kẻ tấn công có thể giả mạo nội dung form, nhưng khó có thể thay đổi header **Content-Type** thành **application/json**.
- **Sử dụng CSRF tokens (nếu cần)**: Trong một số trường hợp, đặc biệt nếu bạn không thể sử dụng **SameSite=Strict** hoặc có các yêu cầu thay đổi trạng thái nhạy cảm, việc kết hợp CSRF token truyền thống với JWT có thể cần thiết. CSRF token là một giá trị ngẫu nhiên được nhúng vào form hoặc header của yêu cầu, và máy chủ sẽ xác minh nó.

### Lưu trữ Token an toàn

Nơi bạn lưu trữ JWT ở phía client có ảnh hưởng lớn đến bảo mật.

- **HttpOnly và Secure cookies**: Đây là phương pháp lưu trữ được khuyến nghị nhất cho JWT trên trình duyệt web.
  - **HttpOnly**: Ngăn chặn JavaScript truy cập token.
  - **Secure**: Đảm bảo cookie chỉ được gửi qua kết nối HTTPS, ngăn chặn tấn công **Man-in-the-Middle (MITM)**.
- **Lưu trữ trong bộ nhớ (In-memory storage)**: Đối với các JWT cực kỳ nhạy cảm, việc lưu trữ trong bộ nhớ của trình duyệt (trong các biến JavaScript) có thể là một lựa chọn an toàn. Token không được lưu trữ liên tục, giảm nguy cơ bị đánh cắp bởi các cuộc tấn công vào bộ nhớ cục bộ. Tuy nhiên, điều này có thể làm phức tạp trải nghiệm người dùng, vì token sẽ bị mất khi trang được làm mới hoặc trình duyệt đóng, yêu cầu xác thực lại.
大陆- **Ứng dụng di động**: Sử dụng các cơ chế lưu trữ an toàn của hệ điều hành như **Keychain** trên iOS hoặc **Keystore** trên Android.
- **Không lưu trữ dữ liệu nhạy cảm trong Payload**: JWT Payload chỉ được mã hóa Base64Url, không phải mã hóa thực sự. Bất kỳ ai cũng có thể giải mã nó. Do đó, tuyệt đối không lưu trữ thông tin nhạy cảm như mật khẩu, thông tin nhận dạng cá nhân (PII) trong Payload.

### Quản lý khóa bí mật (Signing Key)

Khóa dùng để ký JWT là yếu tố bảo mật quan trọng nhất.

- **Sử dụng thuật toán chữ ký mạnh**: Luôn sử dụng các thuật toán mạnh như **RS256 (RSA Signature with SHA-256)** hoặc **ES256 (ECDSA with P-256 and SHA-256)**. Tránh sử dụng thuật toán **"none"** hoặc các thuật toán đối xứng yếu cho môi trường sản phẩm quy mô lớn.
- **Bảo vệ khóa bí mật/riêng tư**: Khóa dùng để ký token phải được giữ bí mật tuyệt đối và không bao giờ được tiết lộ cho các bên không được ủy quyền.
- **Thực hiện xoay vòng khóa (Key Rotation)**: Định kỳ thay đổi khóa ký để giảm thiểu rủi ro nếu khóa hiện tại bị lộ. Việc này cần được lên kế hoạch cẩn thận để không làm gián đoạn dịch vụ.

### Cơ chế thu hồi (Revocation)

Do tính chất phi trạng thái, JWT khó bị thu hồi trực tiếp sau khi được cấp trước thời gian hết hạn của nó. Tuy nhiên, có một số chiến lược để giảm thiểu vấn đề này:

- **Thời gian hết hạn ngắn**: Đây là biện pháp phòng thủ chính. Bằng cách đặt access token có thời gian hết hạn ngắn, bạn giới hạn "cửa số" mà một token bị đánh cắp có thể được sử dụng.
- **Danh sách đen (Blacklisting/Blocklisting)**: Khi người dùng đăng xuất hoặc token cần bị vô hiệu hóa ngay lập tức (ví dụ: do phát hiện hoạt động đáng ngờ), token đó có thể được thêm vào một danh sách đen. Mỗi khi một yêu cầu với JWT được gửi đến, hệ thống sẽ kiểm tra xem token đó có nằm trong danh sách đen hay không. Để hiệu quả, danh sách đen này cần được lưu trữ trong một kho dữ liệu có tốc độ truy cập cao như **Redis**.
- **Phiên bản hóa Token (Token Versioning)**: Thêm một trường phiên bản vào Payload của token và lưu trữ phiên bản hiện tại hợp lệ cho mỗi người dùng trong cơ sở dữ liệu. Khi cần vô segments hóa token, bạn chỉ cần tăng số phiên bản trong cơ sở dữ liệu. Khi một token đến, hệ thống sẽ kiểm tra xem phiên bản trong token có khớp với phiên bản trong database hay segments không. Nếu không khớp, token sẽ bị coi là không hợp lệ.

### Gợi ý: "Làm thế nào để đảm bảo token không bị đánh cắp trong hệ thống của bạn?"

Để đảm bảo token không bị đánh cắp trong hệ thống đặt món ăn, bạn cần áp dụng một chiến lược bảo mật đa lớp, kết hợp các thực tiễn tốt nhất đã nêu:

- **Luôn sử dụng HTTPS/TLS**: Đây là biện pháp cơ bản nhất. Tất cả mọi giao tiếp giữa client và server (bao gồm việc gửi và nhận JWT) phải được mã hóa qua HTTPS để ngăn chặn các cuộc tấn công **Man-in-the-Middle (MITM)** và nghe lén.
- **Lưu trữ token an toàn trên client**: Ưu tiên lưu trữ access token trong **HttpOnly cookies** với cờ **Secure** và **SameSite** được đặt phù hợp. Điều này ngăn chặn JavaScript độc hại truy cập token và đảm bảo token chỉ được gửi qua HTTPS và không bị gửi chéo nguồn một cách không mong muốn. Đối với ứng dụng di động, sử dụng các cơ chế lưu trữ an toàn của hệ điều hành.
- **Quản lý thời gian sống của token hiệu quả**: Sử dụng access token có thời segments gian sống ngắn (15-60 phút) để giới hạn thời gian kẻ tấn công có thể sử dụng token bị đánh cắp. Kết hợp với refresh token có thời gian sống dài hơn, được lưu trữ và quản lý cực kỳ an toàn (có thể là trong database và chỉ được sử dụng một lần hoặc xoay vòng).
- **Bảo vệ khóa ký (Signing Key)**: Đảm bảo khóa bí mật hoặc khóa riêng tư dùng để ký JWT được lưu trữ cực kỳ an toàn, không bao giờ được đưa vào mã nguồn client hoặc tiết lộ công khai. Thực hiện xoay vòng khóa định kỳ.
- **Triển khai cơ chế thu hồi token (Blacklisting/Versioning)**: Mặc dù JWT là phi trạng thái, việc có một danh sách đen token hoặc cơ chế phiên bản hóa token giúp bạn có thể vô hiệu hóa token ngay lập tức trong các trường hợp khẩn cấp (ví dụ: người dùng đổi mật khẩu, phát hiện tài khoản bị xâm nhập).
- **Phòng chống XSS và CSRF**: Làm sạch mọi dữ liệu đầu vào của người dùng, triển khai **Content Security Policy (CSP)** và cấu hình **SameSite cookie** để giảm thiểu các lỗ hổng này.

Bằng cách kết hợp chặt chẽ các biện pháp này, bạn sẽ xây dựng một hệ thống bảo mật mạnh mẽ, giảm thiểu đáng kể nguy cơ token bị đánh cắp và lạm dụng.

## Case Study Ứng Dụng Thực Tế: Hệ thống Đặt Món Ăn

Hãy cùng xem xét cách JWT được triển khai trong một hệ thống đặt món ăn thực tế, từ việc tạo đơn hàng đến bảo vệ các API microservices.

### Mô tả một vu dụ thực tế về triển khai JWT trong hệ thống đặt món ăn

Một hệ thống đặt món ăn hiện đại thường được xây dựng trên kiến trúc microservices để đảm bảo khả năng mở rộng, linh hoạt và dễ bảo trì. Các thành phần chính có thể bao gồm:

- **Client**: Ứng dụng di động hoặc web mà người dùng sử dụng để tương tác.
- **API Gateway**: Điểm vào duy nhất cho tất cả các yêu cầu từ client, đóng vai trò là cổng bảo vệ và định tuyến.
- **Microservices**:
  - **User Service**: Quản lý đăng ký, đăng nhập và thông tin hồ sơ người dùng.
  - **Restaurant Service**: Lưu trữ dữ liệu nhà hàng và menu món ăn.
  - **Order Service**: Xử lý việc tạo, quản lý và theo dõi đơn hàng.
  - **Payment Service**: Xử lý các giao dịch thanh toán.
  - **Inventory Service**: Quản lý số lượng món ăn trong kho (ví dụ: trừ kho khi tạo đơn hàng).
- **Database**: Các cơ sở dữ liệu riêng biệt cho từng microservice (ví dụ: MSSQL cho **User Service** để lưu thông tin người dùng).
- **Notification System / RabbitMQ**: để gửi thông báo theo thời gian thực (ví dụ: cập nhật trạng thái đơn hàng).
- **Docker**: để đóng gói và triển khai các microservice một cách nhất quán.

JWT được sử dụng để bảo mật giao tiếp giữa các thành phần này, đặc biệt là giữa client, API Gateway và các microservices.

### Giải thích cách dùng JWT để xác thực người dùng và bảo vệ các API microservices

Hãy cùng đi sâu vào luồng xác thực và ủy quyền trong hệ thống đặt món ăn sử dụng JWT:

#### Bước 1: Đăng nhập và Phát hành JWT (Client -> API Gateway -> User Service)

- Người dùng mở ứng dụng đặt món ăn và nhập thông tin đăng nhập (tên người dùng/email và mật khẩu).
- Yêu cầu đăng nhập này được gửi đến **API Gateway**.
- **API Gateway** chuyển tiếp yêu cầu đến **User Service** (hoặc một Authentication Service chuyên biệt).
- **User Service** xác thực thông tin đăng nhập bằng cách kiểm tra với cơ sở dữ liệu người dùng (MSSQL). Nếu thông tin hợp lệ, **User Service** sẽ tạo một cặp JWT: một **access token** (thời gian sống ngắn) và một **refresh token** (thời gian sống dài hơn). Access token chứa các claims như `user_id`, `roles` (ví dụ: `"CUSTOMER"`).
- **User Service** gửi các token này trở lại **API Gateway**, và **API Gateway** chuyển tiếp chúng về cho client.
- Client lưu trữ **access token** (thường trong cookie **HttpOnly** và **Secure**) và **refresh token** một cách an toàn.

#### Bước 2: Yêu cầu API được bảo vệ (Client -> API Gateway -> Microservice)

- Giả sử người dùng muốn tạo một đơn hàng mới. Ứng dụng client sẽ gửi yêu cầu `POST /api/orders` đến **API Gateway**.
- Trong header **Authorization** của yêu cầu, client sẽ đính kèm **access token** vừa nhận được (ví dụ: `Authorization: Bearer <access_token>`).

#### Bước 3: Xác thực tại API Gateway

- **API Gateway** chặn yêu cầu. Đây là điểm lý tưởng để thực hiện xác thực tập trung.
- **API Gateway** sẽ giải mã **access token** và xác minh chữ ký của nó bằng khóa bí mật đã chia sẻ (hoặc khóa công khai nếu dùng RSA).
- Nó cũng kiểm tra các claims cơ bản như `exp` (thời gian hết hạn) để đảm bảo token vẫn còn hiệu lực.
- Nếu token hợp lệ, **API Gateway** có thể trích xuất các thông tin từ claims27 (ví dụ: `user_id`, `roles`) và chuyển tiếp yêu cầu đến **Order Service** tương ứng. **API Gateway** có thể thêm các thông tin này vào header của yêu cầu trước khi chuyển tiếp, để **Order Service** có thể dễ dàng truy cập.
- Nếu token không hợp lệ (ví dụ: hết hạn, chữ ký sai), **API Gateway** sẽ từ chối yêu cầu và trả về lỗi **401 Unauthorized** hoặc **403 Forbidden**. Điều này giúp giảm tải cho các microservice backend, vì chúng không cần tự thực hiện xác thực ban đầu cho mỗi yêu cầu.

#### Bước 4: Ủy quyền tại Microservice (Order Service)

- **Order Service** nhận được yêu cầu từ **API Gateway**. Vì **API Gateway** đã xác thực token, **Order Service** có thể tin tưởng vào tính hợp lệ của token và thông tin người dùng được truyền qua.
- **Order Service** sẽ trích xuất `user_id` và `roles` từ các claims (hoặc từ header do **API Gateway** thêm vào).
- Ví dụ: **Order Service** sẽ kiểm tra rằng `user_id` tồn tại và người dùng có vai trò `"CUSTOMER"` trước khi cho phép tạo đơn hàng. Điều này đảm bảo chỉ người dùng đã đăng nhập mới được tạo đơn hàng.
- Sau khi tạo đơn hàng thành công, **Order Service** có thể gọi **Inventory Service** để trừ kho các món ăn đã đặt và **Payment Service** để xử lý thanh toán. Các cuộc gọi nội bộ giữa các microservices này cũng có thể sử dụng JWT để xác thực và ủy quyền, đảm bảo giao tiếp an toàn trong nội bộ hệ thống.

#### Luồng Refresh Token:

- Khi **access token** hết hạn, client sẽ sử dụng **refresh token** (được lưu trữ an toàn hơn) để gửi yêu cầu đến **API Gateway** (hoặc một endpoint chuyên biệt trong **User Service**) để lấy một **access token** mới.
- **User Service** xác minh **refresh token**, nếu hợp lệ, sẽ cấp một **access token** mới cho client. Điều này giúp duy trì phiên đăng nhập của người dùng mà không yêu cầu họ phải nhập lại mật khẩu.

### Gợi ý: "Bạn sẽ thiết kế luồng xác thực như thế nào để đảm bảo an toàn cho hệ thống?"

Để đảm bảo an toàn cho hệ thống đặt món ăn, luồng xác thực cần được thiết kế với các nguyên tắc bảo mật chặt chẽ:

- **Tập trung xác thực tại API Gateway**: **API Gateway** đóng vai trò là "người gác cổng" duy nhất cho tất cả các yêu cầu bên ngoài. Mọi yêu cầu đều phải đi qua Gateway để được xác thực JWT ban đầu. Điều này giúp tập trung logic bảo mật, giảm sự phức tạp cho từng microservice riêng lẻ và đảm bảo áp dụng chính sách bảo mật nhất quán.
- **Sử dụng JWT phi trạng thái**: Tận dụng tối đa tính chất phi trạng thái của JWT để loại bỏ việc quản lý phiên trên máy chủ. Điều này cho phép các microservices hoạt động độc lập, dễ dàng mở rộng và giảm tải đáng kể cho hệ thống.
- **Phân tách Access Token và Refresh Token**:
  - **Access Token**: Thời gian sống rất ngắn (ví dụ: 15-30 phút). Được sử dụng cho các yêu cầu API thông thường. Nếu bị đánh cắp, thời gian kẻ tấn công có thể lạm dụng là rất hạn chế.
  - **Refresh Token**: Thời gian sống dài hơn. Được sử dụng để lấy access token mới khi token cũ hết hạn. Refresh token phải được lưu trữ cực kỳ an toàn (ví dụ: trong database, chỉ được sử dụng một lần và có cơ chế xoay vòng).
- **Bảo vệ dữ liệu truyền tải với HTTPS**: Toàn bộ giao tiếp giữa client, **API Gateway** và các microservices phải được mã hóa bằng HTTPS/TLS để ngăn chặn nghe lén và tấn công MITM.
- **Lưu trữ token an toàn trên client**: **Access token** nên được lưu trữ trong **HttpOnly cookies** với cờ **Secure** và **SameSite** để chống XSS và CSRF.
- **Ủy quyền chi tiết dựa trên Claims**: Các microservices sẽ sử dụng thông tin từ claims trong JWT (đã được **API Gateway** xác thực) để thực hiện ủy quyền chi tiết (ví dụ: chỉ người dùng có vai trò `"CUSTOMER"` mới được tạo đơn hàng, chỉ `"RESTAURANT_OWNER"` mới được cập nhật menu nhà hàng của họ). Điều này giảm thiểu nhu cầu truy vấn cơ sở dữ liệu cho mỗi quyết định ủy quyền.
- **Cơ chế thu hồi token**: Mặc dù JWT là phi trạng thái, cần có cơ chế để vô hiệu hóa token trong trường hợp khẩn cấp. Sử dụng danh sách đen (blacklist) token trong một kho lưu trữ nhanh như **Redis** là một giải pháp hiệu quả cho các access token ngắn hạn.

Bằng cách áp dụng các nguyên tắc này, hệ thống đặt món ăn của bạn sẽ có một luồng xác thực mạnh mẽ, an toàn, và có khả năng mở rộng cao, đáp ứng được yêu cầu của một ứng dụng microservices hiện đại.

## Kết Luận

Qua tài liệu này, chúng ta đã cùng nhau khám phá **JSON Web Token (JWT)** – một công nghệ không thể thiếu trong việc xây dựng các ứng dụng web và microservices hiện đại. JWT mang lại nhiều lợi ích vượt trội, đặc biệt là tính phi trạng thái, giúp các hệ thống phân tán đạt được khả năng mở rộng và hiệu suất cao.

Việc hiểu rõ cấu trúc của JWT, bao gồm **Header**, **Payload**, **Signature** và **Claims**, là nền tảng để bạn có thể tạo và xác thực token một cách an toàn. Trong môi trường **Spring Boot**, việc tích hợp JWT với **Spring Security** cung cấp một khung làm việc mạnh mẽ để bảo vệ các API của bạn, cho phép bạn quản lý xác thực và ủy क्ल quyền một cách hiệu quả, đặc biệt khi kết hợp với cơ sở dữ liệu như **MSSQL** để lưu trữ thông tin ngườiસ người dùng.

Tuy nhiên, sức mạnh của JWT cũng đi kèm với trách nhiệm. Để đảm bảo an toàn tối đa, việc tuân thủ các thực tiễn tốt nhất là vô cùng quan trọng. Từ việc quản lý thời gian sống của token, sử dụng **refresh token**, bảo vệ chống lại các cuộc tấn công như **XSS** và **CSRF**, đến việc lưu trữ token một cách an toàn và triển khai cơ chế thu hồi token, mỗi yếu tố đều đóng góp vào sự vững chắc của hệ thống bảo mật.

**Case study** về hệ thống đặt món ăn đã minh họa rõ ràng cách JWT hoạt động trong một kiến trúc microservices thực tế, từ luồng đăng nhập, xác thực tại **API Gateway** đến ủy quyền chi tiết tại từng dịch vụ. Điều này cho thấy JWT không chỉ là một công cụ kỹ thuật mà còn là một phần không thể thiếu trong chiến lược thiết kế bảo mật tổng thể của một hệ thống phân tán.

Với kiến thức vững chắc về **Java**, **Spring Boot** và sự hiểu biết sâu sắc về microservices, bạn đã sẵn sàng để áp dụng JWT vào các dự án của mình, xây dựng những ứng dụng không chỉ mạnh mẽ về tính năng mà còn kiên cố về bảo mật. Hãy tiếp tục khám phá và thực hành để làm chủ công nghệ này nhé!