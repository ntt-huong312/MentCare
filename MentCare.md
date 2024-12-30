# UC4. Xem lịch sử điều trị

## Phân tích lớp
- **Boundary**:
  - **PatientHistoryForm**: Giao diện để nhân viên lâm sàng tương tác, bao gồm tìm kiếm bệnh nhân và hiển thị lịch sử điều trị.
  - **PatientConnect**: Hệ thống quản lý hồ sơ bệnh nhân đóng vai trò trung gian, nhận yêu cầu từ giao diện Control tương tác với Database
- **Control**:
  - PatientHistoryController: Xử lý logic tìm kiếm trước khi trả kết quả
- **Entity**:
  - PatientProfile: Thông tin cá nhân.
  - PatientDatabase: Thông tin tổng quan của bệnh nhân.

## Biểu đồ Sequence
![Diagram](https://www.planttext.com/plantuml/png/l9IzJiCm58NtFCKHUryWGgXI4NH2bUZ2wAOfiKWSSAuhCY86Xeg19q204581iJ350qCgtkC-0Q-0Gai9_GSarjZtopdsbxpPbsf2GfE9GaTu56kixGJvjK9Nvdsr1f5WbqIduxHYezf2fsW8ahwYkamerkbMh2F7LoHflDBGSKU6lkF5YdGSJWpKXaz3NqyXQx5IlaSJk4r1eYKItt4-Wg2oCIE2YsR-4E50SlOIeSNsJ0LGHH5dUlCquYkKYxsyR-1nTcT0gp6_falaKHaNjS2aR4yLg00T8XtpdUzRIyEVdLqqjKdHvUnMWOByMUs3f9ePvfEoNgdCmd1sWoxRataOXCM5uyY81VLAx76_dO2pnwNfHbAK2JFEVZk_MaegNsI9Ddg1YxeSddR0jhTAsSLQrGAsvnF3WmksfpZs8uHiUrw0XEqZ1XUIxOa1QRQzlrWNSdQRhep-9_dcnW6nlOVtUbMiNQBDzWcXP7jcVYhcBnely74fhV4h8tzquqlrd4yRIZcTRMZbQf3ldq_LL-tYB_yE003__mC0)


## Biểu đồ Lớp

![Diagram](https://www.planttext.com/plantuml/png/f5J1RjD04BtxA-OO3la12rMLaY8YjH0Ln7sxdjWZrhDXTXo840V4WV-00n9dJicXXto9lw2_WEoiYzqwKYKkNcdVl3VpPcPzjxyz3sf4gz8brfaGO6cKaFKb1VMoVU6bXCy9m1G26h75J4XHo40ARrI8ynPR7qcN51HIQ8xdKMSfVaKEpn80Y18HcJo353QUiXRAAAoTsKQiKHZ5Orb3B1J-uuM8boiCmUGuAOzdL-9zy9TaQ7BcMSKxXz9w111K8TpWmp9EEYeCPmxRv1DilYbSVBAuLl9yCcrKY7rTPCXAAq8Pj7I94ZmRj-2Lbz8qWWFyciBxrwjtv1sonG4q9vEp3nG6jsy5ZPR8EamZ6AnGM_0LPcJRJ25Q_dVJs9t2p7EedCPgsf3-rJ5eqJGrg-oZagqZ9clSAwyO-Wi4aAFs3RTD7yBNQBraSrH3BlJnaQ4oMeqJ_L2X3BRAnWNkByVbs7WVwiwDcXiJkh6TN8d_oZZo-gRJiv5zJI4duq6ftjskEreF7xBQXgHWYsfRxxznfC7syBi2M-z-LJs5DhP7xtm_XNxVenw_s_OKLEhTJzZK-w-WnU4Fvw34S5FlltC1N1n-S9AS8sVDp-Wl0000__y30000)

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
-	PatientController:
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
    - clinicalNotes: Ghi chú từ nhân viên lâm sàng.
    
  - Phương thức:
    - getPersonalInfo(): Trả về thông tin cá nhân của bệnh nhân.
    - getRecordDetails(): Trả về thông tin chi tiết của bản ghi lịch sử điều trị.
- PatientConnect:
  + queryPatientList(criteria: String) : List<PatientProfile>
- PatienDatabase:
  - Thuộc tính:
    - List<PatientProfile>
  - Phương thức:
  - queryPatientList(criteria: String): List<PatientProfile> - Truy vấn danh sách bệnh nhân dựa trên tiêu chí.

# UC5. Tạo hồ sơ bệnh nhân
## Phân tích lớp
- **Boundary**:
  - PatientForm: Giao diện người dùng cho nhân viên lâm sàng để nhập thông tin bệnh nhân.
  - PatientConnect: Hệ thống quản lý hồ sơ bệnh nhân.
- **Control**:
  - PatientRecordController: Điều khiển quy trình tạo hồ sơ bệnh nhân, xử lý dữ liệu nhập vào từ Nhân viên lâm sàng, và giao tiếp với hệ thống quản lý.
- **Entity**:
  - PatientProfile: Thông tin cá nhân.
  - PatientDatabase: Thông tin tổng quan của bệnh nhân.


## Biểu đồ Sequence
![Diagram](https://www.planttext.com/plantuml/png/l5MxRjim5Dtr5MTi1_-01YD0aZf06YDeZ08TQOcsY4XaAb41F1OTCdGAEdJeKAiU2WGD6Y2TnC432_y7lo2_453oWwgj8EZGII1vxhtddllGWvhlPPAaCazYZmHIfEX7-Zj_o_GD1ybm9ibev0r5paEIJd1A9ADSlg61ICDN8aqinduzoYMJQy1fAaOifbuWk4n5lBhUhuynJQtTvhJRscAMDuVL-nQF0oB9a6GkyeHmCgO9vV9iaacQU5wL0ZhTYgUF4wE-OSo8GCYCkkBWaIblBo0Z_PkF8HdtgiGwdMwTlOyZPjH73XaPzGaZ-xXjuv5OOb_V8z4pz8yy0FWhShysSW1reAwZX8-UKRVC1JcYTRfjQVeujYGJo9IunYtmAZitwY0rvGoNHdt0kIdd4kzpUo7rpmJdp9Jp12-uAUSv0dt_iftNidG-UhhWJLThhJ2qkaVWjjDSbgkwTzQIDPHlyT0WHkECuhW61irgF5F7T_ecHs3A7pcaAGjHkMZ4IupwolvLtQJTstyNj8KBvU7Mr2nxjorcUoCx8x8pltgoVGmghVzS6tND81TtHituk1daIVjA7eTUe8kbMJMP1qRzGcm7FaTarEm2iL5NxRAltBvUtENFKVgmNc1FDLOlSjN0fPuA18i2cLr8uOPVtSE3o4wT6ti7sHqrZOtwmgnpJ3QD70azjO1guTNrTHrjDjsWZZRKXLXsVsJKPsIBmXAPyWY11NXxb8Vsb_48003__mC0)
# Biểu đồ Lớp
![Diagram](https://www.planttext.com/plantuml/png/l5GzQ-D04EtrAxPq2dEzE48WuK2G49ElVhCxLeQiPvMTMOCvhifFkU8W44YHoYvI1F8_z0lo5y9ALY8vBboTkfrvRzxRqPFULoy7B3f8dBdCECsi9beGICx0-61_-J1JlpEL7gGgof4MdNUOIV1JTD2sIv1rkKZ0qTvsc4Mkd5wSHsE0-GIOTGa9FFTeip_PqCMX9mdUEGYT2nD02mnCZghsj2cubwjhxnreQgcivt3XqmskDSCEh2rk28nqLjAyTMTN2oKG12rmINWNEt9Xq_rP0bBvJREp-rz5ruCQpR4gB93W527awhmbfF840dlIhg2f3pCjw6dGFqE-FPrUeNT01WQj8zGbUKOUL2_Igvqr5-hB160Ji4hpJy2YQPGuLyV8ylEhij-W3prnTB9sqq3wfHPKf53PQ8QMcsNDjKFx5R2q_T76FZKpbjGkStEBsVUlPppUtvBcN9NrwX7LulKXAbCl_yMEsWCDgKtqScLkug9UtPCIh9SlrVO93RP7_qpHBlnFS6z0buXSkRUd-4D2lVohvERrcKebI5bs06JJJ-G3003__mC0)

**Giải thích**
- PatientRecordForm:
  - Thuộc tính:
    - inputData: Patient: Dữ liệu đầu vào từ nhân viên lâm sàng (bệnh nhân)
  - Phương thức:
    - getPatientInput(): Patient: Phương thức để thu thập thông tin bệnh nhân từ giao diện người dùng và trả về một đối tượng Patient.
    - displaySuccessMessage(): void: Phương thức để hiển thị thông báo thành công khi hồ sơ bệnh nhân được tạo thành công.
- PatientController
  - Phương thức: 
    - reatePatientRecord(patient: PatientProfile): Phương thức điều khiển chính để tạo hồ sơ bệnh nhân, sử dụng thông tin bệnh nhân, cơ sở y tế, và liên hệ gia đình.
    - saveToDatabase(patient: Patient): boolean: Phương thức để lưu bệnh nhân vào cơ sở dữ liệu thông qua PatientManagementSystem.
- PatientConnect:
  - Phương thức:
    - savePatient(patient: Patient): boolean: Phương thức lưu thông tin bệnh nhân vào cơ sở dữ liệu.
    - generateUniquePatientId(): string: Phương thức sinh mã bệnh nhân duy nhất khi bệnh nhân không có mã định danh.
      
- PatientDatabase:
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


