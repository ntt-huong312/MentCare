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
![Diagram](https://www.planttext.com/plantuml/png/d5InRjim4Dtv5Mzi1_-0Xo10sZf06YDeZ08TQOasYKXaAb41F1OTCdGAEdJeKAiU2WGD6Y2TnC432_y7lw2_K51oAicEtA2J8DwxUtVl7ldRBFTJJHETnH6XWLO9Xjn-bQ-5lPQWAKurdKp8M6KofCaC9rGB9lKh5gWaVA6Is6FybmHAwaH5RSH1THYnnEFgFyAa5lflkPD4JKJ4F6PzyhoCR_4UKqcdB6PIdyvIpKhsZX0XPUlexPNzzN7ip1TC1LK8XJEN4fAxukOScjkVSWej92a7wkrLG_TnA9nvBw6vCnymyR7j548ZZGDxXzWkC3ma0B11FAoI6e1xdbgGFWREt8WcgA5TRwzhoZwEV9CnT4ARoLrwRP2E4bSiSE7CEvovOgdnDlC7sdwFSIPSiOpnHBfYcI6mTqyVQAkQi2LKBGx6NcSEwHtLAiIYbE6e0WPjyHuvzXjxdI5mnRSCsXMvAakq-69dFel_56D7iN_Etv7BPBXboU6cdLg9fDic3GC-g5TrVVeObTBykdBcIa2lRfrPo6cRP6V-mEQosLvWytLQwVjdpln0v6zJ1kxCuXoHCvVTQxml-t9rctLEZNfZ5Nwd3mQygGOkx5mXMEL8_MqFw_ugousuDtMJ-t4xZPpv97nnp6hVSMNd7b2-9jL-suNMpyYe8XlRNAszoftvY7IL-pxcaYFm0BBFPEYVuJy0003__mC0)
# Biểu đồ Lớp


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


