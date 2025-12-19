# Overview

This project demonstrates a Windows 11 zero-touch deployment using Microsoft Intune and Windows Autopilot (User-Driven mode).
The solution automates device provisioning, Azure AD (Microsoft Entra ID) join, and MDM enrollment with no manual IT configuration on the device.

The lab simulates a real-world enterprise onboarding scenario where new or reset devices are provisioned securely when an end user signs in.

# Business Scenario

An organization needs to deploy Windows 11 devices to end users without:

Local IT intervention

Manual domain joins

Manual software installation

Manual policy configuration

Goal:
Provide a standardized, secure, and scalable provisioning process using cloud-native tools.

# Technologies Used

Microsoft Intune (Endpoint Manager)

Windows Autopilot

Microsoft Entra ID (Azure AD)

Windows 11 (VMware Workstation)

PowerShell

Dynamic Device Groups

# Deployment Model

Autopilot mode: User-Driven

Join type: Microsoft Entra ID Join

MDM: Microsoft Intune

Device ownership: Corporate

Provisioning type: Zero-touch (OOBE based)

# High-Level Architecture

Device hardware hash registered in Windows Autopilot

Dynamic device group targets Autopilot devices

Autopilot deployment profile assigned via Intune

Device reset to Out-of-Box Experience (OOBE)

User signs in with corporate credentials

Device auto-joins Entra ID and enrolls into Intune

Compliance and management enforced automatically

Implementation Steps (Summary)
1. Device Registration

Collected hardware hash using PowerShell

Imported device into Windows Autopilot Devices

2. Dynamic Device Group

Created a dynamic Entra ID device group

Automatically includes Windows Autopilot-registered devices

3. Autopilot Deployment Profile

Created User-Driven Autopilot profile

Configured:

Entra ID Join

Hidden privacy and license screens

Standard user account

Automatic keyboard and region configuration

4. Profile Assignment

Assigned Autopilot profile to dynamic device group

Verified assignment status as Active

5. Device Reset & Provisioning

Reset device to trigger OOBE

User signed in with corporate account

Autopilot flow initiated automatically

Validation & Verification
Device Join Status

Confirmed using:

dsregcmd /status


Expected results:

AzureAdJoined : YES

EnterpriseJoined : NO

MDM enrollment : SUCCESS

Intune Visibility

Device visible under Intune → Windows Devices

Managed by Intune

Ownership: Corporate

Compliance state: Compliant

Primary user assigned correctly

Key Challenges & Resolutions

MDM URL missing initially due to incomplete enrollment

Autopilot not triggering caused by profile assignment timing

VMware-specific behavior required multiple resets to retrigger OOBE

Resolved by validating:

MDM URLs

Profile assignment

Correct user sign-in context

Enrollment status via Event Viewer and PowerShell

Real-World Relevance

This setup mirrors how organizations:

Provision laptops for remote employees

Enforce compliance from first sign-in

Eliminate traditional imaging (MDT/SCCM)

Scale device onboarding securely

Screenshots

Screenshots included demonstrate:

Autopilot device registration

Dynamic group configuration

Deployment profile settings

OOBE sign-in experience

Intune device compliance status

Skills Demonstrated

Windows Autopilot configuration

Microsoft Intune administration

Entra ID device lifecycle management

Troubleshooting MDM enrollment

Enterprise-style documentation

# Validation & Verification

Deployment success was validated using:
- Windows OOBE sign-in experience
- `dsregcmd /status` to confirm Entra ID join
- Intune device enrollment and compliance state
- MDM diagnostic logs (DeviceManagement-Enterprise-Diagnostics)

> Note: VMware virtualization may limit some Autopilot UI screens; however, backend enrollment and compliance states confirm successful zero-touch provisioning.


Author

David G C
IT Support / Endpoint Management Enthusiast
MD-102 (Endpoint Administrator) Focused