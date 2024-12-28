# UC4. Xem lịch sử điều trị

## Phân tích lớp
- **Boundary**:
  - **PatientHistoryForm**: Giao diện để nhân viên lâm sàng tương tác, bao gồm tìm kiếm bệnh nhân và hiển thị lịch sử điều trị.
  - **PatientManagementSystem**: Hệ thống quản lý hồ sơ bệnh nhân đóng vai trò trung gian, nhận yêu cầu từ giao diện Control tương tác với Database
- **Control**:
  - PatientHistoryController: Xử lý logic tìm kiếm trước khi trả kết quả
- **Entity**:
  - PatientDatabase: Thông tin tổng quan của bệnh nhân.
  - TreatmentRecord: Bản ghi chi tiết điều trị của bệnh nhân.

## Biểu đồ Sequence
![Diagram](https://www.planttext.com/plantuml/png/n9N1RjD048Rl-nIZtlC2KOKg5Q5Ug12D41mtwsrsXJs6zRZ2nog77Y8EVG9KK8KeL5muUGyzEE8zvWbu1UH63OdjfKugnDNh-UVVVpxD_l8tUnb9HtaI2waeTN1ege_umbPN23A38vB7nsASvXX9Ly0pILOZ7TYCKbSyILqYL8haqhXnjB_u6clNAdugKKvqef6EYenq8ZIIfUNnOqboB3DzztdajAJwx-TQfIuIujOI31vrc1d2lc7_7a4PzbyKu7oA4zXvgHE8sS-KWOpzzOveLxRr_jnW2A-ggnmKbvzpYBcyB22IQ22hBfI1CVipD81rR28aiIBVl7xjEI_OJn78Sddp1efbDn6eMP6xYsi88vSNSCBb9ORi0R7_2khdHHt31uZOVuVOiZyBDzeT3BewSVa9JjYVRXx4Yc0xYKF3vNNGVjVOLkGwvdPW5xaQzhEWwj-16bNV4dXT3oQvrqnVXgYVvd_3Xqpr0oT05ZljRGn9G0_YsotpDfSFvEKUlrloqiDrhrsqLZm_Pp-5T-iB2URdblrf3kJOpnw-dVfA_rF06djx3R2WmIqtL4Ul9NnRXB7RWxcDnhS1TM7T1MjjgGLiZJUkKRkdCQgV-Dy0003__mC0)


## Biểu đồ Lớp

![Diagram](https://www.planttext.com/plantuml/png/d5GxRjj04ErvYYcLGXSW0iE0v202eaImZVJhvOWSUBchx0wL284B8qKALxb2KWGma2wLMAYGBy8Jv0e1oQNCrIT56YwmR_RDU_FXdt9pxbXOBd8LIIMSWvbWGisloR6ngrV6vl0v0XY2Gs5bDhB4Q4b035TiIQSDjcWVlI7744DzlFGyPmsUa5ieiSB4qtP1rnO5vwZv4gMnIHqCFf5_FtW1CImD9GtaUJnMKnp5VPOGSvdvU66jiLDqJgGuoDkpCx8BlekEbc9aD5kZ5Dgc800MsH8kSL_Dlls3o4wUhzeawKiuNPTCw4HXOs60zJU6YqyI5qn6dnG_isPE2dqF9mbgfZcX3TetG-kC5cgYvyRceYOCy4joj-_cxyaer183Q4mYrSQH2svt-iCq5fsqr0YUOaAooUIyv-URTcP6Hhj2iLVJXFIlsg19tPEaa7kI0LBalgkcCHxUbUWwhBAlaUmb6Gj6YA4-_1nxjtlZtngxmMH76GRapsv3G2hI98LwQnW3g77GwXeZ2rBkg0NVvQdG8iKwxzNACROh2_2XG1iiY_JRUp1mmRZsd_t7hDv5qP6Vo71uTdgXOaX9662grfj5T3Aint7WE0QP5Qkg_A8z3QosZmN8Qlspw1WF7lK8kqM9WMsr_W7Bghm7phQ_TGfC6cwgyglEG6VRx_gVVFjJ5H2ggdoG6RYg_0LFtwWgxuiQBXywoav6GtM4Iz7sKSDjjTvmT8uwgN_SVm400F__0m00)

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
    - FamilyContact: Thông tin liên hệ gia đình
    - HealthFacility: Cơ sở y tế của bệnh nhân
  - Phương thức:
    - getPersonalInfo(): Trả về thông tin cá nhân của bệnh nhân.

- TreatmentRecord:
  - Thuộc tính:
    - consultationDate: Ngày và giờ tư vấn.
    - diagnosis: Chẩn đoán của bác sĩ trong lần khám.
    - prescribedTreatment: Phương pháp điều trị được kê đơn.
    - medications: Danh sách thuốc và liều lượng đã được kê đơn.
    - clinicalNotes: Ghi chú từ nhân viên lâm sàng.
  - Phương thức:
    - getRecordDetails(): Trả về thông tin chi tiết của bản ghi lịch sử điều trị.
- PatientManagementSystem:
  - queryPatientList(criteria: String): List<Patient> - Truy vấn danh sách bệnh nhân dựa trên tiêu chí.
  - queryPatientHistory(patientId: String): List<TreatmentRecord> - Truy vấn lịch sử điều trị của bệnh nhân theo mã định danh.

# UC5. Tạo hồ sơ bệnh nhân

## Biểu đồ Sequence
![Diagram](https://www.planttext.com/plantuml/png/d5InRjim4Dtv5Mzi1_-0Xo10sZf06YDeZ08TQOasYKXaAb41F1OTCdGAEdJeKAiU2WGD6Y2TnC432_y7lw2_K51oAicEtA2J8DwxUtVl7ldRBFTJJHETnH6XWLO9Xjn-bQ-5lPQWAKurdKp8M6KofCaC9rGB9lKh5gWaVA6Is6FybmHAwaH5RSH1THYnnEFgFyAa5lflkPD4JKJ4F6PzyhoCR_4UKqcdB6PIdyvIpKhsZX0XPUlexPNzzN7ip1TC1LK8XJEN4fAxukOScjkVSWej92a7wkrLG_TnA9nvBw6vCnymyR7j548ZZGDxXzWkC3ma0B11FAoI6e1xdbgGFWREt8WcgA5TRwzhoZwEV9CnT4ARoLrwRP2E4bSiSE7CEvovOgdnDlC7sdwFSIPSiOpnHBfYcI6mTqyVQAkQi2LKBGx6NcSEwHtLAiIYbE6e0WPjyHuvzXjxdI5mnRSCsXMvAakq-69dFel_56D7iN_Etv7BPBXboU6cdLg9fDic3GC-g5TrVVeObTBykdBcIa2lRfrPo6cRP6V-mEQosLvWytLQwVjdpln0v6zJ1kxCuXoHCvVTQxml-t9rctLEZNfZ5Nwd3mQygGOkx5mXMEL8_MqFw_ugousuDtMJ-t4xZPpv97nnp6hVSMNd7b2-9jL-suNMpyYe8XlRNAszoftvY7IL-pxcaYFm0BBFPEYVuJy0003__mC0)
## Biểu đồ Lớp

![Diagram](https://www.planttext.com/plantuml/png/Z5J1Rjim3BtxAtHiWGQx6qDHe44m0qiMDEdkZ4Gxn6Gf4-aCmT0lss6Vj5yO5Dk9vQH5V2FvnFVqIFdVdxzFB12agMscBJ2h9GYXanVKFfYP3xNwdQduaTirCWM1lCUq-GgbYuk8kBiVrGtnpi9XrMYDp7DaXWeZQk_9P6_PDTvdxoHuQp7qx3eW22QWkrqRdVWUr1R1odO6cYp98LTValX1bL2JFSJke2LNis5udwkDznR1jOmCUrpxUE4DC5wG3U3ZEyp1GOKrEbaTMF3aOEpOGJvgrxdgC83WgwEVJN-gCD4tba2kkc1T1b-InIFPH1K6dL1967ArQW_4z183UmUsSAKFDGXvbzHVY7zyAx-Jj-Wq9gKfGUKy4oVPTPnBl6fA4v1re5tiFqT3-iZ4kVfAB9_FcSSZ-jaxRgnqQewGOQe55N4ZJAD7afK2OoWcmIwy89_yYRKzM3BdlOd3l1iv3SnKkTRcw_wcIzGFi-pYmYICf_m2QamhO4n0JWMgtTOxN3Jr9WvgMAXGUief2f3bg2tLSjQORFBfpRJXMA6xK1RG7frU-ywe6pLY3MJJLEzu9oNksT3njoox_C5C9e_lFlzShT0PLWO4bFZiFToWntpy_FAuF1X02wjV9DjRclIlALUlZFpXYT5-t70YdLPwu4BzLL4hs2D_cg7eBRRcPDaJEXF_u_y1003__mC0)
