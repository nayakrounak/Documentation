# Master Data Services Functionality

## Master Data Management

### Location Hierarchy

#### Create Location Hierarchy

Upon receiving a request to add Location hierarchy \(e.g., Country - Region - Province - City- LAA\) with the input parameters \(code, name, hierarchy\_level, hierarchy\_level\_name, parent\_loc\_code ,lang\_code and is\_active\), the system stores the Location hierarchy in the Database

While storing the location hierarchy in the database, the system performs the following steps: 1. Validates if all required input parameters have been received as listed below for each specific request

* code - character \(36\) - Mandatory
* name - character \(128\) - Mandatory
* hierarchy\_level - smallint - Mandatory
* hierarchy\_level\_name - character \(64\) - Mandatory
* parent\_loc\_code - character \(32\) - Optional
* lang\_code - character \(3\) - Mandatory
* is\_active - boolean - Mandatory
  1. Validate if the Location name received does not already exist in the hierarchy for which the location is getting created
* If Location name already exist under the hierarchy level, throw an appropriate error
  1. The API should not allow creation of the Location if the data is not received in default language
  2. If the data for the Location is not received in all the configured languages, the API should allow the Location to be created given the Point 3 is satisfied.
  3. The API should activate the Location while creation provided the data for all the configured languages is received during the initial creation
* If the data for all the configured languages is not received, deactivate the Location while creation
  1. While storing the location, 
* cr\_by should be the Username of the user who is accessing this API
* cr\_dtimes should be the date-time at which the user is creating the Location 
  1. Responds with the Location Hierarchy created successfully
  2. The component restricts the bulk creation of Master Data through API. However it could be done through a script as need be depending on the requirement of the country.
  3. In case of exceptions, system triggers error messages as received from the Database

#### Update a Location

On receiving a request to update a Location with the input parameters \(code, name, hierarchy\_level, hierarchy\_level\_name, parent\_loc\_code, lang\_code and is\_active\), the system updates the Location in the Location Database for the code received.

The system performs the following steps to update the location in the Master Database:

1. Validates if all required input parameters have been received as listed below for each specific request
   * code character \(36\) - Mandatory
   * name character \(128\) - Mandatory
   * hierarchy\_level smallint - Mandatory
   * hierarchy\_level\_name character \(64\) - Mandatory
   * parent\_loc\_code character \(32\) - Mandatory
   * lang\_code character \(3\) - Mandatory
   * is\_active boolean - Mandatory
2. Validate if the Location name received does not already exist in the hierarchy of the Location
   * If Location name already exist under the hierarchy level, throw an appropriate error
3. The API should not allow activation of Location if the data for the Location is not present in all the languages which are configured for a country
4. For the code received in the request, replaces all the data received in the request against the data existing in the Location database against the same code.
5. While receiving the request for activation, If the Location is already Active, the API should throw an error message. Refer messages section.
6. While receiving the request for deactivation, If the Location is already Inactive, the API should throw an error message. Refer messages section
7. If for a Location data, is\_active flag is being sent as “False” and there are active child Locations \(also the subsequent child locations\) being mapped to received location, do not deactivate the location. Respond with appropriate message. Refer messages section
8. Deleted record are not be updated
9. upd\_by should be the Username of the user who is accessing this API
10. upd\_dtimes should be the date-time when the Location is being updated
11. Responds with data not found error if deleted record is received in the request
12. Responds with appropriate message if the Location is updated successfully
13. In case of Exceptions, system triggers relevant error messages

#### Verify Location

Upon receiving a request to validate the Location Name with input parameters \(Location Name\), the system checks the Location Name in the Master Database

While checking the location in the Database, the system performs the following steps:

1. Validates if the request contains the following input parameters
   * Location Name - Mandatory
2. If the mandatory input parameters are missing, throw the appropriate message
3. In case of Exceptions, system triggers relevant error messages

**Fetch Location Hierarchy Levels based on a Language Code**

Upon receiving a request to fetch the Location Hierarchy Levels with input parameters \(Language Code\), the system fetches the Location Hierarchy Levels in the requested language. The following steps are performed by the system:

1. Validates if the request contains following input parameters \(Language Code\)
   * Language Code - Mandatory
2. Validates if the response contains the Location Hierarchy Levels with the following attributes
   * Hierarchy Level
   * Hierarchy Name
   * IsActive
3. In case of Exceptions, system triggers relevant error messages

**Fetch the Location Hierarchy Data based on a Location Code and a Language Code**

Upon receiving a request to fetch all the Location Hierarchy Data with input parameters \(Location Code and Language Code\), the system fetches the Location Hierarchy Data based on requested Location code and language code. The following steps are performed by the system:

1. Validates if the request contains the following input parameters
   * Location Code - Mandatory
   * Language Code - Mandatory
2. If the mandatory input parameters are missing, throw the appropriate message. 
3. Validates if the response contains the following location hierarchy data and the corresponding attributes against the Location Code and Language Code received in the input parameter **\(i\) List of Countries against the Location Code**

   * Country Code
   * Country Name
   * IsActive

   **\(ii\) List of Regions against the Location Code**

   * Region Code
   * Region Name
   * IsActive

   **\(iii\) List of Provinces against the Location Code**

   * Province Code
   * Province Name
   * IsActive

   **\(iv\) List of Cities against the Location Code**

   * City Code
   * City Name
   * IsActive

   **\(v\) List of Local Administrative authorities against the Location Code**

   * Local Administrative Authority Code
   * Local Administrative Authority Name
   * IsActive

   **\(vi\) List of Pincodes against the Location Code**

   * Pincode
   * IsActive

4. Responds to the source with all the Location Hierarchy Data based on the Location Code
5. In case of Exceptions, system triggers relevant error messages. 

**Fetch the Location Hierarchy Data for the bottom next hierarchy based on a Location Code and a Language Code**

Upon receiving a request to fetch all the Location Hierarchy Data with input parameters \(Location Code and Language Code\), the system fetches the Location Hierarchy Data for the next hierarchy level. The following steps are performed by the system:

1. Validates if the request contains the following input parameters
   * Location Code - Mandatory
   * Language Code - Mandatory
2. If the mandatory input parameters are missing, throws the appropriate message. 
3. Fetches the Location data of only the child hierarchy of location code received \(For e.g., if the location code for a particular Province is received, responds with the data of all the Cities existing in that Province, similarly if location code of a City is received, responds all the data regarding the Local Administrative Authorities existing under that City\)
4. Responds to the source with the data fetched
5. In case of Exceptions, system should trigger an error message. 

**Delete a Location**

On receiving a request to delete a Location with the input parameters \(code\), the system updates the is\_deleted flag to true in the Location Database against the code received.

The system performs the following steps in order to delete the loaction received in the code:

1. Validates if all required input parameters have been received as listed below for each specific request
2. Delete all records for the code received
3. Deleted record are not be deleted again
4. Responds with data not found error if deleted record is received in the request
5. Responds with dependency found error if a record to be deleted is used as foreign key in the dependent table
6. Responds with the Code for the Location Hierarchy deleted successfully
   * code - character \(36\) - Mandatory
7. In case of Exceptions, system triggers relevant error messages. 

### List of Holidays

#### Create Holiday

Upon receiving a request to add Holiday Data with the input parameters \(location\_code, holiday\_date, holiday\_name, holiday\_desc, lang\_code and is\_active\), the system stores the Holiday in the Database. The following steps are performed by the system:

1. This API should only be accessible to Global Admin
2. The API should accept only the below parameters
   * location\_code - Character - 128 - Mandatory
   * holiday\_date - Date Format \(yyyy-mm-dd\) - Mandatory
   * holiday\_name - Character - 64 - Mandatory
   * holiday\_desc - Character - 128 - Optional
   * lang\_code - Character - 3 - Mandatory
   * is\_active - boolean \(true/false\) - Mandatory
3. All the mandatory input parameter\(s\) should be present in the reqeust. If not, throw an appropriate error message
4. The API should validate the data type and length for each attribute as mentioned above.
5. In case of any failed validation, API should respond with appropriate error message.
6. 'location\_code' received should be from list of 'codes' from 'location' masterdata table
   * If not, the API should throw an error.
7. If all the above validations are successfull, the API should update the data in the database agianst the id received
8. API should perfrom below multi-language validations on the Holiday data recieved
9. If in the database, all the mandatory data is present in primary langauge but not in the secondary langauge, API should update the data but mark the Holiday as Inactive \(is\_acitve = false\) regardless of what is received in the request for is\_active flag
10. API should store upd\_by as the Username of the user who is accessing this API
11. API should store upd\_dtimes as the date-time at which the user is modiying the Holiday details
12. API should only allow creation of one record at a time and should restrict bulk creation
13. API should audit the relevant data when the API is called successfully or when an error is encountered

#### Update Holiday

1. This API should only be accessible to Global Admin
2. The API should accept only the below parameter
   * id - Character - 36 - Mandatory
   * location\_code - Character - 128 - Mandatory
   * holiday\_date - Date Format \(yyyy-mm-dd\) - Mandatory
   * holiday\_name - Character - 64 - Mandatory
   * holiday\_desc - Character - 128 - Optional
   * lang\_code - Character - 3 - Mandatory
   * is\_active - boolean \(true/false\) - Mandatory
3. All the mandatory input parameter\(s\) should be present in the reqeust. If not, throw an appropriate error message
4. The API should validate the data type and length for each attribute as mentioned above.
5. In case of any failed validation, API should respond with appropriate error message.
   * 'location\_code' received should be from list of 'codes' from 'location' masterdata table
6. If not, the API should throw an error.
7. If all the above validations are successfull, the API should update the data in the database agianst the id received
8. API should perfrom below multi-language validations on the Template data recieved
9. If in the database, all the mandatory data is present in primary langauge but not in the secondary langauge, API should update the data but mark the Template as Inactive \(is\_acitve = false\) regardless of what is received in the request for is\_active flag
10. API should store upd\_by as the Username of the user who is accessing this API
11. API should store upd\_dtimes as the date-time at which the user is modiying the Template  details
12. API should only allow creation of one record at a time and should restrict bulk creation
13. API should audit the relevant data when the API is called successfully or when an error is encountered

#### Fetch List of Holidays based on a Registration Center ID, a Year and a Language Code

On receiving a request to fetch the list of Holidays with the input parameters \(Registration Center ID, Year and Language Code\), the system fetches the list of Holidays mapped to a Registration Center and for the year and Language Code received in input parameter as per the below steps:

1. Validates if the received request contains the following input parameters
   * Registration Center ID - Mandatory
   * Year - Mandatory
   * Language Code - Mandatory
2. If the mandatory input parameters are missing, throws the appropriate message
3. Validates if the response contains the List of Holidays against the Registration Center ID and the year received and contains the following attributes for a Region
   * Holiday ID
   * Holiday Date
   * Holiday Name
   * IsActive
4. Responds to the source with the List of Holidays
5. In case of Exceptions, system triggers relevant error messages

### Biometric Authentication Type

#### Create Biometric Authentication Type

On receiving a request to add Biometric Authentication Type \(e.g., Fingerprint, Iris\) with the input parameters \(code, name, descr, lang\_code and is\_active\), the system stores the Biometric Authentication Type in the Database as per the below steps:

1. Validates if all required input parameters have been received as listed below for each specific request
   * code - character \(36\) - Mandatory
   * name - character \(64\) - Mandatory
   * descr - character \(256\) - Optional
   * lang\_code - character \(3\) - Mandatory
   * is\_active - boolean - Mandatory
2. Responds with the Biometric Authentication Type Code and Language Code for the Biometric Authentication Type created successfully
3. The component restricts the bulk creation of Master Data
4. In case of Exceptions, system triggers error messages as received from the Database.

#### Fetch the List of Biometric Authentication Type based on a Language Code

On receiving a request to fetch the List of Biometric Authentication Type with input parameters \(Language Code\), the system fetches the List of Biometric Authentication Type against the Language Code as per the below steps:

1. Validates if the request to add Biometric Authentication Type contains the following parameters
   * Language Code - Mandatory
2. If the mandatory input parameters are missing, responds with all the data.
3. Validates if the response contains the List of Biometric Authentication Type against the Language Code along with the IsActive Flag for each Biometric Authentication Type
4. Responds to the source with List of Biometric Authentication Type
5. In case of Exceptions, system triggers relevant error messages

### Biometric Attribute Type

#### Create Biometric Attribute

On receiving a request to add Biometric Attribute \(e.g., Right Thumb, Left Thumb\) with the input parameters \(code, name, descr, bmtyp\_code, lang\_code and is\_active\), the system stores the Biometric Attribute in the Database as per the below steps:

1. Validates if all required input parameters have been received as listed below for each specific request
   * code - character \(36\) - Mandatory
   * name - character \(64\) - Mandatory
   * descr - character \(128\) - Optional
   * bmtyp\_code - character \(36\) - Mandatory
   * lang\_code - character \(3\) - Mandatory
   * is\_active - boolean - Mandatory
2. Responds with the Biometric Attribute Code and Language Code for the Biometric Attribute created successfully
3. The component restricts the bulk creation of Master Data
4. Responds to the source with the appropriate message.
5. In case of Exceptions, system triggers error messages as received from the Database

#### Fetch the List of Biometric Attributes based on the Biometric Authentication Type and a Language Code

On receiving a request to fetch the List of Biometric Attributes with input parameters \(Biometric Authentication Type and Language Code\), the system fetches the List of Biometric Attributes against the Biometric Authentication Type and the Language Code Received as per the below steps:

1. Validates if the request contains the following input parameters
   * Biometric Authentication Type - Mandatory
   * Language Code - Mandatory
2. If no data is present in the Database for the input parameter received, responds with an appropriate message.
3. If both the input parameter is missing, responds with all the data.
4. If one of the input parameters is missing, throw the appropriate message. Refer "Messages" section.
5. Validates if the response contains the List of Biometric Attributes with all the attributes against Biometric Authentication Type and Language Code Received
   * Biometric Attribute Code - Mandatory
   * Biometric Attribute Name - Mandatory
   * Biometric Attribute Description - Optional
   * IsActive – Mandatory
6. Responds to the source with the Fetched Data
7. In case of Exceptions, system triggers relevant error messages

### Gender

#### Create Gender Types

1. This API should only be accessible to Global Admin
2. The API should accept only the below parameters
   * name - Character - 64 - Mandatory
   * lang\_code - Character - 3 - Mandatory
   * is\_active - boolean \(true/false\) - Mandatory
3. All the mandatory input parameter\(s\) should be present in the reqeust. If not, throw an appropriate error message
4. The API should validate the data type and length for each attribute as mentioned above.
5. In case of any failed validation, API should respond with appropriate error message. Refer messages section
6. API should perfrom below multi-language validations on the Gender Type data recieved
7. If, the data is recieved in secondary language and the data for primary language is not present in the database, the API should not allow creation of the Gender Type and throw an error message. Refer messages section
8. If in the request, all the mandatory data is received in primary langauge but not in the secondary langauge, API should store the data but mark the Gender Type as Inactive \(is\_acitve = false\) regardless of what is received in the request for is\_active flag
9. If all the above validations are successfull, the API should store the data the the database

   Gender Type Code should be generated at the back-end for any Gender Type added using a UUID generator

10. API should store cr\_by as the Username of the user who is accessing this API
11. API should store cr\_dtimes as the date-time at which the user is creating the Gender Type
12. API should only allow creation of one record at a time and should restrict bulk creation
13. API should audit the relevant data when the API is called successfully or when an error is encountered

#### Update a Gender Type

On receiving a request to update a Gender Type with the input parameters \(code, name, lang\_code and is\_active\), the system updates the Gender Type in the Gender Type Database for the code received as per the below steps:

1. This API should only be accessible to Global Admin
2. The API should accept only the below parameters
   * code - Character - 36 - Mandatory
   * name - Character - 64 - Mandatory
   * lang\_code - Character - 3 - Mandatory
   * is\_active - boolean \(true/false\) - Mandatory
3. All the mandatory input parameter\(s\) should be present in the reqeust. If not, throw an appropriate error message
4. The API should validate the data type and length for each attribute as mentioned above.
5. In case of any failed validation, API should respond with appropriate error message. Refer messages section
6. If all the above validations are successfull, the API should update the data in the database agianst the code received
7. API should perfrom below multi-language validations on the Gender Type data recieved
8. If in the database, all the mandatory data is present in primary langauge but not in the secondary langauge, API should update the data but mark the Gender Type as Inactive \(is\_acitve = false\) regardless of what is received in the request for is\_active flag
9. API should store upd\_by as the Username of the user who is accessing this API
10. API should store upd\_dtimes as the date-time at which the user is modiying the Gender Type details
11. API should only allow creation of one record at a time and should restrict bulk creation
12. API should audit the relevant data when the API is called successfully or when an error is encountered

#### Check the existence of a Gender in Master Database

On receiving a request to validate the Gender Name with input parameters \(Gender Name\), the system checks the Gender Name in the Master Database as per the below listed steps:

1. Validates if the request contains the following input parameters
   * Gender Name - Mandatory
2. If the mandatory input parameters are missing, throws the appropriate message. 
3. Responds to the source with the appropriate message
4. In case of Exceptions, system triggers relevant error messages

#### Fetch the List of Gender Types based on a Language Code

On receiving a request to fetch the List of Gender Types with the input parameters \(Language Code\), the system fetches the List of Gender Types against the Language Code received as per the below listed steps:

1. Validates if the request contains the following input parameters
   * Language Code - Mandatory
2. If the Language code is missing, responds with all the data.
3. Validates if the response contains the List of Gender Types with the following attributes
   * Gender Code
   * Gender Name
   * isActive
4. Responds to the source with the List of Gender Types
5. In case of Exceptions, system triggers relevant error messages

### Document Category

#### Create Document Category in Master Database

On receiving a request to add Document Category with the input parameters \(code, name, descr, lang\_code and is\_active\), the system stores the Document Category in the Database as per the below listed steps:

1. This API should only be accessible to Global Admin
2. The API should accept only the below parameters
   * name - Character - 64 - Mandatory
   * descr - Character - 128 - Optional
   * lang\_code - Character - 3 - Mandatory
   * is\_active - boolean \(true/false\) - Mandatory
3. All the mandatory input parameter\(s\) should be present in the reqeust. If not, throw an appropriate error message
4. The API should validate the data type and length for each attribute as mentioned above.
5. In case of any failed validation, API should respond with appropriate error message.
6. API should perfrom below multi-language validations on the Document Category data recieved
7. If, the data is recieved in secondary language and the data for primary language is not present in the database, the 

   API should not allow creation of the Document Category and throw an error message.

8. If in the request, all the mandatory data is received in primary langauge but not in the secondary langauge, API should store the data but mark the Document Category as Inactive \(is\_acitve = false\) regardless of what is received in the request for is\_active flag
9. If all the above validations are successfull, the API should store the data the the database
10. Document Category Code should be generated at the back-end for any Document Category added using a UUID generator
11. API should store cr\_by as the Username of the user who is accessing this API
12. API should store cr\_dtimes as the date-time at which the user is creating the Document Category 
13. API should only allow creation of one record at a time and should restrict bulk creation
14. API should audit the relevant data when the API is called successfully or when an error is encountered

#### Update a Document Category in the Document Category Master Database

On receiving a request to update a Document Category with the input parameters \(code, name, descr, lang\_code and is\_active\), the system update the Document Category in the Document Category Database for the Code received as per the below listed steps:

1. The API should only be accessible to Global Admin
2. The API should accept only the below parameters
   * code - Character - 36 - Mandatory
   * name - Character - 64 - Mandatory
   * descr - Character - 128 - Optional
   * lang\_code - Character - 3 - Mandatory
   * is\_active - boolean \(true/false\) - Mandatory
3. All the mandatory input parameter\(s\) should be present in the reqeust. If not, throw an appropriate error message
4. The API should validate the data type and length for each attribute as mentioned above.
5. In case of any failed validation, API should respond with appropriate error message.
6. If all the above validations are successfull, the API should update the data in the database agianst the code received
7. API should perfrom below multi-language validations on the Document Category data recieved
8. If in the database, all the mandatory data is present in primary langauge but not in the secondary langauge, API should update the data but mark the Document Category as Inactive \(is\_acitve = false\) regardless of what is received in the request for is\_active flag
9. API should store upd\_by as the Username of the user who is accessing this API
10. API should store upd\_dtimes as the date-time at which the user is modiying the Document Category details
11. API should only allow creation of one record at a time and should restrict bulk creation
12. API should audit the relevant data when the API is called successfully or when an error is encountered

#### Fetch list of Document Categories based on a Language Code

On receiving a request to fetch Document Category Details with the input parameters \(Language Code\), the system fetches all the Document Categories for the Language Code Received as per the below listed steps:

1. Validates if all required input parameters have been received as listed below for each specific request
   * Language Code - Mandatory
2. If the mandatory input parameters are missing, responds with all the data.
3. Validates if the response contains the following attributes for the Document Category Code
   * Document Category Code - Mandatory
   * Document Category Name - Mandatory
   * Document Category Description - Optional
   * IsActive - Mandatory
4. In case of Exceptions, system triggers relevant error messages

### Document Type

#### Create Document Type

On receiving a request to add Document Type with the input parameters \(code, name, descr, lang\_code and is\_active\), the system stores the Document Type in the Database

Refer below for the process:

1. Validates if all required input parameters have been received as listed below for each specific request
   * code - character \(36\) - Mandatory
   * name - character \(64\) - Mandatory
   * descr - character \(128\) - Optional
   * lang\_code - character \(3\) - Mandatory
   * is\_active - boolean - Mandatory
2. The API should not allow creation of the Document Type if the data is not received in default language
3. If the data for the Document Type is not received in all the configured languages, the API should allow the Document Type to be created given the Point 2 is satisfied.
4. The API should activate the Document Type while creation provided data for all the configured languages is received during the initial creation
5. cr\_by should be the Username of the user who is accessing this API
6. cr\_dtimes should be the date-time when the user is creating the Document Type
7. If the data for all the configured languages is not received, deactivate the Document Type while creation
8. Responds with an appropriate message for the Document Type created successfully
9. In case of Exceptions, system triggers relevant error messages

#### Update a Document Type

On receiving a request to update a Document Type with the input parameters \(code, name, descr, lang\_code and is\_active\), the system updates the Document Type in the Document Type Database for the Code received

Refer below for the process:

1. Validates if all required input parameters have been received as listed below for each specific request
   * code - character \(36\) - Mandatory
   * name - character \(64\) - Mandatory
   * descr - character \(128\) - Optional
   * lang\_code - character \(3\) - Mandatory
   * is\_active - boolean - Mandatory
2. For the code received in the request, replaces all the data received in the request against the data existing in the Document Type database against the same code
3. upd\_by should be the Username of the user who is accessing this API

   upd\_dtimes should be the date-time when the user updates the Document Type Details

4. The API should not allow activation of Document Type if the data for the Document Type is not present in all the languages which are configured for a country
5. While receiving the request for activation, If the Document Type is already Active, the API should throw an error message. Refer messages section.
6. While receiving the request for deactivation, If the Document Type is already Inactive, the API should throw an error message. Refer messages section.
7. Deleted record are not be updated
8. Responds with data not found error if deleted record is received in the request
9. Responds with the appropriate message for the Document Category updated successfully
10. In case of Exceptions, system triggers relevant error messages

#### Delete a Document Type

On receiving a request to delete a Document Type with the input parameters \(code\), the system updates the is\_deleted flag to true in the Document Type Database against the code received

Refer below for the process:

1. Validates if all required input parameters have been received as listed below for each specific request
   * code - character \(36\) - Mandatory
2. Delete all records for the code received
3. Deleted record are not be deleted again
4. Responds with data not found error if deleted record is received in the request
5. Responds with dependency found error if a record to be deleted is used as foreign key in the dependent table
6. Responds with the Document Category Code for the Document Category deleted successfully
7. In case of Exceptions, system triggers relevant error messages

### Applicant Type - Document Category - Document Type Mapping

#### Fetch list of Document Categories based on Applicant Type from Master Database

Upon receiving a request to fetch List of Document Categories with the input parameters \(Applicant Type Code\), the system fetches all the Document Categories for the Applicant Type Code Received

While fetching the list of documents, the system performs the following steps:

1. Validates if all required input parameters have been received as listed below for each specific request
   * Applicant Type Code - Mandatory
2. If the mandatory input parameter is missing, responds with the appropriate error message
3. Validates if the response contains the following attributes for each Document Category Code
   * Document Category Code
   * Name
   * Description
   * Language Code
   * Is Active
4. In case of Exceptions, system triggers relevant error messages

#### Fetch List of Document Category-Document Type mappings based on Applicant Type and a List of Language Codes

Upon receiving a request to fetch List of Document Category-Document Type mappings with input parameters \(Applicant Type and List of Language Codes\), the system fetches the required data

While fetching the data, the system performs the following steps:

1. Validates if the request contains the following input parameters
   * Applicant Type - Mandatory
   * List of Language Codes - Mandatory
2. If the mandatory input parameters are missing, throws the appropriate message. 
3. Fetches the Document Category-Document Type mapping for all language codes received in response
4. The response contains the List of Mappings of Document Category and Document Type against each Document Category
5. Each Document Category contains the below attributes
   * Document Category Code
   * Name
   * Description
   * Language Code
   * Is Active
6. Each Document Type contains the below attributes
   * Document Type Code
   * Name
   * Description
   * Language Code
   * Is Active
7. In case of Exceptions, system triggers relevant error messages

#### Delete a Document Category-Type mapping in the Document Category-Type mapping Master Database

On receiving a request to delete a Document Category-Type mapping with the input parameters \(doccat\_code, doctyp\_code\), the system updates the is\_deleted flag to true in the Document Category-Type mapping Database against the input received

The system performs the following steps:

1. Validates if all required input parameters have been received as listed below for each specific request
   * doccat\_code - character \(36\) - Mandatory
   * doctyp\_code - character \(36\) - Mandatory
2. Responds with the doc\_type Code and doccat\_code for the Document Category-Type mapping deleted successfully
3. In case of Exceptions, system triggers relevant error messages. 

#### Fetch applicant type based on Individual Type Code, Date of Birth, Gender Type Code and Biometric Exception Type

On receiving a request to get Applicant type with input parameters \(Individual Type Code, Date of Birth, Gender Type Code and Biometric Exception Type\), the system derives the Applicant Type from the input parameter and performs the following steps:

1. Validates if the request contains the following input parameters
   * Individual Type Code - Mandatory
   * Date of Birth - Mandatory    
   * Gender Type Code - Mandatory
   * Biometric Exception Type - Optional
2. Derives the Age Group Type based on following logic
   * Child if Age &lt; 5
   * Adult if Age &gt;= 5
3. If the mandatory input parameters are missing, throws the appropriate message
4. Derives the applicant type as per the define logic
5. In case of Exceptions, system triggers relevant error messages

#### Check the mapping of Applicant Type-Document Category Name-Document Type Name

On receiving a request to check the mapping of Applicant Type-Document Category-Document Type mapping parameters \(Applicant Type, Document Category Name and Document Type Name\), the system checks the mapping and performs the following steps:

1. Validates if the request contains the following input parameters
   * Applicant Type Code
   * Document Category Name
   * Document Type Name
2. If the mandatory input parameters are missing, throws the appropriate message. 
3. If the mapping exists, responds with "Valid".
4. If the mapping does not exist, responds with "Invalid".
5. In case of Exceptions, system triggers relevant error messages

### List of Rejection Reasons

#### Create a Rejection Reason in Reason List Master Database

Upon receiving a request to add a Reason with the input parameters \(code, name, descr, rsncat\_code, lang\_code and is\_active\), the system stores the Reason in the Database

The system performs the following steps:

1. Validates if all required input parameters have been received as listed below for each specific request
   * code - character \(36\) - Mandatory
   * code - character \(64\) - Mandatory    
   * descr - character \(256\) - Mandatory
   * rsncat\_code - character \(36\) – Mandatory \(The parameter rsncat\_code refers to a Language stored in Language Masterdata\)
   * lang\_code - character \(3\) – Mandatory \(The parameter lang\_code refers to a Language stored in Language Masterdata\)
   * is\_active - boolean - Mandatory
2. Validates if the response contains the following attributes for a Reason Category Code added
   * Code
   * Language Code
   * Rsncat\_code \(Reason Category Code\)
3. Responds to the source with the appropriate message.
4. In case of Exceptions, system triggers relevant error messages. 

#### Fetch the requested list of reasons based on Reason Category Code and Language Code

Upon receiving a request to Fetch the requested List of Reasons with the required input parameters \(Reason 1. Category Code, Language Code\), the system fetches the requested List of reasons stored against the Reason Category Code and Language Code received.

The system performs the following steps:

1. Validates if the request contains the following input parameters
   * Language Code - Mandatory
   * Reason Category Code - Mandatory
2. If either of the mandatory input parameters is missing, responds with the appropriate message as define below in message sections
3. Validates if the response contains the:
   * Requested list based on the requested Language Code and Reason Category Code
   * List of Reasons with the corresponding attributes for the list
     * Reason ID
     * Reason Name \(per Reason ID\)
     * Language Code
     * Reason Category Code
     * IsActive
4. Responds to the source with the relevant List of Reasons, as per the stated business rules
5. In case of Exceptions, system triggers relevant error messages as listed below

### List of Languages

#### Create List of Languages

After receiving a request to add Language Details with the input parameters \(code, name, family, native\_name and is\_active\), the system stores the Language Details in the Database and performs the following steps:

1. Validates if all required input parameters have been received as listed below for each specific request
   * code - character \(3\) - Mandatory
   * name - character \(64\) - Mandatory
   * family - character \(64\) - Optional
   * native\_name - character \(64\) - Optional
   * is\_active - boolean - Mandatory
2. Responds with the Language Code for the language successfully created
3. In case of Exceptions, system triggers relevant error messages

#### Fetch the List of Languages

After receiving a request to fetch the List of Languages, the system fetches the List of Languages and performs the following steps:

1. Validates if the response contains the List of all Languages with the following attributes
   * Language Code - Mandatory
   * Language Name - Mandatory
   * IsActive – Mandatory
2. Responds to the source with the List of Languages
3. In case of Exceptions, system triggers relevant error messages

#### Update and Delete a Language in the List of Languages Master Database

**Update**

After receiving a request to update a Language with the input parameters \(code, name, family, native\_name and is\_active\), the system updates the Language Details in the List of languages Database for the Code received in request

The system performs the following steps:

1. Validates if all required input parameters have been received as listed below for each specific request
   * code - character \(3\) - Mandatory
   * name - character \(64\) - Mandatory
   * family - character \(64\) - Optional
   * native\_name - character \(64\) - Optional
   * is\_active - boolean - Mandatory
2. For the Code received in the request, replaces all the data received in the request against the data existing in the List of languages database against the same code.
3. Deleted record are not updated
4. Responds with data not found error if deleted record is received in the request
5. Responds with the Language Code for the language successfully updated
6. In case of Exceptions, system triggers relevant error messages

**Delete**

After receiving a request to delete a Language with the input parameters \(code\), the system updates the is\_deleted flag to true in the List of languages Database against the code received in request

The system performs the following steps:

1. Validates if all required input parameters have been received as listed below for each specific request
   * code - character \(3\) - Mandatory
2. Deleted record should not be deleted again
3. Responds with data not found error  if deleted record is received in the request
4. Responds with the Language Code for the language successfully deleted
5. In case of Exceptions, system triggers relevant error messages. 

### List of Titles

#### Create a Title

On receiving a request to add a Title \(e.g., MR., Mrs.\) with the input parameters \(code, name, descr, lang\_code and is\_active\), the system stores the Title in the Database and performs the following steps:

1. The API should only be accessible to Global Admin
2. The API should accept only the below parameters
   * name - Character - 64 - Mandatory
   * descr - Character - 128 - Optional
   * lang\_code - Character - 3 - Mandatory
   * is\_active - boolean \(true/false\) - Mandatory
3. All the mandatory input parameter\(s\) should be present in the reqeust. If not, throw an appropriate error message
4. The API should validate the data type and length for each attribute as mentioned above.
5. In case of any failed validation, API should respond with appropriate error message. Refer messages section
6. API should perfrom below multi-language validations on the Title data recieved
7. If, the data is recieved in secondary language and the data for primary language is not present in the database, the API should not allow creation of the Title and throw an error message. Refer messages section
8. If in the request, all the mandatory data is received in primary langauge but not in the secondary langauge, API should store the data but mark the Title as Inactive \(is\_acitve = false\) regardless of what is received in the request for is\_active flag
9. If all the above validations are successfull, the API should store the data the the database
10. Title Code should be generated at the back-end for any Title added using a UUID generator
11. API should store cr\_by as the Username of the user who is accessing this API
12. API should store cr\_dtimes as the date-time at which the user is creating the Title
13. API should only allow creation of one record at a time and should restrict bulk creation
14. API should audit the relevant data when the API is called successfully or when an error is encountered

#### Update a Title

On receiving a request to update a Title with the input parameters \(code, name, descr, lang\_code and is\_active\), the system updates the Title in the Title Database for the code received and performs the following steps:

1. This API should only be accessible to Global Admin
2. The API should accept only the below parameters
   * code - Character - 36 - Mandatory
   * name - Character - 64 - Mandatory
   * descr - Character - 128 - Optional
   * lang\_code - Character - 3 - Mandatory
   * is\_active - boolean \(true/false\) - Mandatory
3. All the mandatory input parameter\(s\) should be present in the reqeust. If not, throw an appropriate error message
4. The API should validate the data type and length for each attribute as mentioned above.
5. In case of any failed validation, API should respond with appropriate error message. Refer messages section
6. If all the above validations are successfull, the API should update the data in the database agianst the code received
7. API should perfrom below multi-language validations on the Title data recieved
8. If in the database, all the mandatory data is present in primary langauge but not in the secondary langauge, API should update the data but mark the Title as Inactive \(is\_acitve = false\) regardless of what is received in the request for is\_active flag
9. API should store upd\_by as the Username of the user who is accessing this API
10. API should store upd\_dtimes as the date-time at which the user is modiying the Title details
11. API should only allow creation of one record at a time and should restrict bulk creation
12. API should audit the relevant data when the API is called successfully or when an error is encountered

#### Fetch the List of Titles

On receiving a request to fetch Title Details with the input parameters \(Language Code\), the system fetches all the Titles with all the attributes for the Language Code Received

The system performs the following steps:

1. Validates if all required input parameters have been received as listed below for each specific request
   * Language Code - Mandatory
2. If the mandatory input parameters are missing, responds with all the data.
3. Validates if the response contains List of Titles against the received Language Code along with the following attributes for the Title Code
   * Title Code - Mandatory
   * Title Name - Mandatory
   * Title Description - Optional
   * IsActive - Mandatory
4. In case of Exceptions, system triggers relevant error messages

### Template File Format

#### Create Template File Format

On receiving a request to add Template File Format with the input parameters \(code, descr, lang\_code and is\_active\), the system stores the Template File Format in the Database and performs the following steps:

1. Validates if all required input parameters have been received as listed below for each specific request
   * code - character \(36\) - Mandatory
   * descr - character \(256\) - Mandatory
   * lang\_code - character \(3\) - Mandatory
   * is\_active - boolean - Mandatory
2. Validates if the response contains the following attributes for a Template File Format added
   * Code
   * Language Code
3. Responds with the Template File Format Code and Language Code for the Template File Format created successfully
4. In case of Exceptions, system triggers relevant error messages. 

#### Create Template File Format

Update and Delete a Template File Format in Template File Format Master Database

**Update**

On receiving a request to update a Template File Format with the input parameters \(code, descr, lang\_code and is\_active\), the system updates the Template File Format in the Template File Format Database for the Code received

While updating the Template File Format, the system performs the following steps: 1. Validates if all required input parameters have been received as listed below for each specific request

* code - character \(36\) - Mandatory
* descr - character \(256\) - Optional
* lang\_code - character \(3\) - Mandatory
* is\_active - boolean - Mandatory
  1. For the code received in the request, replaces all the data received in the request against the data existing in the Template File Format database against the same code.
  2. Deleted record are not updated
  3. Responds with data not found error if deleted record is received in the request
  4. Responds with the Template File Format Code and Language Code for the Template File Format updated successfully
  5. In case of Exceptions, system triggers relevant error messages

**Delete**

On receiving a request to delete a Template File Format with the input parameters \(code\), the system updates the is\_deleted flag to true in the Template File Format Database against the code received

While deleting the Template File Format, the system performs the following steps:

1. Validates if all required input parameters have been received as listed below for each specific request
   * code - character \(36\) - Mandatory
2. Delete all records for the code received
3. Deleted record are not deleted again
4. Responds with data not found error if deleted record is received in the request
5. Responds with dependency found error \(Refer Acceptance criteria\) if a record to be deleted is used as foreign key in the dependent table
6. Responds with the Template File Format Code for the Template File Format deleted successfully
7. In case of Exceptions, system triggers relevant error messages. 

### List of Template Types

MOSIP system can create Template Type in the Master Database.

Upon receiving a request to add Template Type \(e.g., SMS Notification template - New Registration\) with the input parameters \(code, descr, lang\_code and is\_active\), the system stores the Template Type in the Database and performs the following steps:

1. Validates if all required input parameters have been received as listed below for each specific request
   * code - character \(36\) - Mandatory
   * descr - character \(256\) - Mandatory
   * lang\_code - character \(3\) - Mandatory
   * is\_active - boolean – Mandatory
2. Responds with the Template Type Code and Language Code for the Template Type created successfully
3. This component also restricts the bulk creation of Master Database
4. In case of Exceptions, system triggers relevant error messages as listed below.

### List of Templates

#### Create Template

On receiving a request to add a Template with the input parameters \(id, name, descr, file\_format\_code, model, file\_txt, module\_id, module\_name, template\_typ\_code, lang\_code and is\_active\), the system stores the Template in the Database and performs the following steps:

1. This API should only be accessible to Global Admin
2. The API should accept only the below parameters
   * name - Character - 128 - Mandatory
   * descr - Character - 256 - Optional
   * file\_format\_code - 36 - Mandatory
   * model - Character - 128 - Optional
   * file\_txt - Character - 4086 - Mandatory
   * module\_id - Character - 36 - Mandatory
   * module\_name - Character - 128 - Mandatory
   * template\_typ\_code - Character - 36 - Mandatory
   * lang\_code - Character - 3 - Mandatory
   * is\_active - boolean \(true/false\) - Mandatory
3. All the mandatory input parameter\(s\) should be present in the reqeust. If not, throw an appropriate error message
4. The API should validate the data type and length for each attribute as mentioned above.
5. In case of any failed validation, API should respond with appropriate error message.
6. 'file\_format\_code' received should be from list of 'codes' from 'template\_file\_format' masterdata table
   * If not, the API should throw an error.
7. 'template\_typ\_code' received should be from list of 'codes' from 'template\_type' masterdata table
   * If not, the API should throw an error.
8. If all the above validations are successfull, the API should update the data in the database agianst the id received
9. API should perfrom below multi-language validations on the Template data recieved
10. If in the database, all the mandatory data is present in primary langauge but not in the secondary langauge, API should update the data but mark the Template as Inactive \(is\_acitve = false\) regardless of what is received in the request for is\_active flag
11. API should store upd\_by as the Username of the user who is accessing this API
12. API should store upd\_dtimes as the date-time at which the user is modiying the Template details
13. API should only allow creation of one record at a time and should restrict bulk creation
14. API should audit the relevant data when the API is called successfully or when an error is encountered

#### Fetch Template based on a Template Type and a Language Code

On receiving a request to fetch a Template with the input parameters \(Template Type Code and List of Language Code\), the system fetches the Template for the Template Type Code and all Language Codes received

Refer below for the process:

1. Validates if all required input parameters have been received as listed below for each specific request
   * Template Type Code - Mandatory
   * List of Language Code - Mandatory
2. If the mandatory input parameters are missing, throws the appropriate message. Refer "Messages" section.
3. Response must contain templates for all the language codes received in the input parameter
4. Validates if the response contains the Template along with the following attributes
   * Template Type Code - Mandatory
   * Template - Mandatory
   * IsActive
5. In case of Exceptions, system triggers relevant error messages

#### Update a Template

On receiving a request to update a Template with the input parameters \(id, name, descr, file\_format\_code, model, file\_txt, module\_id, module\_name, template\_typ\_code, lang\_code and is\_active\), the system updates the Template in the Template Database for the id received and performs the following steps:

1. This API should only be accessible to Global Admin
2. The API should accept only the below parameters
   * id - Character - 36 - Mandatory
   * name - Character - 128 - Mandatory
   * descr - Character - 256 - Optional
   * file\_format\_code - 36 - Mandatory
   * model - Character - 128 - Optional
   * file\_txt - Character - 4086 - Mandatory
   * module\_id - Character - 36 - Mandatory
   * module\_name - Character - 128 - Mandatory
   * template\_typ\_code - Character - 36 - Mandatory
   * lang\_code - Character - 3 - Mandatory
   * is\_active - boolean \(true/false\) - Mandatory
3. All the mandatory input parameter\(s\) should be present in the reqeust. If not, throw an appropriate error message
4. The API should validate the data type and length for each attribute as mentioned above.
5. In case of any failed validation, API should respond with appropriate error message. Refer messages section
6. 'file\_format\_code' received should be from list of 'codes' from 'template\_file\_format' masterdata table
   * If not, the API should throw an error.
7. 'template\_typ\_code' received should be from list of 'codes' from 'template\_type' masterdata table
   * If not, the API should throw an error.
8. If all the above validations are successfull, the API should update the data in the database agianst the id received
9. API should perfrom below multi-language validations on the Template data recieved
10. If in the database, all the mandatory data is present in primary langauge but not in the secondary langauge, API should update the data but mark the Template as Inactive \(is\_acitve = false\) regardless of what is received in the request for is\_active flag
11. API should store upd\_by as the Username of the user who is accessing this API
12. API should store upd\_dtimes as the date-time at which the user is modiying the Template  details
13. API should only allow creation of one record at a time and should restrict bulk creation
14. API should audit the relevant data when the API is called successfully or when an error is encountered

### List of Blacklisted Words

#### Create Blacklisted Words

Upon receiving a request to add a Blacklisted Word with the input parameters \(code, name, descr, lang\_code and is\_active\), the system stores the Blacklisted Word in the Database and performs the following steps:

1. Validates if all required input parameters have been received as listed below for each specific request
   * word - character \(128\) - Mandatory
   * descr - character \(256\) - Optional
   * lang\_code - character \(3\) - Mandatory
   * is\_active - boolean - Mandatory
2. cr\_by should be the Username of the user who is accessing this API
3. cr\_dtimes should be the date-time when the user is creating the Blacklisted Word 
4. Responds with the appropriate message for the Device created successfully
5. The component should restricts the bulk creation of Master Database
6. In case of Exceptions, system triggers error messages as received from the Database. 

#### Update a Blacklisted Word

Upon receiving request to update a Blacklisted Word with the input parameters \(code, name, descr, lang\_code and is\_active\), the system updates the Blacklisted Word in the Blacklisted Word Database for the code received and performs the following steps: 1. Validates if all required input parameters have been received as listed below for each specific request

* word- character \(128\) - Mandatory
* descr - character \(256\) - Optional
* lang\_code - character \(3\) - Mandatory
* is\_active - boolean - Mandatory
  1. For the code received in the request, replaces all the data received in the request against the data existing in the Blacklisted Word database against the same code
  2. upd\_by should be the Username of the user who is accessing this API
  3. upd\_dtimes should be the date-time when the user updates the Blacklisted Word Details
  4. Deleted record are not updated
  5. Responds with data not found error if deleted record is received in the request
  6. Responds with the appropriate message for the Blacklisted word updated successfully
  7. In case of Exceptions, system triggers relevant error messages as listed below

#### Delete a Blacklisted Word

Upon receiving a request to delete a Blacklisted Word with the input parameters \(code\), the system updates the is\_deleted flag to true in the Blacklisted Word Database against the code received and performs the following steps:

1. Validates if all required input parameters have been received as listed below for each specific request
   * word- int - Mandatory
2. Deleted record are not deleted again
3. Responds with data not found error if deleted record is received in the request
4. Responds with the Word for the Blacklisted word deleted successfully
5. In case of Exceptions, system triggers relevant error messages as listed below

#### Fetch List of Blacklisted words based on a Language Code

Upon receiving a request to Fetch the List of Blacklisted words with input parameters \(Language Code\), the system fetches the List of Blacklisted words against the Language Code received

While fetching the black listed words, the system performs the following steps:

1. Validates if the request contains the following input parameters
   * Language Code - Mandatory
2. If the mandatory input parameters are missing, throws the appropriate message. 
3. Validates if the response contains the List of Blacklisted words against Language Code and the corresponding attributes for the Blacklisted word
   * Blacklisted Word
   * IsActive
4. In case of Exceptions, system triggers relevant error messages. 

### List of Reason Categories

MOSIP system can create a Reason Category in Master Database

Upon receiving a request to add Reason Category with the input parameters \(code, name, descr, lang\_code and is\_active\), the system stores the Reason Category in the Database and performs the following steps:

1. Validates if all required input parameters have been received as listed below for each specific request
   * code - character \(36\) - Mandatory
   * name - character \(64\) - Mandatory
   * descr - character \(256\) - Mandatory
   * lang\_code - character \(3\) - Mandatory
   * is\_active - boolean - Mandatory
2. Validates if the response contains the following attributes for a Reason Category added
   * Code
   * Language Code
3. Responds with the Reason Category code and Language Code for the Reason Category created successfully
4. In case of Exceptions, system triggers relevant error messages as listed below

### List of Applications

#### Create a List of Applications

Upon receiving a request to add Application with the input parameters \(code, name, descr, lang\_code and is\_active\), the system stores the Application in the Database

Refer below for the process:

1. Validates if all required input parameters have been received as listed below for each specific request
   * code - character \(36\) - Mandatory
   * name - character \(64\) - Mandatory
   * descr- character \(256\) - Mandatory
   * lang\_code - character \(3\) – Mandatory \(The parameter lang\_code refers to a Language stored in Language Masterdata. Refer\)
   * is\_active - boolean - Mandatory
2. Validates if the response contains the following attributes for an Application added
   * Code
   * Language Code
3. Responds with the Application ID and Language Code for the Application created successfully
4. In case of Exceptions, system triggers relevant error messages as listed below

#### Fetch List of Applications based on received input parameter

**Fetch the List of all Applications**

Upon receiving a request to Fetch List of Applications, the system fetches all the List of Applications and performs the following steps:

1. Validates if the response contains the following attributes for each Application
   * Application ID
   * Application Detail
   * IsActive
2. The response must contain the list of applications in all the languages present in the Database
3. Responds to the source with all the Application attributes.

**Fetch the Application detail based on a Language Code and Application ID**

Upon receiving a request to Fetch List of Applications with the required input parameters \(Application ID, Language Code\), the system fetches the Application Detail based on the Application ID and Language Code received

Refer below for the process:

1. Validates if all required input parameters have been received as listed below for each specific request
   * Application ID - Mandatory
   * Language Code - Mandatory
2. Responds with the Application Data against the Application ID and Language Code Received
3. Validates if the response contains the following attributes for each Application
   * Application ID
   * Application Detail
   * IsActive
4. Responds to the source with the Application Detail
5. If the mandatory input parameters are missing, responds with all the data.
6. In case of Exceptions, system triggers relevant error messages as listed below

### List of ID Types

#### Create an ID type

Upon receiving a request to add an ID Type with the input parameters \(code, name, descr, lang\_code and is\_active\), the system stores the ID Type in the Database

Refer below for the process:

1. Validates if all required input parameters have been received as listed below for each specific request
   * code - character \(36\) - Mandatory
   * code - character \(64\) - Mandatory
   * descr - character \(256\) - Mandatory
   * lang\_code - character \(3\) – Mandatory \(refers to a Language stored in Language Masterdata\)
   * is\_active - boolean - Mandatory
2. Validates if the response contains the following attributes for an ID Type added
   * Code
   * Language Code
3. Responds with the ID Type Code and Language Code for the ID type created successfully
4. In case of Exceptions, system triggers relevant error messages as listed below.

#### Fetch the List of ID Types based on Language Code

Upon receiving a request to fetch the List of ID Types with input parameters \(Language Code\), the system fetches the List of ID Types against the Language Code Received

Refer below for the process:

1. Validates if the request contains the following input parameters
   * Language Code - Mandatory
2. If the mandatory input parameters are missing, throws the appropriate message. Refer "Messages" section below.
3. Validates if the response contains the List of ID Types with the following attributes
   * ID Type Name
   * ID Type Code
   * IsActive
4. In case of Exceptions, system triggers relevant error messages. 

### User Details

#### User Details

Upon receiving a request to fetch the user history record with input parameters \(User ID and Date Timestamp\), the system fetches all the attributes of the user from the history table and performs the following steps:

1. Validates if all required input parameters have been received as listed below for each specific request.
   * User ID - Mandatory
   * Date Timestamp - Mandatory
2. The record fetched are the latest record existing on or before the date received in the input parameter.
3. If the mandatory input parameters are missing, then the system triggers the appropriate message.
4. Response will contain all the attributes for the user including the Active/Inactive status.
5. In case of exceptions, system triggers relevant error messages.

#### Fetch RID based on a User ID

1. Receive request to retrieve RID based on input parameter \(User ID, App ID\)
   * User ID and App ID both will be mandatory
2. Fetch the RID
3. Respond to the source with the fetched data
4. Respond with error 'User doesn't exist' if no user is found for User ID received

### Document Type to Category Mapping

#### Create a mapping record of Document Type and Document Category in Valid Document Mapping Master Database

Upon receiving a request to add a mapping of Document Type and Document Category with the input parameters \(doctyp\_code, doccat\_code\) the system stores the Mapping of Document type and Document category in the Database

Refer below for the process:

1. Validates if all required input parameters have been received as listed below for each specific request
   * doctyp\_code - character - 36 - mandatory
   * doccat\_code - character - 36 - mandatory
2. If the mapping does not exist
   * is\_active flag should be stored as true when the mapping is created
   * Store the default language code against the mapping
   * cr\_by should be the User ID of the user who is accessing this API
   * cr\_dtimes should be the date-time at which the user is creating the Document Category - Document Type Mapping
3. if the mapping already exist but is in inactive state
   * Update the is\_acitve flag as “True”
   * Updated the upd\_by and upd\_dtimes values against the mapping
4. If the mapping already exist in active state, throw appropriate error message
5. Responds with the appropriate message for the mapping being created successfully
6. The API restricts the bulk creation of Master Data
7. In case of Exceptions, system triggers error messages as received from the Database. 

#### Remove a mapping record of Document Type and Document Category in Valid Document Mapping Master Database

Upon receiving a request to add a mapping of Document Type and Document Category with the input parameters \(doctyp\_code, doccat\_code\) the system stores the Mapping of Document type and Document category in the Database

Refer below for the process:

1. Validates if all required input parameters have been received as listed below for each specific request
   * doctyp\_code - character - 36 - mandatory
   * doccat\_code - character - 36 - mandatory
2. If the Document Type is already un-mapped from Document Category, throw an appropriate error message
3. upd\_by should be the User ID of the user who is accessing this API
4. upd\_dtimes should be the date-time when the Document Category - Document Type Mapping is being updated
5. Change the Is\_active flag to “False” for removing the mapping
6. Responds with the appropriate message for the mapping being created successfully
7. The API restricts the bulk creation of Master Data
8. In case of Exceptions, system triggers error messages as received from the Database.

### Working and Non-Working Days

#### API should be able to fetch working days for a Center based on a Center ID

Refer below for the process:

1. The API should support taking Center ID and Language Code as an mandatory input parameter
2. The API should respond to the source with all the days of the week for the Center in the language received
3. Each day should have an attribute marking whether the day is a working day or off-work day
4. Each day should have an attribute defing the calenday order of days of the week

If the working days are not defined against the Center, the API should fetch the globally defined working and non-working days.

The API should throw error messages in scenarios mentioned in error messages section.

### Exceptional Holidays for a Center

#### API should be able to fetch any defined exceptional holiday dates for a Center based on a Center ID

Refer below for the process:

1. Validates if all required input parameters have been received as listed below for each specific request
   * Center ID - character - 10 - mandatory
2. API should respond to the source with all the exceptional holiday dates for the Center ID received
3. API should throw relevant error messages in any error scenarios

## Registration Management

### Registration Center Type

#### Create Registration Center Type

On receiving a request to add Registration Center Type with the input parameters \(code, name, descr, lang\_code and is\_active\), the system stores the Registration Center Type in the Database

Refer below for the process:

1. This API should only be accessible to Global Admin
2. The API should accept only the below parameters
   * name - Character - 64 - Mandatory
   * lang\_code - Character - 3 - Mandatory
   * is\_active - boolean \(true/false\) - Mandatory
3. All the mandatory input parameter\(s\) should be present in the reqeust. If not, throw an appropriate error message
4. The API should validate the data type and length for each attribute as mentioned above.
5. In case of any failed validation, API should respond with appropriate error message. Refer messages section
6. API should perfrom below multi-language validations on the Gender Type data recieved
7. If, the data is recieved in secondary language and the data for primary language is not present in the database, the 8. API should not allow creation of the Gender Type and throw an error message.
8. If in the request, all the mandatory data is received in primary langauge but not in the secondary langauge, API should store the data but mark the Gender Type as Inactive \(is\_acitve = false\) regardless of what is received in the request for is\_active flag
9. If all the above validations are successfull, the API should store the data the the database
10. Gender Type Code should be generated at the back-end for any Gender Type added using a UUID generator
11. API should store cr\_by as the Username of the user who is accessing this API
12. API should store cr\_dtimes as the date-time at which the user is creating the Gender Type
13. API should only allow creation of one record at a time and should restrict bulk creation
14. API should audit the relevant data when the API is called successfully or when an error is encountered

#### Update a Registration Center Type

On receiving a request to update a Registration Center Type with the input parameters \(code, name, descr, lang\_code and is\_active\), the system Updates the Registration Center Type Details in the Registration Center Type Database for the Code received

Refer below for the process:

1. This API should only be accessible to Global Admin
2. The API should accept only the below parameters
   * code - Character - 36 - Mandatory
   * name - Character - 64 - Mandatory
   * lang\_code - Character - 3 - Mandatory
   * is\_active - boolean \(true/false\) - Mandatory
3. All the mandatory input parameter\(s\) should be present in the reqeust. If not, throw an appropriate error message
4. The API should validate the data type and length for each attribute as mentioned above.
5. In case of any failed validation, API should respond with appropriate error message. Refer messages section
6. If all the above validations are successfull, the API should update the data in the database agianst the code received
7. API should perfrom below multi-language validations on the Gender Type data recieved
8. If in the database, all the mandatory data is present in primary langauge but not in the secondary langauge, API should update the data but mark the Gender Type as Inactive \(is\_acitve = false\) regardless of what is received in the request for is\_active flag
9. API should store upd\_by as the Username of the user who is accessing this API
10. API should store upd\_dtimes as the date-time at which the user is modiying the Gender Type details
11. API should only allow creation of one record at a time and should restrict bulk creation
12. API should audit the relevant data when the API is called successfully or when an error is encountered

### Registration Center

#### Create a Registration Center

Upon receiving a request to add Registration Center with the input parameters, the system Stores the Registration Center in the Database

Refer below for the process:

1. The system validates if all required input parameters have been received as listed below for each specific request
   * name - character \(128\) - mandatory
   * cntrtyp\_code - character \(36\) - mandatory
   * addr\_line1 - character \(256\) - mandatory
   * addr\_line2 - character \(256\) - optional
   * addr\_line3 - character \(256\) - optional
   * latitude - character \(32\) - mandatory
   * longitude - character \(32\) - mandatory
   * location\_code - character \(36\) - mandatory
   * contact\_phone - character \(16\) - optional
   * contact\_person - character \(256\) - optional
   * working\_hours - character \(32\) - mandatory
   * per\_kiosk\_process\_time - time - mandatory
   * center\_start\_time - time - mandatory
   * center\_end\_time - time - mandatory
   * lunch\_start\_time - time - optional
   * lunch\_end\_time - time - optional
   * holiday\_loc\_code - character \(36\) - mandatory
   * timezone - string \(128\) - optional
   * lang\_code - character \(3\) - mandatory
   * zone\_code - character \(36\) - mandatory
2. is\_active should be set as “False”
3. number\_of\_kiosks should be kept as zero for creation of a Registration Center
4. center\_end\_time should not be before the center\_start\_time
5. Latitude and Longitude should be in format of “\(-\)XX.XXXX”
   * Latitude and Longitude should contain at-least 4 digits after decimal
6. If lunch\_end\_time and lunch\_start\_time is sent in the request,
   * lunch\_end\_time should not be before the lunch\_start\_time
7. The Zone received should be either same as the Zone mapped of the Administrator or a child zone of the Administrator's Zone
8. cr\_by should be the Username of the user who is accessing this API
9. cr\_dtimes should be the date-time at which the user is creating the Registration Center
10. Center ID should be generated by calling the Registration Center ID Generator and stored against every new Center Created
11. If, the data is recieved in secondary language and the data for primary language is not present in the database, the API should not allow creation of the Registration Center
12. Responds with the appropriate message for the Registration Center created successfully
13. History record should be stores for every creation of a new Registration Center
14. The API should restricts the bulk creation of Master Data
15. In case of Exceptions, system triggers error messages as received from the Database. 

#### Update a Registration Center

On receiving a request to update a Registration Center with the input parameters, the system updates the Registration Center Details in the List of Registration Center Database for the center\_id received

Refer below for the process:

1. The system validates if all required input parameters have been received as listed below for each specific request
   * center\_id - character \(36\) - mandatory
   * name - character \(128\) - mandatory
   * cntrtyp\_code - character \(36\) - mandatory
   * addr\_line1 - character \(256\) - mandatory
   * addr\_line2 - character \(256\) - optional
   * addr\_line3 - character \(256\) - optional
   * latitude - character \(32\) - mandatory
   * longitude - character \(32\) - mandatory
   * location\_code - character \(36\) - mandatory
   * contact\_phone - character \(16\) - optional
   * contact\_person - character \(256\) - optional
   * working\_hours - character \(32\) - mandatory
   * per\_kiosk\_process\_time - time - mandatory
   * center\_start\_time - time - mandatory
   * center\_end\_time - time - mandatory
   * lunch\_start\_time - time - optional
   * lunch\_end\_time - time - optional
   * holiday\_loc\_code - character \(36\) - mandatory
   * timezone - string \(128\) - optional
   * lang\_code - character \(3\) - mandatory
   * zone\_code - character \(36\) - mandatory
   * is\_active - boolean - mandatory
2. For the center\_id received in the request, replaces all the data received in the request against the data existing in the List of Registration Center database against the same center\_id.
3. All the mandatory input parameters should be present 
4. center\_end\_time should not be before the center\_start\_time
5. Latitude and Longitude should be in format of “\(-\)XX.XXXX”
   * Latitude and Longitude should contain at-least 4 digits after decimal
6. If lunch\_end\_time and lunch\_start\_time is sent in the request,
   * lunch\_end\_time should not be before the lunch\_start\_time
7. The Zone received should be either same as the Zone mapped of the Administrator or a child zone of the Administrator's Zone
8. If in the database, all the mandatory data is present in primary langauge but not in the secondary langauge, API should update the data but mark the Registration Center as Inactive \(is\_acitve = false\) regardless of what is received in the request for is\_active flag
9. upd\_by should be the Username of the user who is accessing this API
10. upd\_dtimes should be the date-time at which the user is creating the Registration Center
11. History record should be stores for every modification of a Registration Center
12. Responds with the Registration Center Code and Language Code for the Registration Center updated successfully
13. In case of Exceptions, system triggers relevant error messages

#### Decommission a Registration Center

Upon receiving a request to Decommission a Registration Center with the input parameters \(center\_id\), the system updates the is\_deleted flag to true in the List of Registration Center Database against the center\_id received

Refer below for the process:

1. Validate if all required input parameters have been received as listed below for each specific request
   * center\_id - character \(36\) - Mandatory 
2. Change the “is\_Deleted” flag against Registration Center ID to “True”
3. Change the “is\_Active” flag to “False” against the Registration Center.
4. upd\_by should be the Username of the user who is accessing this API
5. del\_dtimes should be the date-time when the Registration Center is being decommissioned
6. Validate if any Machine, Devices or Users are mapped to the Registration Center
   * If any Machine, Device or User is assigned to the Registration Center, do no decommission the Registration Center, throw an appropriate error message. Refer “Messages Section”.
7. The User accessing the API should only be able to decommission a Center under its administrative zone only
8. Responds with the appropriate message for the Registration Center decommissioned successfully
9. In case of Exceptions, system triggers relevant error messages

#### Fetch Registration Center details based on a Registration Center ID and Language Code.

On receiving a request to fetch Registration Center Details with the input parameters \(Registration Center ID and Language Code\), the system fetches all the Registration Center attributes for the Registration Center ID and Language Code received. The system only fetches active Registration Centers.

Refer below for the process:

1. While fetching the registration center details the system validates if all required input parameters have been received as listed below for each specific request
   * Registration Center ID - Mandatory
   * Language Code - Mandatory
2. If the mandatory input parameters are missing, throws the appropriate message. 
3. System also validates if the response contains the following attributes for the Registration Center ID along with values as applicable
   * Registration Center ID
   * Registration Center Name
   * Longitude
   * Latitude
   * IsActive
   * Center Type Code
   * Address
   * Working Hours
   * Contact Number
   * No. of kiosk
   * Per kiosk Processing time
   * Starting time
   * End time
   * IsActive
4. In case of Exceptions, system triggers relevant error messages. 

#### Fetch Registration Center record based on a Registration center ID, Date and Language Code from the Registration Center Updation/Creation History table

On receiving a request to fetch Registration Center Creation/Updation History Detail with the input parameters \(Registration Center ID, Date and Language Code\), the system fetches all the attributes of Registration Center from the history table for the Registration Center ID, Date and Language Code received

Refer below for the process:

1. While fetching registration center records the system validates if all required input parameters have been received as listed below for each specific request
   * Registration Center ID - Mandatory
   * Date - Mandatory
   * Language Code - Mandatory
2. The record fetched is the latest record existing on or before the date received in the input parameter
3. If the mandatory input parameters are missing, system throws the appropriate message. 
4. Validates if the response contains the following attributes for the Registration Center ID along with values as applicable
   * Registration Center ID
   * Registration Center Name
   * Longitude
   * Latitude
   * IsActive
   * Center Type Code
   * Address
   * Working Hours
   * Contact Number
   * No. of kiosk
   * Per koisk Processing time
   * Starting time
   * End time
   * IsActive
5. In case of Exceptions, system triggers relevant error messages.

#### Fetch Registration Center details based on a Location Code and a Language Code

Upon receiving a request to fetch the List of Registration Centers with the input parameter \(Location Code and Language Code\), the system fetches the list of all the Registration Centers against the Location Code and Language Code received with all the attributes for each Registration Center. The system only fetches active Registration Centers.

Refer below for the process:

1. While fetching the registration center details the system validates if all required input parameters have been received as listed below for each specific request
   * Location Code
   * Language Code
2. If the mandatory input parameters are missing, throws the appropriate message
3. Validates if the response contains all the Registration Center against the Location Code received with the following attributes for the Registration Centers
   * Registration Center ID
   * Registration Center Name
   * Longitude
   * Latitude
   * IsActive
   * Center Type
   * Address
   * Working Hours
   * Contact Number
   * No. of kiosk
   * Per koisk Processing time
   * Starting time
   * End time
   * IsActive
4. In case of Exceptions, system triggers relevant error messages

#### Fetch Registration Center details based on a Longitude and a Latitude, Proximity Distance and Language Code

On receiving a request to fetch the List of Registration Centers with the input parameter \(Longitude and Latitude, Proximity distance and Language Code\), the system fetches the List of Registration Centers against the input parameters received. The system only fetches active Registration Centers.

Refer below for the process:

1. While fetching the registration center details the system validates if all required input parameters have been received as listed below for each specific request
   * Longitude
   * Latitude
   * Proximity Distance
   * Language Code
2. If the mandatory input parameters are missing, throw the appropriate message
3. The responses contain the list of all the Registration Centers in the radius of Proximity distance radius of the Longitude and the Latitude received with all the attributes for each Registration Center
4. System fetches the record against the Language Code Received
5. Validates if the response contains all the Registration Center against the Longitude and the Latitude and the Language Code received with the following attributes for the Registration Centers
   * Registration Center ID
   * Registration Center Name
   * Longitude
   * Latitude
   * IsActive
   * Center Type
   * Address
   * Working Hours
   * Contact Number
   * No. of kiosk
   * Per koisk Processing time
   * Starting time
   * End time
   * IsActive
6. In case of Exceptions, system triggers relevant error messages

#### Fetch the List of Registration Centers based on Location Hierarchy Level, text input and a Language Code

Upon receiving a request to fetch the List of Registration centers with input parameters \(Location Hierarchy Level, Text Input and a Language Code\), the system fetches the List of Registration centers. The system only fetches active Registration Centers.

Refer below for the process:

1. While fetching the list of registration centers the system validates if the request contains the following input parameters
   * Location Hierarchy Level - Mandatory
   * Text Input - Mandatory
   * Language Code - Mandatory
2. If the mandatory input parameters are missing, throws the appropriate message
3. The list of registration center is fetched based on the combination of Location Hierarchy level and Text received.
4. System also fetches the list based on the language code received.
5. The response contains below mentioned attributes for each registration center
   * Registration Center ID
   * Registration Center Name
   * Longitude
   * Latitude
   * IsActive
   * Center Type Code
   * Address
   * Working Hours
   * Contact Number
   * No. of kiosk
   * Per kiosk Processing time
   * Starting time
   * End time
   * IsActive
6. In case of Exceptions, system triggers relevant error messages. 

#### Validates whether a Registration Center is under working hours based on a timestamp received

On receiving a request to fetch Registration Center Details with the input parameters \(Registration Center ID and Date-Timestamp\), the system determines the status of the Registration center as per the logic defined.

Refer below for the process:

1. While determining the status of registration center the system validates if all required input parameters have been received as listed below for each specific request
   * Registration Center ID - Mandatory
   * Date-Timestamp - Mandatory
2. If the mandatory input parameters are missing, system throws the appropriate message. 
3. Responds with "Accept" message if both the following conditions are met:
   * The Registration Center corresponding to the Registration Center ID received must be not on a holiday on the date received in the input parameter.
   * The Timestamp received in the input parameter must be greater the Registration Center Opening time and Less than or equal to Closing time + 1 Hour.
4. Responds with the reject scenario if the above two conditions together are not met.
5. E.g., If the Registration center in not on a holiday and its opening and closing time is \(9:00 AM to 5:00 PM\). Find the sample response below for different timestamp received.
   * Timestamp - 4:00 PM - Accepted
   * Timestamp - 5:00 PM - Accepted
   * Timestamp - 6:00 PM - Accepted
   * Timestamp - 6:01 PM - Rejected
6. In case of Exceptions, system triggers relevant error messages

### List of Machine Types

#### Creation of a Machine Type

Upon receiving a request to add Machine Type \(e.g., Dongle/Desktop\) with the input parameters \(code, name, descr, lang\_code and is\_active\), the system stores the Machine Type in the Database

Refer below for the process:

1. This API should only be accessible to Global Admin
2. The API should accept only the below parameters
   * name - Character - 64 - Mandatory
   * descr - Character - 128 - Optional
   * lang\_code - Character - 3 - Mandatory
   * is\_active - boolean \(true/false\) - Mandatory
3. All the mandatory input parameter\(s\) should be present in the reqeust. If not, throw an appropriate error message
4. The API should validate the data type and length for each attribute as mentioned above.
5. In case of any failed validation, API should respond with appropriate error message. Refer messages section
6. API should perfrom below multi-language validations on the Machine Type data recieved
7. If, the data is recieved in secondary language and the data for primary language is not present in the database, the API should not allow creation of the Machine Type and throw an error message. Refer messages section
8. If in the request, all the mandatory data is received in primary langauge but not in the secondary langauge, API should store the data but mark the Machine Type as Inactive \(is\_acitve = false\) regardless of what is received in the request for is\_active flag
9. If all the above validations are successfull, the API should store the data the the database
10. Machine Type Code should be generated at the back-end for any Machine Type added using a UUID generator
11. API should store cr\_by as the Username of the user who is accessing this API
12. API should store cr\_dtimes as the date-time at which the user is creating the Machine Type
13. API should only allow creation of one record at a time and should restrict bulk creation
14. API should audit the relevant data when the API is called successfully or when an error is encountered 

#### Update of a Machine Type

1. This API should only be accessible to Global Admin
2. The API should accept only the below parameters
   * code - Character - 36 - Mandatory
   * name - Character - 64 - Mandatory
   * descr - Character - 128 - Optional
   * lang\_code - Character - 3 - Mandatory
   * is\_active - boolean \(true/false\) - Mandatory
3. All the mandatory input parameter\(s\) should be present in the reqeust. If not, throw an appropriate error message
4. The API should validate the data type and length for each attribute as mentioned above.
5. In case of any failed validation, API should respond with appropriate error message. Refer messages section
6. If all the above validations are successfull, the API should update the data in the database agianst the code received
7. API should perfrom below multi-language validations on the Machine Type data recieved
8. If in the database, all the mandatory data is present in primary langauge but not in the secondary langauge, API should update the data but mark the Machine Type as Inactive \(is\_acitve = false\) regardless of what is received in the request for is\_active flag
9. API should store upd\_by as the Username of the user who is accessing this API
10. API should store upd\_dtimes as the date-time at which the user is modiying the Machine Type details
11. API should only allow creation of one record at a time and should restrict bulk creation
12. API should audit the relevant data when the API is called successfully or when an error is encountered

### List of Machine Specifications

#### Create Machine Specifications

On receiving a request to add Machine Specifications with the input parameters \(name, brand, model, mtyp\_code, min\_driver\_ver, descr, lang\_code and is\_active\) the system stores the Machine Specifications in the Database

Refer below for the process:

1. This API should only be accessible to Global Admin
2. The API should accept only the below parameters
   * name - Character - 64 - Mandatory
   * brand - Character - 32 - Mandatory
   * model - Character - 16 - Mandatory
   * mtyp\_code - Character - 36 - Mandatory
   * min\_driver\_version - Character - 16 - Mandatory
   * descr - Character - 256 - Optional
   * lang\_code - Character - 3 - Mandatory
   * is\_active - boolean \(true/false\) - Mandatory
3. All the mandatory input parameter\(s\) should be present in the reqeust. If not, throw an appropriate error message
4. The API should validate the data type and length for each attribute as mentioned above.
5. In case of any failed validation, API should respond with appropriate error message. Refer messages section
6. mtyp\_code received should be from list of 'codes' from machine\_type masterdata table
   * If not, the API should throw an error. Refer messages section
7. API should perfrom below multi-language validations on the Machine Specification data recieved
8. If, the data is recieved in secondary language and the data for primary language is not present in the database, the API should not allow creation of the Machine Specification and throw an error message. Refer messages section
9. If in the request, all the mandatory data is received in primary langauge but not in the secondary langauge, API should store the data but mark the Machine Specification as Inactive \(is\_acitve = false\) regardless of what is received in the request for is\_active flag
10. If all the above validations are successfull, the API should store the data the the database
11. Machine Specification Id should be generated at the back-end for any Machine Specification added using a UUID generator
12. API should store cr\_by as the Username of the user who is accessing this API
13. API should store cr\_dtimes as the date-time at which the user is creating the Machine Specification
14. API should only allow creation of one record at a time and should restrict bulk creation
15. API should audit the relevant data when the API is called successfully or when an error is encountered

#### Update a Machine Specification

On receiving a request to update a Machine Specification with the input parameters \(id, name, brand, model, mtyp\_code, min\_driver\_ver, descr, lang\_code and is\_active\), the system updates the Machine Specification Details in the Machine Specification Database for the id received

1. This API should only be accessible to Global Admin
2. The API should accept only the below parameters
   * id - Character - 36 - Mandatory
   * name - Character - 64 - Mandatory
   * brand - Character - 32 - Mandatory
   * model - Character - 16 - Mandatory
   * mtyp\_code - Character - 36 - Mandatory
   * min\_driver\_version - Character - 16 - Mandatory
   * descr - Character - 256 - Optional
   * lang\_code - Character - 3 - Mandatory
   * is\_active - boolean \(true/false\) - Mandatory
3. All the mandatory input parameter\(s\) should be present in the reqeust. If not, throw an appropriate error message
4. The API should validate the data type and length for each attribute as mentioned above.
5. In case of any failed validation, API should respond with appropriate error message. Refer messages section
   * mtyp\_code received should be from list of 'codes' from machine\_type masterdata table
6. If not, the API should throw an error.
7. If all the above validations are successfull, the API should update the data in the database agianst the id received
8. API should perfrom below multi-language validations on the Machine Specification data recieved
9. If in the database, all the mandatory data is present in primary langauge but not in the secondary langauge, API should update the data but mark the Machine Specification as Inactive \(is\_acitve = false\) regardless of what is received in the request for is\_active flag
10. API should store upd\_by as the Username of the user who is accessing this API
11. API should store upd\_dtimes as the date-time at which the user is modiying the Machine Specification details
12. API should only allow creation of one record at a time and should restrict bulk creation
13. API should audit the relevant data when the API is called successfully or when an error is encountered

### List of Machines

#### Create a Machine in Master Database

On receiving a request to add Machine with the input parameters, the system Stores the Machine Details in the Database

Refer below for the process:

1. While creating the machine IDs the system validates if all required input parameters have been received as listed below for each specific request
   * machine\_id - character \(36\) - mandatory
   * name - character \(64\) - mandatory
   * mac\_address - character \(64\) - mandatory
   * serial\_num - character \(64\) - mandatory
   * ip\_address- character \(17\) - optional
   * validity\_end\_dtimes - timestamp
   * mspec\_id - character \(36\) - mandatory
   * lang\_code - character \(3\) - mandatory
   * zone\_code - character \(36\) - mandatory
   * is\_active - boolean - mandatory
2. The Zone received should be either same as the Zone mapped of the Administrator or a child zone of the Administrator's Zone
3. cr\_by should be the Username of the user who is accessing this API
4. cr\_dtimes should be the date-time at which the user is creating the Machine
5. Machine ID should be generated by calling the Machine ID Generator and stored against every new Machine Created
6. If, the data is recieved in secondary language and the data for primary language is not present in the database, the API should not allow creation of the Machine and throw an error message. Refer messages section
7. If in the request, all the mandatory data is received in primary langauge but not in the secondary langauge, API should store the data but mark the Machine as Inactive \(is\_acitve = false\) regardless of what is received in the request for is\_active flag
8. If the request has been received for Deactivating an active machine, and the machine is mapped to a Registration Center, reduce the number of kiosk by 1 for that Registration Center in the Registration Center Master DB.
9. If the request has been received for Activating an Inactive machine, and the machine is mapped to a Registration Center, increase the number of kiosk by 1 for that Registration Center in the Registration Center Master DB.
10. Responds with the appropriate message for the Machine created successfully
11. History record should be stores for every creation of a new Machine
12. The API should restricts the bulk creation of Master Data
13. In case of Exceptions, system triggers error messages as received from the Database. 

#### Update a Machine in the List of Machines Master Database

On receiving a request to update a Machine with the input parameters, the system Updates the Machine Details in the List of Machines Database for the machine\_id received

Refer below for the process:

1. While updating the machine ID the system Validates if all required input parameters have been received as listed below for each specific request
   * machine\_id - character \(36\) - mandatory
   * name - character \(64\) - mandatory
   * mac\_address - character \(64\) - mandatory
   * serial\_num - character \(64\) - mandatory
   * ip\_address- character \(17\) - optional
   * validity\_end\_dtimes - timestamp
   * mspec\_id - character \(36\) - mandatory
   * lang\_code - character \(3\) - mandatory
   * zone\_code - character \(36\) - mandatory
   * is\_active - boolean - mandatory
2. For the machine\_id received in the request, replaces all the data received in the request against the data existing in the List of Registration Center database against the same machine\_id.
3. All the mandatory input parameters should be present 
4. The Zone received should be either same as the Zone mapped of the Administrator or a child zone of the Administrator's Zone
5. The API should not allow activation of Machine if the data for the Machine is not present in all the languages which are configured for a country
6. If in the request, all the mandatory data is received in primary langauge but not in the secondary langauge, API should store the data but mark the Machine as Inactive \(is\_acitve = false\) regardless of what is received in the request for is\_active flag
7. upd\_by should be the Username of the user who is accessing this API
8. upd\_dtimes should be the date-time at which the user is creating the Machine
9. History record should be stores for every modification of a Machine
10. Responds with the Registration Center Code and Language Code for the Machine updated successfully
11. In case of Exceptions, system triggers relevant error messages

#### Decommission a Machine in the List of Machines Master Database

On receiving a request to decommission a Machine with the input parameters \(machine\_id\), the system Updates the is\_deleted flag to true in the List of Machines Database against the machine\_id received

Refer below for the process:

1. While deleting the machine IDs the system Validates if all required input parameters have been received as listed below for each specific request
   * machine\_id - character \(36\) - Mandatory
2. Change the “is\_Deleted” flag against Machine ID to “True”
3. Change the “is\_Active” flag to “False” against the Machine.
4. upd\_by should be the Username of the user who is accessing this API
5. del\_dtimes should be the date-time when the Machine is being decommissioned
6. Validate if the Machine is mapped to the Registration Center
   * If yes, do no decommission the Machine, throw an appropriate error message. Refer “Messages Section”.
7. The User accessing the API should only be able to decommission a Machine under its administrative zone only
8. Responds with the appropriate message for the Machine decommissioned successfully
9. In case of Exceptions, system triggers relevant error messages

#### Fetch Machine Registration/Updation History detail based on a Machine ID and Language Code

Upon receiving a request to fetch Machine History Registration/Updation Detail with the input parameters \(Machine ID, Date and Language Code\), the system Fetches all the attributes of Machine from the history table for the Machine ID, Date and Language Code received

The record fetched is the latest record existing on or before the date received in the input parameter

Refer below for the process:

1. While fetching the machine registration and updation history the system Validates if all required input parameters have been received as listed below for each specific request
   * Machine ID - Mandatory
   * Date - Mandatory
   * Language Code - Mandatory
2. If the mandatory input parameters are missing, throws the appropriate message
3. Validates if the response contains the following attributes for the Machine ID and Language Code Received
   * Machine ID
   * Machine Name
   * Mac Address
   * IP Address
   * Serial Number
   * Machine Spec ID
   * IsActive
4. In case of Exceptions, system triggers relevant error messages

#### Fetch Machine Details based on a Machine ID and a Language Code

On receiving a request to Fetch Machine Details with the input parameters \(Machine ID and Language Code\), the system Fetches all the Machine attributes for the Machine ID and the Language Code Received

Refer below for the process:

1. While fetching the machine IDs the system Validates if all required input parameters have been received as listed below for each specific request
   * Machine ID - Mandatory
   * Language Code
2. If the request has come for fetching all the machine details, responds with all the list of machines
3. If the mandatory input parameters are missing, throws the appropriate message. 
4. Validates if the response contains the following attributes for the Machine ID
   * Machine ID
   * Machine Name
   * Mac Address
   * IP Address
   * Serial Number
   * Machine Spec ID
   * IsActive
5. In case of Exceptions, system triggers relevant error messages. 

### Mappings of Registration Center, Machine and User Mappings

#### Create a mapping record of Center, User and Machine in Center-User-Machine Mapping Master Database

On receiving a request to add a mapping of Center, User and Machine with the input parameters \(regcntr\_id, usr\_id, machine\_id and is\_active\), the system Stores the Mapping of Center, User and Machine in the Database

Refer below for the process:

1. While mapping the system Validates if all required input parameters have been received as listed below for each specific request
   * regcntr\_id - character \(10\) - Mandatory
   * usr\_id- character \(36\) - Mandatory
   * machine\_id - character \(10\) - Mandatory
   * is\_active - boolean - Mandatory
2. Responds with the Center ID, Machine ID ad User ID for the Center, User and Machine mapping created successfully
3. The component restricts the bulk creation of Master Data
4. In case of Exceptions, system triggers error messages as received from the Database.

#### Delete a Center-Machine-User mapping in the Center-Machine-User mapping Master Database

On receiving a request to delete a Center-Machine-User mapping with the input parameters \(regcntr\_id, machine\_id, usr\_id\), the system Updates the is\_deleted flag to true in the Center-Machine-User mapping Database against the input received

Refer below for the process:

1. While deleting the system Validates if all required input parameters have been received as listed below for each specific request
   * regcntr\_id - character \(36\) - Mandatory
   * machine\_id - character \(36\) - Mandatory
   * usr\_id - character \(36\) - Mandatory
2. Responds with the Center ID, Machine ID ad User ID for the Center, User and Machine mapping deleted successfully
3. In case of Exceptions, system triggers relevant error messages. 

#### Fetch Mapping History of Registration Center, Machine and User based on Registration Centre ID, Machine ID, User ID and Date

On receiving a request to fetch Mapping History of Registration, Machine and User with input parameters \(Registration Centre ID, Machine ID, User ID and Date\), the system Fetches all the attributes of Registration, Machine and User Mapping from the history table for the Machine ID and Date received

The record fetched is the latest record existing on or before the date received in the input parameter

Refer below for the process:

1. While fetching the mappings the system Validates if all required input parameters have been received as listed below for each specific request
   * Registration Center ID - Mandatory
   * Machine ID - Mandatory
   * User ID - Mandatory
   * Date - Mandatory
2. If the mandatory input parameters are missing, system throws the appropriate message.
3. Validates if the response contains following attributes
   * Registration Center ID
   * Machine ID
   * User ID
   * IsActive
4. In case of Exceptions, system triggers relevant error messages. 

### List of Devices

#### Create a Device

On receiving request to add a device with the input parameters, the system Stores the device in the Database

Refer below for the process:

1. While creating a device the system Validates if all required input parameters have been received as listed below for each specific request
   * name - character \(64\) - Mandatory
   * mac\_address - character \(64\) - Mandatory
   * serial\_num - character \(64\) - Mandatory
   * ip\_address - character \(17\) - Optional
   * dspec\_id - character \(36\) - Mandatory
   * validity\_end\_date - date - Optional
   * lang\_code - character \(3\) - Mandatory
   * is\_active - boolean - Mandatory
2. The Zone received should be either same as the Zone mapped of the Administrator or a child zone of the Administrator's Zone
3. cr\_by should be the Username of the user who is accessing this API
4. cr\_dtimes should be the date-time at which the user is creating the Device
5. Device ID should be generated by calling the Device ID Generator and stored against every new Device Created
6. If, the data is recieved in secondary language and the data for primary language is not present in the database, the API should not allow creation of the Device and throw an error message. Refer messages section
7. If in the request, all the mandatory data is received in primary langauge but not in the secondary langauge, API should store the data but mark the Device as Inactive \(is\_acitve = false\) regardless of what is received in the request for is\_active flag
8. Responds with the appropriate message for the Device created successfully
9. History record should be stores for every creation of a new Device
10. The API should restricts the bulk creation of Master Data
11. In case of Exceptions, system triggers error messages as received from the Database. 

#### Update a Device

Upon receiving a request update a Device with the input parameters, the system Updates the Device Details in the List of Devices Database for the id received

Refer below for the process:

1. While updating the device in device type list the system Validates if all required input parameters have been received as listed below for each specific request
   * id - character \(36\) - Mandatory
   * name - character \(64\) - Mandatory
   * mac\_address - character \(64\) - Mandatory
   * serial\_num - character \(64\) - Mandatory
   * ip\_address - character \(17\) - Optional
   * dspec\_id - character \(36\) - Mandatory
   * validity\_end\_date - date - Optional
   * lang\_code - character \(3\) - Mandatory
   * is\_active - boolean - Mandatory
2. For the device\_id received in the request, replaces all the data received in the request against the data existing in the List of Registration Center database against the same device\_id.
3. All the mandatory input parameters should be present 
4. The Zone received should be either same as the Zone mapped of the Administrator or a child zone of the Administrator's Zone
5. The API should not allow activation of Device if the data for the Device is not present in all the languages which are configured for a country
6. If in the database, all the mandatory data is present in primary langauge but not in the secondary langauge, API should update the data but mark the Device as Inactive \(is\_acitve = false\) regardless of what is received in the request for is\_active flag
7. upd\_by should be the Username of the user who is accessing this API
8. upd\_dtimes should be the date-time at which the user is creating the Device
9. History record should be stores for every modification of a Device
10. Responds with the Registration Center Code and Language Code for the Device updated successfully
11. In case of Exceptions, system triggers relevant error messages 

#### Decommission a Device

Upon receiving a request to decommission a Device with the input parameters \(id\) and Update the is\_deleted flag to true in the List of Devices Database against the id received

Refer below for the process:

1. While deleting the device in the device list the system validates if all required input parameters have been received as listed below for each specific request
   * id - character \(36\) - Mandatory
2. Change the “is\_Deleted” flag against Device ID to “True”
3. Change the “is\_Active” flag to “False” against the Device.
4. upd\_by should be the Username of the user who is accessing this API
5. del\_dtimes should be the date-time when the Device is being decommissioned
6. Validate if the Device is mapped to the Registration Center
   * If yes, do no decommission the Device, throw an appropriate error message. Refer “Messages Section”.
7. The User accessing the API should only be able to decommission a Device under its administrative zone only
8. Responds with the appropriate message for the Machine decommissioned successfully
9. In case of Exceptions, system triggers relevant error messages

#### Fetch all the List of Devices based on Device Type and Language Code

On receiving request to Fetch list of all Device with the requirement input parameter \(Language Code and/or Device Type\), the system Fetches all the Devices against the Language Code and/or Device Type as requested

Refer below for the process:

1. While fetching the device types the system Validates if the request contains the following input parameters
   * Device Type - Optional
   * Language Code - Mandatory
2. If the mandatory input parameters are missing, system throws the appropriate message. 
3. If the input parameters contain only Language Code:
   * The response contains all the list of devices for all device types against the Languages code received
4. If the input parameters contain both Device Type and Language Code:
   * The response  contains the list of devices against the Languages code for that Device Type only
5. After validation, the above listed parameters system responds with an appropriate message if data does not exist against the Language code/Device Type received. 
6. Validates if the response contains the following attributes for each Device ID, if the input parameters contain only Language Code:
   * Device ID - Mandatory
   * Machine Name - Mandatory
   * Mac Address - Mandatory
   * IP address - Optional
   * Serial Number - Mandatory
   * Device Spec ID - Mandatory
   * IsActive - Mandatory
7. Validates if the response contains the following attributes for each Device ID, if the input parameters contain Device Type and Language Code:
   * Device Type-Mandatory
   * Device ID - Mandatory
   * Machine Name - Mandatory
   * Mac Address - Mandatory
   * IP address - Optional
   * Serial Number - Mandatory
   * Device Spec ID - Mandatory
   * IsActive - Mandatory
8. In case of Exceptions, system triggers relevant error messages. 

#### Fetch Device Registration/Update History detail based on a Device ID and Language Code

On receiving request to fetch Device History Registration/Update Detail with the input parameters \(Device ID, Date and Language Code\), the system fetches all the attributes of Device from the history table for the Device ID, Date and Language Code received

The record fetched is the latest record existing on or before the date received in the input parameter

Refer below for the process:

1. While fetching the device registration and update history the system validates if all required input parameters have been received as listed below for each specific request
   * Device ID - Mandatory
   * Date - Mandatory
   * Language Code - Mandatory
2. If the mandatory input parameters are missing, system throws the appropriate message
3. Validates if the response contains the following attributes for the Device ID and Language Code Received
   * Device ID - Mandatory
   * Device Name - Mandatory
   * Mac Address - Mandatory
   * IP address - Optional
   * Serial Number - Mandatory
   * Device Spec ID - Mandatory
   * Validity Time - Optional
   * Language Code - Mandatory
   * IsActive - Mandatory
4. In case of Exceptions, system triggers relevant error messages. 

### List of Device Specifications

#### Create Device Specifications

On receiving request to add Device Specifications with the input parameters \(name, brand, model, dtype\_code, min\_driver\_ver, descr, lang\_code and is\_active\), the system Stores the Device Specifications in the Database

Refer below for the process:

1. This API should only be accessible to Global Admin
2. The API should accept only the below parameters
   * name - Character - 64 - Mandatory
   * brand - Character - 32 - Mandatory
   * model - Character - 16 - Mandatory
   * dtyp\_code - Character - 36 - Mandatory
   * min\_driver\_version - Character - 16 - Mandatory
   * descr - Character - 256 - Optional
   * lang\_code - Character - 3 - Mandatory
   * is\_active - boolean \(true/false\) - Mandatory
3. All the mandatory input parameter\(s\) should be present in the reqeust. If not, throw an appropriate error message
4. The API should validate the data type and length for each attribute as mentioned above.
5. In case of any failed validation, API should respond with appropriate error message. Refer messages section
6. dtyp\_code received should be from list of 'codes' from device\_type masterdata table
   * If not, the API should throw an error. Refer messages section
7. API should perfrom below multi-language validations on the Device Specification data recieved
8. If, the data is recieved in secondary language and the data for primary language is not present in the database, the API should not allow creation of the Device Specification and throw an error message. Refer messages section
9. If in the request, all the mandatory data is received in primary langauge but not in the secondary langauge, API should store the data but mark the Device Specification as Inactive \(is\_acitve = false\) regardless of what is received in the request for is\_active flag
10. If all the above validations are successfull, the API should store the data the the database
11. Device Specification Id should be generated at the back-end for any Device Specification added using a UUID generator
12. API should store cr\_by as the Username of the user who is accessing this API
13. API should store cr\_dtimes as the date-time at which the user is creating the Device Specification
14. API should only allow creation of one record at a time and should restrict bulk creation
15. API should audit the relevant data when the API is called successfully or when an error is encountered

#### Fetch List of Device Specifications based on a Language Code

On receiving request to fetch the List of Device Specifications with input parameters \(Language Code and/or Device Type\) the system fetches the List of Device Specifications against the Language Code and/or Device Type

While fetching the List of Device Specifications against the Language Code and/or Device Type the system performs the following steps 1. Validates if the request contains the following input parameters

* Language Code - Mandatory
* Device Type - Optional
  1. If the mandatory input parameters are missing, throws the appropriate message. 
  2. If the input parameters contain only Language Code:
* The response contains all the list of device specs against all the devices for the requested Language Code
  1. If the input parameters contain Device Type and Language Code:
* The response contains only the list of device specs against the requested device type for the requested Language Code
  1. Validates if the response contains the List of Device Specifications with the following attributes, if the input parameters contain only Language Code
* Device Specification ID
* Device Name
* Device Brand
* Device Model
* Device Type
* Minimum Driver Version
* IsActive
  1. Validates if the response contains the List of Device Specifications with the following attributes, if the input parameters contain Device Type and Language Code
* Device Type
* Device Specification ID
* Device Name
* Device Brand
* Device Model
* Device Type
* Minimum Driver Version
* IsActive
  1. In case of Exceptions, system triggers relevant error messages

#### Update a Device Specification

On receiving a request to update a Device Specification with the input parameters \(id, name, brand, model, dtype\_code, min\_driver\_ver, descr, lang\_code and is\_active\) the system updates the Device Specification Details in the Device Specification Database for the id received

1. This API should only be accessible to Global Admin
2. The API should accept only the below parameters
   * id - Character - 36 - Mandatory
   * name - Character - 64 - Mandatory
   * brand - Character - 32 - Mandatory
   * model - Character - 16 - Mandatory
   * dtyp\_code - Character - 36 - Mandatory
   * min\_driver\_version - Character - 16 - Mandatory
   * descr - Character - 256 - Optional
   * lang\_code - Character - 3 - Mandatory
   * is\_active - boolean \(true/false\) - Mandatory
3. All the mandatory input parameter\(s\) should be present in the reqeust. If not, throw an appropriate error message
4. The API should validate the data type and length for each attribute as mentioned above.
5. In case of any failed validation, API should respond with appropriate error message. Refer messages section
   * dtyp\_code received should be from list of 'codes' from device\_type masterdata table
6. If not, the API should throw an error.
7. If all the above validations are successfull, the API should update the data in the database agianst the id received
8. API should perfrom below multi-language validations on the Device Specification data recieved
9. If in the database, all the mandatory data is present in primary langauge but not in the secondary langauge, API should update the data but mark the Device Specification as Inactive \(is\_acitve = false\) regardless of what is received in the request for is\_active flag
10. API should store upd\_by as the Username of the user who is accessing this API
11. API should store upd\_dtimes as the date-time at which the user is modiying the Device Specification details
12. API should only allow creation of one record at a time and should restrict bulk creation
13. API should audit the relevant data when the API is called successfully or when an error is encountered

### List of Device Types

#### Create Device Type

Upon receiving a request to add Device Type with the input parameters \(code, name, descr, lang\_code and is\_active\), the system Stores the Device Type in the Database

Refer below for the process:

1. This API should only be accessible to Global Admin
2. The API should accept only the below parameters
   * name - Character - 64 - Mandatory
   * descr - Character - 128 - Optional
   * lang\_code - Character - 3 - Mandatory
   * is\_active - boolean \(true/false\) - Mandatory
3. All the mandatory input parameter\(s\) should be present in the reqeust. If not, throw an appropriate error message
4. The API should validate the data type and length for each attribute as mentioned above.
5. In case of any failed validation, API should respond with appropriate error message. Refer messages section
6. API should perfrom below multi-language validations on the Device Type data recieved
7. If, the data is recieved in secondary language and the data for primary language is not present in the database, the API should not allow creation of the Device Type and throw an error message. Refer messages section
8. If in the request, all the mandatory data is received in primary langauge but not in the secondary langauge, API should store the data but mark the Device Type as Inactive \(is\_acitve = false\) regardless of what is received in the request for is\_active flag
9. If all the above validations are successfull, the API should store the data the the database
10. Device Type Code should be generated at the back-end for any Device Type added using a UUID generator
11. API should store cr\_by as the Username of the user who is accessing this API
12. API should store cr\_dtimes as the date-time at which the user is creating the Device Type
13. API should only allow creation of one record at a time and should restrict bulk creation
14. API should audit the relevant data when the API is called successfully or when an error is encountered 

#### Update Device Type

1. This API should only be accessible to Global Admin
2. The API should accept only the below parameters
   * code - Character - 36 - Mandatory
   * name - Character - 64 - Mandatory
   * descr - Character - 128 - Optional
   * lang\_code - Character - 3 - Mandatory
   * is\_active - boolean \(true/false\) - Mandatory
3. All the mandatory input parameter\(s\) should be present in the reqeust. If not, throw an appropriate error message
4. The API should validate the data type and length for each attribute as mentioned above.
5. In case of any failed validation, API should respond with appropriate error message. Refer messages section
6. If all the above validations are successfull, the API should update the data in the database agianst the code received
7. API should perfrom below multi-language validations on the Device Type data recieved
8. If in the database, all the mandatory data is present in primary langauge but not in the secondary langauge, API should update the data but mark the Device Type as Inactive \(is\_acitve = false\) regardless of what is received in the request for is\_active flag
9. API should store upd\_by as the Username of the user who is accessing this API
10. API should store upd\_dtimes as the date-time at which the user is modiying the Device Type details
11. API should only allow creation of one record at a time and should restrict bulk creation
12. API should audit the relevant data when the API is called successfully or when an error is encountered

### Mappings of Registration Center and Machine

#### Create a mapping record of Machine and Center

Upon receiving a request to add a mapping of Machine and Center with the input parameters \(regcntr\_id, machine\_id, and is\_active\), the system stores the Mapping of Machine and Center in the Database

Refer below for the process:

1. Validates if all required input parameters have been received as listed below for each specific request
   * regcntr\_id - character \(10\) – Mandatory \(refers to a Registration Center stored in Registration Center\)
   * machine\_id - character \(10\) – Mandatory \(refers to a Machine stored in Machine Masterdata\)
   * is\_active - boolean - Mandatory
2. Validate if the Registration Center belongs to the Zone of Admin or belongs to a child Zone of the Admin's Zone
3. Validate if the Registration Center belongs to the Zone of Machine or belongs to a child Zone of the Machine's Zone
4. Validate if the Machine belongs to the Zone of Admin or belongs to a child Zone of the Admin's Zone
5. Validate if the Registration Center and Machine received are not in decommissioned state
6. If the above conditions in point 2, 3, 4 and 5 are not met, throw respective error messages. Refer messages section
7. If the Machine ID is already mapped to another Registration Center ID and the mapping is Active, throw an appropriate error
8. If the mapping is Inactive, create the new mapping
9. Store the default language code against the mapping
10. If the Registration Center ID - Machine ID mapping already exist but is in Inactive state, re-activate the mapping
11. In case of Exceptions/Success, system should trigger relevant messages. Refer “Messages” sectione. 

#### Delete a Center-Machine mapping

Upon receiving a request to delete a Center-Machine mapping with the input parameters \(regcntr\_id, machine\_id\), the system updates the is\_active flag to false in the Center-Machine mapping Database against the input received

Refer below for the process:

1. Validates if all required input parameters have been received as listed below for each specific request
   * regcntr\_id - character \(36\) - Mandatory
   * machine\_id - character \(36\) - Mandatory
2. Validate if the Registration Center belongs to the Zone of Admin or belongs to a child Zone of the Admin's Zone
3. Validate if the Machine belongs to the Zone of Admin or belongs to a child Zone of the Admin's Zone
4. If the above conditions in point 3 and 4 are not met, throw respective error messages. Refer messages section
5. If the mapping does not exist or is in inactive state, throw an appropriate error
6. In case of Exceptions/Success, system should trigger relevant messages. Refer “Messages” section

### Mappings of Registration Center and Device

#### Create a mapping record of Device and Center

Upon receiving a request to add a mapping of Device and Center with the input parameters \(regcntr\_id, device\_id\), the system stores the Mapping of Device and Center in the Database

Refer below for the process:

1. Validates if all required input parameters have been received as listed below for each specific request
   * regcntr\_id - character \(10\) – Mandatory \(refers to a Registration Center stored in Registration Center\)
   * device\_id - character \(36\) – Mandatory \(refers to a Device stored in Device Masterdata\)
2. Validate if the Registration Center belongs to the Zone of Admin or belongs to a child Zone of the Admin's Zone
3. Validate if the Registration Center belongs to the Zone of Device or belongs to a child Zone of the Device's Zone
4. Validate if the Device belongs to the Zone of Admin or belongs to a child Zone of the Admin's Zone
5. Validate if the Registration Center and Device received are not in decommissioned state
6. If the above conditions in point 2, 3, 4 and 5 are not met, throw respective error messages. Refer messages section
7. If the Device ID is already mapped to another Registration Center ID and the mapping is Active, throw an appropriate error
8. If the mapping is Inactive, create the new mapping
9. Store the default language code against the mapping
10. If the Registration Center ID - Device ID mapping already exist but is in Inactive state, re-activate the mapping
11. In case of Exceptions/Success, system should trigger relevant messages. Refer “Messages” section

#### Unmap a Center-Device mapping

Upon receiving a request to delete a Center-Device mapping with the input parameters \(regcntr\_id, device\_id\), the system updates the is\_active flag to false in the Center-Device mapping Database against the input received

Refer below for the process:

1. Validates if all required input parameters have been received as listed below for each specific request
   * regcntr\_id - character \(36\) - Mandatory
   * device\_id - character \(36\) - Mandatory
2. Validate if the Registration Center belongs to the Zone of Admin or belongs to a child Zone of the Admin's Zone
3. Validate if the Device belongs to the Zone of Admin or belongs to a child Zone of the Admin's Zone
4. If the above conditions in point 3 and 4 are not met, throw respective error messages. Refer messages section

   5 If the mapping does not exist or is in inactive state, throw an appropriate error

5. In case of Exceptions/Success, system should trigger relevant messages. Refer “Messages” section

#### Fetch Device-Center History record based on the timestamp received

On receiving a request to fetch Mapping History of Center and Device with input parameters \(Registration Center ID, Device ID and Date Timestamp\) the system fetches all the attributes of Center and Device Mapping from the history table for the Registration Center ID, Device ID and Date received

The record fetched is the latest record existing on or before the date received in the input parameter

While fetching the attributes of Center and Device Mapping from the history table the system performs the following steps

1. Validates if all required input parameters have been received as listed below for each specific request
   * Registration Center ID - Mandatory
   * Device ID - Mandatory
   * Date Timestamp - Mandatory
2. If the mandatory input parameters are missing, throws the appropriate message. 
3. Validates if the response contains following attributes
   * Registration Center ID
   * Device ID
   * IsActive
   * Effective date
4. In case of Exceptions, system triggers relevant error messages

### Mappings of Registration Center, Machine, and Device

#### Create a mapping record of Center, Machine and Device

Upon receiving a request to add a mapping of Center, Machine and Device with the input parameters \(regcntr\_id, machine\_id, device\_id, and is\_active\), the system stores the Mapping of Center, Machine and Device in the Database

Refer below for the process:

1. Validates if all required input parameters have been received as listed below for each specific request
   * regcntr\_id - character \(36\) – Mandatory \(refers to a Registration Center stored in Registration Center Masterdata\)
   * machine\_id - character \(36\) – Mandatory \(refers to a Registration Center stored in Registration Center Masterdata\)
   * device\_id - character \(36\) – Mandatory \(refers to a Device stored in Device Masterdata\)
   * is\_active - boolean - Mandatory
2. Responds with the Device Id, Machine ID and Center ID for the mapping of Center, Machine and Device created successfully
3. The component restricts the bulk creation of Master Data
4. In case of Exceptions, system triggers error messages as received from the Database. 

#### Delete a Center-Machine-Device mapping

Upon receiving a request to delete a Center-Machine-Device mapping with the input parameters \(regcntr\_id, machine\_id, device\_id\), the system updates the is\_deleted flag to true in the Center-Machine-Device mapping Database against the input received

Refer below for the process:

1. Validates if all required input parameters have been received as listed below for each specific request
   * regcntr\_id - character \(36\) - Mandatory
   * machine\_id - character \(36\) - Mandatory
   * device\_id - character \(36\) - Mandatory
2. Deleted record are not be deleted again
3. Responds with data not found error if deleted record is received in the request
4. Responds with the Device Id, Machine ID and Center ID for the mapping of Center, Machine and Device deleted successfully
5. In case of Exceptions, system triggers relevant error messages. 

### Mappings of Registration Center and User

#### Create a mapping record of User and Center

Upon receiving a request to add a mapping of User and Center with the input parameters \(regcntr\_id, usr\_id, and is\_active\), the system stores the Mapping of User and Center in the Database

Refer below for the process:

1. Validates if all required input parameters have been received as listed below for each specific request
   * regcntr\_id - character \(10\) – Mandatory \(refers to a Registration Center stored in Registration Center\)
   * usr\_id - character \(36\) – Mandatory \(refers to a User stored in User Masterdata\)
   * is\_active - boolean - Mandatory
2. Validate if the Registration Center belongs to the Zone of Admin or belongs to a child Zone of the Admin's Zone
3. Validate if the Registration Center belongs to the Zone of User or belongs to a child Zone of the User's Zone
4. Validate if the User belongs to the Zone of Admin or belongs to a child Zone of the Admin's Zone
5. Validate if the Registration Center and User received are not in decommissioned state
6. If the above conditions in point 2, 3, 4 and 5 are not met, throw respective error messages. Refer messages section
7. If the User ID is already mapped to another Registration Center ID and the mapping is Active, throw an appropriate error
8. If the mapping is Inactive, create the new mapping
9. Store the default language code against the mapping
10. If the Registration Center ID - User ID mapping already exist but is in Inactive state, re-activate the mapping
11. In case of Exceptions/Success, system should trigger relevant messages. Refer “Messages” section

#### Delete a Center-User mapping

Upon receiving a request to delete a Center-User mapping with the input parameters \(regcntr\_id, usr\_id\), the system updates the is\_active flag to false in the Center-User mapping Database against the input received

Refer below for the process:

1. Validates if all required input parameters have been received as listed below for each specific request
   * regcntr\_id - character \(36\) - Mandatory
   * usr\_id - character \(36\) - Mandatory
2. Validate if the Registration Center belongs to the Zone of Admin or belongs to a child Zone of the Admin's Zone
3. Validate if the User belongs to the Zone of Admin or belongs to a child Zone of the Admin's Zone
4. If the above conditions in point 3 and 4 are not met, throw respective error messages. Refer messages section
5. If the mapping does not exist or is in inactive state, throw an appropriate error
6. In case of Exceptions/Success, system should trigger relevant messages. Refer “Messages” section

## MISP Management

### License Key Allocation

#### Create MISP

1. The system receives a request to create a MISP with input parameters \(MISP ID, MISP Organization Name, MISP Contact Number, MISP Email ID, MISP Address, MISP User name, MISP Password, MISP License Key, MISP License Key Status, IsActive\)
2. Stores the data in the database
3. Responds to the source with the required message
4. If the mandatory input parameters are missing, throws the appropriate message. 
5. In case of exceptions, system triggers relevant error messages. 

#### Read MISP

1. The system receives a request to fetch a MISP with input parameters \(MISP ID and/or MISP Organization Name\)
2. Fetches the data existing against the input parameter received. 
3. If only MISP ID is received, fetches data against the MISP ID from the database
4. If MISP Organization Name is received, fetches data against the MISP Organization Name from the database
5. If both MISP ID and MISP Organization Name is received, fetches data against the combination of both the input parameters \(Complete match of Org name and MISP ID\)
6. Fetches only active data from the database
7. If the input parameter received is null or empty, fetches all the data
8. If the mandatory input parameters are missing, throws the appropriate message. 
9. If the data does not exist for input parameters received, throws the appropriate message. 
10. In case of Exceptions, system triggers relevant error messages. 

#### Update MISP

1. The system receives a request to update a MISP with input parameters \(MISP ID, MISP Organization Name, MISP Contact Number, MISP Email ID, MISP Address, MISP User name, MISP Password, MISP License Key, MISP License Key Status, IsActive
2. Updates the data and Responds to the source with the required message
3. MISP ID will serves as search criteria to update the record in the database
4. The system updates the data received against the data already existing in the database against the MISP ID received
5. If the mandatory input parameters are missing, throws the appropriate message. 
6. In case of Exceptions, system triggers relevant error messages. 

#### Delete MISP

1. The system receives a request to delete a MISP with input parameters \(MISP ID\)
2. Deletes the data as mentioned as requested
3. Responds to the source with the required message
4. If the mandatory input parameters are missing, throws the appropriate message.
5. In case of exceptions, system triggers relevant error messages. 

