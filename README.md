# RBAC Permissions Documentation

## Role Definitions

### 1. Super Admin

- **Full access** to all features and functionalities
- Can manage other administrators (Create Admin, Reset Password Admin, Assign Role, Edit Admin Data)
- Complete control over player management including balance updates
- Full access to promotions, transactions, and web management
- Has complete control over the application

### 2. Supervisor

- **Cannot** manage other administrators
- Full access to player management including balance updates
- Full access to promotions (Create, Edit, Delete)
- Full access to transactions (Approve/Reject, View History)
- Full access to web management (Config, Bank Providers, Bank Groups)
- Cannot access admin management functions

### 3. Operator

- **Cannot** manage other administrators
- Limited player management (no balance updates, no transaction password reset)
- **Cannot** manage promotions
- Limited transaction access (Approve/Reject only, no history access)
- Full access to web management (Config, Bank Providers, Bank Groups)
- Most restricted administrative role

---

## Sidebar Navigation & Permissions

### 🏠 Dashboard

- **Route:** `/dashboard`
- **Super Admin:** ✅ Full Access
- **Supervisor:** ✅ Full Access
- **Operator:** ✅ Read Only Access

---

### 👥 Players Management

- **Main Route:** `/player`
- **Detail Route:** `/player/[playerId]`

| Feature                    | Super Admin | Supervisor | Operator |
| -------------------------- | ----------- | ---------- | -------- |
| View Players List          | ✅          | ✅         | ✅       |
| View Player Details        | ✅          | ✅         | ✅       |
| Reset Password             | ✅          | ✅         | ✅       |
| Reset Transaction Password | ✅          | ✅         | ✅       |
| Update Balance             | ✅          | ✅         | ❌       |
| Edit Player                | ✅          | ✅         | ✅       |
| Verify Player              | ✅          | ✅         | ✅       |

---

### 🎁 Promotions Management

- **Main Route:** `/promotion`
- **Create Route:** `/promotion/create`
- **Detail Route:** `/promotion/detail/[promotionId]`
- **Bonus Route:** `/promotion/addBonus`

| Feature          | Super Admin | Supervisor | Operator |
| ---------------- | ----------- | ---------- | -------- |
| View Promotions  | ✅          | ✅         | ✅       |
| Create Promotion | ✅          | ✅         | ❌       |
| Edit Promotion   | ✅          | ✅         | ❌       |
| Delete Promotion | ✅          | ✅         | ❌       |

---

### 💰 Transactions Management

| Feature                 | Super Admin | Supervisor | Operator |
| ----------------------- | ----------- | ---------- | -------- |
| Approve/Reject Deposit  | ✅          | ✅         | ✅       |
| Approve/Reject Withdraw | ✅          | ✅         | ✅       |
| Bet History             | ✅          | ✅         | ❌       |
| Win History             | ✅          | ✅         | ❌       |

#### Routes:

- **Deposit:** `/deposit-player`
- **Withdraw:** `/withdraw`
- **Bet:** `/bet`
- **Win:** `/win`

---

### 🌐 Web Management

| Feature              | Super Admin | Supervisor | Operator |
| -------------------- | ----------- | ---------- | -------- |
| Add Config           | ✅          | ✅         | ✅       |
| Edit Config          | ✅          | ✅         | ✅       |
| Delete Config        | ✅          | ✅         | ✅       |
| Add Bank Provider    | ✅          | ✅         | ✅       |
| Edit Bank Provider   | ✅          | ✅         | ✅       |
| Delete Bank Provider | ✅          | ✅         | ✅       |
| Add Bank Group       | ❌          | ✅         | ✅       |
| Edit Bank Group      | ❌          | ✅         | ✅       |
| Delete Bank Group    | ❌          | ✅         | ✅       |

#### Routes:

- **CMS Configuration:** `/cms-config`
- **Bank Provider Management:** `/bank-provider-management`
- **Bank Provider Group Management:** `/bank-provider-group-management`

---

### 👨‍💼 Admin Management

- **Main Route:** `/admin`
- **Create Route:** `/admin/create`
- **Detail Route:** `/admin/[adminId]`

| Feature              | Super Admin | Supervisor | Operator |
| -------------------- | ----------- | ---------- | -------- |
| View Admins List     | ✅          | ❌         | ❌       |
| Create Admin         | ✅          | ❌         | ❌       |
| Reset Password Admin | ✅          | ❌         | ❌       |
| Assign Role          | ✅          | ❌         | ❌       |
| Edit Admin Data      | ✅          | ❌         | ❌       |

---

### ⚙️ Settings

- **Route:** `/settings`
- **Super Admin:** ✅ Full Access
- **Supervisor:** ❌ No Access
- **Operator:** ❌ No Access

---

## Future Features (Currently Commented Out)

### 📊 Reporting

- **Active Player Report:** `/active-player`
- **Win/Lose Player Report:** `/win-lose-player`
- **Esport Game Report:** `/esport-game`
- **Profit Platform Report:** `/profit-platform`

**Planned Access:**

- **Super Admin:** ✅ Full Access
- **Supervisor:** ✅ View Only
- **Operator:** ✅ View Only (Limited reports)

### 🎮 Game Management

- **Esport Games:** `/esport-games`
- **Game Reporting:** `/reporting-game`

**Planned Access:**

- **Super Admin:** ✅ Full Access
- **Supervisor:** ✅ Full Access
- **Operator:** ✅ View Only

---

## Implementation Notes

### Role Hierarchy

```
Super Admin > Supervisor > Operator
```

### Permission Structure

- **Super Admin**: Can access everything including admin management and system settings
- **Supervisor**: Full operational access but cannot manage admins or critical settings
- **Operator**: Limited operational access with restrictions on balance updates, promotion management, and transaction history

### Route Protection

All routes should be protected based on the user's role. Users attempting to access unauthorized routes should be redirected to an "Access Denied" page or the dashboard.

### Component-Level Permissions

Individual buttons and actions within pages should also be hidden/disabled based on user permissions:

- Create/Edit/Delete buttons
- Export functionality
- Administrative actions
- Configuration changes

### Navigation Menu

The sidebar navigation should dynamically show/hide menu items based on the user's role to improve UX and prevent confusion.

## Permission Combinations

| Combination           | Decimal | Binary | Permissions                |
| --------------------- | ------- | ------ | -------------------------- |
| READ only             | 1       | 0001   | Read                       |
| READ + WRITE          | 3       | 0011   | Read, Write                |
| WRITE + DELETE        | 6       | 0110   | Write, Delete              |
| READ + WRITE + DELETE | 7       | 0111   | Read, Write, Delete        |
| ADMIN + READ          | 9       | 1001   | Admin, Read                |
| Full Access           | 15      | 1111   | Read, Write, Delete, Admin |

## Role Permissions

### Super Admin (15 - Full Access)

- **Players**: 15 (Read, Write, Delete, Admin)
- **Promotions**: 15 (Read, Write, Delete, Admin)
- **Transactions**: 15 (Read, Write, Delete, Admin)
- **Web Management**: 15 (Read, Write, Delete, Admin)
- **Admin Management**: 15 (Read, Write, Delete, Admin)
- **Settings**: 15 (Read, Write, Delete, Admin)

### Supervisor (7 - Read, Write, Delete)

- **Players**: 7 (Read, Write, Delete)
- **Player Balance**: 3 (Read, Write)
- **Promotions**: 7 (Read, Write, Delete)
- **Transactions**: 3 (Read, Write - approve/reject)
- **Web Management**: 7 (Read, Write, Delete)
- **Admin Management**: 0 (No access)
- **Settings**: 0 (No access)

### Operator (3 - Read, Write)

- **Players**: 3 (Read, Write)
- **Player Balance**: 1 (Read only)
- **Promotions**: 1 (Read only)
- **Transactions**: 3 (Read, Write - approve/reject)
- **Web Management**: 7 (Read, Write, Delete)
- **Admin Management**: 0 (No access)
- **Settings**: 0 (No access)
