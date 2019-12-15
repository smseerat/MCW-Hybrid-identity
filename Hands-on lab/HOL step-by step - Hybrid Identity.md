![Microsoft Cloud Workshops icon](https://github.com/Microsoft/MCW-Template-Cloud-Workshop/raw/master/Media/ms-cloud-workshop.png "Microsoft Cloud Workshops")

<div class="MCWHeader1">
Hybrid Identity
</div>

<div class="MCWHeader2">
Hands-on lab step-by-step
</div>

<div class="MCWHeader3">
December 2019
</div>


Information in this document, including URL and other Internet Web site references, is subject to change without notice. Unless otherwise noted, the example companies, organizations, products, domain names, e-mail addresses, logos, people, places, and events depicted herein are fictitious, and no association with any real company, organization, product, domain name, e-mail address, logo, person, place or event is intended or should be inferred. Complying with all applicable copyright laws is the responsibility of the user. Without limiting the rights under copyright, no part of this document may be reproduced, stored in or introduced into a retrieval system, or transmitted in any form or by any means (electronic, mechanical, photocopying, recording, or otherwise), or for any purpose, without the express written permission of Microsoft Corporation.

Microsoft may have patents, patent applications, trademarks, copyrights, or other intellectual property rights covering subject matter in this document. Except as expressly provided in any written license agreement from Microsoft, the furnishing of this document does not give you any license to these patents, trademarks, copyrights, or other intellectual property.

The names of manufacturers, products, or URLs are provided for informational purposes only and Microsoft makes no representations and warranties, either expressed, implied, or statutory, regarding these manufacturers or the use of the products with any Microsoft technologies. The inclusion of a manufacturer or product does not imply endorsement of Microsoft of the manufacturer or product. Links may be provided to third party sites. Such sites are not under the control of Microsoft and Microsoft is not responsible for the contents of any linked site or any link contained in a linked site, or any changes or updates to such sites. Microsoft is not responsible for webcasting or any other form of transmission received from any linked site. Microsoft is providing these links to you only as a convenience, and the inclusion of any link does not imply endorsement of Microsoft of the site or the products contained therein.

� 2019 Microsoft Corporation. All rights reserved.

Microsoft and the trademarks listed at <https://www.microsoft.com/en-us/legal/intellectualproperty/Trademarks/Usage/General.aspx> are trademarks of the Microsoft group of companies. All other trademarks are property of their respective owners.

**Contents**

<!-- TOC -->

- [Hybrid Identity Hands On Lab Step by Step](#hybrid-identity-hands-on-lab-step-by-step)
    - [Abstract and learning objectives](#abstract-and-learning-objectives)
    - [Overview](#overview)
    - [Solution architecture](#solution-architecture)
    - [Exercise 1: Integrate an Active Directory forest with an Azure Active Directory tenant](#exercise-1-integrate-an-active-directory-forest-with-an-azure-active-directory-tenant)
        - [Overview](#overview-1)
        - [Task 1: Create an Azure Active Directory tenant and activate an Enterprise Mobility + Security E5 trial](#task-1-create-an-azure-active-directory-tenant-and-activate-an-enterprise-mobility-+-security-e5-trial)
        - [Task 2: Create and configure Azure AD users](#task-2-Create-and-configure-Azure-AD-users)
        - [Task 3: Purchase a custom domain name](#task-3-Purchase-a-custom-domain-name)
        - [Task 4: Assign a custom domain name to the Contoso Azure AD tenant](#task-4-Assign-a-custom-domain-name-to-the-Contoso-Azure-AD-tenant)
        - [Task 5: Configure DNS suffix in the Contoso Active Directory forest](#task-5-Configure-DNS-suffix-in-the-Contoso-Active-Directory-forest)
        - [Task 6: Install Azure AD Connect](#task-6-Install-Azure-AD-Connect)
        - [Task 7: Enable Active Directory Recycle Bin](#task-7-Enable-Active-Directory-Recycle-Bin)
        - [Task 8: Configure Azure AD Connect attribute-level filtering](#task-8-Configure-Azure-AD-Connect-attribute-level-filtering)
        - [Task 9: Initiate and verify directory synchronization](#task-9-Initiate-and-verify-directory-synchronization)
        - [Task 10: Configure Hybrid Azure AD join](#task-10-Configure-Hybrid-Azure-AD-join)
        - [Task 11: Perform Hybrid Azure AD join](#task-11-Perform-Hybrid-Azure-AD-join)
        - [Summary](#summary-1)
    - [Exercise 2: Manage Authentication, Authorization, and Access Protection in Hybrid Scenarios](#exercise-2-Manage-Authentication,-Authorization,-and-Access-Protection-in-Hybrid-Scenarios)
        - [Overview](#overview-2)
        - [Task 1: Create Active Directory groups](#task-1-Create-Active-Directory-groups)
        - [Task 2: Assign EM+S E5 licenses to Azure AD users](#task-2-Assign-EM+S-E5-licenses-to-Azure-AD-users)
        - [Task 3: Enable Azure AD Multi-Factor Authentication](#task-3-Enable-Azure-AD-Multi-Factor-Authentication)
        - [Task 4: Enable password writeback and Self-Service Password Reset](#task-4-Enable-password-writeback-and-Self-Service-Password-Reset)
        - [Task 5: Implement Azure AD Password Protection for Windows Server Active Directory](#task-5-Implement-Azure-AD-Password-Protection-for-Windows-Server-Active-Directory)
        - [Task 6: Enable Azure Active Directory Identity Protection](#task-6-Enable-Azure-Active-Directory-Identity-Protection)
        - [Task 7: Enable Automatic Intune Enrollment](#task-7-Enable-Automatic-Intune-Enrollment)
        - [Task 8: Enable Enterprise-State-Roaming](#task-8-Enable-enterprise-state-roaming)
        - [Task 9: Implement Azure AD Conditional Access Policies](#task-9-Implement-Azure-AD-Conditional-Access-Policies)
        - [Task 10: Implement Azure AD Privileged Identity Management](#task-10-Implement-Azure-AD-Privileged-Identity-Management)
        - [Summary](#summary-2)
    - [Exercise 3: Configure application access in hybrid scenarios](#exercise-3-Configure-application-access-in-hybrid-scenarios)
        - [Overview](#overview-3)
        - [Task 1: Install and configure Azure AD Application Proxy](#task-1-Install-and-configure-Azure-AD-Application-Proxy)
        - [Task 2: Configure an Azure AD Application Proxy application](#task-2-Configure-an-Azure-AD-Application-Proxy-application)
        - [Task 3: Test an Azure AD Application Proxy application](#task-3-Test-an-Azure-AD-Application-Proxy-application)
        - [Task 4: Create an Azure Active Directory tenant and activate an Enterprise Mobility + Security E5 trial](#task-4-Create-an-Azure-Active-Directory-tenant-and-activate-an-Enterprise-Mobility-+-Security-E5-trial)
        - [Task 5: Create and configure Azure AD users](#task-5-Create-and-configure-Azure-AD-users)
        - [Task 6: Create and configure Azure AD guest user and group accounts](#task-6-Create-and-configure-Azure-AD-guest-user-and-group-accounts)
        - [Task 7: Configure an Azure AD Application Proxy application for B2B access](#task-7-Configure-an-Azure-AD-Application-Proxy-application-for-B2B-access)
        - [Task 8: Test an Azure AD Application Proxy application](#task-8-Test-an-Azure-AD-Application-Proxy-application)
        - [Summary](#summary-3)
    - [Lab summary](#lab-summary)
    - [After the hands-on lab](#after-the-hands-on-lab)
        - [Task 1: Delete resources](#task-1-delete-resources)

<!-- /TOC -->

# Hybrid Identity hands-on lab step-by-step 

## Abstract and learning objectives 

In this hands-on lab you will setup and configure a number of different Hybrid Identity scenarios. The scenarios involve an Active Directory single-domain forest named contoso.local, which in this lab environment, consists (for simplicity reasons) of a single domain controller named DC1 and a single domain member server named APP1. The intention is to explore Azure AD-related capabilities that allow you to integrate Active Directory with Azure Active Directory, optimize hybrid authentication and authorization, and provide secure access to on-premises resources from Internet for both organizational users and users who are members of partner organizations. 

As you step through the hands-on-lab, you will learn how to perform the following tasks:

-   Create an Azure Active Directory tenant

-   Create and configure Azure AD users

-   Activate an Enterprise Mobility + Security E5 trial and assign the corresponding product licenses to users

-   Purchase a custom domain name by leveraging Azure Web App functionality

-   Assign a custom domain name to an Azure AD tenant

-   Configure a custom DNS suffix in an Active Directory forest

-   Install Azure AD Connect

-   Enable Active Directory Recycle Bin

-   Configure Azure AD Connect attribute-level filtering

-   Initiate and verify directory synchronization

-   Configure and perform Hybrid Azure AD join 

-   Enable Azure AD Multi-Factor Authentication

-   Enable Azure AD password writeback and Self-Service Password Reset

-   Implement Azure AD Password Protection

-   Enable Azure Active Directory Identity Protection

-   Enable Automatic Intune Enrollment

-   Implement Azure AD Conditional Access Policies

-   Implement Azure AD Privileged Identity Management

-   Install and configure Azure AD Application Proxy

-   Configure and test Azure AD Application Proxy applications

-   Create and configure Azure AD guest user and group accounts

-   Configure and test Azure AD Application Proxy applications for B2B access

## Overview

Contoso has asked you to integrate their on-premises Active Directory single-domain forest named contoso.local with Azure AD and implement all necessary prerequisites to allow them to benefit from such Azure AD features as single sign-on to cloud and on-premises applications, enhanced sing-in security with Multi-Factor Authentication and Windows Hello for Business, Hybrid Azure AD join, Self-Service Password Reset and Password Protection, automatic enrollment of Windows 10 devices into Microsoft Intune, and Azure AD Privileged Identity Protection. They want to also provide secure access to their on-premises, Windows Integrated Authentication-based applications from Internet for both organizational users and users who are members of partner organizations, although they also want to be able to loosen restrictions when access originates from Hybrid Azure AD joined computers residing in their on-premises data centers. The same applications need to also be made avaialble to Contoso's business partners. 

## Solution architecture

From the architectural standpoint, the deployment will consist of the following components:

-   "On-premises" Active Directory environment consisting of a single domain controller (DC1) and one domain member server (APP1), running Windows Server 2016 operating system. 

-   Contoso Azure AD tenant.

-   Fabrikam Azure AD tenant.

## Exercise 1: Integrate an Active Directory forest with an Azure Active Directory tenant

Duration: 150 minutes

### Overview 1

In this exercise, you will integrate an Active Directory forest with an Azure Active Directory tenant by creating an Azure Active Directory tenant and activating an Enterprise Mobility + Security E5 trial, creating and configuring an Azure AD user, purchasing a custom domain name, assigning a custom domain name to the Contoso Azure AD tenant, configuring DNS suffix in the Contoso Active Directory forest, installing Azure AD Connect, enable Active Directory Recycle Bin, configuring Azure AD Connect attribute-level filtering, initiating and verifying directory synchronization, configuring Hybrid Azure AD join, and performing Hybrid Azure AD join of a Windows Server 2016 VM.

### Task 1: Create an Azure Active Directory tenant and activate an Enterprise Mobility + Security E5 trial

In this task, you will create an Azure Active Directory tenant with the following settings: 

-   Organization name: **Contoso**

-   Initial domain name: any valid, unique domain name

-   Country or region: **United States**

1. From the lab computer, start a new Web browser window and navigate to the Azure portal at <https://portal.azure.com>.

1. When prompted, sign into the Azure subscription into which you deployed resources in the Before Hands-On Lab exercises.

1. On the lab computer, in the Azure portal, click **+ Create a resource**

1. On the **New** blade, in the **Search the Marketplace** text box, type **Azure Active Directory** and, in the list of results, click **Azure Active Directory**.

1. On the **Azure Active Directory** blade, click **Create**.

1. On the **Create directory** blade, specify the following settings and click **Create**:

    -   Organization name: **Contoso**

    -   Initial domain name: any valid, unique domain name

    -   Country or region: **United States**

1. In the Azure portal, navigate to the blade of the newly created Azure Active Directory tenant.

1. On the **Contoso - Overview** blade, click **Licenses**.

1. On the **Contoso - Licenses**, blade, click **+ Try/Buy**.

1. On the **Activate** blade, in the **ENTERPRISE MOBILITY + SECURITY E5** section, click **Free trial** and then click **Activate**


### Task 2: Create and configure Azure AD users

In this task, you will configure Azure AD user accounts in the newly created Azure AD tenant with the following settings. This will include assigning EM+S E5 licenses to the user account you are using for this lab as well as creating a new Azure AD user account with the following settings and assigning to it the Global Administrator role as well as the EM+S E5 license.

- Name: **john.doe**

- First name: **John**

- Last name: **Doe**
    
- Password: **Auto-generate password**
    
- Show Password: **Enabled**

- Groups: **0 group selected**
    
- Roles: **Global Administrator**
    
- Block sign in: **No**
    
- Usage location: **United States**
    
- Job title: leave blank
    
- Department: leave blank

1. From the lab computer, in the Azure portal, navigate back to the **Contoso - Overview** blade.

1. On the **Contoso - Overview** blade, click **Users**.

1. On the **Users - All users** blade, click the entry representing your user account.

1. On the **Profile** blade of your user account, in the **Settings** section, click the **edit** link.

1. In the **Settings** section, in the **Usage location** drop-down list, select the **United States** entry and click **Save**.

1. On the **Profile** blade of your user account, click **Licenses**

1. On the **Licenses** blade, click **+ Assignments**.

1. On the **Update license assignments** blade, enable the **Enterprise Mobility + Security E5** checkbox, ensure that all the corresponding license options are enabled, and click **Save**.

1. On the **Users - All users** blade, click **+ New user**

1. On the **New user** blade, ensure that the **Create user** option is selected, specify the following settings, and click **Create**:

    - User name: **john.doe\@*your Azure AD tenant domain name*** where ***your Azure AD tenant domain name*** is the domain name you specified when creating the Contoso Azure AD tenant

    - Name: **john.doe**

    - First name: **John**

    - Last name: **Doe**
    
    - Password: **Auto-generate password**
    
    - Show Password: **Enabled**

    - Groups: **0 group selected**
    
    - Roles: **Global Administrator**
    
    - Block sign in: **No**
    
    - Usage location: **United States**
    
    - Job title: leave blank
    
    - Department: leave blank

    > **Note**: Copy the **User name** and **Password** values into Notepad. You will need them later in this lab.

1. On the **Users - All users** blade, click the entry representing the newly created user account.

1. On the **john.doe - Profile** blade, click **Licenses**

1. On the **john.doe - Licenses** blade, click **+ Assignments**.

1. On the **Update license assignments** blade, enable the **Enterprise Mobility + Security E5** checkbox, ensure that all the corresponding license options are enabled, and click **Save**.


### Task 3: Purchase a custom domain name

In this task, you will purchase a custom DNS domain name by leveraging the functionality described at <https://docs.microsoft.com/en-us/azure/app-service/manage-custom-dns-buy-domain>.

1. From the lab computer, in the browser displaying the Azure portal, verify that you are signed in to the Azure AD tenant associated with the Azure subscription into which you deployed resources in the Before Hands-On Lab exercises. If not, click the **Directory + Subscription** icon in the toolbar of the Azure portal (to the right of the **Cloud Shell** icon) to switch to the correct Azure AD tenant. 

1. In the Azure portal, click **+ Create a resource**

1. On the **New** blade, in the **Search the Marketplace** text box, type **Web App** and, in the list of results, click **Web App**.

1. On the **Web App** blade, click **Create**.

1. On the **Basics** tab of the **Web App** blade, specify the following settings and click **Next: Monitoring**:

    - Subscription: the name of the Azure subscription into which you deployed resources in the Before Hands-On Lab exercises

    - Resource Group: the name of a new resource group **contosohilab-RG**

    - Name: any valid, globally unique name
    
    - Publish: **Code**

    - Runtime stack: **.NET Core 3.0 (Current)**

    - Operating system: **Windows**

    - Region: any Azure region in which you can create Azure Web Apps in the target subscription

    - App Service plan: accept the default

    - Sku and size: **Shared D1**
  
1. On the **Monitoring** tab of the **Web App** blade, specify the following setting and click **Review + create**:

    - Enable Application Insights: **No**

1. On the **Review + create** tab of the **Web App** blade, click **Create**.

1. In the Azure portal, navigate to the blade of the newly provisioned Azure web app and click **Custom domains**.

1. On the **Custom domains** blade, click **+ Buy Domain**

1. On the **App Service Domain** blade, in the **Search for domain** text box, type the domain name you want to purchase and select the checkbox next to one of the available domain names listed below.

1. Click **Contact information**, type required information, and click **OK**.

1. Click **Privacy protection**, ensure that **Disable** is selected, and click **OK**.

1. Leave the **www** and **\@ (Root domain)** checkboxes unchecked.

1. Click **Legal terms**, click **Accept**, and, back on the **App Service Domain** blade, click **OK**.


### Task 4: Assign a custom domain name to the Contoso Azure AD tenant

In this task, you will assign a newly purchased custom DNS domain name to the Contoso Azure AD tenant. 

1. From the lab computer, in the Azure portal, click the **Directory + Subscription** icon in the toolbar of the Azure portal (to the right of the **Cloud Shell** icon) and switch to the Contoso Azure AD tenant. 

1. In the Azure portal, navigate to the **Contoso - Overview** blade.

1. On the **Contoso - Overview** blade, click **Custom domain names**.

1. On the **Custom domain name**, click **+ Add custom domain**.

1. On the **Add custom domain** blade, in the **Custom domain name** text box, type the domain name you purchased in the previous task and click **Add domain**. You will be redirected to a new blade displaying your custom domain name settings.

1. Identify the value of the **TXT** record on the custom domain name blade. 

1. From the lab computer, start another browser window and navigate to the Azure portal.

1. In the Azure portal, click the **Directory + Subscription** icon in the toolbar of the Azure portal (to the right of the **Cloud Shell** icon) to switch to the Azure AD tenant associated with the Azure subscription into which you deployed resources in the Before Hands-On Lab exercises. 

1. In the Azure portal, click **All services**, in the **Search All** textbox, type **DNS zones**, and then click the **DNS zones** entry in the listing of search results.

1. On the **DNS zones** blade, click the entry with the name matching the custom domain name you purchased in the previous task.

1. On the DNS zone blade, click **+ Record set**. 

1. On the **Add record set** blade, specify the following settings and click **OK**:

    - Name: **\@**

    - Type: **TXT**

    - TTL: **1**

    - TTL unit: **Hours**

    - Value: the value of **DESTINATION OR POINTS TO ADDRESS** entry you identified on the custom domain name blade

1. Switch back to the browser window displaying the custom domain name blade and click **Verify**.

1. Ensure that the verification was successful. 

1. Back on the custom domain name blade, click **Make primary** and click **OK** to confirm your change.


### Task 5: Configure DNS suffix in the Contoso Active Directory forest

In this task, you will configure the DNS suffix of the Contoso Active Directory forest to match the newly verified Azure AD custom domain name.

1. From the lab computer, in the Azure portal, verify that you are signed in to the Azure AD tenant associated with the Azure subscription into which you deployed resources in the Before Hands-On Lab exercises. If not, click the **Directory + Subscription** icon in the toolbar of the Azure portal (to the right of the **Cloud Shell** icon) to switch to that Azure AD tenant. 

1. In the Azure portal, navigate to the blade of the **DC1** virtual machine.

1. From the **DC1** virtual machine blade, connect to **DC1** via Remote Desktop. When prompted to sign in, use the **CONTOSO\\demouser** name with the **demo\@pass123** password. 

1. Within the Remote Desktop session to **DC1**, from the **Server Manager** window, start **Active Directory Domains and Trusts** console. 

1. In the **Active Directory Domains and Trusts** console, right-click the **Active Directory Domains and Trusts [DC1.contoso.local]** node and, in the right-click menu, click **Properties**.

1. On the **UPN Suffixes** tab of the **Active Directory Domains and Trusts [DC1.contoso.local]** window, in the **Alternative UPN suffixes** textbox, type the name of the custom domain you verified in the previous task, click **Add**, and then click **OK**.

1. Within the Remote Desktop session to **DC1**, from the **Server Manager** window, start **Active Directory Users and Computers** console. 

1. In the **Active Directory Users and Computers** console, expand the **contoso.local** node and examine the organizational unit hierarchy of the domain and the group membership of the domain groups. 

1. Within the Remote Desktop session to **DC1**, start Windows PowerShell ISE and, from the Script pane, run the following to replace the UPN suffix of all users who are members of the **Engineering** group with the one matching the custom verified domain name of the Contoso Azure AD tenant (replace the placeholder `<custom_domain_name>` with the actual name of the custom verified domain name you assigned to the Contoso Azure AD tenant). 

    ```pwsh
    $domainName = '<custom_domain_name>'
    $users = Get-ADGroupMember -Identity 'Engineering' -Recursive | Where-Object {$_.objectClass -eq 'user'}

    foreach ($user in $users) {
        $user = Get-ADUser -Identity $User.SamAccountName
        $userName = $user.UserPrincipalName.Split('@')[0] 
        $upn = $userName + "@" + $domainName 
        $user | Set-ADUser -UserPrincipalName $upn
    }
    ```

### Task 6: Install Azure AD Connect

In this task, you will install Azure AD Connect.

1. Within the Remote Desktop session to **DC1**, in Server Manager, click **Local Server**, then click the **On** link next to the **IE Enhanced Security Configuration**, set the **Administrators** settings to **Off**, and click **OK**.

1. Within the Remote Desktop session to **DC1**, start Internet Explorer and navigate to the Azure portal at <https://portal.azure.com>.

1. When prompted to sign in, provide the credentials of the **john.doe** Azure AD user account, which you copied into Notepad earlier in this exercise.

1. When prompted, change the password for the **john.doe** user account. 
  
    > **Note**: If you receive the message **We've seen that password too many times before. Choose something harder to guess**, you'll need to modify the password until it is unique enough to be accepted.

1. If prompted whether to **Stay signed in?"** click **No**. You will be redirected to the Azure portal interface. 

1. If presented with the **Welcome to Microsoft Azure** dialog box, click **Maybe later**. 

1. in the Azure portal, navigate to the **Contoso - Overview** blade.

1. On the **Contoso - Overview** blade, click **Azure AD Connect**.

1. On the **Azure AD Connect** blade, click the **Download Azure AD Connect** link.

1. On the **Microsoft Azure Active Directory Connect** web page of the Microsoft Downloads site, click **Download**.

1. When prompted whether to run or save **AzureADConnect.msi**, click **Run**. This will download the file and automatically start the **Microsoft Azure Active Directory Connect** wizard. 

1. On the **Welcome to Azure AD Connect** page, enable the **I agree to the license terms and privacy notice** checkbox and click **Continue**.

1. On the **Express Settings** page, click the **Customize** button.

1. On the **Install required components** page, leave all optional configuration options deselected and click **Install**.

1. On the **User sign-in** page, select the **Pass-through authentication** option and the **Enable single sign-on** checkboxes, and click **Next**.

    ![On the User sign-in page of Microsoft Azure AD Connect wizard, the Pass-through authentication option and the Enable single sign-on checkboxes are selected.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/AzureADConnect_UserSign-in.png)

1. On the **Connect to Azure AD** page, sign in by using the credentials of the **john.doe** account and click **Next**.

1. On the **Connect your directories** page, ensure that the **contoso.local** entry appears in the **FOREST** drop down list and click **Add Directory**. In the **AD foest account**, ensure that the **Create new AD account** option is selected, in the **ENTERPRISE ADMIN USERNAME** textbox, type **CONTOSO\\demouser**, in the **PASSWORD** textbox, type **demo\@pass123**, and click **OK**.

    ![On the Connect your directories page of Microsoft Azure AD Connect wizard, contoso.local has been added.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/AzureADConnect_ConnectyourDirectories.png)

1. Back on the **Connect your directories** page, click **Next**.

1. On the **Azure AD sign-in configuration** page, ensure that your custom domain name is listed as the verified **Active Directory UPN Suffix**, and that the **userPrincipalName** entry appears in the **USER PRINCIPAL NAME** drop-down list. Note the warning stating **Users will not be able to sign-in to Azure AD with on-premises credentials if the UPN suffix does not match a verified domain name**. Enable the checkbox **Continue without matching all UPN suffixes to verified domain** and click **Next**. 

   > **Note**: This is expected, since some users are still configured with the **contoso.local** UPN suffix, which is not routable and cannot be configured as a verified custom domain name of an Azure AD tenant.

    ![On the Azure AD sign-in configuration page of Microsoft Azure AD Connect wizard, the custom domain name is listed as verified, and the userPrincipalName is listed as the attribute to use as the AzureAD username.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/AzureADConnect_AzureADsign-inconfiguration.png)

1. On the **Domain and OU filtering** page, ensure that only the **DemoAccounts** OU and all of its children OUs are selected and click **Next**. 

    ![On the Domain and OU filtering page of Microsoft Azure AD Connect wizard, Demo Accounts OU and all of its child OUs are selected.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/AzureADConnect_DomainandOUFiltering.png)

1. On the **Uniquely identifying your users** page, accept the default settings and click **Next**. 

    ![On the Uniquely identifying your users page of Microsoft Azure AD Connect wizard, the default settings are displayed.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/AzureADConnect_UniquelyIdentifyingyourusers.png)

1. On the **Filter users and devices** page, accept the default settings and click **Next**. 

    ![On the Filter users and devices page of Microsoft Azure AD Connect wizard, the default settings are displayed.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/AzureADConnect_FilterUsersandDevices.png)

1. On the **Optional features** page, accept the default settings and click **Next**.

    ![On the Optional features page of Microsoft Azure AD Connect wizard, the default settings are displayed.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/AzureADConnect_OptionalFeatures.png)

1. On the **Enable single sign-on** page, click **Enter credentials**, in the **Forest credentials** dialog box, sign in with the **CONTOSO\\demouser** name and **demo\@pass123** password, and click **Next**.

    ![On the Enable single sign-on page of Microsoft Azure AD Connect wizard, the prompt for forest credentials is displayed.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/AzureADConnect_EnableSingleSign-on.png)

1. On the **Ready to configure** page, ensure that the **Start the synchronization process when configuration completes** checkbox is **NOT** selected and click **Install**.

    ![On the Enable single sign-on page of Microsoft Azure AD Connect wizard, the Start the synchronization process when configuration completes is cleared.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/AzureADConnect_ReadytoConfigure.png)

   > **Note**: You will configure attribute-level filtering before enabling the synchronization process.

   > **Note**: Installation should take about 2 minutes.

1. On the **Configuration complete** page, click **Exit**.

    ![On the Configuration complete page of Microsoft Azure AD Connect wizard, the status of the installation is displayed.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/AzureADConnect_ConfigurationComplete.png)


### Task 7: Enable Active Directory Recycle Bin

In this task, you will enable Recycle Bin in the Contoso Active Directory domain. 

1. Within the Remote Desktop session to **DC1**, from the Tools menu in the Server Manager console, start **Active Directory Administrative Center**.

1. In the **Active Directory Administrative Center** console, right-click the node representing the contoso.local domain and, in the context sensitive menu, click **Enable Recycle Bin**.

    ![In the Active Directory Administrative Center console, the **Enable Recycle Bin** option is displayed.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/AD_EnableRecycleBin.png)

1. When prompted to confirm, click **OK**.

1. When prompted to refresh AD Administrative Center, click **OK**.

   > **Note**: For information regarding benefits of the Recycle Bin in hybrid scenarios, refer to <https://docs.microsoft.com/en-us/azure/active-directory/hybrid/how-to-connect-sync-recycle-bin>


### Task 8: Configure Azure AD Connect attribute-level filtering

In this task, you will configure Azure AD Connect attribute level filtering that will limit synchronization of user accounts to those with the UPN suffix matching the custom domain name of the target Azure AD tenant.

   > **Note**: The positive filtering option requires at least two sync rules. One of them determines the correct scope of objects to synchronize. The second catch-all sync rule filters out all objects that have not yet been identified as an object that should be synchronized.

1. Within the Remote Desktop session to **DC1**, start **Synchronization Rules Editor**

1. In the Synchronization Rules Editor window, on the **View and manage your synchronization rules** page, ensure that **Inbound** appears in the **Direction** drop-down list and click **Add new rule**. This will launch the **Create inbound synchronization rule** wizard.

    ![In the Synchronization Rules Editor, Inbound rules are displayed.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/SynchronizationRulesEditor_AddNewRule.png)

1. On the **Description** page, specify the following settings and click **Next**:

    - Name: **Custom In from AD - UPN Filter**

    - Description: **Custom Inbound Rule - includes users with UPN set to match the Azure AD custom domain**

    - Connected System: **contoso.local**

    - Connected System Object Type: **user**

    - Metaverse Object Type: **person**

    - Link Type: **join**

    - Precedence: **50**

    - Tag: not set

    - Enable Password Sync: not set

    - Disabled: not set

    ![On the description page of the Create inbound synchronization rule wizard, the configuration settings are displayed.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/CreateInboundSynchronizationRule_Description.png)

1. On the **Scoping filter** page, click **Add Group**, click **Add clause** specify the following, and click **Next**:

    - Attribute: **userPrincipalName**

    - Operator: **ENDSWITH**

    - Value: **@*<custom_domain_name>***

    ![On the scoping filter page of the Create inbound synchronization rule wizard, the configuration settings are displayed.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/CreateInboundSynchronizationRule_ScopingFilter.png)

1. On the **Join Rules** page, click **Next**.

    ![On the Join Rules page of the Create inbound synchronization rule wizard, the configuration settings are displayed.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/CreateInboundSynchronizationRule_JoinRules.png)

1. On the **Transformations** page, click **Add transformation** specify the following and click **Add**:

    - FlowType: **Constant**

    - Target Attribute: **cloudFiltered**

    - Source: **False**

    ![On the Transformations page of the Create inbound synchronization rule wizard, the configuration settings are displayed.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/CreateInboundSynchronizationRule_Transformations.png)

1. When presented with a **Warning** dialog box displaying message stating that **A full import and full synchronization will be run on 'contoso.local' during your next synchronization cycle**, click **OK**.

   > **Note**: This should bring you back to the View and manage your synchronization rules interface, with the new rule listed at the top of the rule list. 

1. Back in the Synchronization Rules Editor window, on the **View and manage your synchronization rules** page, ensure that **Inbound** appears in the **Direction** drop-down list and click **Add new rule** again. This will launch the **Create inbound synchronization rule** wizard.

1. On the **Description** page, specify the following settings and click **Next**:

    - Name: **Custom In from AD - Catch-all Filter**

    - Description: **Custom Inbound Rule - excludes all users with UPN not set to match the Azure AD custom domain**

    - Connected System: **contoso.local**

    - Connected System Object Type: **user**

    - Metaverse Object Type: **person**

    - Link Type: **join**

    - Precedence: **51**

    - Tag: not set

    - Enable Password Sync: not set

    - Disabled: not set

    ![On the description page of the Create inbound synchronization rule wizard, the configuration settings are displayed.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/CreateInboundSynchronizationRule_DescriptionCatchAll.png)

1. On the **Scoping filer** page, click **Next**

    ![On the scoping filter page of the Create inbound synchronization rule wizard, the configuration settings are displayed.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/CreateInboundSynchronizationRule_ScopingFilterCatchAll.png)

1. On the **JoinRules** page, click **Next**.

    ![On the Join Rules page of the Create inbound synchronization rule wizard, the configuration settings are displayed.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/CreateInboundSynchronizationRule_JoinRulesCatchAll.png)

1. On the **Transformations** page, click **Add transformation** specify the following and click **Add**:

    - FlowType: **Constant**

    - Target Attribute: **cloudFiltered**

    - Source: **True**

    ![On the Transformations page of the Create inbound synchronization rule wizard, the configuration settings are displayed.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/CreateInboundSynchronizationRule_TransformationsCatchAll.png)

1. When presented with a **Warning** dialog box displaying message stating that **A full import and full synchronization will be run on 'contoso.local' during your next synchronization cycle**, click **OK**.

   > **Note**: This should bring you back to the View and manage your synchronization rules interface, with the new rules listed at the top of the rule list. 

    ![In the Synchronization Rules Editor, Inbound rules, including the two new rules, are displayed.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/SynchronizationRulesEditor_AddNewRule_withRules.png)


#### Task 9: Initiate and verify directory synchronization

1. Within the Remote Desktop session to **DC1**, double-click the **Azure AD Connect** desktop shortcut.

1. On the **Welcome to Azure AD Connect** page, click **Configure**. 

1. On the **Additional tasks** page, click **Customize synchronization options** and click **Next**.

1. On the **Connect to Azure AD** page, sign in by using the credentials of the **john.doe** account and click **Next**.

1. On the **Connect your directories** page, click **Next**.

1. On the **Domain and OU filtering** page, click **Next**. 

1. On the **Optional features** page, accept the default settings and click **Next**.

1. On the **Enable single sign-on** page, click **Next**.

1. On the **Ready to configure** page, select the **Start the synchronization process when configuration completes** checkbox and click **Configure**.

1. On the **Configuration complete** page, click **Exit**.

1. Within the Remote Desktop session to **DC1**, in the Internet Explorer window displaying the Azure portal, navigate to the **Users - All users** blade of the Contoso Azure AD tenant.

1. On the **Users - All users** blade, note that the list of user objects includes all user accounts with the UPN suffix matching the custom domain name of the Azure AD tenant. 

1. In the Azure portal, navigate to the **Groups - All groups** blade and note that all of the contoso.local domain groups have been synchronized as well. 

1. In the Azure portal, navigate to the **Contoso - Azure AD Connect** blade and review its settings. Verify Azure AD Connect Sync Status (enabled), Last Sync timestamp, Password Hash Sync (disabled), as well as the user sign-in configuration (Federation disabled, Seamless single sign-on enabled for 1 domain , and Pass-through authentication enabled with 1 agent).

   > **Note**: In a production environment, you would install additional agents for redundancy. For more information, refer to <https://docs.microsoft.com/en-us/azure/active-directory/hybrid/how-to-connect-pta-quick-start>


### Task 10: Configure Hybrid Azure AD join

In this task, you will configure Azure AD Connect device synchronization options.

1. Within the Remote Desktop session to **DC1**, double-click the **Azure AD Connect** desktop shortcut.

1. On the **Welcome to Azure AD Connect** page, click **Configure**. 

1. On the **Additional tasks** page, click **Configure device options** and click **Next**.

1. On the **Oveview** page, review the information regarding **Hybrid Azure AD join** and **Device writeback**, and click **Next**.

1. On the **Connect to Azure AD** page, sign in by using the credentials of the **john.doe** account and click **Next**.

1. On the **Device options** page, ensure that the **Configure Hybrid Azure AD join** option is selected and click **Next**. 

1. On the **Device operating system** page, select the **Windows 10 or later domain-joined devices** and **Supported Windows downlevel domain-joined devices** checkboxes, and click **Next**. 

   > **Note**: Windows downlevel devices are supported only if you are using Seamless SSO for managed domains or a federation service such as AD FS for federated domains.

1. On the **SCP configuration** page, enable the checkbox for the **contoso.local** Active Directory forest, select **Azure Active Directory** entry in the **Authentication Service** dropdown list, and click **Add**.

1. When prompted for Enterprise Admin Credentials for contoso.local, in the **Windows Security** dialog box, sign in with the **CONTOSO\\demouser** user name and **demo\@pass123** password.

1. Back on the **SCP configuration** page, click **Next**.

1. On the **Ready to configure** page, click **Configure**.

1. On the **Configuration complete** page verify that the task completed successfully and click **Exit**.

   > **Note**: For more information regarding configuring hybrid Azure Active Directory join for managed domains, refer to <https://docs.microsoft.com/en-us/azure/active-directory/devices/hybrid-azuread-join-managed-domains#configure-hybrid-azure-ad-join>


### Task 11: Perform Hybrid Azure AD join

1. From the lab computer, in the Azure portal, verify that you are signed in to the Azure AD tenant associated with the Azure subscription into which you deployed resources in the Before Hands-On Lab exercises. If not, click the **Directory + Subscription** icon in the toolbar of the Azure portal (to the right of the **Cloud Shell** icon) to switch to that Azure AD tenant. 

1. In the Azure portal, navigate to the blade of the **APP1** virtual machine.

1. From the **APP1** virtual machine blade, connect to **APP1** via Remote Desktop. When prompted to sign in, use the **AGAyers\@<custom_domain_name>** user name with the **demo@pass123** password (where **<custom_domain_name>** placeholder represents the custom DNS domain name you assigned to the Contoso Azure AD tenant earlier in this exercise.

1. Within Remote Desktop session to **APP1**, from the **Server Manager** window, start **Task Scheduler**. 

1. In the **Task Scheduler** console, naviagate to the **Task Scheduler Library**, **Microsoft**, **Windows**, and **Workplace Join**. From there, enable and start the **Automatic-Device-Join** task. 

1. Switch to the Remote Desktop session to **DC1** and, from the console pane of the Windows PowerShell ISE window, start Azure AD Connect delta synchronization by running the following:

   ```pwsh
   Import-Module -Name 'C:\Program Files\Microsoft Azure AD Sync\Bin\ADSync\ADSync.psd1'
   
   Start-ADSyncSyncCycle -PolicyType Delta
   ```

1. Switch back to the Remote Desktop session to **APP1** and start **Command Prompt**.

1. From the Command Prompt window, check the Azure AD registration status of APP1 by running the following: 

   ```
   dsregcmd /status
   ```

1. Verify that the output of the command resembles the following:

   ```
   +----------------------------------------------------------------------+
   | Device State                                                         |
   +----------------------------------------------------------------------+

        AzureAdJoined : YES
     EnterpriseJoined : NO
             DeviceId : 61eea2b8-efbe-43d9-b267-126433c8ee34
           Thumbprint : BBAAA0FB4A55E880388851BED955A2669A961A96
       KeyContainerId : 2eb75eb8-0a1d-437b-99d9-9dd161ca0d90
          KeyProvider : Microsoft Software Key Storage Provider
         TpmProtected : NO
         KeySignTest: : PASSED
                  Idp : login.windows.net
             TenantId : xxxxxxx-xxxx-xxx-xxxx-xxxxxxxxxx
           TenantName : xxxxxxx-xxxx-xxx-xxxx-xxxxxxxxxx
          AuthCodeUrl : https://login.microsoftonline.com/xxxxxxx-xxxx-xxx-xxxx-xxxxxxxxxx/oauth2/authorize
       AccessTokenUrl : https://login.microsoftonline.com/xxxxxxx-xxxx-xxx-xxxx-xxxxxxxxxx/oauth2/token
               MdmUrl :
            MdmTouUrl :
     MdmComplianceUrl :
          SettingsUrl :
       JoinSrvVersion : 1.0
           JoinSrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/device/
            JoinSrvId : urn:ms-drs:enterpriseregistration.windows.net
        KeySrvVersion : 1.0
            KeySrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/key/
             KeySrvId : urn:ms-drs:enterpriseregistration.windows.net
         DomainJoined : YES
           DomainName : CONTOSO

   +----------------------------------------------------------------------+
   | User State                                                           |
   +----------------------------------------------------------------------+

               NgcSet : NO
      WorkplaceJoined : NO
        WamDefaultSet : NO
           AzureAdPrt : NO

   +----------------------------------------------------------------------+
   | Ngc Prerequisite Check                                               |
   +----------------------------------------------------------------------+

        IsUserAzureAD : NO
        PolicyEnabled : NO
       DeviceEligible : YES
   SessionIsNotRemote : NO
     X509CertRequired : NO
         PreReqResult : WillNotProvision

   ```
1. Switch back to the Remote Desktop session to **DC1**, in the Internet Explorer window displaying the Azure portal, navigate to the **Devices - All devices** blade of the Contoso Azure AD tenant and verify that there is an entry representing the APP1 server, with the **Join Type** set to **Hybrid Azure AD joined**.

   > **Note**: You might need to wait until the Azure AD registration status is correctly reported and its Azure AD object appears in the Azure portal.

    ![In the Azure portal, on the Devices - All devices blade, an entry representing the APP1 server is displayed.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/APP1_HybridAzureADjoined.png)


### Summary 1

In this exercise, you integrated an Active Directory forest with an Azure Active Directory tenant by creating an Azure Active Directory tenant and activating an Enterprise Mobility + Security E5 trial, creating and configuring an Azure AD user, purchasing a custom domain name, assigning a custom domain name to the Contoso Azure AD tenant, configuring DNS suffix in the Contoso Active Directory forest, installing Azure AD Connect, enable Active Directory Recycle Bin, configuring Azure AD Connect attribute-level filtering, initiating and verifying directory synchronization, configuring Hybrid Azure AD join, and performing Hybrid Azure AD join of a Windows Server 2016 VM.


## Exercise 2: Manage Authentication, Authorization, and Access Protection in Hybrid Scenarios

Duration: 150 minutes

### Overview 2

In this exercise, you will optimize authentication, authorization, and access protection for Contoso Active Directory environment integrated with the Contoso Azure AD tenant by enabling Azure AD Multi-Factor Authentication, enabling Azure AD password writeback and Self-Service Password Reset, implementing, Azure AD Password Protection, enabling Azure Active Directory Identity Protection, enabling Automatic Intune Enrollment, as well as implementing Azure AD Privileged Identity Management and Azure AD Conditional Access Policies.


### Task 1: Create Active Directory groups

In this task, you will create and configure Active Directory groups that will be used to control authentication, authorization, and access control and synchronize them to the Contoso Azure AD tenant. 

1. Within the Remote Desktop session to **DC1**, from the **Server Manager** window, start **Active Directory Users and Computers** console. 

1. In the **Active Directory Users and Computers** console, expand the **contoso.local** node and navigate to the **Demo Accounts\\Groups** OU. 

1. In the **Groups** OU, create a new group with the following settings:

    - Group name: **Engineering - Mandatory MFA**

    - Group name (pre-Windows 2000): **Engineering - Mandatory MFA**

    - Group scope: **Global**

    - Group type: **Security**

1. Open the **Properties** window of the **Engineering - Mandatory MFA** group, in the **Description** text box, type **Engineering users with user state-based MFA enforcement (without Conditional Access)**

1. Within the Remote Desktop session to **DC1**, from the Script pane of the Windows PowerShell ISE window, run the following to add designated users to the newly created group (replace the placeholder `<custom_domain_name>` with the actual name of the custom verified domain name you assigned to the Contoso Azure AD tenant).

    ```pwsh
    $domainName = '<custom_domain_name>'
    $users = Get-ADGroupMember -Identity 'Engineering' -Recursive | Where-Object {($_.objectClass -eq 'user') -and ($_.distinguishedName -like "*OU=NY,OU=US,OU=Users,OU=Demo Accounts,DC=contoso,DC=local")}
    foreach ($user in $users) {
        $user = Get-ADUser -Identity $User.SamAccountName
        Add-ADGroupMember -Identity 'Engineering - Mandatory MFA' -Members $user
    }
    ```

1. From the console pane of the Windows PowerShell ISE window, start Azure AD Connect delta synchronization by running the following:

   ```pwsh
   Import-Module -Name 'C:\Program Files\Microsoft Azure AD Sync\Bin\ADSync\ADSync.psd1'
   
   Start-ADSyncSyncCycle -PolicyType Delta
   ```

1. In the Remote Desktop session to **DC1**, in the Internet Explorer window displaying the Azure portal, navigate to the **Contoso - Overview** blade of the Contoso Azure AD tenant and click **Groups**.

1. On the **Contoso - All groups** blade, verify that there is an entry representing the **Engineering - Mandatory MFA** group containing the Azure AD user accounts matching Active Directory uesr accounts which are members of the Active Directory **Engineering - Mandatory MFA** group.


### Task 2: Assign EM+S E5 licenses to Azure AD users

In this task, you assign a value to the **UsageLocation** attribute of each user account and assign an Azure AD Premium license to each user. This is necessary in order to implement Azure AD-based Multi-Factor Authentication for these users.

1. Within the Remote Desktop session to **DC1**, from the Script pane of the Windows PowerShell ISE window, run the following to install Azure AD Graph PowerShell module for Graph (click **Yes to All** when prompted whether to proceed with the installation):

    ```pwsh
    Install-Module AzureAD
    ```

1. From the Script pane of the Windows PowerShell ISE window, run the following to sign in to the Contoso Azure AD tenant. 

    ```pwsh
    Connect-AzureAD
    ```

1. When prompted, sign in with the **john.doe** Azure AD user account, which you created in the previous exercise.

1. From the Script pane of the Windows PowerShell ISE window, run the following to set the **Location** attribute to **United States** for all Azure AD user accounts with the UPN suffix matching the custom verified domain name of the Contoso Azure AD tenant. 

    ```pwsh
    $domainName = (Get-AzureADDomain | Where-Object IsDefault -eq 'True').Name
    Get-AzureADUser | Where-Object {$_.UserPrincipalName -like "*@$domainName"} | Set-AzureADUser -UsageLocation 'US'
    ```
1. From the Script pane of the Windows PowerShell ISE window, run the following to assign the EM+S E5 trial licenses to all Azure AD user accounts with the UPN suffix matching the custom verified domain name of the Contoso Azure AD tenant. 

    ```pwsh
    $license = New-Object -TypeName Microsoft.Open.AzureAD.Model.AssignedLicense
    $license.SkuId = (Get-AzureADSubscribedSku | Where-Object {$_.SkuPartNumber -eq 'EMSPREMIUM'}).SkuId
    $licensesToAssign = New-Object -TypeName Microsoft.Open.AzureAD.Model.AssignedLicenses
    $licensesToAssign.AddLicenses = $license
    $users = Get-AzureADUser | Where-Object {$_.UserPrincipalName -like "*@$domainName"}
    foreach($user in $users) { 
        Set-AzureADUserLicense -ObjectId $user.ObjectId -AssignedLicenses $licensesToAssign
    }
    ```

### Task 3: Enable Azure AD Multi-Factor Authentication

In this task, you will configure user state-based Azure AD Multi-Factor Authentication for members of the **Engineering - Mandatory MFA** group.

   > **Note**: In general, enabling Azure Multi-Factor Authentication using Conditional Access policies is the recommended approach, since it offers more flexibility. Setting Multi-Factor Authentication by modifying the user state requires users to perform two-step verification every time they sign in and overrides Conditional Access policies. On the other hand, this approach might be required if existing licensing arrangement does not include Conditional Access.

1. Within the Remote Desktop session to **DC1**, from the Script pane of the Windows PowerShell ISE window, run the following to install Azure AD MSOnline PowerShell module for Graph (click **Yes to All** when prompted whether to proceed with the installation):

    ```pwsh
    Install-Module MSOnline
    ```

1. From the Script pane of the Windows PowerShell ISE window, run the following to sign in to the Contoso Azure AD tenant. 

    ```pwsh
    Connect-MsolService
    ```

1. When prompted, sign in with the **john.doe** Azure AD user account, which you created in the previous exercise.

1. From the Script pane of the Windows PowerShell ISE window, run the following to enable Azure AD Multi-Factor Authentication for all Azure AD user accounts with the UPN suffix matching the custom verified domain name of the Contoso Azure AD tenant. 

    ```pwsh
    $objectIdGUID = (Get-MsolGroup | Where-Object {$_.DisplayName -eq 'Engineering - Mandatory MFA'}).objectId.Guid
    $users = Get-MsolGroupMember -GroupObjectId $objectIdGUID
    $st = New-Object -TypeName Microsoft.Online.Administration.StrongAuthenticationRequirement
    $st.RelyingParty = "*"
    $st.State = "Enabled"
    $sta = @($st)
    foreach($user in $users) { 
        Set-MsolUser -ObjectId $user.ObjectId -StrongAuthenticationRequirements $sta
    }
    ```

1. To verify the outcome, within the Remote Desktop session to **DC1**, in the Internet Explorer window displaying the Azure portal, navigate to the **Users - All users** blade of the Contoso Azure AD tenant and click **Multi-Factor Authentication** (you might need to click **More...** first). This will open a new tab in the Internet Explorer window displaying the **multi-factor authentication** portal.

1. In the the **multi-factor authentication** portal, on the **users** tab, ensure that all users have the **MULTI-FACTOR AUTH STATUS** set to **Enabled**.


### Task 4: Enable password writeback and Self-Service Password Reset

In this task, you will enable password writeback and Self-Service Password Reset (SSPR) for Contoso users that had their accounts synchronized to the Contoso Azure AD tenant.

1. Within the Remote Desktop session to **DC1**, double-click the **Azure AD Connect** desktop shortcut.

1. On the **Welcome to Azure AD Connect** page, click **Configure**. 

1. On the **Additional tasks** page, click **Customize synchronization options** and click **Next**.

1. On the **Connect to Azure AD** page, sign in by using the credentials of the **john.doe** account and click **Next**.

1. On the **Connect your directories** page, click **Next**.

1. On the **Domain and OU filtering** page, click **Next**. 

1. On the **Optional features** page, select the **Password writeback** checkbox and click **Next**.

1. On the **Enable single sign-on** page, click **Next**.

1. On the **Ready to configure** page, ensure that the **Start the synchronization process when configuration completes** checkbox is selected and click **Configure**.

1. On the **Configuration complete** page, click **Exit**.

1. Within the Remote Desktop session to **DC1**, in the Internet Explorer window displaying the Azure portal, navigate to the **Contoso - Overview** blade of the Contoso Azure AD tenant.

1. On the **Contoso - Overview** blade, click **Password reset**. 

1. On the **Password reset - Properties** blade, set **Self service password reset enabled** to **Selected**, click **Select group**, on the **Default password reset policy**, click **Engineering**, click **Select**, and click **Save**.

1. On the **Password reset - Properties** blade, click **Authentication methods**.

1. On the **Password reset - Authentication methods**, set **Number of methods required to reset** to **2**, enable all **Methods available to users**, including **Mobile app notification**, **Mobile app code**, **Email**, **Mobile phone (SMS only)**, and **Security questions**. 

   > **Note**: The **Office phone** method is not available in trial subscriptions.

1. Set **Number of security questions required to register** and **Number of questions required to reset** to **3**. 

1. Click **Select securitiy questions**, on the **Select security questions** blade, click **+ Predefined**, on the **Add predefined security questions** blade, select any 5 questions, click **OK** twice, and, back on the **Password reset - Authentication methods** blade, click **Save**.

1. On the **Password reset - Authentication methods**, click **Registration** and ensure that **Require users to register when signing in** is set to **Yes** and that **Number of days before usres are asked to re-confirm their authentication information** is set to **180**.

1. On the **Password reset - Registration** blade, click **On-premises integration** and verify that the **Write back passwords to your on-premises directory** setting is set to **Yes**. Note that you have the option to **Allow users to unlock accounts without resetting their passwords**.


### Task 5: Implement Azure AD Password Protection for Windows Server Active Directory

In this task, you will implement Azure AD password Protection for Windows Server Active Directory

1. Within the Remote Desktop session to **DC1**, from the **Server Manager** window, start **Group Policy Management** console. 

1. In the **Group Policy Management** console, navigate to the **Forest: contoso.local\\Domains\\contoso.local** node, right click **Default Domain Policy** and, in the right-click menu, click **Edit**. 

1. In the **Group Policy Management Editor**, navigate to **Computer Configuration\\Policies\\Windows Settings\\Security Settings\\Account Policies\\Account Lockout Policy**. 

1. Set the value of the **Account lockout threshold** to **10** and click **OK** and accept the settings in the **Suggested Value Changes**. 

    ![In the Group Policy Management Editor, the Account Lockout policy settings are displayed.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/AzureADPasswordProtectionPolicy_ADLockout.png)

1. Within the Remote Desktop session to **DC1**, in the Internet Explorer window displaying the Azure portal, navigate to the **Contoso - Overview** blade of the Contoso Azure AD tenant.

1. On the **Contoso - Overview** blade, click **Security**.

1. On the **Security - Getting started** blade, click **Authentication methods**.

1. On the **Authentication methods - Authentication methods policy (Preview)** blade, click **Password protection**.

1. On the **Authentication methods - Password protection** blade, specify the following settings and click **Save**:

    - Lockout threshold: **5**

    - Lockout duration in seconds: **3600**

    - Enforce custom list: **Yes**

    - Custom banned password list: **Contoso**, **password**, **pass**

    - Enable password protection on Windows Server Active Directory: **Yes**

    - Mode: **Audit**

1. Switch to the Remote Desktop session to **APP1** virtual machine, where you are signed in as the user **AGAyers** with the **demo@pass123** password. 

1. Within the Remote Desktop session to **APP1**, start Internet Explorer, navigate to the **Azure AD Password Protection for Windows Server Active Directory** page at <https://www.microsoft.com/download/details.aspx?id=57071> and download **AzureADPasswordProtectionProxySetup.exe** 

1. Within the Remote Desktop session to **APP1**, start File Explorer, navigate to the download location, and run the installation of the **Azure AD Password Protection Proxy Bundle** with the default options.

1. Within the Remote Desktop session to **APP1**, start Windows PowerShell ISE, and, from the console pane, run the following to register the proxy (replace the `<domain_name>` placeholder with the name of the default domain name associated with the Contoso Azure AD tenant):

    ```pwsh
    Import-Module AzureADPasswordProtection
    Register-AzureADPasswordProtectionProxy -AccountUpn 'john.doe@<domain_name>.onmicrosoft.com'
    ```

1. When prompted, sign in to the Contoso Azure AD tenant using credentials of the **john.doe** user account. 

1. From the Windows PowerShell ISE console, run the following to register the Active Directory forest (replace the `<domain_name>` placeholder with the name of the default domain name associated with the Contoso Azure AD tenant):

    ```pwsh
    Register-AzureADPasswordProtectionForest -AccountUpn 'john.doe@<domain_name>.onmicrosoft.com'
    ```

1. Switch to the Remote Desktop session to **DC1** virtual machine, where you are signed in as the user **CONTOSO\demouser** with the **demo@pass123** password. 

1. Within the Remote Desktop session to **DC1**, start Internet Explorer, navigate to the **Azure AD Password Protection for Windows Server Active Directory** page at <https://www.microsoft.com/download/details.aspx?id=57071> and download **AzureADPasswordProtectionDCAgentSetup.exe** 

1. Within the Remote Desktop session to **DC1**, start File Explorer, navigate to the download location, and run **Azure AD Password Protection DC Agent Setup** with the default options.

1. Restart the operating system of DC1 once the setup completes.


### Task 6: Enable Azure Active Directory Identity Protection

In this task, you will enable Azure AD Identity Protection

1. From the lab computer, in the Azure portal, navigate to the blade of the **DC1** virtual machine.

1. From the **DC1** virtual machine blade, connect to **DC1** via Remote Desktop. When prompted to sign in, use the **CONTOSO\\demouser** name with the **demo\@pass123** password. 

1. Within the Remote Desktop session to **DC1**, start Internet Explorer and navigate to the Azure portal at <https://portal.azure.com>.

1. When prompted to sign in, provide the credentials of the **john.doe** Azure AD user account, which you copied into Notepad earlier in this exercise.

1. In the Azure portal, click **+ Create a resource**.

1. On the **New** blade, in the **Search the Marketplace** text box, type **Identity Protection** and, in the list of search results, click **Azure AD Identity Protection**. 

1. On the **Azure AD Identity Protection** blade, click **Create** twice.

1. In the Azure portal, navigate to the **All services** blade, in the **Search All** text box, type **Azure AD Identity Protection** blade, and, in the list of results, click **Azure AD Identity Protection**.

1. On the **Azure AD Identity Protection** blade, click **MFA registration policy**.

1. On the **Azure AD Identity Protection - MFA registration policy** blade, in the **Assignments** section, click **Users**. 

1. On the **Users** blade, on the **Include** blade, click **Select individual users and groups**, click **Select users**, on the **Select users** blade, in the **Select** text box, type **Engineering**, in the list of results, click **Engineering** and click **Select**.

    ![In the Azure portal, on the Include tab of the Users blade, the group included in the scope of the MFA registration policy is displayed.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/IdentityProtection_MFAregistrationpolicy_UsersInclude.png)

1. On the **Users** blade, on the **Exclude** blade, click **Select excluded users**, on the **Select users** blade, in the **Select** text box, type **Engineering - Mandatory MFA**, in the list of results, click **Engineering - Mandatory MFA**, click **Select**, and, back on the **Users** blade, click **Done**.

    ![In the Azure portal, on the Exclude tab of the Users blade, the group excluded from the scope of the MFA registration policy is displayed.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/IdentityProtection_MFAregistrationpolicy_UsersExclude.png)

1. Back on the **Azure AD Identity Protection - MFA registration policy** blade, in the **Controls** section, click **Access**, on the **Access** blade, ensure that the **Require Azure MFA registration** is selected, and click **Select**.

1. Back on the **Azure AD Identity Protection - MFA registration policy** blade, set **Enforce Policy** to **On** and click **Save**

    ![In the Azure portal, the MFA registration policy settings are displayed.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/IdentityProtection_MFAregistrationpolicy_EnforcePolicy.png)

1. On the **Azure AD Identity Protection** blade, click **User risk policy**.

1. On the **Azure AD Identity Protection - User risk policy** blade, configure the **User risk remediation policy** with the following settings save your configuration:

    - Assignments: 

        - Users: **All users**

        - Conditions:

            - User risk: **Low and above**

    - Controls:

        - Access: **Allow access** and **Require password change**

    - Enforce Policy: **On**

    ![In the Azure portal, the User risk policy settings are displayed.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/IdentityProtection_UserRiskPolicy.png)


### Task 7: Enable Automatic Intune Enrollment

In this task, you will enable automatic enrollment of hybrid Azure AD devices into Intune. 

1. Within the Remote Desktop session to **DC1**, in the Internet Explorer window displaying the Azure portal, navigate to the **All services** blade.

1. On the **All services** blade, search for **Intue** and, in the list of results, click **Intune**.

1. On the **Microsoft Intune - Overview** blade, click **Device enrollment**.

1. On the **Device enrollment** blade, click **Windows enrollment**.

1. On the **Windows enrollment** blade, click **Automatic Enrollment**.

1. On the **Configure** blade, set **MDM user scope** to **All** and click **Save**.


### Task 8: Enable Enterprise-State-Roaming

1. Within the Remote Desktop session to **DC1**, in the Internet Explorer window displaying the Azure portal, navigate to the blade of the Contoso Azure AD tenant.

1. On the **Contoso - Overview** blade, click **Devices**.

1. On the **Devices - All devices** blade, click **Enterprise State Roaming**.

1. On the **Devices - Enterprise State Roaming** blade, click **Selected** select the **Engineering** group from the list of Azure AD tenant users and groups, and click **Save**.


### Task 9: Implement Azure AD Conditional Access Policies

In this task, you will implement Azure AD Conditional Access Policies 

1. Within the Remote Desktop session to **DC1**, in the Internet Explorer window displaying the Azure portal, navigate to the **Contoso - Overview ** blade of the Contoso Azure AD tenant.

1. On the **Contoso - Overview** blade, click **Security**.

1. On the **Security - Getting started** blade, click **Named locations**.

1. On the **Security - Named locations** blade, click **+ New location**.

1. On the **New named location** blade, specify the following settings and click **Create**

    - Name: **Contoso Headquarters**

    - Define the location using: **IP ranges**

    - Mark as trusted location: enabled

    - IP ranges: the public IP address assigned the APP1 Azure VM in the CIDR notation (i.e. /32)

    ![In the Azure portal, named location settings are displayed.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/AzureADConditionalAccess_Namedlocations.png)

1. On the **Security - Named locations** blade, click **Configure MFA trusted IPs**. This will open a new tab in the Internet Explorer window displaying the **service settings** tab of the **multi-factor authentication** portal.

    ![In the MFA portal, service settings are displayed.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/AzureADConditionalAccess_MFA_servicesettings.png)

1. On the **service tab**, in the **trusted ip** text box, type the same public IP address assigned the APP1 Azure VM in the CIDR notation (i.e. /32) and click **Save**.

1. Navigate back to the **Security - Getting started** blade and click **Conditional Access**.

1. On the **Conditional Access - Policies** blade, click **+ New policy**

1. On the **New** blade, in the **Name** text box, type **Contoso Engineering On-Premises Conditional Access Policy**.

1. On the **New** blade, in the **Assignments** section, click **Users and groups**

1. On the **Users and groups** blade, on the **Include** tab, choose the **Select users and groups** option, select the **Users and groups** checkbox, on the **Select** blade, type **Engineering**, in the list of results, click **Engineering**, and click **Select**.

    ![In the Azure portal, on the Users and groups blade, on the Include tab, the configuration settings are displayed.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/AzureADConditionalAccess_UsersandGroupsInclude.png)

1. On the **Users and groups** blade, on the **Exclude** tab, choose the **Select users and groups** option, select the **Users and groups** checkbox, on the **Select** blade, type **Engineering**, in the list of results, click **Engineering - Mandatory MFA**, and click **Select**.

    ![In the Azure portal, on the Users and groups blade, on the Exclude tab, the configuration settings are displayed.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/AzureADConditionalAccess_UsersandGroupsExclude.png)

1. Back on the **Users and groups** blade, click **Done**.

1. On the **New** blade, in the **Assignments** section, click **Cloud apps or actions**

1. On the **Cloud apps or actions** blade, on the **Include** tab, choose the **Select apps** option, on the **Select** blade, click the **Microsoft Azure Management** checkbox, click **Select**, and then click **Done**.

    ![In the Azure portal, on the Cloud apps or actions blade, on the Include tab, the selected app is displayed.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/AzureADConditionalAccess_CloudppsandActionsInclude.png)

   > **Note**: Review the warning stating **Don't lock yourself out! This policy impacts the Azure portal. Before you continue, ensure that you or someone else will be able to get back into the portal. Disregard this warning if you are conifguring persistent browser session policy that works correctly only if "All cloud apps" are selected.**

1. On the **New** blade, in the **Assignments** section, click **Conditions**.

1. On the **Conditions** blade, click **Sign-in risk**, set **Configure** to **Yes**, enable the **No risk** checkboxes, and click **Select**.

    ![In the Azure portal, on the Sign-in risk blade, the settings are displayed.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/AzureADConditionalAccess_SigninRisk.png)

1. Back on the **Conditions** blade, click **Device platforms**, on the **Device platforms** blade, set **Configure** to **Yes**, on the **Include** tab, click **Select device platforms**, enable the **Windows** checkbox, and click **Done**.

    ![In the Azure portal, on the Device platforms blade, the settings are displayed.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/AzureADConditionalAccess_DevicePlatforms.png)

1. Back on the **Conditions** blade, click **Locations**, on the **Locations** blade, set **Configure** to **Yes**, on the **Include** tab, click **Selected locations**, click **Select**, on the **Select** blade, enable the **Contoso Headquarters** checkbox, click **Select**, and then, on the **Locations** blade, click **Done**.

    ![In the Azure portal, on the Locations blade, the settings are displayed.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/AzureADConditionalAccess_Locations.png)

1. Back on the **Conditions** blade, click **Client apps (Preview)**, on the **Client apps (Preview)** blade, set **Configure** to **Yes**, enable the **Browser**, **Mobile apps and desktop clients**, **Modern authentication clients**, **Exchange ActiveSync clients**, and **Other clients** checkboxes, and click **Done**.

    ![In the Azure portal, on the Client apps (Preview) blade, the settings are displayed.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/AzureADConditionalAccess_Clientapps.png)

1. Back on the **Conditions** blade, click **Device state (Preview)**, on the **Device state (Preview)** blade, set **Configure** to **Yes**, on the **Include** tab, select the **All device state** option and click **Done**.

    ![In the Azure portal, on the Device state (Preview) blade, the settings are displayed.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/AzureADConditionalAccess_Devicestate.png)

1. Back on the **Conditions** blade, click **Done**

1. Back on the **New** blade, in the **Access controls** section, click **Grant**.

1. On the **Grant** blade, ensure that the **Grant access** option is selected, enable the checkbox **Require Hybrid Azure AD joined device**, accept the default choice of **Require all the selected controls** for multiple controls, and click **Select**.

   > **Note**: Review the warning **Don't lock yourself out! Make sure that your device is Hybrid Azure AD Joined**.

    ![In the Azure portal, on the Grant blade, the settings and the warning are displayed.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/AzureADConditionalAccess_AccesscontrolsGrant.png)

1. Back on the **New** blade, in the **Access controls** section, click **Session**. 

1. Review the **Session** blade settings but do not modify them.

1. On the **New** blade, set **Enable policy** to **On** and click **Create**

    ![In the Azure portal, the final settings of the new conditional access policy are displayed.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/AzureADConditionalAccess_Final.png)

1. Back on the **Conditional Access - Policies** blade, click **What If**.

1. On the **What If** blade, specify the following settings and click **What If**:

    - User: **Teresa F. Bell**

    - Cloud apps or actions: **Microsoft Azure Management**

    - IP address: the public IP address assigned the APP1 Azure VM

    - Country: **United States**

    - Device platform: **Windows**

    - Client apps (Preview): **Browser**

    - Device state (Preview): **Device Hybrid AD Joined**

    - Sign-in risk: **No risk**

1. Review the evaluation results and note the policy and the grant controls that will apply.

    ![In the Azure portal, the What If settings and the evaluation results of the new conditional access policy are displayed.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/AzureADConditionalAccess_WhatIf_parameters.png)

1. Re-run the evaluation but first change the **Sign-in risk** to **Low** and review the evaluation results.


### Task 10: Implement Azure AD Privileged Identity Management

In this task, you will implement Azure AD Privileged Identity Management

1. Within the Remote Desktop session to **DC1**, in the Internet Explorer window displaying the Azure portal, navigate to the **All services** blade.

1. In the search text box, type **Privileged Identity Management** and, in the list of results, click **Azure AD Privileged Identity Management**.

1. On the **Privileged Identity Management** blade, click **Consent to PIM**.

1. On the **Privileged Identity Management - Consent to PIM** blade, click **Verify my identity**. 

1. When prompted to provide additional information, click **Next**, on the **Aditional security verification** page, specify the following settings:

    - **Step 1: How should we contact you?**

        - Authentication phone: select your country or region and specify a mobile phone number you intend to use in this lab

        - Method: **Send me a code by text message**

    - **Step 2: We've send a text message to your phone**

        - Use the code in the text message you received, click **Verify**, and following successful verification, click **Done**.

1. Navigate back to the **Privileged Identity Management** blade, click **Consent to PIM**, click **Consent**, when prompted for a confirmation to proceed, click **Yes**, and refresh the Internet Explorer window.

1. In the Azure portal, from the **Privileged Identity Management** blade, click **Azure AD roles**. 

1. On the **Azure AD roles - Quick start** blade, click **Sign up PIM for Azure AD Roles**, click **Sign up**, when prompted for a confirmation, click **Yes**, and refresh the Internet Explorer window.

1. On the **Azure AD roles - Overview** blade, click **Roles**.

1. On the **Azure AD roles - Roles** blade, click **Add member**.

1. On the **Add managed members** blade, specify the following settings to designate **Ann G. Ayers** as an eligible member of the **Authentication Administrator** role:

    - Select a role: **Authentication Administrator**

    - Select members: **Ann G. Ayers**

   > **Note**: **Authentication Administrator** role grants privileges to set or reset non-password credentials and update passwords for all users. Authentication Administrators can require users to re-register against existing non-password credential (for example, MFA or FIDO) and revoke remember MFA on the device, which prompts for MFA on the next sign-in.

1. On the **Azure AD roles - Roles** blade, click **Members** and note that **Ann G. Ayers** is listed as eligible for the **Authentication Administrator** role.

1. Switch to the Remote Desktop session to **APP1**, where you are signed in by using Active Directory user account of **Ann G. Ayers**, start Internet Explorer, and browse to the Azure portal at [**http://portal.azure.com**](http://portal.azure.com). 

1. When prompted to provide additional information, click **Next**, on the **Aditional security verification** page, specify the following settings:

    - **Step 1: How should we contact you?**

        - Authentication phone: select your country or region and specify a mobile phone number you intend to use in this lab

        - Method: **Send me a code by text message**

    - **Step 2: We've send a text message to your phone**

        - Use the code in the text message you received, click **Verify**

    - **Step 3: Keep using your existing application**

        - Note that you have the option of using **app password** and click **Done**.

   > **Note**: 

1. When prompted again to provide additional information, click **Next**, on the **confirm your current password** page, click **re-enter my password**, and, when prompted, provide the password for the Active Directory user account of **Ann G. Ayers**.

1. When prompted, type the code sent to the mobile phone you specified previously and click **Verify**.

   > **Note**: 

1. On the **don't lose access to your account!** page, click **Verify** next to the **Authentication Phone** entry and then click **text me**. Next, type the code send to your mobile phone and click **verify**.

1. On the **don't lose access to your account!** page, click **Set it up now** next to the **Authentication Email is not configured** entry. Next, in the **Authentication Email** text box, type an email address that you want to use for verification and click **email me**.

1. Retrieve the email with the code, type it in the textbox next to the **verify** button, and click **verify**

1. On the **don't lose access to your account!** page, click **Set them up now** next to the **Security Questions are not configured** entry. Next, select each security question, provide the corresponding answer, and click **save answers**.

1. On the **don't lose access to your account!** page, click **finish**. You will be redirected to the Azure portal.

1. In the Azure portal, navigate to the **Privileged Identity Management - Quick start** blade. 

1. On the **Privileged Identity Management - Quick start** blade, click **My roles**.

1. On the **My roles - Azure AD roles** blade, on the **Eligible roles** tab, click **Activate** next to the **Authentication Administrator** role entry. 

1. On the **Authentication Administrator** blade, click **Activate**.

1. On the **Activation** blade, accept the default activation start time and duration (1 hour) type a reason for the activation in the **Activation reason** text box, and click **Activate**.

1. On the **Activation status**, monitor changes to your activation request. Once the activation is completed, click the **Sign out** link and then sign in back to the Azure portal to start using your newly activated role.

1. In the Azure portal, navigate back to the **My roles - Azure AD roles** blade.

1. On the **My roles - Azure AD roles** blade, on the **Active roles** tab, note that the role assignment has been activated. 

### Summary 2

In this exercise, you optimized authentication, authorization, and access protection for Contoso Active Directory environment integrated with the Contoso Azure AD tenant by enabling Azure AD Multi-Factor Authentication, enabling Azure AD password writeback and Self-Service Password Reset, implementing, Azure AD Password Protection, enabling Azure Active Directory Identity Protection, enabling Automatic Intune Enrollment, as well as implementing Azure AD Privileged Identity Management and Azure AD Conditional Access Policies.


## Exercise 3: Configure application access in hybrid scenarios

Duration: 90 minutes

### Overview 3

In this exercise, you will configure access to on-premises Integrated Windows Authentication app (implemented as the default IIS web site) from Internet by installing and configuring Azure AD Application Proxy. You will test access to this application by using a Contoso Azure AD tenant user account as well as by using a Fabrikam Azure AD tenant user account configured as a guest account in the Contoso Azure AD tenant. 


### Task 1: Install and configure Azure AD Application Proxy

In this task, you will install and configure Azure AD Application Proxy

1. Within the Remote Desktop session to **DC1**, in the Internet Explorer window displaying the Azure portal, navigate to the **Contoso - Overview** blade of the Contoso Azure AD tenant.

1. On the **Contoso - Overview** blade of the Contoso Azure AD tenant, click **Application proxy**.

1. On the **Contoso - Application proxy** blade, click the **download a connector** link.

1. On the **Application Proxy Connector Download** blade, review the system requirements and click **Accept terms & Download**.

1. When prompted whether to save or run **AADApplicationProxyConnectorInstaller.exe**, click **Run**.

   > **Note**: In a production environment, you would install the connector on a domain member server. We are using a domain controller strictly for simplicity.

1. Install Microsoft Azure Active Directory Application Proxy Connector with default settings. When prompted to sign in, provide the credentials of the **john.doe** Azure AD user account, which you created in the first exercise of this lab.

1. Refresh the Internet Explorer page displaying the **Contoso - Application proxy** blade and verify that it includes the DC1.contoso.local entry in the **Default** connector group.

1. On the **Contoso - Application proxy** blade, click **Enable application proxy** and, when prompted for confirmation, click **Yes**.


### Task 2: Configure an Azure AD Application Proxy application

In this task, you will configure an Azure AD Application Proxy application.

1. On the **Contoso - Application proxy** blade, click **+ Configure an app**.

1. On the **Add your own on-premises application** blade, specify the following settings and click **+ Add**.

    - Name: **APP1 Default Web Site**

    - Internal Url: **http://app1.contoso.local**

    - External Url: accept the default value

    - Pre Authentication: **Azure Active Directory**

    - Connector Group: **Default**

    - Backend Application Timeout: **Default**

    - Use HTTP-Only Cookie: **No**

    - Use Secure Cookie: **Yes**

    - Use Persistent Cookie: **No**

    - Translate URLs in Headers: **Yes**

    - Translate URLs in Application Body: **No**

1. You will be automatically redirected to the **APP1 Default Web Site - Overview** blade.

1. On the **APP1 Default Web Site - Overview** blade, in the **Getting Started** section, click the **Assign users and groups** link.

1. On the **APP1 Default Web Site - Users and groups** blade, click **+ Add user**.

1. On the **Add Assignment** blade, specify the following settings and click **Assign**:

    - Users and groups: **Engineering**

    - Select Role: **User**

1. On the **APP1 Default Web Site - Users and groups** blade, click **Single sign-on**.

1. On the **APP1 Default Web Site - Single sign-on** blade, click **Windows Integrated Authentication**.

1. Within the Remote Desktop session to **DC1**, start **Command Prompt** and, from the **Command Prompt**, run the following to identify Service Principal Names associated with the APP1 computer account.

    ```
    setspn -L APP1
    ```

1. From the **Command Prompt**, run the following to register http specific Service Principal Names associated with the APP1 computer account.

    ```
    setspn -S http/APP1.contoso.local APP1
    setspn -S http/APP1 APP1
    ```
1. Review the output, switch back to the Internet Explorer window displaying the Azure portal, and, on the **APP1 Default Web Site - Configure Integrated Windows Authentiation (IWA)**, specify the following settings and click **Save**.

    - Internal Application SPN: **HTTP/APP1.contoso.local**

    - Delegated Login Identity: **User principal name**

   > **Note**: The HTTP service class is one of the built-in services that act as an alias to the HOST SPN. For more information, refer to **How to use SPNs when you configure Web applications that are hosted on Internet Information Services** at <https://support.microsoft.com/en-us/help/929650/how-to-use-spns-when-you-configure-web-applications-that-are-hosted-on> and 

1. Within the Remote Desktop session to **DC1**, in the Server Manager console, click **Tools** and then click **Active Directory Users and Computers**. 

1. In the **Active Directory Users and Computers** console, click **View** and, in the **View** menu, enable **Advanced Features**.

1. In the **Active Directory Users and Computers** console, locate the computer account hosting the Azure AD Application Proxy connector (**DC1** in our case) and display its **Properties** window.

1. In the **DC1 Properties** window, switch to the **Delegation** tab and select the option **Trust this computer for delegation to specified services only**.

1. Select the option **Use any authentication protocol**, click **Add**, in the **Add Services** window, click **Users or Computers**, in the **Select Users or Computers** dialog box, in the **Enter the object names to select, type **APP1** and click **OK**. 

1. Back in the **Add Services** window, select the **http** entry and click **OK**. 

    ![In the Active Directory Users and Computers console, the Kerberos Constrained Delegation configuration is displayed.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/AzureADApplicationProxy_Delegation_http.png)

1. Back in the **DC1 Properties** window, click **OK**.


### Task 3: Test an Azure AD Application Proxy application

1. From the lab computer, start a browser in Private mode and browse to <https://myapps.microsoft.com>

1. When prompted to sign in, use the **AGAyers\@<custom_domain_name>** user name with the **demo@pass123** password (where **<custom_domain_name>** placeholder represents the custom DNS domain name you assigned to the Contoso Azure AD tenant in the first exercise of this lab.

1. When prompted to enter code, type the code which was texted to the mobile phone number that you provided in the previous exercise.

1. On the **Apps** page of the **Application Access Panel**, click the **APP1 Default Web Site** icon. This will automatically open a new browser tab displaying the Default Web Site page on APP1.


### Task 4: Create an Azure Active Directory tenant and activate an Enterprise Mobility + Security E5 trial

In this task, you will create another Azure Active Directory tenant representing the Fabrikam organization, with the following settings: 

-   Organization name: **Fabrikam**

-   Initial domain name: any valid, unique domain name

-   Country or region: **United States**

1. From the lab computer, start a new Web browser window and navigate to the Azure portal at <https://portal.azure.com>.

1. When prompted, sign into the Azure subscription into which you deployed resources in the Before Hands-On Lab exercises.

1. On the lab computer, in the Azure portal, click **+ Create a resource**

1. On the **New** blade, in the **Search the Marketplace** text box, type **Azure Active Directory** and, in the list of results, click **Azure Active Directory**.

1. On the **Azure Active Directory** blade, click **Create**.

1. On the **Create directory** blade, specify the following settings and click **Create**:

    -   Organization name: **Fabrikam**

    -   Initial domain name: any valid, unique domain name

    -   Country or region: **United States**

1. In the Azure portal, navigate to the blade of the newly created Azure Active Directory tenant.

1. On the **Contoso - Overview** blade, click **Licenses**.

1. On the **Contoso - Licenses**, blade, click **+ Try/Buy**.

1. On the **Activate** blade, in the **ENTERPRISE MOBILITY + SECURITY E5** section, click **Free trial** and then click **Activate**


### Task 5: Create and configure Azure AD users

In this task, you will configure Azure AD user accounts in the newly created Azure AD tenant with the following settings. This will include assigning EM+S E5 licenses to the user account you are using for this lab as well as creating a new Azure AD user account with the following settings and assigning to it the Global Administrator role as well as the EM+S E5 license.

- Name: **jane.doe**

- First name: **Jane**

- Last name: **Doe**
    
- Password: **Auto-generate password**
    
- Show Password: **Enabled**

- Groups: **0 group selected**
    
- Roles: **Global Administrator**
    
- Block sign in: **No**
    
- Usage location: **United States**
    
- Job title: leave blank
    
- Department: leave blank

1. From the lab computer, in the Azure portal, navigate back to the **Fabrikam - Overview** blade.

1. On the **Fabrikam - Overview** blade, click **Users**.

1. On the **Users - All users** blade, click the entry representing your user account.

1. On the **Profile** blade of your user account, in the **Settings** section, click the **edit** link.

1. In the **Settings** section, in the **Usage location** drop-down list, select the **United States** entry and click **Save**.

1. On the **Profile** blade of your user account, click **Licenses**

1. On the **Licenses** blade, click **+ Assignments**.

1. On the **Update license assignments** blade, enable the **Enterprise Mobility + Security E5** checkbox, ensure that all the corresponding license options are enabled, and click **Save**.

1. On the **Users - All users** blade, click **+ New user**

1. On the **New user** blade, ensure that the **Create user** option is selected, specify the following settings, and click **Create**:

    - User name: **jane.doe\@*your Azure AD tenant domain name*** where ***your Azure AD tenant domain name*** is the domain name you specified when creating the Fabrikam Azure AD tenant in the previous task

    - Name: **jane.doe**

    - First name: **Jane**

    - Last name: **Doe**
    
    - Password: **Auto-generate password**
    
    - Show Password: **Enabled**

    - Groups: **0 group selected**
    
    - Roles: **Global Administrator**
    
    - Block sign in: **No**
    
    - Usage location: **United States**
    
    - Job title: leave blank
    
    - Department: leave blank

    > **Note**: Copy the **User name** and **Password** values into Notepad. You will need them later in this lab.

1. On the **Users - All users** blade, click the entry representing the newly created user account.

1. On the **jane.doe - Profile** blade, click **Licenses**

1. On the **jane.doe - Licenses** blade, click **+ Assignments**.

1. On the **Update license assignments** blade, enable the **Enterprise Mobility + Security E5** checkbox, ensure that all the corresponding license options are enabled, and click **Save**.


### Task 6: Create and configure Azure AD guest user and group accounts

In this task, you will create and configure Azure AD guest accounts in the Contoso Azure AD tenant representing users in the Fabrikam Azure AD tenant.

1. Switch to the Remote Desktop session to **DC1**, in the Internet Explorer window displaying the Azure portal at <https://portal.azure.com> into which you are signed in with the **john.doe** credentials, navigate to the **Contoso - Overview** blade of the Contoso Azure AD tenant.

1. On the **Contoso - Overview** blade, click **Users**.

1. On the **Users - All users** blade, click **+ New guest user**.

1. On the **New user** blade, ensure that the **Invite user** option is selected, specify the following settings, and click **Invite**:

    -  Name: **fabrikam-jane.doe**

    -  User name: the UPN of the jane.doe Fabrikam Azure AD user you created earlier in this exercise

    -  First name: **Jane**

    -  Last name: **Doe**

    -  Personal message : **Welcome to the Contoso Azure AD tenant**

    -  Groups: not set

    -  Roles: **User**

    -  Block sign in: **No**

    -  Usage location: **United States**

    -  Job title : not set

    -  Department : not set

1. In the Azure portal navigate back to the **Contoso - Overview** blade of the Contoso Azure AD tenant and click **Groups**.

1. On the **Groups - All groups** blade, click **+ New group**. 

1. On the **New group** blade, specify the following settings, and click **Create**:

    -  Group type: **Security**

    -  Group name: **Fabrikam B2B users**

    -  Group description: **Fabrikam B2B users**

    -  Membership type: **Assigned**

    -  Owners: not set

    -  Members: **jane.doe**

1. On the **Groups - All groups** blade, click the newly created group and, on the **Fabrikam B2B users** group, copy its **Object id** value. You will need it later in this exercise.

1. Switch to the lab computer, start a web browser using in private/incognito mode and browse to the following URL (where `<contoso_tenant>` represents the custom DNS name of the Contoso Azure AD tenant).

     ```
     https://portal.azure.com/#@<contoso_tenant>.onmicrosoft.com
     ```

1. When prompted, sign in by using the credentials of the **jane.doe** Fabrikam Azure AD user account.

1. When prompted, grant the Contoso Azure AD tenant requested permissions by clicking **Accept**. 

1. When prompted, change the password for the **jane.doe** Fabrikam Azure AD user account. 
  
    > **Note**: If you receive the message **We've seen that password too many times before. Choose something harder to guess**, you'll need to modify the password until it is unique enough to be accepted.

1. In the Azure portal, sign out from the Contoso Azure AD tenant and close the window of the web browser using in private/incognito mode.


### Task 7: Configure an Azure AD Application Proxy application for B2B access

In this task, you will configure an Azure AD Application Proxy application for B2B access

1. Within the Remote Desktop session to **DC1**, in the Internet Explorer window displaying the Azure portal, navigate to the **Contoso - Overview** blade of the Contoso Azure AD tenant.

1. On the **Contoso - Overview** blade of the Contoso Azure AD tenant, click **Enterprise applications**.

1. On the **Enterprise applications - All applications** blade, click **APP1 Default Web Site**.

1. On the **APP1 Default Web Site - Overview** blade, click **Users and groups**.

1. On the **APP1 Default Web Site - Users and groups** blade, click **+ Add user**.

1. On the **Add Assignment** blade, specify the following settings and click **Assign**:

    - Users and groups: **jane.doe**

    - Select Role: **User**

1. Within the Remote Desktop session to **DC1**, in the Azure portal, navigate back to the **Contoso - Overview** blade of the Contoso Azure AD tenant.

1. On the **Contoso - Overview** blade, click **App registrations**.

1. On the **Contoso - App registrations** blade, click **+ New registration**.

1. On the **Register an application** blade, specify the following information and click **Register**:

    - Name: **Sync B2B users**

    - Supported account types: **Accounts in this organizational directory only (Contoso only - Single tenant)**

    - Redirect URI (Optional): **Web** and **https://loopback**

1. You will be automatically redirected to the **Sync B2B users** blade

1. On the **Sync B2B users** blade, click **API permissions**. 

1. On the **Sync B2B users - API permissions** blade, in the **Configured permissions** section, click **+ Add a permission**

1. On the **Request API permission** blade, switch to the **APIs my organization uses** tab, in the search text box, type **Windows Azure Active Directory**, in the list of results, click **Windows Azure Active Directory**, and then click **Application permissions**.

1. On the **Request API permission** blade, in the **Select permissions** section, expand the **Directory** subsection, enable the **Directory.Read.All** checkbox, and click **Add permisssion**.

    ![In the Azure portal, the API permission settings are displayed.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/SyncB2BUsers_RequestAPIpermissions.png)

1. Back on the **Sync B2B users - API permissions** blade, in the **Configured permissions** section, click **Grant admin consent for Contoso**.

1. When prompted, sign in with the credentials of the **john.doe** Contoso Azure AD user account and, on the **Permissions requested Accept for your organization** page, click **Accept**.

1. Review the status of the permissions listed in the **Configured permissions** section on the **Sync B2B users - API permissions** blade and ensure that they it is listed as **Granted for Contoso**.

1. On the **Sync B2B users - API permission** blade, click **Certificates & secrets**.

1. On the **Sync B2B users - Certificates & secrets** blade, click **+ New client secret**.

1. On the **Add a client secret** blade, specify the following information and click **Add**.

    - Description: **Sync B2B users secret 1**

    - Expires: **In 1 year**

1. Copy the resulting secret value. You will need it later in this task.

    > **Note**: This value will not be displayed again and cannot be retrieved once you navigate away from the current page. If you lose it, you will have to delete the secret and create another one.

1. On the **Sync B2B users** blade, click **Overview**.

1. On the **Sync B2B users - Overview** blade, note the values of the **Application (client) ID** and **Directory (tenant) ID**. You will need them later in this task.

1. Within the Remote Desktop session to **DC1**, switch to the **Active Directory Users and Computers** console. 

1. In the **Active Directory Users and Computers** console, expand the **contoso.local** node, create an organizational unit named **Demo B2B Accounts** directly in the root of the domain with two child organizational units named **Enabled** and **Disabled**.

    > **Note**: These OUs must NOT be synchronized back to the Azure AD tenant using Azure AD Connect. Make sure not to include the guest user objects in the synchronization scope.

1. Within the Remote Desktop session to **DC1**, switch to the Windows PowerShell ISE window and, from the console pane, run the following to add a suffix matching the default DNS name of the Contoso Azure AD tenant (replace the `<domain_name>` placeholder with the name of the default domain name associated with the Contoso Azure AD tenant):

    ```pwsh
    Get-ADForest | Set-ADForest -UPNSuffixes @{Add="<domain_name>.onmicrosoft.com"}
    ```

1. Within the Remote Desktop session to **DC1**, start Internet Explorer and browse to <https://www.microsoft.com/en-us/download/details.aspx?id=51495>.

1. From the **Connectors for Microsoft Identity Manager 2016 SP1 and Forefront Identity Manager 2010 R2 SP1** page, download **1.1.953.0\Script and Readme to pull Azure AD B2B users on-prem_v1.0.3.zip** and extract its content.

1. Within the Remote Desktop session to **DC1**, in the Windows PowerShell ISE window, open the newly extracted PowerShell script **AppProxy-GuestAccountCreation-v1.0.3.ps1** and modify its content by replacing the `TODO` placehoders following the instructions provided in the script:

    ```pwsh
    $B2BGroupSid = "TODO" #Fabrikam B2B users Azure AD group's ObjectID that you identified earlier in this exercise.
    $ShadowAccountOU = "OU=Enabled,OU=Demo B2B Accounts,DC=contoso,DC=local" #Organizational Unit for placing shadow accounts
    $ShadowAccountOUArchive = "OU=Disabled,OU=Demo B2B Accounts,DC=contoso,DC=local" #Organizational Unit for moving disabled shadows

    # Requires Azure AD configuration - refer to documentation
    $appID = "TODO" #The value of Client ID parameter of the Sync B2B users application you identified earlier in this exercise
    $appSecret = "TODO" #The value of the secret of the Sync B2B users application you identified earlier in this exercise
    $tenantdomain   = "TODO" #<domain_name>.onmicrosoft.com, where `<domain_name>` designates the name of the default domain name associated with the Contoso Azure AD tenant
    $tenantID = "TODO" #The value of Azure AD tenant ID parameter of the Sync B2B users application you identified earlier in this exercise
    ```
    > **Note**: For more information regarding the script and its implementation, refer to the **Readme - Script to pull Azure AD B2B users on-prem_v1.0.3.pdf** file, included in the **1.1.953.0\Script and Readme to pull Azure AD B2B users on-prem_v1.0.3.zip** file you downloaded earlier in this task.

1. Execute the script and ensure that it did not return any error messages. 

    > **Note**: You can schedule script execution in regular intervals by using Windows Scheduled Tasks. For details, refer to the **Readme - Script to pull Azure AD B2B users on-prem_v1.0.3.pdf** file

1. Switch back to the Azure Active Directory Users and Computers console and verify that a user account of **jane.doe** is listed in the **Demo B2B Accounts\\Enabled** organizational unit.

    > **Note**: In a production environment, you could provide access to Integrated Windows Authentication apps by leveraging Microsoft Identity Manager. You can also provide access to on-premises apps that support SAML-based authentication directly from the Azure portal. For more information, refer to Grant B2B users in Azure AD access to your on-premises applications at <https://docs.microsoft.com/en-us/azure/active-directory/b2b/hybrid-cloud-to-on-premises>.


### Task 8: Test an Azure AD Application Proxy application

1. From the lab computer, start a browser in Private mode and browse to <https://myapps.microsoft.com>

1. When prompted, sign in by using the **jane.doe** Fabrikam Azure AD user account. 

1. Once signed in, click the **Jane Fabrikam** icon in the upper right corner of the Application Access Panel page and, in the drop down menu, click **Contoso**.

1. On the **Apps** page of the **Application Access Panel**, click the **APP1 Default Web Site** icon. This will automatically open a new browser tab displaying the Default Web Site page on APP1.


### Summary 3

In this exercise, you configured access to on-premises Integrated Windows Authentication app (implemented as the default IIS web site) from Internet by installing and configuring Azure AD Application Proxy. You also tested access to this application by using a Contoso Azure AD tenant user account as well as by using a Fabrikam Azure AD tenant user account configured as a guest account in the Contoso Azure AD tenant. 

## Lab summary

In this hands-on lab, you setup and configured a number of different Hybrid Identity scenarios. The scenarios involved an Active Directory single-domain forest named contoso.local, which in this lab environment, consisted (for simplicity reasons) of a single domain controller named DC1 and a single domain member server named APP1. You explored Azure AD-related capabilities that allowed you to integrate Active Directory with Azure Active Directory, optimized hybrid authentication and authorization, and provided secure access to on-premises resources from Internet for both organizational users and users who are members of partner organizations. 

## After the hands-on lab

Duration: 20 Minutes

### Task 1: Delete resources

1.  Now that the HOL is complete, go ahead and delete all of the Resource Groups created for this HOL. You will no longer need those resources, and it will be beneficial to clean up your Azure Subscription.
