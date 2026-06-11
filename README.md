# Active Directory Group Policy Enforcement & Workstation Security Lab

## 🧠 Overview
This project simulates enterprise endpoint hardening and workstation baseline security configurations using Windows Server Group Policy Objects (GPOs). Operating within a controlled `mydomain.local` virtual sandbox, this lab demonstrates how to centrally restrict system settings, enforce administrative compliance, and mitigate internal security risks across specific organizational layers.

---

## 🎯 Objectives
* Deploy and configure a centralized custom Group Policy Object (GPO).
* Implement endpoint hardening using Administrative Templates (`gpmc.msc`).
* Target policies accurately by linking GPOs to specific Organizational Units (OUs).
* Force and verify client-side enforcement on active domain user sessions using the command line.

---

## 🏗️ Environment & Architecture
* **Domain Controller:** Windows Server with Active Directory Domain Services (AD DS)
* **Domain Name:** `mydomain.local`
* **Target OU Branch:** `_Employees`
* **Test Identity Profile:** `Mike Vance` (Domain User Account)
* **Virtualization Platform:** VirtualBox
* **Core Management Engine:** Group Policy Management Console (GPMC)

---

## 🔄 Step-by-Step Implementation & Evidence

### 01 – Group Policy Environment Baseline
Opening the Group Policy Management Console (`gpmc.msc`) to review our active domain structure. Our pre-configured organizational units (`_Employees`, `Finance`, `HR`, `IT`, `Disabled Users`) are visible and ready for policy deployment.

![Group Policy Environment Baseline](./01_group_policy_environment_baseline.png)
*Caption: Navigating the Group Policy Management Console tree to verify our Active Directory domain structure before creating any new rules.*

---

### 02 – Custom GPO Creation
Creating a brand-new, independent Group Policy Object named `GPO_Workstation_Security_Baseline` inside the central Group Policy Objects vault. This ensures our custom adjustments are kept separate from the Default Domain Policy.

![Custom GPO Creation](./02_custom_gpo_creation.png)
*Caption: Provisioning the empty GPO shell inside the central container to establish a clean starting point for our workstation security rules.*

---

### 03 – GPO Configuration & Administrative Templates
Drilling down into the policy editor (`User Configuration -> Policies -> Administrative Templates -> Control Panel`) to modify system rules. The policy **"Prohibit access to Control Panel and PC settings"** has been explicitly set to **Enabled**.

![GPO Configuration Settings](./03_gpo_configuration_settings.png)
*Caption: Activating the administrative template rule inside the Group Policy Editor to completely block access to the Control Panel and Windows Settings.*

---

### 04 – Organizational Unit Linkage
Linking our newly configured `GPO_Workstation_Security_Baseline` directly to the target **`_Employees`** Organizational Unit. This ensures the security rule actively maps to all user accounts nested under this branch.

![GPO OU Linkage](./04_gpo_ou_linkage.png)
*Caption: Connecting the completed GPO to the employee organizational unit so the server knows exactly which users should be restricted.*

---

### 05 – Client-Side Verification & Active Enforcement
Logging into a domain-joined workstation using a new test employee account (**Mike Vance**). Running the command `gpupdate /force` pulls down the new policy from the Domain Controller immediately. Any subsequent attempt to open the Windows Settings app or Control Panel is instantly blocked by a native OS restriction alert.

![GPO Client Verification](./05_gpo_client_verification.png)
*Caption: Success proof on the client machine. The command prompt shows a successful policy update next to the Windows error pop-up blocking the user from entering system settings.*

---

## 📌 Project Outcome
This lab successfully demonstrates centralized security administration. By decoupling custom desktop lockdown rules from global domain defaults and systematically targeting specific OUs, this project proves practical competency in Group Policy propagation, endpoint hardening, and corporate compliance enforcement.
