# Fuel Member System - Module/Screen/Use Case Flowchart

This flowchart represents the structure found in mobile_app_ui.html with proper flow direction:
- **Modules**: Top-level organization of system components
- **Screens**: Sequential flow downward (screen1 → screen2 → screen3)
- **Use Cases**: Specific actions or conditions that users perform in each screen - what the user actually does, including decision points for different user roles (Member vs Employee)

## Complete System Flow

```mermaid
graph TD
    START([Start: Fuel Member Card]) --> COMMON[Common Module]
    START --> REG[Registration Module]
    START --> AUTH[Authentication Module]
    START --> QR[QR Code Module]
    START --> HIST[History/Transaction Module]
    START --> PROF[Profile Module]
```

## 1. Common Module

```mermaid
graph TD
    COMMON[Common Module] --> STEP1[Screen 1: Home Page]
    
    STEP1 -->CUST_HOME[Member Home Dashboard<br/>COMMON_HOME_01]
    STEP1 -->EMP_HOME[Employee Home Dashboard<br/>COMMON_HOME_02]
    
```

## 2. Registration Module

```mermaid
graph TD
    REG[Registration Module] --> STEP1[Screen 1: Register]
    
    STEP1 -->UC1[Use Case 1:<br/>Register New Member Success<br/>REG_REGISTER_01]
    STEP1 -->UC2[Use Case 2:<br/>Register Failed - Duplicate Data Alert<br/>REG_REGISTER_02]

    UC1 -->STEP2[Screen 2: Verify OTP]
    UC2 -->STAY_SCREEN_1[Stay Screen 1: Register]

    STEP2 -->UC5[Use Case 1:<br/>Submit Success<br/>AUTH_VERIFY_01]
    STEP2 -->UC6[Use Case 2:<br/>OTP Expired Alert Message<br/>AUTH_VERIFY_02]
    STEP2 -->UC7[Use Case 3:<br/>Send OTP Again Alert Message Confirm<br/>AUTH_VERIFY_04]
    STEP2 -->UC8[Use Case 4:<br/>Submit Fail Alert Message<br/>AUTH_VERIFY_03]

    UC5 -->SUCCESS[Redirect to Home Page]
    UC6 -->STAY_SCREEN_2[Stay Screen 2: Verify OTP]
    UC7 -->STAY_SCREEN_2
    UC8 -->STAY_SCREEN_2
```


## 3. Authentication Module

```mermaid
graph TD
    AUTH[Authentication Module] --> STEP1[Screen 1: Login]
    
    STEP1 -->UC1[Use Case 1:<br/>User Found and Registered<br/>AUTH_LOGIN_01]
    STEP1 -->UC2[Use Case 2:<br/>User Found but Not Registered<br/>AUTH_LOGIN_02]
    STEP1 -->UC3[Use Case 3:<br/>User Found with Multiple Roles - Select Role<br/>AUTH_LOGIN_03]
    STEP1 -->UC4[Use Case 4:<br/>User Not Found - Show Error<br/>AUTH_LOGIN_04]

    UC1 -->STEP2[Screen 2: Verify OTP]
    UC2 -->STEP2
    UC3 -->STEP2
    UC4 -->STAY_SCREEN_1[Stay Screen 1: Login]
    
    STEP2 -->UC5[Use Case 1:<br/>Submit Success<br/>AUTH_VERIFY_01]
    STEP2 -->UC6[Use Case 2:<br/>OTP Expired Alert Message<br/>AUTH_VERIFY_02]
    STEP2 -->UC7[Use Case 3:<br/>Send OTP Again Alert Message Confirm<br/>AUTH_VERIFY_04]
    STEP2 -->UC8[Use Case 4:<br/>Submit Fail Alert Message<br/>AUTH_VERIFY_03]

    UC5 -->SUCCESS[Redirect to Home Page]
    UC6 -->STAY_SCREEN_2[Stay Screen 2: Verify OTP]
    UC7 -->STAY_SCREEN_2
    UC8 -->STAY_SCREEN_2
    
```


## 4. QR Code Module

```mermaid
graph TD
    QR[QR Code Module] --> STEP1[Screen 1:<br/>*Member:* generate QR Code<br/>QR_QRCODE_01]
    
    STEP1 --> STEP2[Screen 2:<br/>*Employee:* Scan QR Code with Camera<br/>QR_SCAN_01]
    STEP2 --> STEP3[Screen 3:<br/>*Employee:* Scaned and Fill Data]
    STEP3 -->FILL_STANDARD[Use Case 1:<br/>*Employee:* Fill Fuel Details and Send OTP<br/>QR_FILL_01]
    STEP3 -->CUSTOM_PRICE[Use Case 2:<br/>*Employee:* Custom Price/Unit Manual Input<br/>QR_FILL_02]
    STEP3 -->USE_COUPON[Use Case 3:<br/>*Employee:* Use Coupon Quota Instead of Member Quota<br/>QR_FILL_05]
    
    USE_COUPON -->LICENSE_VERIFY{*Employee:* License Plate Verification}
    LICENSE_VERIFY -->|License Matches| LICENSE_APPROVED[Use Case 6:<br/>*Employee:* License Matches - Proceed<br/>QR_FILL_06]
    LICENSE_VERIFY -->|License Not Matches| LICENSE_BLOCKED[Use Case 7:<br/>*Employee:* License Not Matches - Blocked<br/>QR_FILL_07]
    
    FILL_STANDARD -->CONNECTION_1[*Employee:* Fill All Data Required]
    CUSTOM_PRICE -->CONNECTION_1
    LICENSE_APPROVED -->CONNECTION_1
    LICENSE_BLOCKED -->RETRY_LICENSE[*Employee:* Retry License Capture]
    RETRY_LICENSE -->LICENSE_VERIFY
    
    CONNECTION_1 -->WAITING[*Employee:* Send OTP to Member <br/>and Waiting for Member Verification<br/>QR_FILL_03]
    CONNECTION_1 -->CONFIRM_BACK[*Employee:* Cancel Transaction<br/>QR_FILL_04]
    
    WAITING --> STEP4[Screen 4:<br/>*Member:* Verification<br/>QR_VERIFY_01]
    CONFIRM_BACK --> END_TRANSACTION[END]

    STEP4 -->VERIFY_DATA[Use Case 1:<br/>*Member:* Verify Details]
    STEP4 -->CANCEL_VERIFY[Use Case 2:<br/>*Member:* Cancel Verify Purchase<br/>QR_VERIFY_02]
    STEP4 -->OTP_EXPIRED[Use Case 3:<br/>OTP Expired - *Member:* Contact Employee<br/>QR_VERIFY_03]
    
    CANCEL_VERIFY -->END_VERIFY[END]

    VERIFY_DATA --> UC6{*Member:* Verify?}
    UC6 -->|Yes| STEP5[Screen 5:<br/>Success and Details]
    UC6 -->|No| STAY[Stay on Screen 4<br/>*Member:* Verification]

    OTP_EXPIRED -->STAY2[Stay on Screen 4<br/>*Member:* Verification]
    
    STEP5 -->CUST_SUCCESS[*Member:* Transaction Success/Receipt<br/>QR_SUCCESS_01]
    STEP5 -->EMP_SUCCESS[*Employee:* Transaction Success/Receipt<br/>QR_SUCCESS_02]
    
    CUST_SUCCESS --> END_QR[Transaction Complete]
    EMP_SUCCESS --> END_QR
```

## 5. History/Transaction Module

```mermaid
graph TD
    HIST[History/Transaction Module] --> STEP1[Screen 1: Transaction History]
    
    STEP1 -->CUST_HIST[*Member:* Transaction History Screen<br/>HIST_HISTORY_01]
    STEP1 -->EMP_HIST[*Employee:* Transaction History Screen<br/>HIST_HISTORY_02]
    
```

## 6. Profile Module

```mermaid
graph TD
    PROF[Profile Module] --> STEP1[Screen 1: Profile Page]
    
    STEP1 -->CUST_PROF[*Member:* Profile Screen<br/>PROF_PROFILE_01]
    STEP1 -->EMP_PROF[*Employee:* Profile Screen<br/>PROF_PROFILE_02]
```

## Summary Statistics

- **Total Modules**: 6 (Common, Registration, Authentication, QR Code, History/Transaction, Profile)
- **Total Screens**: 10
- **Total Use Cases**: 29
- **Member Use Cases**: 15
- **Employee Use Cases**: 13
- **Shared Use Cases**: 1
- **Decision Points**: 26 (diamond shapes)
- **Navigation Items**: 4 (Home, QR Code, History, Profile)

## Screen Reference Map

| Module | Screen | Use Case | Screen ID | User Type |
|--------|------|----------|-----------|-----------|
| Common | 1 | 1 | COMMON_HOME_01 | Member |
| Common | 1 | 2 | COMMON_HOME_02 | Employee |
| Registration | 1 | 1 | REG_REGISTER_01 | Member |
| Registration | 1 | 2 | REG_REGISTER_02 | Member |
| Auth | 1 | 1 | AUTH_LOGIN_01 | Member |
| Auth | 1 | 2 | AUTH_LOGIN_02 | Member |
| Auth | 1 | 3 | AUTH_LOGIN_03 | Member/Employee |
| Auth | 1 | 4 | AUTH_LOGIN_04 | Member |
| Auth | 2 | 1 | AUTH_VERIFY_01 | Member |
| Auth | 2 | 2 | AUTH_VERIFY_02 | Member |
| Auth | 2 | 3 | AUTH_VERIFY_03 | Member |
| Auth | 2 | 4 | AUTH_VERIFY_04 | Member |
| QR | 1 | 1 | QR_QRCODE_01 | Member |
| QR | 2 | 1 | QR_SCAN_01 | Employee |
| QR | 3 | 1 | QR_FILL_01 | Employee |
| QR | 3 | 2 | QR_FILL_02 | Employee |
| QR | 3 | 3 | QR_FILL_03 | Employee |
| QR | 3 | 4 | QR_FILL_04 | Employee |
| QR | 3 | 5 | QR_FILL_05 | Employee |
| QR | 3 | 6 | QR_FILL_06 | Employee |
| QR | 3 | 7 | QR_FILL_07 | Employee |
| QR | 4 | 1 | QR_VERIFY_01 | Member |
| QR | 4 | 2 | QR_VERIFY_02 | Member |
| QR | 4 | 3 | QR_VERIFY_03 | Member |
| QR | 4 | 4 | QR_VERIFY_04 | Member |
| QR | 5 | 1 | QR_SUCCESS_01 | Member |
| QR | 5 | 2 | QR_SUCCESS_02 | Employee |
| History | 1 | 1 | HIST_HISTORY_01 | Member |
| History | 1 | 2 | HIST_HISTORY_02 | Employee |
| Profile | 1 | 1 | PROF_PROFILE_01 | Member |
| Profile | 1 | 2 | PROF_PROFILE_02 | Employee |