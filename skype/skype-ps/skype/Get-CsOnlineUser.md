---
external help file: Microsoft.Rtc.Management.Hosted.dll-help.xml 
online version: https://docs.microsoft.com/powershell/module/skype/get-csonlineuser
applicable: Microsoft Teams, Skype for Business Online
title: Get-CsOnlineUser
schema: 2.0.0
manager: bulenteg
author: tomkau
ms.author: tomkau
ms.reviewer:
---

# Get-CsOnlineUser

## SYNOPSIS
Returns information about users who have accounts homed on Microsoft Teams or Skype for Business Online.

## SYNTAX

```
Get-CsOnlineUser 
[-Filter <String>] 
[-LdapFilter <String>] 
[-OnOfficeCommunicationServer] 
[-OnModernServer]
[-UnassignedUser] 
[-SkipUserPolicies] 
[-OU <OUIdParameter>] 
[-DomainController <Fqdn>]
[-Credential <PSCredential>] 
[[-Identity] <UserIdParameter>] 
[-ResultSize <>] [<CommonParameters>]
```

## DESCRIPTION
The Get-CsOnlineUser cmdlet returns information about users who have accounts homed on Microsoft Teams or Skype for Business Online.
The returned information includes standard Active Directory account information (such as the department the user works in, his or her address and phone number, etc.) as well as Skype for Business Server 2015 specific information: the Get-CsOnlineUser cmdlet returns information about such things as whether or not the user has been enabled for Enterprise Voice and which per-user policies (if any) have been assigned to the user.

Note that the Get-CsOnlineUser cmdlet does not have a TenantId parameter; that means you cannot use a command similar to this in order to limit the returned data to users who have accounts with a specific Microsoft Teams or Skype for Business Online tenant:

`Get-CsOnlineUser -TenantId "bf19b7db-6960-41e5-a139-2aa373474354"`

However, if you have multiple you can return users from a specified tenant by using the Filter parameter and a command similar to this:

`Get-CsOnlineUser -Filter {TenantId -eq "bf19b7db-6960-41e5-a139-2aa373474354"}`

That command will limit the returned data to user accounts belong to the tenant with the TenantId "bf19b7db-6960-41e5-a139-2aa373474354".
If you do not know your tenant IDs you can return that information by using this command:

`Get-CsTenant`

If you have a hybrid or "split domain" deployment (that is, a deployment in which some users have accounts homed on Skype for Business Online while other users have accounts homed on an on-premises version of Skype for Business Server 2015) keep in mind that the Get-CsOnlineUser cmdlet only returns information for Skype for Business Online users.
However, the cmdlet will return information for both online users and on-premises users.
If you want to exclude Skype for Business Online users from the data returned by the Get-CsUser cmdlet, use the following command:

`Get-CsUser -Filter {TenantId -eq "00000000-0000-0000-0000-000000000000"}`

By definition, users homed on the on-premises version will always have a TenantId equal to 00000000-0000-0000-0000-000000000000.
Users homed on Skype for Business Online will a TenantId that is equal to some value other than 00000000-0000-0000-0000-000000000000.

**Note:**

The following updates are applicable for TeamsOnly customers using Microsoft Teams PowerShell version 3.0.0 and above.

*Deprecated Attributes* - Theses are no longer relevant to Teams

- AcpInfo
- AdminDescription
- ArchivingPolicy
- AudioVideoDisabled
- BaseSimpleUrl
- BroadcastMeetingPolicy
- CallViaWorkPolicy
- ClientPolicy
- ClientUpdateOverridePolicy
- ClientVersionPolicy
- CloudMeetingOpsPolicy
- CloudMeetingPolicy
- CloudVideoInteropPolicy
- ContactOptionFlags
- CountryOrRegionDisplayName
- Description
- DistinguishedName
- EnabledForRichPresence
- ExchangeArchivingPolicy
- ExchUserHoldPolicies
- ExperiencePolicy
- ExternalUserCommunicationPolicy
- ExUmEnabled
- Guid
- HomeServer
- HostedVoicemailPolicy
- IPPBXSoftPhoneRoutingEnabled
- IPPhone
- IPPhonePolicy
- IsByPassValidation
- IsValid
- LegalInterceptPolicy
- LicenseRemovalTimestamp
- LineServerURI
- Manager
- MNCReady
- Name
- NonPrimaryResource
- ObjectCategory
- ObjectClass
- ObjectState
- OnPremHideFromAddressLists
- OriginalPreferredDataLocation
- OriginatingServer
- OriginatorSid
- OverridePreferredDataLocation
- PendingDeletion
- PrivateLine
- ProvisioningCounter
- ProvisioningStamp
- PublishingCounter
- PublishingStamp
- Puid
- RemoteCallControlTelephonyEnabled
- RemoteMachine
- SamAccountName
- ServiceInfo
- StsRefreshTokensValidFrom
- SubProvisioningCounter
- SubProvisioningStamp
- SubProvisionLineType
- SyncingCounter
- TargetRegistrarPool
- TargetServerIfMoving
- TeamsInteropPolicy
- ThumbnailPhoto
- UpgradeRetryCounter
- UserAccountControl
- UserProvisionType
- UserRoutingGroupId
- VoicePolicy
- XForestMovePolicy
- AddressBookPolicy
- GraphPolicy
- PinPolicy
- PreferredDataLocationOverwritePolicy
- PresencePolicy
- SmsServicePolicy
- TeamsVoiceRoute
- ThirdPartyVideoSystemPolicy
- UserServicesPolicy
- ConferencingPolicy
- Id
- Identity
- MobilityPolicy
- OnlineDialinConferencingPolicy
- Sid
- TeamsWorkLoadPolicy
- VoiceRoutingPolicy
- ClientUpdatePolicy
- HomePhone
- HostedVoiceMail
- MobilePhone
- OtherTelephone
- StreetAddress
- WebPage
- AssignedLicenses
- OnPremisesUserPrincipalName
- HostedVoiceMail
- LicenseAssignmentStates
- OnPremDomainName
- OnPremSecurityIdentifier
- OnPremSamAccountName
- CallerIdPolicy
- Fax
- LastName
- Office
- Phone
- WindowsEmailAddress*

*Supported filters* - The Filtering functionality has been limited to the following attributes:

- accountEnabled
- ownerUrn
- displayName
- givenName
- lineUri
- userPrincipalName
- ExternalAccessPolicy
- OnlineDialOutPolicy
- OnlineVoiceRoutingPolicy
- TeamsMeetingPolicy
- TeamsMeetingBroadcastPolicy
- TeamsMessagingPolicy
- TeamsCallParkPolicy
- TeamsEmergencyCallingPolicy
- TeamsEmergencyCallRoutingPolicy
- TeamsChannelsPolicy
- TeamsUpdateManagementPolicy
- TeamsCallingPolicy
- TeamsUpgradePolicy
- TeamsUpgradeOverridePolicy
- TeamsAppSetupPolicy
- TeamsAppPermissionPolicy
- TeamsVerticalPackagePolicy
- TeamsSurvivableBranchAppliancePolicy
- TeamsCallHoldPolicy
- TenantDialPlan
- OnlineVoicemailPolicy
- OnlineAudioConferencingRoutingPolicy
- TeamsAudioConferencingPolicy
- TeamsVdiPolicy
- TeamsFeedbackPolicy
- TeamsIPPhonePolicy
- TeamsShiftsAppPolicy
- TeamsShiftsPolicy
- TeamsTargetingPolicy
- TeamsTemplatePermissionPolicy
- TeamsSyntheticAutomatedCallPolicy
- TeamsMobilityPolicy
- TeamsCortanaPolicy
- TeamsMeetingBrandingPolicy
- TeamsNotificationAndFeedsPolicy
- TeamsVideoInteropServicePolicy
- TeamsEducationAssignmentsAppPolicy
- TeamsComplianceRecordingPolicy
- AssignedPlan
- EnterpriseVoiceEnabled
- Identity
- department
- UserDirSyncEnabled
- Title
- CountryAbbreviation
- UsageLocation

*Attributes renamed/replaced:*
- FirstName renamed to GivenName
- DirSyncEnabled renamed to UserDirSyncEnabled
- MCOValidationErrors renamed to UserValidationErrors
- OnPremSIPEnabled renamed to OnPremIsSipEnabled

*New User Attributes*

FeatureTypes – Array of unique strings specifying what features are enabled for a user (plan not displayed).

*Deprecated input parameters*

LdapFilter has been deprecated due to low usage.

*Changes in "-Filter" parameter*
- Assigned Plan filter - Previous format will no longer be supported. Existing filters like `AssignedPlan -eq '<some-xml-string>'` will stop working. This will need to be modified to one of the following formats:
  - AssignedPlans -eq '*MCO' or 'MCO*'or '*MCO*' - for contains checks.
The output format has also changed, the xml object is now a json object.

- EnterpriseVoiceEnabled filter
  - EnterpriseVoiceEnabled -eq true / false


## EXAMPLES

### -------------------------- Example 1 --------------------------
```
Get-CsOnlineUser
```

The command shown in Example 1 returns information for all the users configured as online users.

### -------------------------- Example 2 --------------------------
```
Get-CsOnlineUser -Identity "sip:kenmyer@litwareinc.com"
```

In Example 2 information is returned for a single online user: the user with the SIP address "sip:kenmyer@litwareinc.com".

### -------------------------- Example 3 --------------------------
```
Get-CsOnlineUser -Filter {ArchivingPolicy -eq "RedmondArchiving"}
```

Example 3 uses the Filter parameter to limit the returned data to online users who have been assigned the per-user archiving policy RedmondArchiving.
To do this, the filter value {ArchivingPolicy -eq "RedmondArchiving"} is employed; that syntax limits returned data to users where the ArchivingPolicy property is equal to (-eq) "RedmondArchiving".

### -------------------------- Example 4 --------------------------
```
Get-CsOnlineUser -Filter {HideFromAddressLists -eq $True}
```

Example 4 returns information only for user accounts that have been configured so that the account does not appear in Microsoft Exchange address lists.
(That is, the Active Directory attribute msExchHideFromAddressLists is True.) To carry out this task, the Filter parameter is included along with the filter value {HideFromAddressLists -eq $True}.

### -------------------------- Example 5 --------------------------
```
Get-CsOnlineUser -Filter {TenantId -eq "bf19b7db-6960-41e5-a139-2aa373474354"}
```

The command shown in Example 5 returns information for all the online users assigned to the tenant with the TenantID "bf19b7db-6960-41e5-a139-2aa373474354".
To accomplish the task, the command includes the Filter parameter along with the filter value {TenantId -eq "bf19b7db-6960-41e5-a139-2aa373474354"}.
This filter limits the returned data to online users assigned to the tenant "bf19b7db-6960-41e5-a139-2aa373474354".

### -------------------------- Example 6 --------------------------
```
PS C:\> $MeetingPolicy="Kiosk"
PS C:\> $filterString = 'TeamsMeetingPolicy -eq "{0}"' -f $MeetingPolicy
PS C:\> Get-CsOnlineUser -Filter $filterString
```

The commands shown in Example 6 filters all the online users with a certain TeamsMeetingPolicy assigned using a variable as filter input.
To accomplish the task, the filter string is first constructed and resolved locally and then used by the Get-CsOnlineUser cmdlet.

## PARAMETERS

### -Credential

  *This parameter has been deprecated from Teams PowerShell Modules 3.0 and above as it is no longer relevant to Microsoft Teams*.
 
```yaml
Type: PSCredential
Parameter Sets: (All)
Aliases: 
Applicable: Microsoft Teams, Skype for Business Online

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -DomainController

  *This parameter has been deprecated from Teams PowerShell Module 3.0 and above as it is no longer relevant to Microsoft Teams*.
 
```yaml
Type: Fqdn
Parameter Sets: (All)
Aliases: 
Applicable: Microsoft Teams, Skype for Business Online

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Filter
Enables you to limit the returned data by filtering on specific attributes.
For example, you can limit returned data to users who have been assigned a specific voice policy, or users who have not been assigned a specific voice policy.

The Filter parameter uses the same filtering syntax that is used by the Where-Object cmdlet.
For example, a filter that returns only users who have been enabled for Enterprise Voice would look like this, with EnterpriseVoiceEnabled representing the Active Directory attribute, -eq representing the comparison operator (equal to), and $True (a built-in Windows PowerShell variable) representing the filter value:

`{EnterpriseVoiceEnabled -eq $True}`

```yaml
Type: String
Parameter Sets: (All)
Aliases: 
Applicable: Microsoft Teams, Skype for Business Online

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Identity
Indicates the Identity of the user account to be retrieved.
User Identities can be specified using one of the following formats: 1) the user's SIP address; 2) the user's user principal name (UPN); or, 3) the user's Active Directory display name (for example, Ken Myer).

You can use the asterisk ( * ) wildcard character when using the Display Name as the user Identity.
For example, the Identity "* Smith" returns all the users who have a display name that ends with the string value " Smith". 

Note that in Microsoft Teams PowerShell Version 2.5.1, using this parameter will cause the Get-CsOnlineUser command to no longer emit deprecated properties as part of the modernization effort.

```yaml
Type: UserIdParameter
Parameter Sets: (All)
Aliases: 
Applicable: Microsoft Teams, Skype for Business Online

Required: False
Position: 1
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -LdapFilter
 
  *This parameter has been deprecated from Teams PowerShell Modules 3.0 and above as it is no longer relevant to Microsoft Teams*.
 
Enables you to limit the returned data by filtering on generic Active Directory attributes (that is, attributes that are not specific to Microsoft Teams or Skype for Business).
For example, you can limit returned data to users who work in a specific department, or users who have a specified manager or job title.

The LdapFilter parameter uses the LDAP query language when creating filters.
For example, a filter that returns only users who work in the city of Redmond would look like this: "l=Redmond", with "l" (a lowercase L) representing the Active Directory attribute (locality); "=" representing the comparison operator (equal to); and "Redmond" representing the filter value.

```yaml
Type: String
Parameter Sets: (All)
Aliases: 
Applicable: Microsoft Teams, Skype for Business Online

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -OnModernServer
 
 *This parameter has been deprecated from Teams PowerShell Modules 3.0 and above due to limited usage*.

When present, the cmdlet returns a collection of users homed on Microsoft Teams or Skype for Business.
Users with accounts on previous versions of the software will not be returned when you use this parameter.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases: OnLyncServer
Applicable: Microsoft Teams, Skype for Business Online

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -OnOfficeCommunicationServer
 
 *This parameter has been deprecated from Teams PowerShell Modules 3.0 and above as it is no longer relevant to Microsoft Teams*.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases: 
Applicable: Microsoft Teams, Skype for Business Online

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -OU
 
 *This parameter has been deprecated from Teams PowerShell Modules 3.0 and above as it is no longer relevant to Microsoft Teams*.


```yaml
Type: OUIdParameter
Parameter Sets: (All)
Aliases: 
Applicable: Microsoft Teams, Skype for Business Online

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -ResultSize
Enables you to limit the number of records returned by the cmdlet.
For example, to return seven users (regardless of the number of users that are in your forest) include the ResultSize parameter and set the parameter value to 7.
Note that there is no way to guarantee which seven users will be returned.

The result size can be set to any whole number between 0 and 2147483647, inclusive.
If set to 0 the command will run, but no data will be returned.
If you set the ResultSize to 7 but you have only three users in your forest, the command will return those three users, and then complete without error.

```yaml
Type: Int32
Parameter Sets: (All)
Aliases: 
Applicable: Microsoft Teams, Skype for Business Online

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -SkipUserPolicies
 
PARAMVALUE: SwitchParameter

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases: 
Applicable: Microsoft Teams, Skype for Business Online

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -UnassignedUser
 
 *This parameter has been deprecated from Teams PowerShell Modules 3.0 and above due to limited usage*.

Enables you to return a collection of all the users who have been enabled for Skype for Business but are not currently assigned to a Registrar pool.
Users are not allowed to log on to unless they are assigned to a Registrar pool.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases: 
Applicable: Microsoft Teams, Skype for Business Online

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### CommonParameters
 
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable. For more information, see about_CommonParameters (https://go.microsoft.com/fwlink/?LinkID=113216).


## INPUTS

### Microsoft.Rtc.Management.ADConnect.Schema.OCSADUser or String
A String must represent a valid user account Identity (for example, "sip:kenmyer@litwareinc.com").


## OUTPUTS

### Microsoft.Rtc.Management.ADConnect.Schema.ADOCOnlineUser


## NOTES


## RELATED LINKS

[Set-CsUser](Set-CsUser.md)

