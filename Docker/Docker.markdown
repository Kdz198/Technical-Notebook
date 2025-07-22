# Báo cáo Chuyên sâu về Docker: Từ Khái niệm đến Triển khai Thực tế với Java Spring Boot và Các Phương pháp Tốt nhất

## 1. Giới thiệu về Docker

### 1.1. Docker là gì và vai trò trong Chu trình Phát triển Phần mềm (SDLC)

Docker là một nền tảng mã nguồn mở mạnh mẽ, cách mạng hóa cách các ứng dụng được phát triển, triển khai và quản lý. Nền tảng này cho phép các nhà phát triển và quản trị hệ thống dễ dàng xây dựng, kiểm thử, triển khai và quản lý ứng dụng bằng cách đóng gói chúng vào các môi trường cô lập, được gọi là container. Container là một đơn vị phần mềm độc lập, chứa tất cả những gì cần thiết để chạy một ứng dụng: mã nguồn, thời gian chạy (runtime), thư viện hệ thống, công cụ hệ thống và cài đặt. Docker cung cấp một lớp trừu tượng và tự động hóa ảo hóa dựa trên Linux, cho phép ứng dụng "xây dựng, vận chuyển, chạy bất kỳ ứng dụng nào ở bất kỳ đâu".

Trong Chu trình Phát triển Phần mềm (SDLC), Docker đóng một vai trò trung tâm, cải thiện đáng kể hiệu quả và độ tin cậy ở mọi giai đoạn:

- **Phát triển**: Docker tạo môi trường phát triển riêng biệt, nhất quán và dễ chia sẻ giữa các thành viên trong nhóm. Điều này giải quyết triệt để vấn đề kinh điển "chạy trên máy tôi nhưng không chạy trên máy bạn". Bằng cách đảm bảo môi trường phát triển đồng nhất với môi trường sản xuất, Docker giúp tăng tốc độ thử nghiệm và giảm thiểu xung đột môi trường.

- **Triển khai**: Docker đóng gói ứng dụng cùng môi trường và các phụ thuộc của nó vào một container duy nhất. Điều này giúp việc triển khai trở nên linh hoạt và nhất quán trên mọi môi trường, từ máy tính cá nhân của nhà phát triển đến môi trường thử nghiệm, staging và sản xuất. Khả năng di động này giảm thiểu thời gian triển khai và đơn giản hóa quy trình.

- **Vận hành**: Docker hỗ trợ cách ly các ứng dụng với nhau, giúp theo dõi và quản lý chúng dễ dàng hơn, đồng thời tăng tốc độ khắc phục sự cố. Các container nhẹ và nhanh, cho phép chạy nhiều khối lượng công việc hơn trên cùng một phần cứng, tối ưu hóa việc sử dụng tài nguyên và giảm chi phí vận hành.

Việc Docker có khả năng duy trì sự nhất quán của môi trường là một yếu tố then chốt. Điều này không chỉ giới hạn ở môi trường phát triển cục bộ mà còn mở rộng ra toàn bộ SDLC. Bằng cách đóng gói ứng dụng với các phụ thuộc và cấu hình chính xác, Docker thực sự tiêu chuẩn hóa môi trường thực thi. Sự tiêu chuẩn hóa này là vô cùng quan trọng đối với các quy trình Tích hợp Liên tục/Phân phối Liên tục (CI/CD), nơi các bài kiểm tra và triển khai tự động phụ thuộc rất nhiều vào các môi trường có thể dự đoán được. Docker hoạt động như một lớp trừu tượng thời gian chạy phổ quát, loại bỏ sự khác biệt về hệ điều hành và cơ sở hạ tầng bên dưới, cho phép các ứng dụng hoạt động giống hệt nhau bất kể chúng chạy ở đâu. Điều này giúp giảm đáng kể chi phí gỡ lỗi liên quan đến sự không khớp môi trường và tăng tốc toàn bộ quy trình phân phối phần mềm.

### 1.2. Lịch sử hình thành và phát triển của Docker

Docker được tạo ra bởi Solomon Hykes và Sebastien Pahl vào năm 2010 và chính thức ra mắt vào năm 2011. Ban đầu, dự án này là một phần nội bộ của dotCloud, một công ty cung cấp nền tảng dưới dạng dịch vụ (PaaS), với mục tiêu đơn giản hóa việc triển khai ứng dụng trên nền tảng đám mây của họ.

Sự phát triển của công nghệ container đã thúc đẩy sự ra mắt công khai của Docker vào năm 2013. Ngay lập tức, Docker đã thu hút sự chú ý đáng kể từ cộng đồng công nghệ nhờ tính tiện ích và khả năng di động hóa ứng dụng vượt trội của nó. Khả năng đóng gói ứng dụng và môi trường của chúng một cách dễ dàng đã giải quyết một vấn đề nhức nhối trong ngành phát triển phần mềm.

Vào tháng 2 năm 2016, Docker giới thiệu sản phẩm thương mại đầu tiên của mình, Docker Enterprise Edition. Đến năm 2020, Docker đã khẳng định vị thế là lựa chọn toàn cầu cho các container, thống nhất dưới một nền tảng đơn giản để sử dụng với giao diện dòng lệnh (CLI) và một Daemon. Hiện tại, cộng đồng mã nguồn mở Docker rất lớn mạnh, với hơn 3.300 người đóng góp.

Quỹ đạo phát triển của Docker, từ một công cụ nội bộ giải quyết các vấn đề triển khai của dotCloud đến một tiêu chuẩn công nghiệp được áp dụng rộng rãi, là một minh chứng cho sức mạnh của sự đơn giản hóa. Thành công của Docker không chỉ đến từ sự đổi mới kỹ thuật (công nghệ container đã tồn tại trước đó) mà còn từ việc nó đã đơn giản hóa công nghệ container và làm cho nó dễ tiếp cận hơn thông qua một giao diện CLI thân thiện với người dùng và một nền tảng rõ ràng. Sự dễ sử dụng này, kết hợp với khả năng giải quyết các vấn đề triển khai phổ biến, đã thúc đẩy nó từ một công cụ nội bộ chuyên biệt trở thành một dự án mã nguồn mở được áp dụng rộng rãi và cuối cùng là một sản phẩm thương mại. Sự chấp nhận nhanh chóng từ cộng đồng và việc thương mại hóa sau đó cho thấy một nhu cầu thị trường mạnh mẽ đối với việc đóng gói ứng dụng theo cách tiêu chuẩn hóa và di động. Hành trình của Docker từ công cụ nội bộ của dotCloud đến dự án CNCF đã tốt nghiệp (thông qua containerd) và một doanh nghiệp thương mại thể hiện sức mạnh của sự trừu tượng hóa và trải nghiệm người dùng trong việc thúc đẩy việc áp dụng công nghệ.

### 1.3. So sánh Docker và Máy ảo (Virtual Machine - VM)

Docker và Máy ảo (VM) là hai công nghệ ảo hóa được sử dụng rộng rãi trong triển khai ứng dụng, nhưng chúng có những khác biệt cơ bản về kiến trúc, hiệu năng, tài nguyên, tính di động và bảo mật.

**Kiến trúc**:

- **Máy ảo (VM)**: VM là một bản sao kỹ thuật số của máy vật lý, mô phỏng các thành phần phần cứng như CPU, bộ nhớ và card mạng. Mỗi VM chạy một hệ điều hành khách (Guest OS) hoàn chỉnh riêng biệt, bao gồm kernel riêng của nó, trên một hệ điều hành máy chủ (Host OS). Điều này tạo ra một lớp cách ly mạnh mẽ giữa các VM.

- **Docker (Container)**: Container Docker sử dụng các phiên bản không gian người dùng (user-space instances) được gọi là container. Chúng lưu trữ trên một máy chủ vật lý duy nhất và chia sẻ cùng một hệ điều hành máy chủ (cụ thể là kernel của Host OS). Docker Engine hỗ trợ ảo hóa trong Docker, cung cấp khả năng điều phối giữa các container đang chạy và hệ điều hành cơ sở.

**Hiệu năng & Tài nguyên**:

- **Máy ảo (VM)**: Tiêu tốn nhiều tài nguyên hơn vì mỗi VM phải chạy một hệ điều hành khách đầy đủ, bao gồm kernel và các thư viện hệ thống riêng. Việc khởi động VM cũng mất nhiều thời gian hơn.

- **Docker (Container)**: Nhẹ hơn và nhanh hơn VM đáng kể vì chúng dùng chung hệ điều hành host và không cần chia tách process và bộ nhớ như VM. Container Docker chỉ chứa các thành phần phụ thuộc của ứng dụng và yêu cầu tài nguyên theo nhu cầu từ kernel, dẫn đến việc sử dụng ít tài nguyên hệ thống hơn so với VM. Điều này cho phép chạy nhiều container hơn trên cùng một máy chủ vật lý.

**Tính di động**:

- **Máy ảo (VM)**: VM được tách biệt khỏi hệ điều hành và có thể chạy trên bất kỳ phần cứng nào có hypervisor tương thích. Tuy nhiên, việc di chuyển VM thường liên quan đến việc sao chép toàn bộ hệ điều hành khách, có thể nặng và chậm.

- **Docker (Container)**: Container độc lập với hệ điều hành và có thể chạy ứng dụng trong mọi môi trường có Docker Engine. Container nhẹ, khởi động và dừng trong thời gian rất ngắn, dễ dàng triển khai và di chuyển giữa các máy chủ.

**Bảo mật**:

- **Máy ảo (VM)**: Cung cấp khả năng cách ly cao hơn do mỗi VM chạy một hệ điều hành riêng, tạo thêm một tầng cách ly mạnh mẽ. Do đó, VM phù hợp cho các ứng dụng cần nhiều đặc quyền và bảo mật nghiêm ngặt.

- **Docker (Container)**: Vì chia sẻ kernel với hệ điều hành host, có rủi ro nếu có lỗ hổng trong kernel, vì một lỗ hổng có thể ảnh hưởng đến tất cả các container trên cùng một host. Tuy nhiên, Docker cũng cung cấp nhiều biện pháp kiểm soát bảo mật nâng cao, và việc cấp quyền truy cập root cho ứng dụng trong container không được khuyến khích.

**Trường hợp sử dụng**:

- **Máy ảo (VM)**: Cần thiết nếu các ứng dụng hoặc dịch vụ yêu cầu chạy trên các hệ điều hành khác nhau (ví dụ: chạy ứng dụng Windows trên Host Linux). Thích hợp cho việc ảo hóa toàn bộ máy chủ vật lý hoặc khi cần mức độ cách ly cao nhất.

- **Docker (Container)**: Tốt nhất khi chạy các ứng dụng có yêu cầu tài nguyên gọn nhẹ hoặc kiến trúc vi dịch vụ (microservices). Phù hợp cho môi trường hạ tầng vật lý phân tán (bao gồm máy chủ đám mây), chu kỳ triển khai nhanh, và yêu cầu khả năng điều chỉnh quy mô nhanh chóng. Các container Docker cũng có thể chạy trên các máy ảo, tận dụng lợi ích của cả hai công nghệ.

Sự lựa chọn giữa Docker và VM (hoặc sự kết hợp của cả hai) thường phụ thuộc vào các yêu cầu cụ thể của ứng dụng về bảo mật, hiệu suất và sử dụng tài nguyên. Đây là một sự đánh đổi cơ bản giữa mức độ cách ly và hiệu quả. Mức độ cách ly cao hơn (VM) đi kèm với chi phí tài nguyên tăng lên và thời gian khởi động chậm hơn. Ngược lại, hiệu quả cao hơn (Docker) đi kèm với ranh giới cách ly giảm, khiến các lỗ hổng kernel trở thành rủi ro chung trên các container trên cùng một host. Đối với các kiến trúc microservices, nơi nhiều dịch vụ nhỏ, cô lập cần chạy hiệu quả, mô hình của Docker thường được ưu tiên. Đối với các ứng dụng nhạy cảm cao yêu cầu cách ly tối đa, VM có thể được chọn, hoặc các container Docker có thể được chạy bên trong VM để tận dụng cả hai lợi ích. Điều này nhấn mạnh khái niệm "bảo mật phân lớp" và "hiệu quả phân lớp" trong các kiến trúc đám mây gốc (cloud-native).

**Bảng: So sánh Docker và Máy ảo**

| **Tiêu chí** | **Docker (Container)** | **Máy ảo (Virtual Machine - VM)** |
|--------------|-----------------------|-----------------------------------|
| **Kiến trúc** | Chia sẻ kernel của Host OS. Chỉ đóng gói ứng dụng và các phụ thuộc. | Mỗi VM có Guest OS riêng (bao gồm kernel). Mô phỏng phần cứng vật lý. |
| **Hiệu năng** | Khởi động nhanh (giây), hiệu năng gần như native. | Khởi động chậm (phút), hiệu năng thấp hơn native do overhead của Guest OS. |
| **Tài nguyên** | Nhẹ, tiêu thụ ít tài nguyên (CPU, RAM). | Nặng, tiêu thụ nhiều tài nguyên (CPU, RAM) cho mỗi Guest OS. |
| **Tính di động** | Rất cao, dễ dàng di chuyển giữa các môi trường. | Cao, nhưng nặng hơn và chậm hơn khi di chuyển. |
| **Cách ly** | Cách ly ở cấp độ tiến trình (OS-level virtualization). Rủi ro chia sẻ kernel. | Cách ly ở cấp độ phần cứng ảo hóa. Mức độ bảo mật cao hơn. |
| **Kích thước** | Rất nhỏ (MB). | Lớn (GB). |
| **Trường hợp sử dụng** | Microservices, CI/CD, phát triển ứng dụng, tối ưu hóa tài nguyên. | Chạy nhiều hệ điều hành khác nhau trên cùng một phần cứng, ứng dụng yêu cầu cách ly cao. |

### 1.4. Lợi ích chính khi sử dụng Docker

Việc áp dụng Docker mang lại nhiều lợi ích đáng kể cho quá trình phát triển, triển khai và vận hành phần mềm:

- **Cô lập môi trường (Environment Isolation)**: Docker đóng gói ứng dụng và tất cả các phụ thuộc của nó vào một container độc lập. Điều này đảm bảo rằng ứng dụng sẽ chạy nhất quán, bất kể môi trường cơ sở là gì, loại bỏ vấn đề "nó chạy trên máy tôi". Các container được cách ly với nhau, ngăn chặn xung đột giữa các ứng dụng hoặc phiên bản thư viện khác nhau.

- **Khả năng di động (Portability)**: Một Docker image được xây dựng có thể chạy trên bất kỳ hệ thống nào đã cài đặt Docker Engine, từ máy tính xách tay của nhà phát triển đến máy chủ vật lý, máy ảo hoặc các nhà cung cấp dịch vụ đám mây. Điều này giúp di chuyển ứng dụng mượt mà qua các môi trường phát triển, thử nghiệm và sản xuất mà không cần thay đổi mã nguồn hay cấu hình.

- **Tăng tốc độ triển khai (Accelerated Deployment)**: Docker đơn giản hóa quy trình xây dựng, kiểm thử và triển khai ứng dụng. Với các container được đóng gói sẵn, việc thiết lập môi trường và chạy ứng dụng trở nên nhanh chóng hơn nhiều, giảm thiểu thời gian đưa sản phẩm ra thị trường. Các tổ chức sử dụng Docker cho thấy tốc độ vận chuyển phần mềm nhanh hơn trung bình 7 lần so với những người không sử dụng.

- **Quản lý phụ thuộc (Dependency Management)**: Docker giải quyết sự phức tạp của việc quản lý phụ thuộc bằng cách đóng gói tất cả các thư viện, framework và cấu hình cần thiết cùng với ứng dụng. Điều này đảm bảo rằng ứng dụng luôn có môi trường chính xác để chạy, tránh các lỗi do thiếu hoặc không tương thích phụ thuộc.

- **Tiết kiệm tài nguyên (Resource Efficiency)**: Do container chia sẻ kernel của hệ điều hành host thay vì chạy một Guest OS đầy đủ như VM, chúng tiêu thụ ít tài nguyên CPU và bộ nhớ hơn đáng kể. Điều này cho phép chạy nhiều ứng dụng hơn trên cùng một máy chủ, cải thiện khả năng tận dụng phần cứng và giảm chi phí cơ sở hạ tầng.

- **Tiêu chuẩn hóa quy trình vận hành (Standardized Operations)**: Docker cung cấp một cách tiếp cận đồng nhất để đóng gói và triển khai ứng dụng, giúp việc triển khai, xác định vấn đề và khắc phục trở nên dễ dàng hơn. Điều này đặc biệt hữu ích trong các kiến trúc microservices, nơi mỗi dịch vụ có thể chạy độc lập trong một container và giao tiếp với nhau.

## 2. Các Khái niệm Cốt lõi của Docker

### 2.1. Docker Image: Định nghĩa, vai trò, cách tạo (Dockerfile), Docker Hub

**Định nghĩa**: Docker Image là một mẫu (template) chỉ đọc chứa tất cả các phần cần thiết để chạy một ứng dụng, bao gồm mã nguồn, thư viện, các phụ thuộc và cấu hình hệ thống. Nó giống như một "ảnh chụp nhanh" hoặc "kế hoạch chi tiết" cho container.

**Vai trò**: Image là nền tảng để tạo ra các container. Từ một image ban đầu, có thể tạo ra nhiều container mà chỉ tốn rất ít dung lượng ổ đĩa do các container chia sẻ các lớp chỉ đọc của image và chỉ tạo thêm một lớp có thể ghi (container-layer) cho các thay đổi. Image có tính bất biến; một khi đã tạo, nó không thể sửa đổi. Mọi thay đổi cần tạo một image mới.

**Cách tạo (Dockerfile)**:

- **docker commit (Không khuyến nghị)**: Tạo một container, chạy các lệnh cần thiết bên trong nó, sau đó sử dụng lệnh docker commit để tạo image mới từ trạng thái của container đó. Phương pháp này không được khuyến nghị vì nó không minh bạch và khó tái tạo.

- **Dockerfile (Khuyến nghị)**: Cách phổ biến và được khuyến nghị nhất là viết một Dockerfile. Dockerfile là một tệp văn bản chứa các hướng dẫn từng bước để xây dựng image. Mỗi lệnh trong Dockerfile tạo ra một lớp (layer) mới trong image, và các lớp này được xếp chồng lên nhau.

**Docker Hub**: Docker Hub là một dịch vụ do Docker cung cấp, hoạt động như một kho lưu trữ công cộng lớn nhất thế giới cho các Docker Image. Nó cho phép người dùng tìm kiếm, chia sẻ (push/pull) các container image. Các tính năng chính của Docker Hub bao gồm repositories (công khai và riêng tư), Official Images (image chất lượng cao từ Docker), Publisher Images (từ các nhà cung cấp khác), và khả năng tự động tạo image từ GitHub/Bitbucket (Builds). Việc đăng nhập vào Docker Hub (docker login) là cần thiết để push/pull các image riêng tư hoặc quản lý repositories.

**Bảng: So sánh Docker Image và Container**

| **Tiêu chí** | **Docker Image** | **Docker Container** |
|--------------|------------------|---------------------|
| **Định nghĩa** | Mẫu chỉ đọc, bản thiết kế chứa hướng dẫn để tạo container. | Phiên bản thời gian chạy (runtime instance) của một image. |
| **Nguồn gốc** | Tạo từ Dockerfile (mã nguồn, phụ thuộc, thư viện). | Tạo trực tiếp từ một Docker Image. |
| **Thành phần** | Các lớp chỉ đọc (read-only layers). | Các lớp chỉ đọc của image cộng với một lớp đọc-ghi bổ sung (writable layer) ở trên cùng. |
| **Khả năng biến đổi** | Bất biến (immutable) - không thể thay đổi sau khi tạo. | Có thể biến đổi (mutable) - có thể thay đổi trong thời gian hoạt động. |
| **Mục đích** | Lưu trữ cấu hình ứng dụng dưới dạng mẫu, để chia sẻ và tái sử dụng. | Chạy ứng dụng. |

### 2.2. Docker Container: Định nghĩa, mối quan hệ với Image, vòng đời của Container

**Định nghĩa**: Docker Container là một gói phần mềm duy nhất, độc lập, chứa tất cả các thành phần thiết yếu – như mã, thành phần phụ thuộc và thư viện – cần thiết để chạy mã ứng dụng mà không cần sử dụng đến thành phần phụ thuộc của máy chủ. Nó là một môi trường thời gian hoạt động (runtime environment) được cách ly nhẹ, có hệ thống tệp, cấu trúc thành phần phụ thuộc, quy trình và khả năng mạng riêng.

**Mối quan hệ với Image**: Container là một thực thể chạy của một Docker Image. Có thể hình dung Image là bản thiết kế hoặc khuôn mẫu, còn Container là sản phẩm được tạo ra từ bản thiết kế đó. Một Image có thể được sử dụng để tạo ra nhiều Container giống hệt nhau, đảm bảo tính nhất quán trong môi trường triển khai.

**Vòng đời của Container**: Một Docker Container trải qua nhiều trạng thái trong vòng đời của nó, từ lúc được tạo cho đến khi bị hủy bỏ. Các lệnh CLI cơ bản được sử dụng để quản lý các trạng thái này.

- **Create**: Tạo một container mới từ một image. Container chưa chạy. Lệnh: `docker create --name <container-name> <image-name>`.

- **Run**: Chạy một container từ một image. Nếu image chưa có, Docker sẽ tự động tải về. Lệnh này cũng có thể tạo container nếu chưa có. Lệnh: `docker run -it -d --name <container-name> <image-name> [command]`.

- **Pause/Unpause**: Tạm dừng hoặc tiếp tục các tiến trình bên trong container mà không dừng hẳn container. Lệnh: `docker pause <container-id/name>` và `docker unpause <container-id/name>`.

- **Start**: Khởi động một container đã dừng trước đó, giữ nguyên trạng thái. Lệnh: `docker start <container-id/name>`.

- **Stop**: Dừng một container đang chạy và các tiến trình bên trong nó một cách graceful. Lệnh: `docker stop <container-id/name>`.

- **Restart**: Khởi động lại một container. Lệnh: `docker restart <container-id/name>`.

- **Kill**: Buộc dừng một container ngay lập tức (không graceful). Lệnh: `docker kill <container-id/name>`.

- **Remove (Destroy)**: Xóa một container đã dừng. Không nên xóa container đang chạy. Lệnh: `docker rm <container-id/name>`.

### 2.3. Dockerfile: Cấu trúc, các lệnh phổ biến và thực hành tốt nhất

**Cấu trúc Dockerfile**: Dockerfile là một tệp văn bản chứa các hướng dẫn tuần tự mà Docker Engine đọc để xây dựng một Docker Image. Mỗi hướng dẫn trong Dockerfile tạo ra một lớp (layer) mới trong image. Các lớp này được xếp chồng lên nhau, và mỗi lớp là một delta thể hiện những thay đổi được áp dụng cho lớp trước đó. Tên tệp mặc định là `Dockerfile` (không có phần mở rộng), cho phép lệnh `docker build` chạy mà không cần cờ bổ sung.

**Các lệnh phổ biến**:

- **FROM `<image>[:<tag>]`**: Định nghĩa base image cho image của bạn. Đây là lệnh bắt buộc đầu tiên (sau chỉ thị cú pháp).

- **RUN `<command>`**: Thực thi bất kỳ lệnh nào trong một lớp mới trên đầu image hiện tại và commit kết quả. Thường dùng để cài đặt gói, tạo thư mục, v.v.

- **CMD `["executable", "param1", "param2"]`**: Cung cấp lệnh mặc định hoặc các đối số cho ENTRYPOINT khi container khởi động. Chỉ có một lệnh CMD cuối cùng được thực thi nếu có nhiều lệnh.

- **ENTRYPOINT `["executable", "param1", "param2"]`**: Định nghĩa lệnh chính sẽ được thực thi khi container khởi động. Khi kết hợp với CMD, ENTRYPOINT đặt lệnh chính và CMD cung cấp các tham số mặc định.

- **EXPOSE `<port> [<port>...]`**: Thông báo rằng container sẽ lắng nghe trên các cổng được chỉ định tại thời gian chạy. Đây chỉ là thông tin tài liệu và không tự động publish cổng.

- **VOLUME `["/path/to/volume"]`**: Tạo một điểm mount cho volume, cho phép lưu trữ dữ liệu bền vững bên ngoài lớp có thể ghi của container.

- **WORKDIR `/path/to/workdir`**: Đặt thư mục làm việc cho bất kỳ lệnh RUN, CMD, ENTRYPOINT, COPY và ADD nào theo sau nó trong Dockerfile. Nếu thư mục không tồn tại, nó sẽ được tạo tự động.

- **COPY `<src> <dest>`**: Sao chép các tệp hoặc thư mục mới từ `<src>` (trên host) và thêm chúng vào hệ thống tệp của container tại đường dẫn `<dest>`. COPY được khuyến nghị hơn ADD vì tính minh bạch.

- **ADD `<src> <dest>`**: Tương tự COPY, nhưng có thêm khả năng giải nén các tệp tar cục bộ và hỗ trợ URL từ xa. ADD chỉ nên dùng cho việc giải nén tệp tar cục bộ.

**Thực hành tốt nhất khi viết Dockerfile**:

- **Sử dụng Multi-stage Builds**: Để tạo ra các image nhỏ gọn và an toàn, loại bỏ các công cụ và phụ thuộc chỉ cần thiết cho quá trình build.

- **Chọn base image phù hợp**: Ưu tiên các image tối giản như alpine hoặc các biến thể slim (ví dụ: openjdk:17-jre-alpine) để giảm kích thước image và bề mặt tấn công.

- **Tối ưu hóa caching**: Sắp xếp các lệnh trong Dockerfile từ ít thay đổi nhất đến thường xuyên thay đổi nhất để tận dụng cache hiệu quả, tăng tốc độ build.

- **Tránh cài đặt các gói không cần thiết**: Giảm thiểu complexity, phụ thuộc, kích thước tệp và thời gian build.

- **Sử dụng COPY --from thay vì ADD**: COPY minh bạch hơn và ít có khả năng gây ra các vấn đề bảo mật không mong muốn.

- **Thiết lập user không có quyền root**: Chạy ứng dụng bên trong container bằng một người dùng không có quyền root để giảm thiểu rủi ro bảo mật.

- **Sử dụng .dockerignore file**: Loại trừ các tệp và thư mục không cần thiết khỏi build context để tăng tốc độ build và giảm kích thước image cuối cùng.

**Bảng: Các lệnh Dockerfile phổ biến**

| **Lệnh** | **Mô tả** | **Ví dụ** |
|----------|-----------|-----------|
| FROM | Định nghĩa base image cho image. | `FROM openjdk:17-jre-alpine` |
| RUN | Thực thi lệnh trong một lớp mới. | `RUN apt-get update && apt-get install -y curl` |
| CMD | Lệnh hoặc đối số mặc định khi container khởi động. | `CMD ["java", "-jar", "app.jar"]` |
| ENTRYPOINT | Lệnh chính sẽ được thực thi khi container khởi động. | `ENTRYPOINT ["java", "-jar", "/app.jar"]` |
| EXPOSE | Thông báo cổng mà container lắng nghe. | `EXPOSE 8080` |
| VOLUME | Tạo một điểm mount cho volume. | `VOLUME /app/logs` |
| WORKDIR | Đặt thư mục làm việc cho các lệnh tiếp theo. | `WORKDIR /app` |
| COPY | Sao chép tệp/thư mục từ host vào image. | `COPY target/app.jar /app/app.jar` |
| ADD | Tương tự COPY, có thêm tính năng giải nén tar/URL. | `ADD https://example.com/app.tar.gz /app/` |

### 2.4. Docker Registry: Vai trò, Docker Hub, Private Registry

**Vai trò**: Docker Registry là một dịch vụ lưu trữ và phân phối các Docker Image. Nó đóng vai trò trung tâm trong hệ sinh thái Docker, cho phép người dùng quản lý phiên bản, chia sẻ và kiểm soát quyền truy cập vào các image. Registry giúp giảm thời gian build bằng cách tập trung các image container và cho phép tải xuống các image nén chứa tất cả các thành phần ứng dụng.

**Docker Hub**: Đây là registry công cộng mặc định và lớn nhất do Docker cung cấp. Docker Hub cho phép người dùng tìm kiếm và chia sẻ các container image. Các tính năng chính bao gồm:

- **Repositories**: Nơi lưu trữ các image, có thể là công khai (cho phép chia sẻ và cộng tác mã nguồn mở) hoặc riêng tư (quản lý quyền truy cập an toàn cho nội dung nhạy cảm).

- **Official Images & Verified Publisher Images**: Cung cấp các image chất lượng cao, an toàn, được kiểm tra và cập nhật thường xuyên, tuân thủ các thực hành tốt nhất.

- **Automated Builds & Webhooks**: Tự động tạo image từ GitHub/Bitbucket và kích hoạt các hành động tự động sau khi push image thành công.

- **Quản lý**: Có thể quản lý các image trên Docker Hub thông qua Docker Desktop (chạy, pull, push, inspect).

**Private Registry**: Ngoài Docker Hub, các tổ chức có thể thiết lập Private Registry (Registry riêng tư) trên máy chủ của mình hoặc sử dụng các dịch vụ đám mây (ví dụ: Amazon ECR, GitHub Container Registry, Google Container Registry, GitLab Container Registry, Nexus, Artifactory). Private Registry cung cấp khả năng kiểm soát cao hơn về bảo mật, xác thực (ví dụ: sử dụng `htpasswd`), và tùy chỉnh cấu hình. Việc xác thực với registry (công khai hoặc riêng tư) được thực hiện bằng lệnh `docker login`.

### 2.5. Docker Volume: Mục đích, các loại Volume (Bind Mounts, Named Volumes, tmpfs Mounts), cách sử dụng để lưu trữ dữ liệu bền vững

Khi một Docker container được khởi động lại hoặc bị xóa, mọi dữ liệu được ghi vào hệ thống tệp của nó sẽ bị mất. Điều này đặt ra một thách thức lớn cho việc duy trì dữ liệu ứng dụng. Docker giải quyết vấn đề này bằng cách cung cấp các cơ chế mount dữ liệu, cho phép lưu trữ dữ liệu một cách bền vững, độc lập với vòng đời của container.

Sự khác biệt chính giữa các loại mount này nằm ở vị trí lưu trữ dữ liệu trên Docker host.

**Mục đích**: Đảm bảo dữ liệu được tạo ra bởi và sử dụng bởi các container vẫn tồn tại ngay cả khi container bị dừng hoặc loại bỏ. Volumes cũng hỗ trợ chia sẻ dữ liệu giữa nhiều container đang chạy.

**Các loại Volume**:

- **Named Volumes (Volumes được đặt tên)**:

  - **Mục đích**: Là cơ chế lưu trữ dữ liệu bền vững được Docker daemon quản lý hoàn toàn. Dữ liệu được lưu trữ trong một thư mục trên Host OS (thường là `/var/lib/docker/volumes/` trên Linux).

  - **Lợi ích**: Hiệu suất tốt hơn do sử dụng các driver và hệ thống tệp được tối ưu hóa. Dễ dàng sao lưu, khôi phục hoặc di chuyển giữa các cài đặt Docker khác nhau. Hoạt động trên cả Linux và Windows containers. An toàn hơn khi chia sẻ giữa nhiều container.

  - **Trường hợp sử dụng**: Lưu trữ dữ liệu cơ sở dữ liệu, file upload/download, file log, file cấu hình thay đổi thường xuyên, sao lưu và khôi phục.

  - **Cách sử dụng**: Tạo bằng `docker volume create <tên_volume>`. Mount vào container bằng `--mount type=volume,source=<tên_volume>,target=/đường/dẫn/trong/container` hoặc `-v <tên_volume>:/đường/dẫn/trong/container`.

- **Bind Mounts**:

  - **Mục đích**: Cho phép kết nối trực tiếp một thư mục hoặc tệp từ hệ thống tệp của Host OS vào một vị trí cụ thể bên trong container. Điều này cho phép container truy cập trực tiếp vào hệ thống tệp của host.

  - **Lợi ích**: Dễ dàng chia sẻ tệp giữa host và container. Cập nhật theo thời gian thực cho các tệp được chia sẻ. Cung cấp lưu trữ bền vững cho dữ liệu dài hạn. Có thể chia sẻ giữa nhiều container.

  - **Trường hợp sử dụng**: Môi trường phát triển (để chỉnh sửa mã nguồn trực tiếp), tải file cấu hình và live reload, truy cập các tài nguyên đặc thù của host (ví dụ: thiết bị, file hệ thống).

  - **Lưu ý quan trọng**: Bind mounts liên kết chặt chẽ container với hệ thống tệp của máy host, có nghĩa là các tiến trình trong container có thể thay đổi (tạo, sửa, xóa) hệ thống tệp của host. Cần cẩn trọng với quyền và kiểm soát truy cập thích hợp để ngăn chặn rủi ro bảo mật.

  - **Cách sử dụng**: Mount bằng `--mount type=bind,source=/đường/dẫn/trên/host,target=/đường/dẫn/trong/container` hoặc `-v /đường/dẫn/trên/host:/đường/dẫn/trong/container`.

- **tmpfs Mounts**:

  - **Mục đích**: Cho phép tạo một hệ thống tệp tạm thời trong bộ nhớ của Host OS, không bao giờ ghi dữ liệu vào đĩa. Dữ liệu trong tmpfs mount là tạm thời và sẽ bị mất khi container dừng, khởi động lại hoặc khi host khởi động lại.

  - **Lợi ích**: Lưu trữ rất nhanh và nhẹ (do trong bộ nhớ), loại bỏ các hoạt động I/O đĩa.

  - **Trường hợp sử dụng**: Lưu trữ dữ liệu tạm thời không cần tồn tại lâu dài, không muốn dữ liệu tồn tại trên host vì lý do bảo mật, hoặc để cải thiện hiệu suất khi ghi một lượng lớn dữ liệu không liên tục (ví dụ: caching trong bộ nhớ, xử lý dữ liệu nhạy cảm hoặc tạm thời).

  - **Hạn chế**: Không thể chia sẻ dữ liệu giữa các container. Chỉ hoạt động với Linux containers.

  - **Cách sử dụng**: Mount bằng `--mount type=tmpfs,source=<tên_tùy_chọn>,target=/đường/dẫn/trong/container`.

**Bảng: Các loại Docker Volume**

| **Loại Volume** | **Mục đích chính** | **Lợi ích** | **Trường hợp sử dụng điển hình** |
|-----------------|-------------------|-------------|---------------------------------|
| Named Volumes | Lưu trữ dữ liệu bền vững, được Docker quản lý. | Hiệu suất cao, dễ sao lưu/di chuyển, quản lý bằng CLI/API, an toàn khi chia sẻ. | Dữ liệu database, file upload, log file, cấu hình ứng dụng. |
| Bind Mounts | Chia sẻ tệp/thư mục từ Host OS vào container. | Cập nhật thời gian thực, truy cập tài nguyên host, phát triển cục bộ. | Môi trường phát triển, file cấu hình, mã nguồn. |
| tmpfs Mounts | Lưu trữ dữ liệu tạm thời trong bộ nhớ. | Rất nhanh, không ghi vào đĩa, bảo mật cho dữ liệu nhạy cảm. | Cache, dữ liệu tạm thời, thông tin xác thực. |

### 2.6. Docker Network: Các chế độ mạng Docker (Bridge, Host, None, Overlay), cách các Container giao tiếp

Hệ thống mạng của Docker là một phần quan trọng, cho phép các container giao tiếp với nhau và với thế giới bên ngoài. Docker cung cấp một hệ thống mạng có thể cắm được (pluggable), sử dụng các driver khác nhau để đáp ứng các nhu cầu kết nối đa dạng.

**Các loại Network Driver mặc định**:

- **Bridge Network**:

  - **Mô tả**: Đây là network driver mặc định nếu không chỉ định driver khi chạy container. Docker tạo một bridge ảo trên Host OS, và các container được kết nối vào bridge này, nhận một dải IP ngẫu nhiên.

  - **Cách giao tiếp**: Các container trên cùng một bridge network có thể giao tiếp với nhau bằng địa chỉ IP hoặc tên dịch vụ (thông qua DNS nhúng của Docker). Bridge network thường được sử dụng khi ứng dụng trong container cần giao tiếp với bên ngoài (thông qua port mapping) hoặc với các container khác trên cùng một host.

  - **Hạn chế**: Không thể định tuyến lưu lượng liên tục giữa các container trên các host khác nhau, điều này là một hạn chế trong môi trường đa host được thiết kế cho tính sẵn sàng cao (HA).

- **Host Network**:

  - **Mô tả**: Chế độ host loại bỏ sự cách ly mạng giữa container và Host OS, cho phép container sử dụng trực tiếp mạng của host. Điều này có nghĩa là container chia sẻ ngăn xếp mạng của host.

  - **Cách giao tiếp**: Nếu một ứng dụng trong container lắng nghe trên cổng 8080, nó sẽ có thể truy cập được trên cổng 8080 của Host OS mà không cần ánh xạ cổng (port mapping).

  - **Trường hợp sử dụng**: Thích hợp cho các container độc lập không có nhu cầu giao tiếp với bên ngoài hoặc khi cần hiệu suất mạng tối đa và không quan tâm đến cách ly mạng.

- **None Network**:

  - **Mô tả**: Driver này hoàn toàn cách ly container khỏi mạng, không có giao diện mạng nào được gắn vào container.

  - **Cách giao tiếp**: Container không thể giao tiếp với Host OS, các container khác hoặc internet.

  - **Trường hợp sử dụng**: Thường được sử dụng cho các tác vụ tính toán không cần mạng hoặc khi kết hợp với các network driver tùy chỉnh.

- **Overlay Network**:

  - **Mô tả**: Overlay networks kết nối nhiều Docker daemon với nhau, cho phép các dịch vụ Swarm và các container giao tiếp xuyên suốt các node khác nhau. Chiến lược này loại bỏ nhu cầu định tuyến ở cấp độ hệ điều hành.

  - **Cách giao tiếp**: Cho phép giao tiếp giữa một dịch vụ Swarm và một container standalone, hoặc giữa hai standalone container trên các Docker daemon khác nhau.

  - **Trường hợp sử dụng**: Tốt nhất khi cần các container chạy trên các Docker host khác nhau giao tiếp với nhau, hoặc khi nhiều ứng dụng hoạt động cùng nhau bằng cách sử dụng Swarm services.

**Các loại Network Driver khác**:

- **IPvlan**: Cung cấp toàn quyền kiểm soát địa chỉ IPv4 và IPv6, hỗ trợ VLAN tagging layer 2 và định tuyến L3 cho tích hợp underlay network.

- **Macvlan**: Cho phép gán địa chỉ MAC cho container, làm cho nó xuất hiện như một thiết bị vật lý trên mạng. Thích hợp cho các ứng dụng legacy mong đợi kết nối trực tiếp với mạng vật lý.

- **Network plugins**: Docker cũng hỗ trợ cài đặt và sử dụng các plugin mạng của bên thứ ba để tích hợp với các ngăn xếp mạng chuyên biệt.

**Bảng: Các loại Docker Network Driver**

| **Driver** | **Mô tả** | **Cách giao tiếp** | **Trường hợp sử dụng chính** |
|------------|-----------|-------------------|-----------------------------|
| Bridge | Mặc định. Tạo bridge ảo trên host, container kết nối vào đó. | Giữa các container cùng host, với bên ngoài qua port mapping. | Hầu hết các ứng dụng đơn lẻ hoặc đa container trên cùng host. |
| Host | Loại bỏ cách ly mạng, container sử dụng trực tiếp mạng của host. | Trực tiếp với host, không cần port mapping. | Cần hiệu suất mạng tối đa, không quan tâm cách ly. |
| None | Vô hiệu hóa mọi kết nối mạng cho container. | Không có giao tiếp mạng. | Tác vụ tính toán không cần mạng, kết hợp với driver tùy chỉnh. |
| Overlay | Kết nối nhiều Docker daemon, cho phép container giao tiếp xuyên node. | Giữa các container trên các host khác nhau (Swarm). | Kiến trúc phân tán, Swarm services. |
| IPvlan | Kiểm soát địa chỉ IPv4/IPv6, hỗ trợ VLAN tagging. | Giao tiếp mạng được kiểm soát chặt chẽ. | Tích hợp sâu với mạng vật lý, kiểm soát IP chi tiết. |
| Macvlan | Gán địa chỉ MAC riêng cho container, xuất hiện như thiết bị vật lý. | Container xuất hiện như thiết bị độc lập trên mạng vật lý. | Ứng dụng legacy yêu cầu kết nối mạng trực tiếp. |

### 2.7. Docker Compose: Mục đích, cấu trúc file docker-compose.yml, quản lý multi-container applications

**Mục đích**: Docker Compose là một công cụ mạnh mẽ để định nghĩa và chạy các ứng dụng đa container (multi-container applications). Nó giải quyết sự phức tạp của việc quản lý nhiều container riêng lẻ bằng cách cho phép người dùng định cấu hình toàn bộ ngăn xếp ứng dụng (application stack) trong một tệp YAML duy nhất. Với một lệnh duy nhất (`docker compose up`), Compose có thể tạo và khởi động tất cả các dịch vụ được định nghĩa trong tệp cấu hình.

**Cấu trúc file docker-compose.yml**: Tệp cấu hình của Docker Compose thường được đặt tên là `compose.yml` hoặc `docker-compose.yml`. Cấu trúc cơ bản bao gồm:

- **version**: Chỉ định phiên bản định dạng của tệp Compose.

- **services**: Định nghĩa các dịch vụ (container) tạo nên ứng dụng của bạn. Mỗi dịch vụ có thể có các thuộc tính như `image` (sử dụng image có sẵn), `build` (xây dựng image từ Dockerfile), `ports` (ánh xạ cổng), `volumes` (mount volume), `networks` (kết nối mạng), `environment` (biến môi trường), và `depends_on` (thiết lập thứ tự khởi động).

- **volumes**: Định nghĩa các volume được sử dụng bởi các dịch vụ để lưu trữ dữ liệu bền vững.

- **networks**: Định nghĩa các mạng tùy chỉnh để các dịch vụ có thể giao tiếp với nhau.

**Quản lý multi-container applications**: Docker Compose đơn giản hóa việc quản lý ứng dụng đa container thông qua các khả năng sau:

- **Cấu hình tập trung**: Tất cả các cấu hình cho container, phụ thuộc, biến môi trường, volume và mạng được định nghĩa trong một tệp YAML duy nhất.

- **Triển khai đơn giản**: Thay vì chạy nhiều lệnh `docker run` riêng lẻ, chỉ cần một lệnh `docker compose up` để khởi động toàn bộ ngăn xếp ứng dụng.

- **Quản lý mạng tự động**: Compose tự động tạo mạng và đảm bảo các container có thể giao tiếp với nhau dễ dàng bằng tên dịch vụ.

- **Khả năng mở rộng**: Có thể dễ dàng tăng hoặc giảm số lượng instance của từng dịch vụ trong thiết lập đa container.

- **Quản lý volume bền vững**: Dễ dàng triển khai các volume bền vững để đảm bảo dữ liệu không bị mất khi container dừng hoặc bị xóa.

- **Quản lý biến môi trường hợp lý**: Biến môi trường có thể được thiết lập một lần trong tệp Compose, đơn giản hóa việc quản lý chúng.

- **Vòng đời ứng dụng**: Compose cung cấp các lệnh để quản lý toàn bộ vòng đời của ứng dụng, bao gồm khởi động, dừng, xây dựng lại dịch vụ, xem trạng thái, theo dõi log và chạy các lệnh một lần.

## 3. Các Thành phần Kiến trúc Docker

### 3.1. Docker Engine: Kiến trúc (Docker Daemon, Docker CLI, REST API) và vai trò của mỗi thành phần

Docker Engine là một ứng dụng client-server, đóng vai trò là cốt lõi của hệ thống Docker. Nó được cài đặt trên máy chủ (host) và chịu trách nhiệm quản lý các container Docker. Kiến trúc của Docker Engine bao gồm ba thành phần chính:

**Docker Daemon (dockerd)**:

- **Mô tả**: Docker Daemon, còn gọi là `dockerd`, là một tiến trình chạy nền trên Host OS. Nó là thành phần "server" của Docker Engine.

- **Vai trò**: Daemon lắng nghe các yêu cầu Docker API và thực hiện các công việc nặng nhọc như xây dựng (build), chạy (run), và quản lý các đối tượng Docker. Các đối tượng này bao gồm:

  - **Images**: Quản lý việc tạo, lưu trữ và phân phối image.
  - **Containers**: Khởi tạo, chạy, dừng, giám sát và hủy bỏ container.
  - **Networks**: Quản lý các kết nối mạng giữa các container và với Host OS.
  - **Volumes**: Quản lý lưu trữ dữ liệu bền vững cho container.

  Daemon cũng có khả năng giao tiếp với các daemon Docker khác để quản lý các dịch vụ Docker phân tán (như trong Docker Swarm).

**Docker Client (docker CLI)**:

- **Mô tả**: Docker Client, hay `docker`, là giao diện dòng lệnh (CLI) mà người dùng tương tác với Docker. Nó là thành phần "client" của Docker Engine.

- **Vai trò**: Khi người dùng nhập các lệnh Docker (ví dụ: `docker run`, `docker build`, `docker pull`), client sẽ gửi các lệnh này đến Docker Daemon. Docker Client có thể chạy trên cùng một hệ thống với daemon hoặc kết nối với một Docker daemon từ xa. Nó cũng có thể giao tiếp với nhiều daemon khác nhau.

**REST API**:

- **Mô tả**: Docker Client và Docker Daemon giao tiếp với nhau thông qua một REST API.

- **Vai trò**: REST API định nghĩa các giao diện mà các ứng dụng hoặc Docker Client sử dụng để tương tác với Docker Daemon. Nó là cầu nối để chuyển các yêu cầu từ phía người dùng (qua CLI) đến daemon để thực thi.

### 3.2. Docker Client: Các lệnh Docker CLI phổ biến

Docker Client cung cấp một bộ lệnh dòng lệnh phong phú để tương tác và quản lý các đối tượng Docker như image, container, network và volume. Dưới đây là các lệnh CLI phổ biến mà các nhà phát triển và quản trị viên hệ thống thường xuyên sử dụng:

**Quản lý Image**:

- `docker build -t <image_name> .`: Xây dựng một Docker image từ Dockerfile trong thư mục hiện tại.

- `docker images` hoặc `docker image ls`: Liệt kê tất cả các Docker image có sẵn trên máy cục bộ.

- `docker pull <image_name>`: Tải một Docker image từ Docker Hub (hoặc registry đã cấu hình) về máy cục bộ.

- `docker rmi <image_name>`: Xóa một Docker image khỏi máy cục bộ (chỉ khi không có container nào đang sử dụng).

- `docker image prune`: Xóa tất cả các image không được sử dụng bởi bất kỳ container nào.

- `docker push <username>/<image_name>`: Đẩy một Docker image lên Docker Hub hoặc registry đã cấu hình.

**Quản lý Container**:

- `docker run --name <container_name> -p <host_port>:<container_port> -d <image_name>`: Tạo và chạy một container từ một image, với tên tùy chỉnh, ánh xạ cổng và chạy ở chế độ nền (detached mode).

- `docker ps`: Liệt kê tất cả các container đang chạy.

- `docker ps -a` hoặc `docker ps --all`: Liệt kê tất cả các container, bao gồm cả những container đã dừng.

- `docker start <container_id/name>`: Khởi động một container đã dừng.

- `docker stop <container_id/name>`: Dừng một container đang chạy.

- `docker rm <container_id/name>`: Xóa một container đã dừng.

- `docker exec -it <container_id/name> <command>`: Thực thi một lệnh bên trong một container đang chạy (ví dụ: mở shell sh hoặc bash).

- `docker logs -f <container_id/name>`: Lấy và theo dõi (stream) log của một container.

- `docker inspect <container_id/name>`: Hiển thị thông tin chi tiết cấp thấp về một container đang chạy.

- `docker container prune`: Xóa tất cả các container không chạy.

**Quản lý Network**:

- `docker network ls`: Liệt kê tất cả các network có sẵn.

- `docker network create --driver <driver_name> <network_name>`: Tạo một network mới.

- `docker network inspect <network_name>`: Kiểm tra thông tin chi tiết của một network.

- `docker network rm <network_name>`: Xóa một network.

**Quản lý Volume**:

- `docker volume ls`: Hiển thị danh sách các volume.

- `docker volume create <volume_name>`: Tạo một volume mới.

- `docker volume inspect <volume_name>`: Xem thông tin chi tiết của một volume.

- `docker volume rm <volume_name>`: Xóa một volume.

- `docker volume prune`: Xóa tất cả các volume không sử dụng.

**Các lệnh chung**:

- `docker info`: Hiển thị thông tin hệ thống về cài đặt Docker.

- `docker --help`: Hiển thị trợ giúp chung về Docker.

**Bảng: Các lệnh Docker CLI phổ biến (cheat sheet)**

| **Lệnh** | **Mô tả** |
|----------|-----------|
| `docker build -t <image_name> .` | Xây dựng image từ Dockerfile. |
| `docker images` | Liệt kê các image cục bộ. |
| `docker pull <image_name>` | Tải image từ Docker Hub. |
| `docker push <username>/<image_name>` | Đẩy image lên Docker Hub. |
| `docker rmi <image_name>` | Xóa image. |
| `docker run -d -p <host_port>:<container_port> <image_name>` | Chạy container ở chế độ nền, ánh xạ cổng. |
| `docker ps` | Liệt kê container đang chạy. |
| `docker ps -a` | Liệt kê tất cả container (chạy và dừng). |
| `docker start <container_name>` | Khởi động container đã dừng. |
| `docker stop <container_name>` | Dừng container đang chạy. |
| `docker rm <container_name>` | Xóa container đã dừng. |
| `docker exec -it <container_name> bash` | Mở shell bên trong container. |
| `docker logs -f <container_name>` | Xem và theo dõi log của container. |
| `docker network ls` | Liệt kê các mạng. |
| `docker volume ls` | Liệt kê các volume. |

### 3.3. Docker Daemon: Chức năng chính

Docker Daemon, hay `dockerd`, là thành phần cốt lõi của Docker Engine, hoạt động như một máy chủ (server) trong kiến trúc client-server của Docker. Chức năng chính của nó là lắng nghe các yêu cầu từ Docker Client (thông qua REST API) và thực hiện các tác vụ quản lý nặng nhọc liên quan đến các đối tượng Docker.

**Các chức năng chính của Docker Daemon bao gồm**:

- **Quản lý Images**: Daemon chịu trách nhiệm cho toàn bộ vòng đời của Docker Image, bao gồm việc kéo (pull) image từ registry, lưu trữ image cục bộ, và xây dựng (build) image từ Dockerfile.

- **Quản lý Containers**: Đây là chức năng trung tâm của daemon. Nó khởi tạo, chạy, dừng, tạm dừng, khởi động lại, và hủy bỏ các container. Daemon cũng giám sát trạng thái của các container đang chạy.

- **Quản lý Networks**: Daemon quản lý việc tạo và cấu hình các mạng Docker (như bridge, host, overlay) để cho phép các container giao tiếp với nhau và với Host OS.

- **Quản lý Volumes**: Daemon xử lý việc tạo, gắn (mount) và quản lý các volume để đảm bảo dữ liệu bền vững cho container.

- **Giao tiếp với các Daemon khác**: Trong các thiết lập Docker phân tán (ví dụ: Docker Swarm), một daemon có thể giao tiếp với các daemon khác để quản lý và điều phối các dịch vụ Docker trên nhiều máy chủ.

Tóm lại, Docker Daemon là "bộ não" của hệ thống Docker, thực hiện tất cả các hoạt động cấp thấp cần thiết để chạy và quản lý các ứng dụng được đóng gói trong container.

### 3.4. Containerd: Vai trò trong hệ sinh thái Docker và mối quan hệ với Docker Engine

**Vai trò của Containerd**: Containerd là một runtime container tiêu chuẩn công nghiệp, tập trung vào sự đơn giản, mạnh mẽ và tính di động. Nó hoạt động như một daemon cho cả hệ điều hành Linux và Windows, có khả năng quản lý toàn bộ vòng đời của container trên hệ thống host. Các chức năng của nó bao gồm chuyển giao và lưu trữ image, thực thi và giám sát container, cũng như quản lý lưu trữ cấp thấp và các kết nối mạng. Containerd được thiết kế để được nhúng vào một hệ thống lớn hơn, thay vì được sử dụng trực tiếp bởi các nhà phát triển hoặc người dùng cuối.

**Mối quan hệ với Docker Engine**:

- Containerd ban đầu là một phần của Docker Engine, nhưng sau đó đã được tách ra thành một dự án độc lập để tăng tính mô-đun và khả năng sử dụng lại trong hệ sinh thái container rộng lớn hơn.

- Docker Engine hiện sử dụng Containerd làm runtime container cốt lõi của nó để quản lý vòng đời của container, bao gồm tạo, khởi động và dừng container. Việc tích hợp này cho phép Docker tập trung vào các chức năng cấp cao hơn (như trải nghiệm người dùng, build image) trong khi tận dụng Containerd cho các hoạt động cấp thấp hơn.

- Containerd cung cấp một API quản lý container mà các công cụ cấp cao hơn như Docker có thể sử dụng để tương tác với container và image trên host của Containerd.

- Containerd cũng là một thành phần quan trọng trong hệ sinh thái Kubernetes. Kể từ Kubernetes 1.20, Docker đã bị loại bỏ vai trò runtime, và Kubernetes hiện sử dụng các runtime container triển khai Container Runtime Interface (CRI), chẳng hạn như Containerd hoặc CRI-O, để quản lý container hiệu quả và tiêu chuẩn hóa hơn.

### 3.5. RunC: Vai trò là một runtime cho Container và mối quan hệ với Containerd

**Vai trò của RunC**: RunC là một công cụ runtime container nhẹ và phổ quát, tuân thủ đặc tả OCI (Open Container Initiative). Nó là thành phần cấp thấp nhất trong ngăn xếp công nghệ container, chịu trách nhiệm tương tác trực tiếp với kernel của Host OS để thực thi và chạy container. RunC trừu tượng hóa các thành phần hệ thống Linux như cgroups và user namespaces, vốn là những yếu tố cốt lõi giúp container hóa có thể thực hiện được.

**Mối quan hệ với Containerd**:

- RunC là một thành phần của Containerd và đóng vai trò là bộ thực thi cho các container. Containerd sử dụng RunC để khởi tạo và chạy các container theo đặc tả OCI.

- Theo mặc định, Containerd sử dụng RunC làm runtime container của nó. Containerd quản lý và tạo điều kiện thuận lợi cho RunC, vốn là runtime container thực sự. Containerd chuẩn bị image dưới dạng gói OCI và sau đó thực hiện lệnh gọi API tới RunC để khởi động gói OCI đó.

- Có thể hình dung mối quan hệ này như một hệ thống phân cấp: Docker Engine ở trên cùng, giao tiếp với Containerd, và Containerd sau đó giao tiếp với RunC để thực hiện các tác vụ cấp thấp nhất liên quan đến việc chạy container.

Sự phân tách Docker Engine thành các thành phần nhỏ hơn như Containerd và RunC đã tăng cường tính mô-đun và khả năng sử dụng lại của công nghệ container. Điều này cho phép các công cụ khác nhau trong hệ sinh thái (như Kubernetes) có thể sử dụng các thành phần cấp thấp mà không cần phụ thuộc vào toàn bộ Docker Engine.

## 4. Triển khai Ứng dụng Java Spring Boot với Docker

### 4.1. Tại sao nên sử dụng Docker với Spring Boot?

Việc kết hợp Docker với các ứng dụng Java Spring Boot mang lại nhiều lợi ích chiến lược, giúp đơn giản hóa đáng kể quá trình phát triển và triển khai:

**Đảm bảo môi trường nhất quán**:

- Spring Boot ứng dụng thường yêu cầu một phiên bản Java cụ thể và các phụ thuộc khác. Docker cho phép đóng gói ứng dụng Spring Boot cùng với phiên bản JDK/JRE chính xác và tất cả các thư viện cần thiết vào một image duy nhất.

- Điều này loại bỏ hoàn toàn vấn đề "nó chạy trên máy tôi nhưng không chạy trên máy bạn". Mọi nhà phát triển trong nhóm, môi trường thử nghiệm, staging và sản xuất đều sử dụng cùng một môi trường được đóng gói, đảm bảo hành vi ứng dụng nhất quán.

**Đơn giản hóa CI/CD**:

- Docker container hóa ứng dụng giúp tiêu chuẩn hóa các bước trong pipeline CI/CD. Việc build, test và deploy trở nên dễ dàng và đáng tin cậy hơn vì môi trường thực thi luôn giống nhau.

- Các công cụ CI/CD (như Jenkins, GitHub Actions) có thể dễ dàng build Docker image, push lên registry và triển khai container, tự động hóa toàn bộ quy trình phân phối phần mềm.

**Quản lý phụ thuộc bên ngoài dễ dàng hơn**:

- Các ứng dụng Spring Boot thường phụ thuộc vào các dịch vụ bên ngoài như cơ sở dữ liệu (PostgreSQL, MySQL), message brokers, cache. Docker Compose cho phép định nghĩa và chạy tất cả các dịch vụ này trong các container riêng biệt và liên kết chúng lại với nhau trong một mạng nội bộ.

- Điều này đơn giản hóa việc thiết lập môi trường phức tạp chỉ với một tệp cấu hình YAML và một lệnh duy nhất (`docker compose up`).

**Khả năng mở rộng và quản lý linh hoạt**:

- Các container Docker nhẹ và khởi động nhanh, giúp dễ dàng mở rộng ứng dụng Spring Boot theo chiều ngang bằng cách chạy nhiều instance container.

- Việc quản lý cấu hình ứng dụng thông qua biến môi trường trở nên linh hoạt hơn, cho phép điều chỉnh hành vi ứng dụng mà không cần rebuild image.

**Bảng: Lợi ích của Docker cho Spring Boot**

| **Lợi ích** | **Mô tả chi tiết** |
|-------------|-------------------|
| Môi trường nhất quán | Đóng gói ứng dụng với phiên bản Java và phụ thuộc chính xác, loại bỏ lỗi "chạy trên máy tôi". |
| Đơn giản hóa CI/CD | Chuẩn hóa quy trình build, test, deploy, tăng tốc độ và độ tin cậy của pipeline tự động. |
| Quản lý phụ thuộc | Dễ dàng thiết lập và liên kết các dịch vụ bên ngoài (database, cache) bằng Docker Compose. |
| Khả năng di động | Ứng dụng có thể chạy trên mọi môi trường có Docker Engine mà không cần cấu hình lại. |
| Tối ưu tài nguyên | Container nhẹ hơn VM, giúp chạy nhiều ứng dụng hơn trên cùng một phần cứng. |
| Quản lý cấu hình linh hoạt | Sử dụng biến môi trường và Spring Profiles để cấu hình ứng dụng mà không cần rebuild image. |

### 4.2. Chuẩn bị ứng dụng Spring Boot: Ví dụ REST API và cách đóng gói JAR/WAR

Để triển khai ứng dụng Spring Boot với Docker, bước đầu tiên là chuẩn bị ứng dụng và đóng gói nó thành một định dạng thực thi.

**Ví dụ một ứng dụng Spring Boot cơ bản (REST API)**:

Một ứng dụng Spring Boot cơ bản thường là một REST API đơn giản. Ví dụ, một ứng dụng có thể tạo một endpoint trả về một thông báo tĩnh:

```java
package com.example.demo;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@SpringBootApplication
@RestController
public class DemoApplication {

    public static void main(String[] args) {
        SpringApplication.run(DemoApplication.class, args);
    }

    @GetMapping("/messages")
    public String getMessage() {
        return "Hello from Docker!";
    }
}
```

Ứng dụng này sẽ lắng nghe các yêu cầu HTTP GET trên đường dẫn `/messages` và trả về chuỗi "Hello from Docker!". Để tạo một dự án Spring Boot cơ bản như vậy, có thể sử dụng Spring Initializr (`https://start.spring.io`) và chọn các phụ thuộc cần thiết như Spring Web.

**Cách đóng gói ứng dụng Spring Boot thành JAR/WAR file**:

Ứng dụng Spring Boot có thể được đóng gói thành tệp JAR (Java Archive) hoặc WAR (Web Application Archive) tùy thuộc vào mục đích triển khai.

- **Đóng gói thành JAR file (phổ biến nhất cho Spring Boot)**:

  - Spring Boot mặc định tạo ra các JAR file thực thi (executable JARs) chứa tất cả các phụ thuộc và một máy chủ nhúng (như Tomcat, Jetty, hoặc Undertow). Điều này cho phép chạy ứng dụng trực tiếp bằng lệnh `java -jar`.

  - Để tạo JAR file, sử dụng Maven hoặc Gradle. Với Maven, đảm bảo plugin `spring-boot-maven-plugin` được thêm vào `pom.xml`.

  - Chạy lệnh sau trong thư mục gốc của dự án:

    ```bash
    ./mvnw clean package
    # hoặc với Maven:
    # mvn clean package
    ```

    Lệnh này sẽ biên dịch dự án, chạy các bài kiểm tra (nếu có) và đóng gói ứng dụng thành một tệp `.jar` (ví dụ: `your-app-0.0.1-SNAPSHOT.jar`) trong thư mục `target/`.

- **Đóng gói thành WAR file (để triển khai trên máy chủ ứng dụng bên ngoài)**:

  - Nếu muốn triển khai ứng dụng Spring Boot trên một máy chủ ứng dụng truyền thống (như Tomcat, JBoss, Wildfly) thay vì sử dụng máy chủ nhúng, cần đóng gói thành tệp WAR.

  - **Các bước chính để chuyển đổi sang WAR**:

    - Thay đổi `<packaging>` trong `pom.xml` từ `jar` thành `war`.

    - Đặt `spring-boot-starter-tomcat` (hoặc starter cho máy chủ nhúng khác) với scope là `provided` trong `pom.xml` để tránh xung đột với máy chủ bên ngoài.

    - Lớp main của ứng dụng Spring Boot cần kế thừa `SpringBootServletInitializer` và override phương thức `configure`.

    - Cấu hình `maven-war-plugin` để không bị lỗi nếu `web.xml` bị thiếu.

    - Sau khi cấu hình, chạy lệnh `mvn clean package` để tạo tệp `.war`.

### 4.3. Viết Dockerfile tối ưu cho ứng dụng Spring Boot: Multi-stage builds, chọn base image phù hợp, tối ưu caching

Viết một Dockerfile tối ưu là rất quan trọng để tạo ra các Docker Image nhỏ gọn, an toàn và có thời gian build nhanh, đặc biệt đối với các ứng dụng Java Spring Boot.

**Dockerfile tối ưu cho Spring Boot**:

Một Dockerfile tối ưu cho Spring Boot thường sử dụng kỹ thuật multi-stage builds và chọn base image phù hợp để giảm kích thước image cuối cùng.

```dockerfile
# Giai đoạn 1: Build ứng dụng
FROM maven:3.8.3-openjdk-17 AS builder
WORKDIR /app
COPY pom.xml .
COPY src ./src
RUN mvn -f pom.xml clean package -DskipTests

# Giai đoạn 2: Tạo image runtime nhỏ gọn
FROM eclipse-temurin:17-jre-alpine
WORKDIR /app
# Sử dụng tính năng Layered JAR của Spring Boot để tối ưu caching
# Trích xuất các lớp của JAR từ giai đoạn builder
COPY --from=builder /app/target/*.jar app.jar
RUN java -Djarmode=layertools -jar app.jar extract

# Giai đoạn cuối: Image runtime thực tế
FROM eclipse-temurin:17-jre-alpine
WORKDIR /app
# Sao chép các lớp đã được trích xuất
COPY --from=builder /app/extracted/dependencies/ ./
COPY --from=builder /app/extracted/spring-boot-loader/ ./
COPY --from=builder /app/extracted/snapshot-dependencies/ ./
COPY --from=builder /app/extracted/application/ ./

EXPOSE 8080
ENTRYPOINT ["java", "org.springframework.boot.loader.launch.JarLauncher"]
```

**Giải thích chi tiết các lệnh và tối ưu hóa**:

- **Sử dụng Multi-stage Builds để giảm kích thước image**:

  - Dockerfile trên sử dụng ba giai đoạn (builder, extracted layers, và final runtime image).

  - `FROM maven:3.8.3-openjdk-17 AS builder`: Giai đoạn đầu tiên sử dụng một image Maven đầy đủ (bao gồm JDK và Maven) để biên dịch và đóng gói ứng dụng Spring Boot thành tệp JAR. Việc này đảm bảo rằng các công cụ build nặng không bị đưa vào image cuối cùng.

  - `RUN mvn -f pom.xml clean package -DskipTests`: Thực thi quá trình build Maven để tạo ra tệp JAR.

  - `FROM eclipse-temurin:17-jre-alpine` (giai đoạn trích xuất layer và giai đoạn cuối): Giai đoạn thứ hai và thứ ba sử dụng một base image nhẹ hơn nhiều, chỉ chứa Java Runtime Environment (JRE) thay vì JDK đầy đủ.

  - `eclipse-temurin:17-jre-alpine` là một lựa chọn tuyệt vời vì nó dựa trên Alpine Linux, một bản phân phối Linux rất nhỏ gọn, giúp giảm đáng kể kích thước image.

  - `COPY --from=builder...`: Các lệnh `COPY --from` cho phép sao chép các artifact cụ thể từ các giai đoạn trước vào giai đoạn hiện tại. Điều này đảm bảo rằng chỉ những tệp cần thiết cho thời gian chạy (runtime) mới được đưa vào image cuối cùng, loại bỏ các tệp build trung gian và công cụ không cần thiết.

- **Tối ưu caching với Layered JARs (Spring Boot 2.3+)**:

  - `RUN java -Djarmode=layertools -jar app.jar extract`: Lệnh này tận dụng tính năng Layered JAR của Spring Boot. Nó trích xuất các thành phần của ứng dụng (dependencies, spring-boot-loader, snapshot-dependencies, application) thành các thư mục riêng biệt.

  - Bằng cách sao chép từng lớp này riêng lẻ (`COPY --from=builder extracted/...`), Docker có thể tận dụng cache build hiệu quả hơn. Nếu chỉ mã ứng dụng thay đổi, Docker chỉ cần rebuild và copy lớp `application/`, giúp tăng tốc độ build đáng kể cho các lần sau.

- **Chọn base image phù hợp (JRE thay vì JDK)**:

  - Đối với các ứng dụng Spring Boot đã build xong, chỉ cần JRE để chạy, không cần JDK. Việc sử dụng image JRE (ví dụ: `eclipse-temurin:17-jre-alpine`) thay vì JDK (ví dụ: `openjdk:17-jdk-alpine`) có thể giảm kích thước image từ hàng trăm MB xuống còn dưới 100 MB.

- **EXPOSE 8080**: Khai báo cổng mà ứng dụng Spring Boot sẽ lắng nghe. Đây là một thực hành tốt để tài liệu hóa cổng của ứng dụng.

- **ENTRYPOINT ["java", "org.springframework.boot.loader.launch.JarLauncher"]**: Định nghĩa lệnh sẽ chạy khi container khởi động. Đối với Layered JARs, cần sử dụng `org.springframework.boot.loader.launch.JarLauncher` (hoặc `org.springframework.boot.loader.JarLauncher` cho các phiên bản Spring Boot cũ hơn 3.2) để khởi động ứng dụng một cách tối ưu.

### 4.4. Build và Run Docker Image: Lệnh docker build và docker run với các tham số quan trọng (port mapping, volume mounting, network configuration)

Sau khi đã có Dockerfile, các bước tiếp theo là xây dựng image và chạy container.

**Lệnh docker build và các tham số quan trọng**:

Lệnh `docker build` được sử dụng để xây dựng Docker Image từ Dockerfile.

- **Cú pháp cơ bản**: `docker build PATH | URL | -`.

  - **PATH**: Đường dẫn đến thư mục chứa Dockerfile (thường là `.` cho thư mục hiện tại).

- **Tham số quan trọng**:

  - `-t, --tag <name>[:<tag>]`: Đặt tên và tag cho image. Ví dụ: `docker build -t my-spring-app:1.0 .`.

  - `--no-cache`: Không sử dụng cache trong quá trình build. Hữu ích khi cần đảm bảo một bản build hoàn toàn mới.

  - `--build-arg <key>=<value>`: Đặt giá trị cho các biến môi trường được định nghĩa bằng `ARG` trong Dockerfile.

- **Ví dụ**:

  ```bash
  docker build -t spring-boot-app:latest .
  ```

  Lệnh này sẽ xây dựng một image có tên `spring-boot-app` với tag `latest` từ Dockerfile trong thư mục hiện tại.

**Lệnh docker run và các tham số quan trọng (port mapping, volume mounting, network configuration)**:

Lệnh `docker run` được dùng để tạo và chạy một container từ một Docker Image.

- **Cú pháp cơ bản**: `docker run IMAGE`.

- **Tham số quan trọng**:

  - `-p, --publish <host_port>:<container_port>` (Port Mapping): Ánh xạ một cổng trên Host OS đến một cổng bên trong container. Điều này cho phép truy cập ứng dụng từ bên ngoài container.

    - Ví dụ: `docker run -p 8080:8080 spring-boot-app:latest` sẽ ánh xạ cổng 8080 của host đến cổng 8080 của container.

    - **Lưu ý**: Một cổng trên host chỉ có thể được ánh xạ tới một container tại một thời điểm.

  - `-v, --volume <host_path>:<container_path>` (Volume Mounting): Mount một volume hoặc một thư mục từ Host OS vào một vị trí bên trong container để lưu trữ dữ liệu bền vững.

    - Ví dụ: `docker run -v my_data_volume:/app/data spring-boot-app:latest` sẽ mount volume `my_data_volume` vào thư mục `/app/data` bên trong container.

    - Hoặc `docker run -v /host/path/logs:/app/logs spring-boot-app:latest` sẽ mount thư mục `/host/path/logs` trên host vào `/app/logs` trong container.

  - `--network <network_name>` (Network Configuration): Kết nối container đến một Docker network cụ thể, cho phép nó giao tiếp với các container khác trong cùng network.

    - Ví dụ: `docker run --network my_app_network spring-boot-app:latest` sẽ kết nối container vào mạng `my_app_network`.

  - `-d, --detach`: Chạy container ở chế độ nền (background).

  - `--name <container_name>`: Đặt tên cho container.

### 4.5. Quản lý phụ thuộc (Dependencies): Xử lý các phụ thuộc bên ngoài (ví dụ: database) bằng Docker Compose

Các ứng dụng Spring Boot thường phụ thuộc vào các dịch vụ bên ngoài như cơ sở dữ liệu (PostgreSQL, MySQL), message brokers, hoặc cache. Việc quản lý và khởi động các dịch vụ này cùng với ứng dụng chính có thể phức tạp. Docker Compose giải quyết vấn đề này bằng cách cho phép định nghĩa và điều phối nhiều container như một đơn vị duy nhất thông qua một tệp `docker-compose.yml`.

**Mục đích của Docker Compose trong quản lý phụ thuộc**:

- **Đơn giản hóa thiết lập môi trường**: Thay vì cài đặt và cấu hình từng dịch vụ bên ngoài trên máy host hoặc chạy từng container riêng lẻ, Docker Compose cho phép định nghĩa tất cả trong một tệp duy nhất.

- **Đảm bảo thứ tự khởi động**: `depends_on` trong Compose đảm bảo các dịch vụ phụ thuộc (ví dụ: database) khởi động trước ứng dụng chính.

- **Quản lý mạng nội bộ**: Compose tự động tạo một mạng nội bộ cho các dịch vụ, cho phép chúng giao tiếp với nhau bằng tên dịch vụ (ví dụ: ứng dụng Spring Boot có thể kết nối đến database bằng hostname `db` thay vì địa chỉ IP).

**Ví dụ docker-compose.yml để chạy ứng dụng Spring Boot với PostgreSQL/MySQL**:

- **Ví dụ với PostgreSQL**:

```yaml
version: '3.8' # Sử dụng phiên bản Compose mới nhất
services:
  app:
    image: 'spring-boot-app:latest' # Tên image Spring Boot đã build
    build:
      context: . # Xây dựng image từ Dockerfile trong thư mục hiện tại
    container_name: spring-app-container
    ports:
      - "8080:8080" # Ánh xạ cổng ứng dụng
    depends_on:
      - db # Đảm bảo dịch vụ 'db' khởi động trước
    environment: # Cấu hình biến môi trường cho ứng dụng Spring Boot
      - SPRING_DATASOURCE_URL=jdbc:postgresql://db:5432/compose-postgres
      - SPRING_DATASOURCE_USERNAME=compose-postgres
      - SPRING_DATASOURCE_PASSWORD=compose-postgres
      - SPRING_JPA_HIBERNATE_DDL_AUTO=update # Tùy chọn, để Hibernate tự động cập nhật schema

  db:
    image: 'postgres:13.1-alpine' # Sử dụng image PostgreSQL nhẹ
    container_name: postgres-db-container
    ports:
      - "5432:5432" # Ánh xạ cổng database (tùy chọn, chỉ để truy cập từ host)
    environment: # Cấu hình biến môi trường cho PostgreSQL
      - POSTGRES_DB=compose-postgres
      - POSTGRES_USER=compose-postgres
      - POSTGRES_PASSWORD=compose-postgres
    volumes:
      - postgres_data:/var/lib/postgresql/data # Lưu trữ dữ liệu bền vững

volumes:
  postgres_data: # Định nghĩa named volume
```

**Giải thích**: Dịch vụ `app` (ứng dụng Spring Boot) được xây dựng từ Dockerfile trong thư mục hiện tại. Nó phụ thuộc vào dịch vụ `db` (PostgreSQL). Các biến môi trường `SPRING_DATASOURCE_URL`, `USERNAME`, `PASSWORD` được thiết lập để ứng dụng kết nối đến database `db` bằng tên dịch vụ. Dịch vụ `db` sử dụng image `postgres:13.1-alpine` và có các biến môi trường để cấu hình user, password, database. `postgres_data` volume được sử dụng để đảm bảo dữ liệu database không bị mất khi container `db` khởi động lại hoặc bị xóa.

- **Ví dụ với MySQL**:

```yaml
version: '3.8'
services:
  api_service:
    build: . # Xây dựng image từ Dockerfile trong thư mục hiện tại
    restart: always
    ports:
      - "8080:8080"
    networks:
      - springapimysql-net # Kết nối vào mạng tùy chỉnh
    environment:
      - spring.datasource.url=jdbc:mysql://mysqldb:3306/basics?allowPublicKeyRetrieval=true
      - spring.datasource.username=amila_one
      - spring.datasource.password=Amila_pw
    depends_on:
      - mysqldb
    volumes:
      - .m2:/root/.m2 # Tùy chọn: để cache Maven dependencies

  mysqldb:
    image: "mysql:8.0" # Sử dụng image MySQL
    restart: always
    ports:
      - "3306:3306"
    networks:
      - springapimysql-net
    environment:
      MYSQL_DATABASE: basics
      MYSQL_USER: amila_one
      MYSQL_PASSWORD: Amila_pw
      MYSQL_ROOT_PASSWORD: Amila_Rpw
    # volumes: # Có thể thêm volume để lưu trữ dữ liệu MySQL bền vững
    #   - mysql_data:/var/lib/mysql

networks:
  springapimysql-net: # Định nghĩa mạng tùy chỉnh để các dịch vụ giao tiếp
# volumes: # Định nghĩa named volume nếu sử dụng
#   mysql_data:
```

**Giải thích**: Tương tự như PostgreSQL, dịch vụ `api_service` (ứng dụng Spring Boot) phụ thuộc vào `mysqldb`. Tên host trong `SPRING_DATASOURCE_URL` được thay bằng `mysqldb` (tên dịch vụ MySQL trong Compose). Các biến môi trường `MYSQL_DATABASE`, `MYSQL_USER`, `MYSQL_PASSWORD`, `MYSQL_ROOT_PASSWORD` được sử dụng để cấu hình database MySQL. Một mạng tùy chỉnh `springapimysql-net` được định nghĩa và cả hai dịch vụ đều được gán vào mạng này để giao tiếp.

**Chạy ứng dụng với Docker Compose**:

Để khởi động toàn bộ ngăn xếp ứng dụng, điều hướng đến thư mục chứa tệp `docker-compose.yml` và chạy lệnh:

```bash
docker compose up -d --build
```

Lệnh này sẽ xây dựng các image (nếu cần), tạo các container, thiết lập mạng và khởi động tất cả các dịch vụ theo đúng thứ tự phụ thuộc. Cờ `-d` để chạy ở chế độ nền và `--build` để xây dựng lại image nếu có thay đổi.

### 4.6. Cấu hình ứng dụng trong Docker: Sử dụng biến môi trường (Environment Variables) và Spring Profiles

Cấu hình ứng dụng Spring Boot bên trong Docker container là một khía cạnh quan trọng để đảm bảo tính linh hoạt và khả năng thích ứng với các môi trường khác nhau (phát triển, thử nghiệm, sản xuất). Biến môi trường và Spring Profiles là hai công cụ chính để đạt được điều này.

**Sử dụng biến môi trường (Environment Variables) để cấu hình ứng dụng Spring Boot bên trong Container**:

Biến môi trường là một phương pháp tiêu chuẩn để cung cấp cấu hình cho các ứng dụng trong môi trường container. Spring Boot tự động ánh xạ các biến môi trường có tên phù hợp với các thuộc tính cấu hình trong `application.properties` hoặc `application.yaml`.

**Trong application.yaml hoặc application.properties**:

Ứng dụng Spring Boot có thể tham chiếu các biến môi trường bằng cú pháp `${BIEN_MOI_TRUONG}`.

Ví dụ:

```yaml
server:
  port: ${PORT:8080} # Cổng mặc định là 8080 nếu biến PORT không được đặt
spring:
  datasource:
    url: ${DB_URL}
    username: ${DB_USER}
    password: ${DB_PASS}
```

Ở đây, `PORT`, `DB_URL`, `DB_USER`, `DB_PASS` sẽ được đọc từ các biến môi trường của container.

**Truyền biến môi trường khi chạy container**:

Khi sử dụng lệnh `docker run`, có thể truyền biến môi trường bằng cờ `-e` hoặc `--env`:

```bash