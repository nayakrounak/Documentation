# Pre-Registration Configuration

## Configurations in Pre-Registration Properties files

**File Name**: [pre-registration-mz.properties](https://github.com/mosip/mosip-config/blob/master/sandbox/pre-registration-mz.properties)

## Templates used by Pre-Registration

### Email Acknowledgment

This template is used in email notification sent to the applicants when they completes their pre-registration appointment booking. This email is sent to the applicant's email id which is collected as part of pre-registration data collection.

**Template type code**: Email-Acknowledgement

**Sample template**:

```text
Dear $name,

Your Pre-Registration for UIN is Completed Successfully on $Date at $Time. Your ID is #$PRID.
Appointment is scheduled for $Appointmentdate at $Appointmenttime.
you will also receive the details on your registered Mobile Number
```

**Attributes**:

* $name - Name of the applicant 
* $date - Date when pre-registration was done
* $time - Time when pre-registration was done
* $PRID - Pre-registration ID of the applicant
* $Appointmentdate - Appointment date
* $Appointmenttime - Appointment time

### SMS Acknowledgement

This template is used in sms notification sent to the applicants when they completes their pre-registration appointment booking. This sms is sent to the applicant's mobile number which is collected as part of pre-registration data collection.

**Template type code**: SMS-Acknowledgement

**Sample template**:

```text
Your Pre-Registration for UIN is Completed Successfully on $Date at $Time. 
Your ID is #$PRID.
Appointment is scheduled for $Appointmentdate at $Appointmenttime.
You will also receive the details on your registered email address.
```

**Attributes**:

* $date - Date when pre-registration was done
* $time - Time when pre-registration was done
* $PRID - Pre-registration ID of the applicant
* $Appointmentdate - Appointment date
* $Appointmenttime - Appointment time

### Subject for Email Acknowledgement

This template is used to set the subject of the email notification sent to the resident.

**Template type code**: Acknowledgement-email-subject

**Sample template**:

```text
Pre-Registration $PRID: Acknowledgement
```

**Attributes**:

* $PRID - Pre-registration ID of the applicant

### Consent

This is a template for taking consent of the applicant before he/she provides his/her demographic details.

**Template Type Code**:

**Sample Template**: consent

```text
I understand that the data collected about me during pre-registration by the said authority includes my -  
  • Name
  • Date of birth
  • Gender
  • Address
  • Contact details
  • Documents
I also understand that this information will be stored and processed for the purpose of verifying my identity in order to access various services, or to comply with a legal obligation. I give my consent for the collection of this data for this purpose.
```

**Attributes**: This template doesn't support any attributes.

### Cancel Appointment

This template is used in the SMS or Email notification sent to resident when their appointment is cancelled.

**Template type code**:

**Sample template**:

```text
Dear $name,

Your appointment for pre-registration id, $PRID and appointment date and time, $Appointmentdate $Appointmenttime has been canceled due to a government emergency/holiday. Please re-book another slot for Registration.

Thanks
```

**Attributes**:

* $name - Name of the applicant
* $PRID - Pre-registration ID of the applicant
* $Appointmentdate - Appointment date of the applicant
* $Appointmenttime - Appointment time of the applicant

### Onscreen Acknowledgement

**Template type code**: Onscreen-Acknowledgement

**Sample template**:

```text
1. Guideline 1
2. Guideline 2
3. Guideline 3
4. Guideline 4
5. Guideline 5
6. Guideline 6
7. Guideline 7
8. Guideline 8
9. Guideline 9
10. Guideline 10
```

**Attributes**: This template doesn't support any attributes.

## Pre-Registration UI Specification

**File Name**: [pre-registration-demographic.json](pre-registration-configuration.md)

For details about the pre-registration UI specification, please go throught [this](ui-specification-for-pre-registration.md) page.

## Pre-Registration Mapping JSON

This is a mapping file for the Pre-registration ID object. The fields name, proofOfAddress, and postalCode are the only attributes which are used internally in Pre-registration.

* name - Name of the applicant. It is used in notification templates & in Pre-registration dashboard screen.
* proofOfAddress - Document containing Proof of Address. It is used in document upload screen to fetch the address document from another applicant.
* postalCode - Postal Code in the Address. To fetch the list of center for the postal code provided by the individual while providing the demographic details.

**File Name**: [pre-registration-identity-mapping.json](pre-registration-configuration.md)

```javascript
{
    "identity": {
        "name": {
            "value": "fullName",
            "isMandatory" : true
        },
        "proofOfAddress": {
            "value" : "proofOfAddress"
        },
        "postalCode": {
            "value" : "postalCode"
        }
    }
}
```

