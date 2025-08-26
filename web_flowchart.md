# Admin Register Member Flow Diagram

## English Version
```mermaid
flowchart TD
    A[Member registration] --> B[Create new department<br/>MEMBER_MANAGEMENT_01/TAB_1]
    A -->C[Select department<br/>MEMBER_MANAGEMENT_01/TAB_1]

    B -->D[Department Profile<br/>MEMBER_MANAGEMENT_03]
    C -->D
    
    D --> E[Member Management<br/>MEMBER_MANAGEMENT_01]
    E --> E1[Create new member<br/>MEMBER_MANAGEMENT_06]
    E --> E2[Select member<br/>MEMBER_MANAGEMENT_06]
    E1 --> F[Member Profile<br/>MEMBER_MANAGEMENT_02]
    E2 --> F
    
    F --> G[Member Increase Quota History<br/>MEMBER_MANAGEMENT_04]
    G --> G1[Increase Quota<br/>MEMBER_MANAGEMENT_04/MODAL_1]
    
    D -->I[Department Increase Quota History<br/>MEMBER_MANAGEMENT_07]
    I --> I1[Increase Quota<br/>MEMBER_MANAGEMENT_07/MODAL_1]
    I1 --> K[Auto-distribute quota to members<br/>MEMBER_MANAGEMENT_03]
    I1 --> K1[Return to the Department Profile page and manually add member quotas]
    
```

## Screen Reference Mapping

| Screen | Screen Code | Purpose |
|--------|-------------|---------|
| Screen 1: Member Management | MEMBER_MANAGEMENT_01 | Department and Member creation/management dashboard |
| Screen 2: Member Profile Details | MEMBER_MANAGEMENT_02 | Individual member profile view and management |
| Screen 3: Department Details | MEMBER_MANAGEMENT_03 | Department profile view and quota management |
| Screen 4: Increase Quota History | MEMBER_MANAGEMENT_04 | Individual quota increase tracking and management |
| Screen 4: Coupon Quota History | MEMBER_MANAGEMENT_05 | Coupon-based quota increase tracking |

## Process Details

### Main Case Flow:
1. **Department Setup** (if needed)
   - Admin creates new department with company details
   - Sets department type and contact information

2. **Member Creation**
   - Admin creates individual member
   - Links member to department
   - Sets basic member information

3. **Individual Quota Assignment**
   - Admin manually increases quota for specific member
   - Records reason and amount
   - Creates audit trail

### Sub Case Flow:
1. **Department Setup** (if needed)
   - Same as main case

2. **Department Quota Allocation**
   - Admin sets total department quota
   - Defines auto-distribution rules

3. **Auto Top-up Process**
   - System automatically distributes quota to all department members
   - Equal or rule-based distribution
   - Bulk quota assignment

## Business Rules

### Main Case:
- Individual member quota increases require manual approval
- Each quota increase is tracked with full audit trail
- Members must belong to a valid department

### Sub Case:
- Department quota can be distributed automatically
- Auto-allocation rules can be equal split or custom
- New members added to department automatically receive quota share
- Department total quota acts as the master pool