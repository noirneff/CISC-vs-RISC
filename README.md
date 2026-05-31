# CISC-vs-RISC

---

## 1. Yêu cầu cụ thể

### 1.1. Giới thiệu khái niệm cơ bản về CISC (Complex Instruction Set Computer) và RISC (Reduced Instruction Set Computer)

Trong kiến trúc máy tính, việc tối ưu hóa hiệu suất giữa phần cứng (đơn vị xử lý trung tâm - CPU) và phần mềm (trình biên dịch và hệ thống mã lệnh) luôn là bài toán cốt lõi. Hiệu năng của một bộ vi xử lý được định nghĩa qua phương trình kinh điển:

Thời gian thực thi CPU = Số lượng lệnh x CPI (Cycles Per Instruction) x Thời gian chu kỳ xung nhịp

Để tối ưu hóa phương trình này, hai trường phái kiến trúc lớn nhất đã ra đời với hai triết lý thiết kế hoàn toàn trái ngược nhau: CISC và RISC.

- Kiến trúc CISC (Complex Instruction Set Computer): CISC là triết lý thiết kế thống trị trong giai đoạn đầu của ngành công nghiệp máy tính (1970 - 1980). Triết lý cốt lõi của CISC là dịch chuyển độ phức tạp từ phần mềm xuống phần cứng. Mục tiêu của CISC là thực hiện các tác vụ lớn chỉ bằng một vài lệnh phức tạp ở cấp độ ngôn ngữ máy. Một lệnh CISC duy nhất có thể tích hợp nhiều hành động phức tạp như: tải dữ liệu từ bộ nhớ RAM, thực hiện phép toán số học/logic, và lưu kết quả trở lại bộ nhớ. Để thực thi được các lệnh có độ dài biến đổi và cấu trúc phức tạp này, phần cứng CPU bắt buộc phải trang bị một khối điều khiển vi chương trình nội bộ (Microcode Control Unit). Khối này có nhiệm vụ phân rã các lệnh vĩ mô (Macro-instructions) thành các chuỗi vi lệnh (Micro-operations) nhỏ hơn để mạch phần cứng có thể xử lý trực tiếp.

- Kiến trúc RISC (Reduced Instruction Set Computer): RISC (1980) ra đời từ các dự án nghiên cứu đột phá tại IBM, UC Berkeley và Đại học Stanford, nhằm giải quyết sự cồng kềnh và kém hiệu quả của CISC. Triết lý cốt lõi của RISC ngược lại hoàn toàn: giữ cho phần cứng càng đơn giản càng tốt và chuyển gánh nặng tối ưu hóa sang cho trình biên dịch (phần mềm). Tập lệnh của RISC bao gồm các lệnh đơn giản, có kích thước cố định (thường là 32-bit hoặc 64-bit) và hầu hết đều được thiết kế để thực thi trong một chu kỳ xung nhịp duy nhất. RISC loại bỏ hoàn toàn việc cho phép các lệnh toán học tương tác trực tiếp với bộ nhớ. Thay vào đó, nó áp dụng mô hình Load/Store nghiêm ngặt: chỉ có lệnh Load (nạp) và Store (lưu) được phép truy cập bộ nhớ RAM; tất cả các phép toán số học và logic khác bắt buộc phải thực hiện trực tiếp trên các thanh ghi đa năng (General-Purpose Registers). Mạch điều khiển của RISC được thiết kế theo dạng mạch nối cứng (Hardwired Control), giúp loại bỏ hoàn toàn tầng vi chương trình (Microcode) chậm chạp.

---

### 1.2. Trình bày ưu điểm và nhược điểm của từng loại kiến trúc

- Kiến trúc CISC:
    - Ưu điểm: Tối ưu hóa dung lượng bộ nhớ (Code Density cao):Do một lệnh phức tạp có thể thay thế cho một chuỗi lệnh dài, kích thước tệp mã máy sau khi biên dịch của CISC rất nhỏ gọn. Điều này cực kỳ có ý nghĩa trong kỷ nguyên bộ nhớ RAM và Flash còn đắt đỏ và hạn chế.
    - Đơn giản hóa cho lập trình viên và trình biên dịch:Trình biên dịch không cần thực hiện quá nhiều bước phân rã lệnh phức tạp, vì phần cứng đã đảm nhiệm phần lớn các thao tác phối hợp. Việc lập trình bằng ngôn ngữ hợp ngữ (Assembly) trên CISC cũng trực quan và gần gũi với ngôn ngữ bậc cao hơn.
    - Khả năng tương thích ngược tốt:Nhờ tầng vi chương trình (Microcode), các nhà sản xuất có thể dễ dàng duy trì tính tương thích ngược cho các thế hệ chip mới bằng cách cập nhật tập vi lệnh nội bộ mà không cần thay đổi cấu trúc phần cứng cốt lõi.
      
    - Nhược điểm: Phần cứng phức tạp và tiêu hao năng lượng lớn:Việc tích hợp mạch giải mã lệnh biến đổi và khối vi chương trình khiến chip CISC sở hữu số lượng bóng bán dẫn (transistors) khổng lồ. Điều này dẫn đến diện tích đế chip lớn, tỏa nhiệt cao và tiêu thụ điện năng lớn.
    - Hiệu suất chu kỳ lệnh thấp (CPI cao):Do tính chất phức tạp, các lệnh CISC cần số lượng chu kỳ xung nhịp rất khác nhau để hoàn thành (CPI biến thiên mạnh và thường lớn hơn 1 rất nhiều), gây khó khăn lớn cho việc tăng tần số xung nhịp tổng thể.
    - Hạn chế trong kiến trúc đường ống (Pipelining):Độ dài lệnh không cố định và thời gian thực thi bất định khiến việc triển khai kỹ thuật đường ống xử lý lệnh song song gặp nhiều xung đột (Hazards) phức tạp.

- Kiến trúc RISC:
    - Ưu điểm: Hiệu suất thực thi vượt trội nhờ kỹ thuật đường ống (Pipelining):Nhờ kích thước lệnh cố định và thời gian thực thi đồng đều, CPU RISC có thể dễ dàng triển khai kiến trúc đường ống nhiều tầng một cách tối ưu. Điều này cho phép nạp và thực thi các lệnh gối đầu nhau liên tục, hướng tới mục tiêu lý tưởng là CPI = 1.
    - Phần cứng tinh gọn và tiết kiệm điện năng:Việc loại bỏ khối điều khiển vi chương trình và đơn giản hóa mạch giải mã giúp giảm thiểu số lượng bóng bán dẫn. Kết quả là chip RISC có mức tiêu thụ điện năng cực thấp, diện tích nhỏ và chi phí sản xuất rẻ.
    - Tần số xung nhịp cao:Đường dòng điện đi qua các cổng logic nối cứng của RISC ngắn và đồng đều hơn, cho phép đẩy tần số xung nhịp (Clock speed) lên mức rất cao mà không gặp rào cản lớn về nhiệt độ.
      
    - Nhược điểm: Kích thước chương trình lớn (Code Density thấp):Để thực hiện cùng một tác vụ phức tạp, trình biên dịch trên kiến trúc RISC phải phân rã thành một chuỗi gồm nhiều lệnh đơn giản, khiến kích thước file thực thi lớn hơn đáng kể so với CISC.
    - Áp lực nặng lên trình biên dịch:Trình biên dịch phải cực kỳ thông minh để sắp xếp, phân bổ và tối ưu hóa thứ tự các lệnh đơn giản nhằm khai thác tối đa tài nguyên thanh ghi, đồng thời chủ động phòng ngừa các xung đột dữ liệu và xung đột điều khiển trong đường ống.

---

### 1.3. So sánh CISC và RISC theo các tiêu chí

#### 1.3.1. Cấu trúc tập lệnh
- CISC sở hữu số lượng lệnh lớn, độ dài lệnh biến đổi linh hoạt từ 1 đến nhiều bytes và định dạng lệnh phức tạp, tập trung tối đa vào các lệnh vĩ mô ở tầng phần cứng.
- RISC sở hữu số lượng lệnh hạn chế, độ dài lệnh cố định (thường là 32-bit hoặc 64-bit) và định dạng lệnh đồng nhất, hoàn toàn tập trung vào các lệnh đơn giản.

#### 1.3.2. Tốc độ xử lý
- CISC có tốc độ xử lý chậm hơn ở cấp độ lệnh đơn lẻ do mất nhiều chu kỳ xung nhịp để hoàn thành một lệnh (CPI lớn hơn nhiều so với 1) và rất khó tối ưu hóa kỹ thuật đường ống.
- RISC đạt tốc độ xử lý rất nhanh nhờ cơ chế pipeline tối ưu sâu, hầu hết mọi lệnh đều được hoàn thành chỉ trong 1 chu kỳ xung nhịp duy nhất (CPI xấp xỉ bằng 1).

#### 1.3.3. Kích thước chương trình
- Nhờ các lệnh phức tạp tích hợp nhiều thao tác, chương trình viết trên kiến trúc CISC cực kỳ nhỏ gọn và chiếm rất ít dung lượng bộ nhớ lưu trữ.
- RISC, do phải phân rã một tác vụ thành nhiều lệnh đơn lẻ, kích thước chương trình sẽ lớn hơn đáng kể và đòi hỏi nhiều dung lượng bộ nhớ hơn cho cùng một bài toán xử lý.

#### 1.3.4. Độ phức tạp phần cứng
- Phần cứng của kiến trúc CISC rất phức tạp, bắt buộc phải sử dụng vi chương trình (Microcode Control Unit) cùng mạch giải mã lớn, đồng thời trang bị ít thanh ghi đa năng (chỉ từ 8 đến 16 thanh ghi).
- Phần cứng RISC được thiết kế theo hướng đơn giản hóa tối đa, sử dụng mạch logic nối cứng (Hardwired Control) không cần microcode và trang bị một số lượng rất lớn các thanh ghi đa năng (thường từ 32 thanh ghi trở lên).

#### 1.3.5. Ứng dụng thực tế
- Kiến trúc CISC hiện nay đang thống trị thị trường máy tính cá nhân (PC), laptop và máy chủ (Server) hiệu năng cao với ví dụ tiêu biểu nhất là dòng kiến trúc x86/x64 do Intel và AMD phát triển (như các dòng chip Intel Core hay AMD Ryzen). 
- Kiến trúc RISC lại chiếm thế độc tôn tại thị trường thiết bị di động, thiết bị IoT, siêu máy tính và đặc biệt là hệ thống nhúng. Các ví dụ tiêu biểu bao gồm kiến trúc ARM (được dùng trong Apple Silicon M-series, chip Snapdragon, hay các vi điều khiển phổ biến như STM32) và kiến trúc mã nguồn mở mạnh mẽ RISC-V.

---

### 1.4. Nêu quan điểm cá nhân: Trong bối cảnh phát triển hệ thống nhúng hiện nay, kiến trúc nào phù hợp hơn? Vì sao?

Trong bối cảnh cách mạng công nghệ hiện nay, hệ thống nhúng không còn bó hẹp trong các mạch điều khiển tuyến tính đơn giản mà đã mở rộng mạnh mẽ thành hệ sinh thái Internet vạn vật (IoT), thiết bị đeo thông minh (Wearables), tự động hóa thế hệ mới và các hệ thống tính toán biên tích hợp trí tuệ nhân tạo (Edge AI). Các hệ thống này luôn đặt ra bốn bài toán tối hạn: Hiệu suất trên mỗi Watt (Performance-per-Watt), Tính thời gian thực (Real-time Determinism), Chi phí sản xuất (Silicon Cost), và Khả năng tùy biến chuyên dụng.

Dựa trên các yêu tố đó, kiến trúc RISC hoàn toàn phù hợp và vượt trội hơn CISC trong phát triển hệ thống nhúng hiện nay. Nhận định này được minh chứng qua các luận điểm kỹ thuật sau:

- Hiệu suất năng lượng tuyệt đối (Performance-per-Watt). Các thiết bị nhúng và IoT đa số vận hành độc lập, không có hệ thống tản nhiệt cưỡng bức và thường xuyên phải cấp nguồn bằng pin. Triết lý lược bỏ mạch điều khiển vi chương trình cồng kềnh của RISC giúp giảm hàng triệu bóng bán dẫn vô công, từ đó giảm thiểu dòng rò điện tĩnh (Static leakage current) và điện năng tiêu thụ động, giúp các vi điều khiển dựa trên nền tảng RISC đạt tỷ lệ hiệu suất trên năng lượng tiêu thụ tốt nhất.

- Tính đáp ứng thời gian thực nghiêm ngặt (Deterministic Execution). Trong các hệ thống nhúng điều khiển động cơ, robot hay y tế, tính ổn định về thời gian phản hồi là sống còn. Do các lệnh của RISC hầu hết đều thực thi trong một chu kỳ xung nhịp cố định và có cấu trúc đồng nhất, việc tính toán thời gian thực thi của chương trình và độ trễ ngắt (Interrupt latency) trở nên cực kỳ chính xác và dễ dự đoán, tránh được sự biến thiên chu kỳ lệnh gây nguy cơ cho các hệ điều hành thời gian thực (RTOS).

- Sự nhạt nhòa của nhược điểm dung lượng bộ nhớ. Rào cản lớn nhất của RISC trong quá khứ là kích thước chương trình lớn làm tốn bộ nhớ. Tuy nhiên, nhờ sự tiến bộ vượt bậc của công nghệ bán dẫn, giá thành của bộ nhớ Flash và SRAM tích hợp trên chip đã giảm sâu đáng kể. Đồng thời, các tập lệnh nén thông minh (như chế độ Thumb/Thumb-2 của ARM hay phần mở rộng C của RISC-V) giúp giảm kích thước code từ 30% đến 40%, triệt tiêu hoàn toàn điểm yếu về mật độ mã nguồn so với CISC.

- Sự bùng nổ của kiến trúc mã nguồn mở RISC-V và xu hướng Cá nhân hóa Chip (Custom SoC). Bản quyền kiến trúc x86 (CISC) bị độc quyền hoàn toàn bởi Intel và AMD, ngăn cản các công ty công nghệ tự thiết kế vi xử lý nhúng riêng. Trong khi đó, mô hình cấp phép lõi IP của ARM và đặc biệt là sự trỗi dậy của kiến trúc mã nguồn mở RISC-V mang lại sự tự do tuyệt đối. Các kỹ sư nhúng có thể tự do thêm hoặc bớt các tập lệnh chuyên dụng (như phần mở rộng cho xử lý tín hiệu số DSP, thuật toán mã hóa AES, hoặc bộ tăng tốc AI/NPU) ngay trên lõi CPU RISC để tạo ra các chip SoC chuyên dụng cho từng sản phẩm, tối ưu hóa tối đa giá thành và diện tích phần cứng.

KẾT LUẬN:Trong khi CISC vẫn giữ vai trò quan trọng ở mảng tính toán nặng, đa dụng như PC và Server nhờ di sản phần mềm đồ sộ, thì tại thị trường hệ thống nhúng - nơi mà sự tinh gọn, hiệu quả năng lượng và tính chuyên biệt hóa đặt lên hàng đầu, triết lý thiết kế của RISC chắc chắn là bệ phóng vững chắc cho tương lai công nghệ kết nối toàn cầu.
