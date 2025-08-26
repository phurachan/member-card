# ระบบบัตรสมาชิก

## การใช้งานบนอุปกรณ์เคลื่อนที่ (มือถือ,แท็บเล็ต)
### โมดูลทั้งหมด

```mermaid
graph TD
    START([ระบบบัตรสมาชิก]) --> COMMON[โมดูลทั่วไป]
    START --> REG[โมดูลการลงทะเบียน]
    START --> AUTH[โมดูลการตรวจสอบสิทธิ์]
    START --> QR[โมดูล QR Code]
    START --> HIST[โมดูลประวัติ/ธุรกรรม]
    START --> PROF[โมดูลโปรไฟล์]
```

### 1. โมดูลทั่วไป

```mermaid
graph TD
    COMMON[โมดูลทั่วไป] --> STEP1[หน้าจอ 1: หน้าหลัก]
    
    STEP1 -->CUST_HOME[แดชบอร์ดหน้าหลักสมาชิก<br/>COMMON_HOME_01]
    STEP1 -->EMP_HOME[แดชบอร์ดหน้าหลักพนักงาน<br/>COMMON_HOME_02]
    
```

### 2. การลงทะเบียนสมาชิกด้วยมือถือ (สมาชิกทำด้วยตัวเอง)

```mermaid
graph TD
    REG[การลงทะเบียนสมาชิกด้วยมือถือ] --> STEP1[หน้าจอ 1: ลงทะเบียน]
    
    STEP1 -->UC1[กรณีการใช้งาน 1:<br/>ลงทะเบียนสมาชิกใหม่ ป้อนข้อมูลบังคับครบถ้วน<br/>REG_REGISTER_01]
    STEP1 -->UC2[กรณีการใช้งาน 2:<br/>ลงทะเบียนล้มเหลว - แจ้งเตือนข้อมูลซ้ำ<br/>REG_REGISTER_02]

    UC1 -->STEP2[หน้าจอ 2: ยืนยัน OTP]
    UC2 -->STAY_SCREEN_1[อยู่หน้าเดิม<br/>หน้าจอ 1: ลงทะเบียน]

    STEP2 -->UC5[กรณีการใช้งาน 1:<br/>ส่งข้อมูลสำเร็จ<br/>AUTH_VERIFY_01]
    STEP2 -->UC6[กรณีการใช้งาน 2:<br/>ข้อความแจ้งเตือน OTP หมดอายุ<br/>AUTH_VERIFY_02]
    STEP2 -->UC7[กรณีการใช้งาน 3:<br/>ข้อความแจ้งเตือนยืนยันส่ง OTP อีกครั้ง<br/>AUTH_VERIFY_04]
    STEP2 -->UC8[กรณีการใช้งาน 4:<br/>ข้อความแจ้งเตือนส่งข้อมูลล้มเหลว<br/>AUTH_VERIFY_03]

    UC5 -->SUCCESS[เปลี่ยนเส้นทางไปหน้าหลัก]
    UC6 -->STAY_SCREEN_2[อยู่หน้าเดิม<br/>หน้าจอ 2: ยืนยัน OTP]
    UC7 -->STAY_SCREEN_2
    UC8 -->STAY_SCREEN_2
```

### 3. การเข้าสู่ระบบ

```mermaid
graph TD
    AUTH[การเข้าสู่ระบบ] --> STEP1[หน้าจอ 1: เข้าสู่ระบบ<br/>ป้อนข้อมูลเบอร์โทรศัพท์]
    
    STEP1 -->UC1[กรณีการใช้งาน 1:<br/>พบผู้ใช้และลงทะเบียนแล้ว<br/>AUTH_LOGIN_01]
    STEP1 -->UC2[กรณีการใช้งาน 2:<br/>พบผู้ใช้แต่ยังไม่ได้ลงทะเบียน<br/>AUTH_LOGIN_02]
    STEP1 -->UC3[กรณีการใช้งาน 3:<br/>พบผู้ใช้ที่มีหลายบทบาท - เลือกบทบาท<br/>AUTH_LOGIN_03]
    STEP1 -->UC4[กรณีการใช้งาน 4:<br/>ไม่พบผู้ใช้ - แสดงข้อผิดพลาด<br/>AUTH_LOGIN_04]

    UC1 -->STEP2[หน้าจอ 2: ยืนยัน OTP]
    UC2 -->STEP2
    UC3 -->STEP2
    UC4 -->STAY_SCREEN_1[อยู่หน้าจอเดิม<br/>หน้าจอ 1: เข้าสู่ระบบ]
    
    STEP2 -->UC5[กรณีการใช้งาน 1:<br/>ส่งข้อมูลสำเร็จ<br/>AUTH_VERIFY_01]
    STEP2 -->UC6[กรณีการใช้งาน 2:<br/>ข้อความแจ้งเตือน OTP หมดอายุ<br/>AUTH_VERIFY_02]
    STEP2 -->UC7[กรณีการใช้งาน 3:<br/>ข้อความแจ้งเตือนยืนยันส่ง OTP อีกครั้ง<br/>AUTH_VERIFY_04]
    STEP2 -->UC8[กรณีการใช้งาน 4:<br/>ข้อความแจ้งเตือนส่งข้อมูลล้มเหลว<br/>AUTH_VERIFY_03]

    UC5 -->SUCCESS[เปลี่ยนเส้นทางไปหน้าหลัก]
    UC6 -->STAY_SCREEN_2[อยู่หน้าจอเดิม<br/>หน้าจอ 2: ยืนยัน OTP]
    UC7 -->STAY_SCREEN_2
    UC8 -->STAY_SCREEN_2
    
```

### 4. โมดูล QR Code

```mermaid
graph TD
    QR[โมดูล QR Code] --> STEP1[หน้าจอ 1:<br/>*สมาชิก:* สร้าง QR Code<br/>QR_QRCODE_01]
    
    STEP1 --> STEP2[หน้าจอ 2:<br/>*พนักงาน:* สแกน QR Code ผ่านหน้าสแกน<br/>QR_SCAN_01]
    STEP2 --> STEP3[หน้าจอ 3:<br/>*พนักงาน:* การป้อนข้อมูล<br/>QR_FILL_01]
    STEP3 -->FILL_STANDARD[กรณีการใช้งาน 1:<br/>*พนักงาน:* ป้อนรายละเอียดและใช้ราคา/หน่วย จากส่วนกลาง<br/>QR_FILL_01]
    STEP3 -->CUSTOM_PRICE[กรณีการใช้งาน 2:<br/>*พนักงาน:* ป้อนรายละเอียดและราคา/หน่วย ด้วยตนเอง<br/>QR_FILL_02]
    STEP3 -->USE_COUPON[กรณีการใช้งาน 3:<br/>การใช้โควต้าคูปองแทนโควต้าสมาชิก<br/>QR_FILL_05]
    
    USE_COUPON -->LICENSE_VERIFY{*พนักงาน:* ตรวจสอบป้ายทะเบียน}
    LICENSE_VERIFY -->|ป้ายทะเบียนตรงกัน| LICENSE_APPROVED[กรณีการใช้งาน 6:<br/>*พนักงาน:* ป้ายทะเบียนตรงกัน และป้อนรายละเอียด<br/>QR_FILL_06]
    LICENSE_VERIFY -->|ป้ายทะเบียนไม่ตรงกัน| LICENSE_BLOCKED[กรณีการใช้งาน 7:<br/>*พนักงาน:* ป้ายทะเบียนไม่ตรงกัน<br/>QR_FILL_07]
    
    FILL_STANDARD -->CONNECTION_1[*พนักงาน:* ป้อนข้อมูลการเติมน้ำมันบังคับครบถ้วน]
    CUSTOM_PRICE -->CONNECTION_1
    LICENSE_APPROVED -->CONNECTION_1
    LICENSE_BLOCKED -->CANCEL[*พนักงาน:* ยกเลิกธุรกรรม<br/>QR_FILL_04]
    LICENSE_BLOCKED -->RETRY_LICENSE[*พนักงาน:* ลองถ่ายป้ายทะเบียนใหม่]
    RETRY_LICENSE -->LICENSE_VERIFY
    
    CONNECTION_1 -->WAITING[*พนักงาน:* ส่ง OTP ให้สมาชิก <br/>และรอการยืนยันจากสมาชิก<br/>QR_FILL_03]
    CONNECTION_1 -->CONFIRM_BACK[*พนักงาน:* ยกเลิกธุรกรรม<br/>QR_FILL_04]
    
    WAITING --> STEP4[หน้าจอ 4:<br/>*สมาชิก:* การยืนยันข้อมูลการเติมน้ำมัน<br/>QR_VERIFY_01]

    STEP4 -->VERIFY_DATA[กรณีการใช้งาน 1:<br/>*สมาชิก:* ยืนยันรายละเอียด]
    STEP4 -->CANCEL_VERIFY[กรณีการใช้งาน 2:<br/>*สมาชิก:* ยกเลิกการใช้โควตา<br/>QR_VERIFY_02]
    STEP4 -->OTP_EXPIRED[กรณีการใช้งาน 3:<br/>*สมาชิก:* OTP หมดอายุ ติดต่อพนักงาน<br/>QR_VERIFY_03]

    VERIFY_DATA --> UC6{*สมาชิก:* ยืนยัน?}
    UC6 -->|ใช่| STEP5[หน้าจอ 5:<br/>การยืนยันข้อมูลสำเร็จ]
    UC6 -->|ไม่| STAY[อยู่หน้าเดิม<br/>หน้าจอ 4: *สมาชิก:* การยืนยันข้อมูลการเติมน้ำมัน]

    OTP_EXPIRED -->STAY2[อยู่หน้าเดิม<br/>หน้าจอ 4: *สมาชิก:* การยืนยันข้อมูลการเติมน้ำมัน]
    
    STEP5 -->CUST_SUCCESS[*สมาชิก:* ธุรกรรมสำเร็จ/ใบเสร็จ<br/>QR_SUCCESS_01]
    STEP5 -->EMP_SUCCESS[*พนักงาน:* ธุรกรรมสำเร็จ/ใบเสร็จ<br/>QR_SUCCESS_02]
    
    CUST_SUCCESS --> END_QR[ธุรกรรมเสร็จสิ้น]
    EMP_SUCCESS --> END_QR
```

### 5. โมดูลประวัติ/ธุรกรรม

```mermaid
graph TD
    HIST[โมดูลประวัติ/ธุรกรรม] --> STEP1[หน้าจอ 1: ประวัติธุรกรรม]
    
    STEP1 -->CUST_HIST[*สมาชิก:* หน้าจอประวัติธุรกรรม<br/>HIST_HISTORY_01]
    STEP1 -->EMP_HIST[*พนักงาน:* หน้าจอประวัติธุรกรรม<br/>HIST_HISTORY_02]
    
```

### 6. โมดูลโปรไฟล์

```mermaid
graph TD
    PROF[โมดูลโปรไฟล์] --> STEP1[หน้าจอ 1: หน้าโปรไฟล์]
    
    STEP1 -->CUST_PROF[*สมาชิก:* หน้าจอโปรไฟล์<br/>PROF_PROFILE_01]
    STEP1 -->EMP_PROF[*พนักงาน:* หน้าจอโปรไฟล์<br/>PROF_PROFILE_02]
```


## การจัดการผ่านเว็บแอพพลิเคชัน
### โมดูลทั้งหมด

```mermaid
graph TD
    START([ระบบบัตรสมาชิก]) --> COMMON[โมดูลทั่วไป]
    START --> AUTH[โมดูลการตรวจสอบสิทธิ์]
    START --> USER[โมดูลจัดการสิทธิ์การใช้งาน]
    START --> MEMB[โมดูลจัดการสมาชิก]
    START --> STAT[โมดูลจัดการสถานีให้บริการ]
    START --> HIST[โมดูลประวัติ/ธุรกรรม]
    START --> REPT[โมดูลรายงาน]
    START --> SETT[โมดูลตั้งค่า]

    USER --> AUTH_1[การจัดการกลุ่มผู้ใช้งาน]
    USER --> AUTH_2[การจัดการสิทธิ์การใช้งาน]
    USER --> AUTH_3[การจัดการผู้ใช้งาน]

    MEMB --> MEMB_1[การจัดการหน่วยงาน]
    MEMB --> MEMB_2[การจัดการรายชื่อสมาชิก]
    MEMB --> MEMB_3[การจัดการคูปอง]

    STAT --> STAT_1[การจัดการสถานีให้บริการ]
    STAT --> STAT_2[การจัดการรายชื่อพนักงาน]
    STAT --> STAT_3[การจัดการอุปกรณ์]
```

### ผู้ดูแลระบบ ลงทะเบียนสมาชิก
```mermaid
flowchart TD
    A[การลงทะเบียนสมาชิก] --> B[สร้างหน่วยงานใหม่<br/>MEMBER_MANAGEMENT_01/TAB_1/MODAL_1]
    A -->C[เลือกหน่วยงานที่มีอยู่แล้ว<br/>MEMBER_MANAGEMENT_01/TAB_1]

    B -->D[โปรไฟล์หน่วยงาน<br/>MEMBER_MANAGEMENT_03]
    C -->D
    
    D --> E[การจัดการสมาชิก<br/>MEMBER_MANAGEMENT_01]
    E --> E1[สร้างสมาชิกใหม่<br/>MEMBER_MANAGEMENT_06/MODAL_1]
    E --> E2[เลือกสมาชิกที่มีอยู่แล้ว<br/>MEMBER_MANAGEMENT_06]
    E1 --> F[โปรไฟล์สมาชิก<br/>MEMBER_MANAGEMENT_02]
    E2 --> F
    
    F --> G[ประวัติการเพิ่มโควต้า ระดับสมาชิก<br/>MEMBER_MANAGEMENT_04]
    G --> G1[เพิ่มโควต้า ระดับสมาชิก<br/>MEMBER_MANAGEMENT_04/MODAL_1]
    
    D -->I[ประวัติการเพิ่มโควต้า ระดับหน่วยงาน<br/>MEMBER_MANAGEMENT_07]
    I --> I1[เพิ่มโควต้า ระดับหน่วยงาน<br/>MEMBER_MANAGEMENT_07/MODAL_1]
    I1 --> K[แจกจ่ายโควต้าให้สมาชิกอัตโนมัติ *หรือด้วยหลักการบางอย่างที่ถูกกำหนดขึ้น<br/>MEMBER_MANAGEMENT_03]
    I1 --> K1[กลับไปที่หน้าโปรไฟล์หน่วยงานและเพิ่มโควต้า ระดับสมาชิกด้วยตนเอง]

    style K fill:red
    
```

### ผู้ดูแลระบบ ลงทะเบียนเจ้าหน้าที่ ผู้ให้บริการ
```mermaid
flowchart TD
    A[การลงทะเบียนเจ้าหน้าที่ ผู้ให้บริการ] --> B[สร้างสถานีให้บริการใหม่<br/>STATION_MANAGEMENT_01/TAB_1/MODAL_1]
    A -->C[เลือกสถานีให้บริการที่มีอยู่แล้ว<br/>STATION_MANAGEMENT_01/TAB_1]
    B -->D[โปรไฟล์สถานีให้บริการ<br/>STATION_MANAGEMENT_02]
    C -->D

    D --> E[การจัดการเจ้าหน้าที่<br/>STATION_MANAGEMENT_01/TAB_2]
    E --> E1[สร้างเจ้าหน้าที่ใหม่<br/>STATION_MANAGEMENT_01/TAB_2/MODAL_1]
    
    D -->I[การจัดการอุปกรณ์<br/>STATION_MANAGEMENT_01/TAB_3]
    I --> I1[เพิ่มอุปกรณ์ใหม่<br/>STATION_MANAGEMENT_07/MODAL_1]

```