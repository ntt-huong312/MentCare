# UC4. Xem lịch sử điều trị

## Phân tích lớp
- **Boundary**:
  - **PatientHistoryForm**: Giao diện để nhân viên lâm sàng tương tác, bao gồm tìm kiếm bệnh nhân và hiển thị lịch sử điều trị.
  - **PatientConnect**: Hệ thống quản lý hồ sơ bệnh nhân đóng vai trò trung gian, nhận yêu cầu từ giao diện Control tương tác với Database
- **Control**:
  - PatientHistoryController: Xử lý logic tìm kiếm trước khi trả kết quả
- **Entity**:
  - PatientDatabase: Thông tin tổng quan của bệnh nhân.
  - TreatmentRecord: Bản ghi chi tiết điều trị của bệnh nhân.

## Biểu đồ Sequence
![Diagram](https://www.planttext.com/plantuml/png/l9J1Ji9048RlVOe9Trw064DIOpWH4pdeSId5RjnkTJjBx95mu40yy0H63J51YHTFtGE74jzZdi1NCBK2bG92JBpkx7px_pD_ziDCgo4oXTeN5dCmK52gUyc3X0vFnh84B8HJPEssrGoqR34LmGb3xagiyH035Hq7ohUSGA8An4h9paw5gmhDTY2bww3bIkIuE3rYo9eiT2thwqae7wvvh0ADvCM7Iqxnr8SccRxqGAQIhUBb8c8fgWBdoLY3G_6J1joDkUpEaR_DLC3sT4Ic9m5Jq1L42xxrysgkUUwv0Wsb8-XGF9A0Nl8cBm2vN2jcJZaebzTXA7w43fdk9Wo8TBLmhTaMUpdsmb_TetZogxhy-7EKDVElyMnQ7fd1BcAtnyBsoDokDC-6P7fmu_eWo0mS3q8o4vWDEPck1bHa1dz9ZQ1u5EsC_gVmY4ro0CayW_D-dzRke4Nc5GGdqzVx1alixtXBdlPQpHw9sipDSbH4PK4wsngNgYjRwMVv2G00__y30000)


## Biểu đồ Lớp

![Diagram](https://www.planttext.com/plantuml/png/d5IzZjD04Exz55E68YzWeTD9oI4Y4OZk4FtUUcAFME-6sN4WGbSW2ju32YHgggIu8a_Y9xXNGBRNEMz-6XgljDytttxpvwVTuxKNnLAL9j56UGyB9OHMNfCNnvjNZalucW2CmQDYNKoO19aKf70dJ3PliLKNz8QyG0hDyJBeNBLuHdvbr0Qp8DkJtZCgAT7ABMh7MKE6y5287xs05DQEiXOAEW5h9CxYuPKOyuNxVCFiU8xUgnn7PNVsYHp83ydPKaoS5NR68BS50M0K9bpZiPlZz4-OlRrGjLasj72vBeMocS4sXH4stnHklcXS2JbxqVo2tP8CXXxEChH2IqAEshT0ziugCxDBnwLg12Fyblp7TyiFv0nQZH4q9PLRvyb7jmV_yJECNZErXkUOaMvVyY7dvvjkPYRE-if8SDDIXbSTQTRq9AlqYMKze4wL8AJG764QWsU8XxYpTu_PmNvCA9yznu0sP4ahyzO9HX10ZZAiRZiWCTorU8gYoFWXVjpAkR8gnyRMtSOBTdi9yAb2ZZP2XnKzcQfe9eTX_p6G3qbovayn7bzTtfeKSb8EXEhju-eeUa0RQ9nad88kgasz-sw336psVohGzVPtrIkU10q4-sr8GRZU_e9rlVi6Kkp_sXo4BDpNkn-s05liVzeakKQRDJ_6Vm000F__0m00)

**Giải thích**
- PatientHistoryForm:
  - Thuộc tính:
    - searchCriteria: Tiêu chí tìm kiếm (ví dụ: PID hoặc thông tin cá nhân bệnh nhân).
    - patientList: Danh sách bệnh nhân (sau khi tìm kiếm hoặc lấy từ hệ thống)
    - displayHistory: Lịch sử điều trị của bệnh nhân được chọn.
  -	Phương thức:
    -	searchPatient(): Xử lý bệnh nhân dựa trên searchCriteria
    -	displayPatientList(): Hiển thị danh sách bệnh nhân trên giao diện.
    -	displayHistory(): Hiển thị lịch sử điều trị của bệnh nhân được chọn.
    -	showErrorMessage(): Hiển thị thông báo lỗi trong trường hợp xảy ra lỗi (ví dụ: không tìm thấy bệnh nhân).
-	PatientHistoryController:
  -	Thuộc tính:
    -	staffAccessLevel: Mức độ quyền truy cập của nhân viên lâm sàng (được dùng để kiểm tra quyền).
  -	Phương thức:
    - validateAccess(): Kiểm tra xem nhân viên có quyền truy cập thông tin lịch sử của bệnh nhân hay không.
    - retrievePatientList(): Lấy danh sách bệnh nhân dựa trên quyền truy cập của nhân viên.
    - retrieveHistory(): Lấy lịch sử điều trị của bệnh nhân từ cơ sở dữ liệu.
    - handleError(): Xử lý lỗi khi có sự cố xảy ra (ví dụ: quyền không đủ, bệnh nhân không tồn tại).
- PatientProfile:
  - Thuộc tính:
    - patientId: Mã định danh duy nhất của bệnh nhân.
    - PersonalInformation: Thông tin cá nhân của bệnh nhân (ví dụ: họ tên, ngày sinh, địa chỉ).
    - RiskOfViolence: Đánh giá rủi ro về tự gây hại/bạo lực
    - Diagnosis: Chẩn đoán các tình trạng (bệnh nhân có thể mắc nhiều tình trạng cùng một lúc)
    - Treatment: Phương pháp điều trị (nhiều phương pháp điều trị có thể được kê đơn, bao gồm CBT)
    - PrescriptionMedications: Các loại thuốc đã kê đơn
    - Consultation: Các cuộc tư vấn
    - Introduction: Giới thiệu (thông tin về các giới thiệu đến các khoa lâm sàng khác, dịch vụ xã hội, v.v.)
    - consultationDate: Ngày và giờ tư vấn.
    - diagnosis: Chẩn đoán của bác sĩ trong lần khám.
    - prescribedTreatment: Phương pháp điều trị được kê đơn.
    - medications: Danh sách thuốc và liều lượng đã được kê đơn.
    - clinicalNotes: Ghi chú từ nhân viên lâm sàng.
    
  - Phương thức:
    - getPersonalInfo(): Trả về thông tin cá nhân của bệnh nhân.
    - getRecordDetails(): Trả về thông tin chi tiết của bản ghi lịch sử điều trị.
    
- PatientManagementSystem:
  - queryPatientList(criteria: String): List<Patient> - Truy vấn danh sách bệnh nhân dựa trên tiêu chí.
  - queryPatientHistory(patientId: String): List<TreatmentRecord> - Truy vấn lịch sử điều trị của bệnh nhân theo mã định danh.

# UC5. Tạo hồ sơ bệnh nhân

## Biểu đồ Sequence
![Diagram](https://www.planttext.com/plantuml/png/d5InRjim4Dtv5Mzi1_-0Xo10sZf06YDeZ08TQOasYKXaAb41F1OTCdGAEdJeKAiU2WGD6Y2TnC432_y7lw2_K51oAicEtA2J8DwxUtVl7ldRBFTJJHETnH6XWLO9Xjn-bQ-5lPQWAKurdKp8M6KofCaC9rGB9lKh5gWaVA6Is6FybmHAwaH5RSH1THYnnEFgFyAa5lflkPD4JKJ4F6PzyhoCR_4UKqcdB6PIdyvIpKhsZX0XPUlexPNzzN7ip1TC1LK8XJEN4fAxukOScjkVSWej92a7wkrLG_TnA9nvBw6vCnymyR7j548ZZGDxXzWkC3ma0B11FAoI6e1xdbgGFWREt8WcgA5TRwzhoZwEV9CnT4ARoLrwRP2E4bSiSE7CEvovOgdnDlC7sdwFSIPSiOpnHBfYcI6mTqyVQAkQi2LKBGx6NcSEwHtLAiIYbE6e0WPjyHuvzXjxdI5mnRSCsXMvAakq-69dFel_56D7iN_Etv7BPBXboU6cdLg9fDic3GC-g5TrVVeObTBykdBcIa2lRfrPo6cRP6V-mEQosLvWytLQwVjdpln0v6zJ1kxCuXoHCvVTQxml-t9rctLEZNfZ5Nwd3mQygGOkx5mXMEL8_MqFw_ugousuDtMJ-t4xZPpv97nnp6hVSMNd7b2-9jL-suNMpyYe8XlRNAszoftvY7IL-pxcaYFm0BBFPEYVuJy0003__mC0)
# Biểu đồ Lớp
## Phân tích lớp
- **Boundary**:
  - PatientRecordForm: Giao diện người dùng cho nhân viên lâm sàng để nhập thông tin bệnh nhân.
  - PatientManagementSystem: Hệ thống quản lý hồ sơ bệnh nhân.
- **Control**:
  - PatientRecordController: Điều khiển quy trình tạo hồ sơ bệnh nhân, xử lý dữ liệu nhập vào từ Nhân viên lâm sàng, và giao tiếp với hệ thống quản lý.
- **Entity**:
  - PatientProfile: thông tin cá nhân

![Diagram](https://www.planttext.com/plantuml/png/Z5F1JW913BtlLymH3iJxnX0JZSac4WahtkjCMHg73awx66ByCWz-ahzWPfSL5Z1XRzE-rxw-Td--lcz48Mgzyfdr86Ace8IiCxGXkliGL-OZC-aZNjTw1mfvXvd6i22FRRf2tOMB11mCpyCSoTh3jgojHP49Ya252Rm9vBBFx9oAsy0QW_SOEoqs8YZsG8Dr-pfkEypDImWUWLkgm0QVGfhZ1GGlO1rhcW13XIjaBRUY-ETFAho3NAgbGiO8YdEcjxeZ5oxP8Hg9gvFckq9Dpv4f7BBIWZ3cfcm9AJp5A8715xm8SGLAWNlv6Sdhu-APWaUss4lT4LGSXAGNVKfsfudxRIAAZRHEzIVeo3QT93SF97gzZumRz6rWgRtkr3IGmr0BAjAYNMtxaXkpDk39xPUU5ZWuyXD4gEBMp6CNizEx7et6_zvPRafa9yQ1Wj7GPn_W3cgSt4MUni48LiMyaoulATBjDpTpGUaO9wNFCahOe5pTezebjigpx0RPfN_x5m00__y30000)

**Giải thích**
- PatientRecordForm:
  - Thuộc tính:
    - inputData: Patient: Dữ liệu đầu vào từ nhân viên lâm sàng (bệnh nhân)
  - Phương thức:
    - getPatientInput(): Patient: Phương thức để thu thập thông tin bệnh nhân từ giao diện người dùng và trả về một đối tượng Patient.
    - displaySuccessMessage(): void: Phương thức để hiển thị thông báo thành công khi hồ sơ bệnh nhân được tạo thành công.
- PatientRecordController
  - Phương thức: 
    - reatePatientRecord(patient: PatientProfile): Phương thức điều khiển chính để tạo hồ sơ bệnh nhân, sử dụng thông tin bệnh nhân, cơ sở y tế, và liên hệ gia đình.
    - saveToDatabase(patient: Patient): boolean: Phương thức để lưu bệnh nhân vào cơ sở dữ liệu thông qua PatientManagementSystem.

- PatientRecordController:
  - Phương thức:
    - savePatient(patient: Patient): boolean: Phương thức lưu thông tin bệnh nhân vào cơ sở dữ liệu.
    - generateUniquePatientId(): string: Phương thức sinh mã bệnh nhân duy nhất khi bệnh nhân không có mã định danh.
      
- PatientProfile:
  - Thuộc tính:
    - patientId: Mã định danh duy nhất của bệnh nhân.
    - PersonalInformation: Thông tin cá nhân của bệnh nhân (ví dụ: họ tên, ngày sinh, địa chỉ).
    - RiskOfViolence: Đánh giá rủi ro về tự gây hại/bạo lực
    - Diagnosis: Chẩn đoán các tình trạng (bệnh nhân có thể mắc nhiều tình trạng cùng một lúc)
    - Treatment: Phương pháp điều trị (nhiều phương pháp điều trị có thể được kê đơn, bao gồm CBT)
    - PrescriptionMedications: Các loại thuốc đã kê đơn
    - Consultation: Các cuộc tư vấn
    - Introduction: Giới thiệu (thông tin về các giới thiệu đến các khoa lâm sàng khác, dịch vụ xã hội, v.v.)
    - FamilyContact: Thông tin liên hệ gia đình
    - HealthFacility: Cơ sở y tế của bệnh nhân
  - Phương thức:
    - validatePatientData(): boolean: Phương thức kiểm tra tính hợp lệ của thông tin bệnh nhân.
    - assignUniqueId(): string: Phương thức gán mã bệnh nhân duy nhất.


