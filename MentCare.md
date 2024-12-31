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

![Diagram](https://www.planttext.com/plantuml/png/l9CzQWCn48LxdKAbNPZqMmH3Gi15mEJd06FjH1R8euqqCfYGAaT94GW4KgIo2nU6t6DFa2k4zQuSUxs5gwWJyzvyJoFfPxKU1WRFSMQ5iX2270CR9Bv1vNn-vVnCFWbPBOtSr4PKHExriwGTU_TWBDQot8J2mk8sAeKXN6C8eB4Ipvt9nRCun5muOk-iHPymoYCm7gJe5VMk3UndSkASHQ3Q6c2ET-uI62OGy0HNHnf2nIbArQ-fd1f18w47ndioZp6PHtbr_i3Ua3vYfhZ_2cqQDSmvM9F_3RrAr6in80IZgGQCMft5yPCP3CuxRZYJkbnz6BdOl4UfokLRJDOzqQ5rUnsPLDEuA5Sl9DcKotNHtM6htRFl9fjrw7V5FKEQIYRjzsSyOrykNoLFDr-a9HiIOeYKLp_b5m00__y30000)

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
  -	Th
  -	Phương thức:
    - retrieveHistory(): Lấy lịch sử điều trị của bệnh nhân từ cơ sở dữ liệu.
    - handleError(): Xử lý lỗi khi có sự cố xảy ra (ví dụ: quyền không đủ, bệnh nhân không tồn tại).
- PatientProfile:
  - Thuộc tính:
    - patientId: Mã định danh duy nhất của bệnh nhân.
    - patientName: Tên bệnh nhân
    - address: Địa chỉ
    - birthday: Ngày sinh
    - contactInfo: Thông tin liên lạc
    - registeredMedicalFacility: Cơ sở y tế đã đăng ký
    - familyContactInfo: Thông tin liên hệ gia đình
    - RiskOfViolence: Đánh giá rủi ro về tự gây hại/bạo lực
    - Diagnosis: Chẩn đoán các tình trạng (bệnh nhân có thể mắc nhiều tình trạng cùng một lúc)
    - Treatment: Phương pháp điều trị (nhiều phương pháp điều trị có thể được kê đơn, bao gồm CBT)
    - PrescriptionMedications: Các loại thuốc đã kê đơn
    - Consultation: Các cuộc tư vấn
    - Introduction: Giới thiệu (thông tin về các giới thiệu đến các khoa lâm sàng khác, dịch vụ xã hội, v.v.)
    
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
  - PatientController: Điều khiển quy trình tạo hồ sơ bệnh nhân, xử lý dữ liệu nhập vào từ Nhân viên lâm sàng, và giao tiếp với hệ thống quản lý.
- **Entity**:
  - PatientProfile: Thông tin cá nhân.
  - PatientDatabase: Thông tin tổng quan của bệnh nhân.


## Biểu đồ Sequence
![Diagram](https://www.planttext.com/plantuml/png/l5MxRjim5Dtv5GVP_GCUZ00EcW113QCr2dIaPJeY8f6fH0N8M7J8qB53Xmwrww60qQ13Euc31mBv3tv1Vw6Wv8SaIxRgePCWwfvp3yzzw8zUdSUAHYe90q8z9ICCVFDDlE5cAK1Zl5PqEYLZcOW9ZHumf8epeLunJqQJ5p8ANOnx4YOKLzk0OIIdF634aq95CjWSz_FNW4KEjtkheFjI2EOf5rC-sHDoGHKTqvWLGZT7X6JQqUbb0hjuQVLNt70gCU5MFme8twPFTr2--IrkeBWWsOqwdLv-xIwkkDKV19HlzKTCtSTz3A61Gj_yGcWM65mH0AXa7kIWGa2Ug5Ume8jBgvzuCQZWLgTNSQABQwSjX8fe4LDnS8VRs784k3MqKvDo5DbqWNkht-FMfYk5TuaxKEP7Y5jkqrM8MX6LYxQbATv_fsRTMbrSchae4soBWh4hi0_XUhaeQGtE-FBQb4hSm032WfZXEl_gbMkzProDvIERpcK6Aj66Ld_XfxX_dAc5zmT8_h_p3MAOcEpDyNgQcd9kHgjMT05qRsQoZAmghHlFmk0V7i-tPfd0i-dtn66MOTtjMWnh6vfi0vrTMFqJWTji2Noh5tS8h7uyQz-ZJVGdz6VJ79tIfiUv_hLR3qiQdhOYCfwyHlcs6FbkbMLbstHCZTYQ387LdxbhJppiYkzBCtC1sPyh7ujQfb6URMpc4YhREhxLdn0_pvsGcV3XkG1opiGa2OE_0000__y30000)
# Biểu đồ Lớp
![Diagram](https://www.planttext.com/plantuml/png/l9CzQWCn48LxdKAbNPZqMmH3Gi15mEJd06FjH1R8euqqCfYGAaT94GW4KgIo2nU6t6DFa2k4zQuSUxs5gwWJyzvyJoFfPxKU1WRFSMQ5iX2270CR9Bv1vNn-vVnCFWbPBOtSr4PKHExriwGTU_TWBDQot8J2mk8sAeKXN6C8eB4Ipvt9nRCun5muOk-iHPymoYCm7gJe5VMk3UndSkASHQ3Q6c2ET-uI62OGy0HNHnf2nIbArQ-fd1f18w47ndioZp6PHtbr_i3Ua3vYfhZ_2cqQDSmvM9F_3RrAr6in80IZgGQCMft5yPCP3CuxRZYJkbnz6BdOl4UfokLRJDOzqQ5rUnsPLDEuA5Sl9DcKotNHtM6htRFl9fjrw7V5FKEQIYRjzsSyOrykNoLFDr-a9HiIOeYKLp_b5m00__y30000)

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
    - patientName: Tên bệnh nhân
    - address: Địa chỉ
    - birthday: Ngày sinh
    - contactInfo: Thông tin liên lạc
    - registeredMedicalFacility: Cơ sở y tế đã đăng ký
    - familyContactInfo: Thông tin liên hệ gia đình
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


