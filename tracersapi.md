FORMAT: 1A
HOST: https://api.galaxysearchapi.com/

# Tracers Search

Performs a criteria search, and returns a list of matching people.

## Are you an API partner?

If you are an API partner then please start here. This section of the documentation outlines the specific elements related to the various searches that we provide to partners.

### Getting Started

You should have an API access profile user and password that was supplied to you by your account manager. If you do not have an access profile user and password, then please contact your account manager. If you do have an access profile user and password then please continue reading.

Your access profile user and password is used for authenticating all requests to our search API. You <strong>MUST</strong> pass the user and password each time you perform a search request. Access profiles determines the types of searches that an API partner has access to as well as the specific data elements that are returned with each search type. The access profile also defines whether or not various data elements are masked or if counts are limited (For example, a teaser result, we may only provide 5 relatives with masked names. In the actual person search you will get all relatives with no name masking). 

Please note that you do not need to pass in any includes or filters with your API call. For API partners, the includes and filters are pre-set, so any data elements/includes that are configured on your access profile will be returned in the repsonse.

### Search Types

We provide various search types to our API partners. If you are working with our API and receive the message "You do not have access to this search type", then your access profile is not configured to allow you to execute this search type. If you would like access to additional search types, please contact your account manager.  

The following search types are supported in our API:

1. Person Searches
    * <strong>Teaser</strong> - This search type is used to "entice/tease" customers with data, but not too much data. This is mainly used for what we refer to as "logged out" users. Most of the data elements in a teaser search are masked and/or limited by the quantity returned. This should be used as your initial search before drilling down to the specific user information.
    * <strong>Person</strong> - This search type should be used for more detailed information pertaining to the subjects. This is mainly used for "logged in or paying" users.
    * <strong>BackgroundReport</strong> - This search type is used to drill down to a specific subject and run a background report on them. A background report can include many data elements. The data elements contained in a background report depend on how your access profile is configured. Typically a background report contains all addresses, emails, phones, relatives/associates, property records, criminal records etc. If you are not seeing data elements in your background reports that you need access to, please contact your account manager. 
    
    <strong><i>IMPORTANT: Please make sure you pass in a specific Tahoe Id or the person's name and DOB when performing background reports. You will see a significant decrease in performance if you are performing background reports with vague search criteria.</i></strong>
            
2. Reverse Phone Searches (Please note that this is a person search as well, but can be configured differently in you API access profile. For example, we may setup your reverse phone to return results based on the most current owner of the phone being search on...and your person search may be configured to return your results based on the person name and most recent address)
    * <strong>ReversePhonePersonTeaser</strong>- This search type is used to "entice/tease" customers with data, but not too much data. This is mainly used for what we refer to as "logged out" users. Most of the data elements in a teaser search are masked and/or limited by the quantity returned. This should be used as your initial search before drilling down to the specific user information.
    * <strong>ReversePhonePerson</strong> - This search type should be used for more detailed information pertaining to the subjects. This is mainly used for "logged in or paying" users.

3. Other Searches
    * If you would like to perform and independant record search other than a person search, please refer to the search section in navigation bar located to the left of this page. These section conain the specific includes, filters and supported search types such as Criminal Searches, Workplace Searches, Marriage Searches etc.

## Person Search [/PersonSearch]

Performs a person search, and returns a list of people matching the search criteria. Person Search is a flexible tool that allows users to search for data in a variety of ways. In section 2 there is a list of all available search inputs for person search. You can use this search as a standard person search by ssn, name/dob, name/address. You can also use this search to reverse emails, phones, and addresses.

### Search [POST]
***Click on the grey search box above, to view sample request/response objects for the Person Search.***

Perform a search:
1. Add your Access Profile username and password to the request headers.
    * galaxy-ap-name: [Access Profile Name]
    * galaxy-ap-password: [Access Profile Password]
    * galaxy-client-session-id: (Optional) Session ID for logging
    * galaxy-client-type: [Galaxy Client Type] (required for Javascript clients)
    * galaxy-search-type: [Galaxy Search Type] (optional)
        * To auto-populate all includes and filter options in your requests (**default includes listed below search type**), you must provide a search type value in your request header. If additional includes are required please reach out to your account rep. You can reference the full list of available includes in the defined schema below. Applicable search type values and default includes for this endpoint are as follows: 
            1. Teaser
                * `Addresses`
                * `Akas`
                * `AssociatesSummary`
                * `DatesOfDeath`
                * `DeathRecords`
                * `EmailAddresses`
                * `MergedNames`
                * `RelativesSummary`
            2. Person
                * `Addresses`
                * `Akas`
                * `Associates`
                * `AssociatesSummary`
                * `DatesOfDeath`
                * `DeathRecords`
                * `EmailAddresses`
                * `MergedNames`
                * `PhoneNumbers`
                * `RelativesSummary`
                * `TahoeAddressPhones`
                * `Indicators`
            3. BackgroundReport
                * `Addresses`
                * `Akas`
                * `Associates`
                * `AssociatesSummary`
                * `BusinessRecords`
                * `DatesOfBirth`
                * `DatesOfDeath`
                * `DeathRecords`
                * `DebtV2Records`
                * `EmailAddresses`
                * `EvictionRecords`
                * `ForeclosureRecords`
                * `MergedNames`
                * `Neighbors`
                * `NeighborSummaryRecords`
                * `PhoneNumbers`
                * `ProfessionalLicenseRecords`
                * `PropertyRecords`
                * `Relatives`
                * `RelativesSummary`
                * `WorkPlace`
                * `Domain`
                * `TahoeAddressPhones`
                * `Marriage`
                * `Divorce`
                * `FeinRecords`
                * `CriminalV2Records`
                * `DeaRecords`
                * `Indicators`
            4. ReversePhonePersonTeaser   
                * `Addresses`
                * `Akas`
                * `Associates`
                * `AssociatesSummary`
                * `DatesOfDeath`
                * `DeathRecords`
                * `EmailAddresses`
                * `MergedNames`
                * `PhoneNumbers`
                * `RelativesSummary`
                * `TahoeAddressPhones`
                * `Indicators`
            5. ReversePhonePerson  
                * `Addresses`
                * `Akas`
                * `Associates`
                * `AssociatesSummary`
                * `DatesOfDeath`
                * `DeathRecords`
                * `EmailAddresses`
                * `MergedNames`
                * `PhoneNumbers`
                * `RelativesSummary`
                * `TahoeAddressPhones`
                * `Indicators`
            
2. Add search criteria to your request: (Person Search can be run by a variety of inputs. For Example it can be run by a combination of inputs or by single inputs such as SSN, Email, Phone, or Address)
    ```
    {
        "FirstName": "",
        "MiddleName": "",
        "LastName": "",
        "DOB": "",
        "Age": "".
        "AgeRangeMinAge": "",
        "AgeRangeMaxAge": "",
        "Email": "",
        "Phone": "",
        "SSN": "",
        "TahoeID": "",
        "Domain": "",
        "AddressLine1: "",
        "AddressLine2: "",
        
    }
    ```
3. Select the data types you would like to receive in the output (i.e. the Includes):
    ```
    {
        "FirstName": "John",
        "MiddleName": "J",
        "LastName": "Smith",
        "Dob": "1/1/1980",
        "Includes": ["Addresses", "PhoneNumbers"] - <i>Please note, includes do not apply to API partners. Includes are configured at the access profile level and will autmotically be applied.</i>
    }
    ```
4. Select any desired data filters:
    ```
    {
        "FirstName": "John",
        "MiddleName": "J",
        "LastName": "Smith",
        "Dob": "1/1/1980",
        "Includes": ["Addresses", "PhoneNumbers"],
        "FilterOptions": ["IncludeLowQualityAddresses"] - <i>Please note, filters do not apply to API partners. Includes are configured at the access profile level and will autmotically be applied.</i>
    }
    ```
5. Set the desired pagination rules:
    ```
    {
        "FirstName": "John",
        "MiddleName": "J",
        "LastName": "Smith",
        "Dob": "1/1/1980",
        "Includes": ["Addresses", "PhoneNumbers"], - <i>Please note, includes do not apply to API partners. Includes are configured at the access profile level and will autmotically be applied.</i>
        "FilterOptions": ["IncludeLowQualityAddresses"], - <i>Please note, filters do not apply to API partners. Includes are configured at the access profile level and will autmotically be applied.</i>
        "Page": 1,
        "ResultsPerPage": 10
    }
    ```
6. Submit your search.

A complete list of JSON request properties follows:

* `FirstName` = null (optional, string) ... First name.
* `MiddleName` = null (optional, string) ... Middle name or middle initial.
* `LastName` = null (optional, string) ... Last name.
* `Akas` = null (optional, Name[]) ... Alternative names.
* `Dob` = null (optional, string) ... Date of birth (format: MM/DD/YYYY).
* `Age` = null (optional, int) ... Age.
* `AgeRangeMinAge` = null (optional, int) ... Age range minimum.
* `AgeRangeMaxAge` = null (optional, int) ... Age range maximum.
* `AgeRange` = null (optional, string) ... Age range (format: ## - ##).
* `Ssn` = null (optional, string) ... Social security number (format: ###-##-####).
* `Addresses` = null (optional, Addresses[]) ... List of addresses.
    * Members
        * `AddressLine1` = null (optional, string) ... House number and street name or PO Box (i.e. 1821 Q Street).
        * `AddressLine2` = null (optional, string) ... State or City and State or Zip (i.e. Sacramento, CA).
        * `Unit` = null (optional, string) ... Unit number (i.e. Unit 102).
* `County` = null (optional, string) ... County.            
* `Email` = null (optional, string) ... E-mail address.
* `Phone` = null (optional, string) ... Phone number (formats: ###-###-####, (###) ###-####).
* `Relatives` = null (optional, Name[]) ... List of names of relatives.
* `TahoeIds` = null (optional, string[]) ... Tahoe IDs
* `DPPAUsecode` = null (optional, string[]) ... DPPA Use Code. Required if using the <strong>AutoRecords</strong> include. Valid values are: 1 = Government, 2 = Law Enforcement, 3 = Parking, 4 = Verify Fraud/Debt, 5 = Verify Fraud/Debt (Plate), 6 = Investigate for Litigation, 7 = Insurance Claims, 8 = Insurance Underwriting, 9 = Towed and Impounded, 10 = Private Toll

<i><strong>If you are an API partner</strong> and are missing any include/members listed below, then please contact our revenue department so we can adjust your access profile configuration.</i>

* `Includes` (optional, string[]) ... Data to be included in the response.
    * Members
        * `Addresses`
        * `Akas`
        * `Associates` (requires `AssociatesSummary`)
        * `AssociatesSummary`
        * `AutoRecords` (requires `DPPAUsecode` to be passed in the request)
        * `BusinessRecords`
        * `BusinessSummaryRecords`
        * `CensusRecords`
        * `ConsumerProfiles`
        * `CriminalV2Records`
        * `DatesOfBirth`
        * `DatesOfDeath`
        * `DeathRecords`
        * `DebtSummaryRecords`
        * `DebtRecordsV2`
        * `Divorce`
        * `Domain`
        * `EmailAddresses`
        * `EvictionRecords`
        * `FeinRecords`
        * `ForeclosureRecords`
        * `Indicators`
        * `Marriage`
        * `MergedNames`
        * `Neighbors`
        * `NeighborSummaryRecords`
        * `PhoneNumbers`
        * `ProfessionalLicenseRecords`
        * `PropertyRecords`
        * `PropertySummaryRecords`
        * `Relatives` (requires `RelativesSummary`)
        * `RelativesSummary`
        * `SocialSecurityNumbers`
        * `TahoePhoneAddresses`
        * `VehicleRegistrations`
        * `Workplace`
        * `WorldWarTwoRecords`
        
<i><strong>If you are an API partner</strong> you <strong>DO NOT</strong> need to pass these includes or filters. These items are pre-configured on your access profile. If you are missing one of these data elements or would like to enable or disable a filter, then please contact our revenue department so we can adjust your access profile configuration.</i>
        
* `FilterOptions` (optional, string[]) ... Data filtering options.
    * Members
        * `DisableFirstNameSynonymMatching`
        * `DisableSmartSearch`
        * `IncludePrivateData`
        * `IncludeOptOutData`
        * `IncludeEmptyFirstNameResults`
        * `IncludeSevenDigitPhoneNumbers`
        * `IncludeLowQualityAddresses`
        * `IncludeVendorNameInSources`
        * `IncludeFullSsnValues`
        * `IncludeSources`
        * `IncludeResultsWithMinimalData`
        * `IncludeLatestRecordOnly`
        
* `ResultSort` (optional, string) ... How the final results must be sorted.
    * Members
        * `TahoeRanking`
        * `ClosestDob`
        * `PhoneSearchRanking`
* `NameSort` (optional, string) ... How names must be sorted.
    * Members
        * `TahoeNameRank`
        * `BestQuality`
        * `MatchSearchInput`
        * `All`
* `AddressSort` (optional, string) ... How addresses must be sorted.
    * Members
        * `Default`
        * `MatchSearchInput`
        * `TahoeRanking`
        * `BestQuality`
* `Page` = 1 (optional, int) ... The page of data to return.
* `ResultsPerPage` = 10 (optional, int) ... The number of results to return per page.

<h2>Identifying New Data</h2>
The Galaxy API provides a field at the root level of each name, address and phone record called PublicFirstSeenDate. This property can be used to determine if the name, address or phone was recently added to the database. Please refer to the sample below:

* Code sample to show "New Data" flag/label for a new address (120 days or newer):
    
<strong>Sample address JSON</strong>
   

    
    
    i.e. Where minDate = PublicFirstSeenDate (10/8/2018)
    
    Sample C# Code:
    
    {
        Addresses: [
        {
            IsDeliverable: true,
            IsMergedAddress: false,
            AddressQualityCodes: [],
            AddressHash: "-524222733570250630",
            HouseNumber: "8124",
            StreetPreDirection: "",
            StreetName: "Gloriann",
            StreetPostDirection: "",
            StreetType: "Way",
            Unit: "",
            UnitType: null,
            City: "Antelope",
            State: "CA",
            County: "Sacramento",
            Zip: "95843",
            Zip4: "4836",
            Latitude: "38.717414",
            Longitude: "-121.370000",
            AddressOrder: 1,
            FirstReportedDate: "4/3/2016",
            LastReportedDate: "10/8/2018",
            PublicFirstSeenDate: 10/1/2018,
            TotalFirstSeenDate: "12/6/2016",
            PhoneNumbers: [1 item],
            Neighbors: [],
            NeighborSummaryRecords: [],
            FullAddress: "8124 Gloriann Way; Antelope, CA 95843-4836",
            Sources: {2 items}
        }
        ]   
    }
    
    private bool IsNewData(string minDate)
    {   
        const int Max_Days = -120;

        if(string.IsNullOrEmpty(minDate))
    {
    return false;
    }

    if(!string.IsNullOrEmpty(minDate))
    {
        DateTime dt = DateTime.MinValue;

        DateTime.TryParse(minDate, out dt);

    if(dt>DateTime.Now.AddDays(Max_Days))
    {
        return true;
    }

    }

    return false;

    }

+ Request (application/json)

    + Headers
            
                galaxy-ap-name: Access Profile Name
                galaxy-ap-password: Access Profile Password
                galaxy-client-session-id: APIARY
                galaxy-client-type: Galaxy Client Type

    + Body

            {
                "FirstName": "John",
                "MiddleName": "J",
                "LastName": "Smith",
                "Dob": "1/1/1980",
                "Includes": ["Addresses", "PhoneNumbers"],
                "FilterOptions": ["IncludeLowQualityAddresses"],
                "Page": 1,
                "ResultsPerPage": 10
            }

+ Response 200 (application/json)

            {
                TahoeId : "G2079364443230568704",
                Name : {
                    Prefix : "",
                    FirstName : "John",
                    MiddleName : "",
                    LastName : "Smith",
                    Suffix : ""
                },
                IsPublic : true,
                IsOptedOut : false,
                Addresses : [{
                        IsDeliverable : true,
                        IsMergedAddress : false,
                        AddressQualityCodes : [],
                        AddressHash : "-555557771286295555",
                        HouseNumber : "555",
                        StreetPreDirection : "",
                        StreetName : "Main",
                        StreetPostDirection : "",
                        StreetType : "",
                        Unit : "",
                        UnitType : null,
                        City : "Springfield",
                        State : "CA",
                        Zip : "55555",
                        Zip4 : "5555",
                        Latitude : ".000000",
                        Longitude : ".00000",
                        FirstReportedDate : null,
                        LastReportedDate : null,
                        FullAddress : "1347 Cmr 416; Apo, AE 09140-0014"
                    }
                ],
                PhoneNumbers : [{
                        phoneNumber : "(912) 332-4762",
                        company : "New Cingular Wireless PCS LLC - GA",
                        location : "",
                        phoneType : "Wireless",
                        IsConnected : false,
                        latitude : "55.5555",
                        longitude : "-55.55555"
                    }, {
                        phoneNumber : "(555) 555-5555",
                        company : "CenturyTel of Alabama LLC (Southern) dba CenturyLink",
                        location : "",
                        phoneType : "LandLine/Services",
                        IsConnected : false,
                        latitude : "55.5555",
                        longitude : "-55.55555"
                    }
                ],
                RawData : "",
                FullName : "John Smith"
            }

+ Request (application/json)

    + Headers

            galaxy-ap-name: Access Profile Name
            galaxy-ap-password: Access Profile Password
            galaxy-client-session-id: APIARY

    + Body

            {
                "FirstName": "John",
                "LastName": "Smith",
                "Addresses": [
                    {
                        "HouseNumber": "1234",
                        "Street": "Main",
                        "Unit": "4",
                        "City": "Springfield",
                        "State": "IL",
                        "Zip": "55555"
                    },
                    {
                        "AddressLine1": "1234 Main St.",
                        "AddressLine2": "Springfield, IL 55555"
                    }
                ],
                "Includes": ["Addresses", "PhoneNumbers"],
                "Page": 1,
                "ResultsPerPage": 10
            }

+ Response 200 (application/json)

            {
                TahoeId : "G2079364443230568704",
                Name : {
                    Prefix : "",
                    FirstName : "John",
                    MiddleName : "",
                    LastName : "Smith",
                    Suffix : ""
                },
                IsPublic : true,
                IsOptedOut : false,
                Addresses : [{
                        IsDeliverable : true,
                        IsMergedAddress : false,
                        AddressQualityCodes : [],
                        AddressHash : "-555557771286295555",
                        HouseNumber : "555",
                        StreetPreDirection : "",
                        StreetName : "Main",
                        StreetPostDirection : "",
                        StreetType : "",
                        Unit : "",
                        UnitType : null,
                        City : "Springfield",
                        State : "CA",
                        Zip : "55555",
                        Zip4 : "5555",
                        Latitude : ".000000",
                        Longitude : ".00000",
                        FirstReportedDate : null,
                        LastReportedDate : null,
                        FullAddress : "1347 Cmr 416; Apo, AE 09140-0014"
                    }
                ],
                PhoneNumbers : [{
                        phoneNumber : "(912) 332-4762",
                        company : "New Cingular Wireless PCS LLC - GA",
                        location : "",
                        phoneType : "Wireless",
                        IsConnected : false,
                        latitude : "55.5555",
                        longitude : "-55.55555"
                    }, {
                        phoneNumber : "(555) 555-5555",
                        company : "CenturyTel of Alabama LLC (Southern) dba CenturyLink",
                        location : "",
                        phoneType : "LandLine/Services",
                        IsConnected : false,
                        latitude : "55.5555",
                        longitude : "-55.55555"
                    }
                ],
                RawData : "",
                FullName : "John Smith"
            }
    

## Business Search [/BusinessSearch]

Performs a criteria search, and returns a list of matching businesses.

### Search [POST]
***Click on the grey search box above, to view sample request/response objects for the Business Search.***

Perform a search:
1. Add your Access Profile username and password to the request headers.
    * galaxy-ap-name: [Access Profile Name]
    * galaxy-ap-password: [Access Profile Password]
    * galaxy-client-session-id: (Optional) Session ID for logging
    * galaxy-client-type: [Galaxy Client Type] (required for Javascript clients)
    * galaxy-search-type: [Galaxy Search Type] (optional)
        * To auto-populate all includes and filter options in your requests, you may provide a search type value in your request header. A search type is required for all API Customers. Applicable search type values for this endpoint include: 
            1. Business
2. Add search criteria to your request:
    ```
    {
        "FirstName": "John",
        "LastName": "Smith",
        "Dob": "1/1/1975"
    }
    ```
3. Set the desired pagination rules:
    ```
    {
        "FirstName": "John",
        "LastName": "Smith",
        "Dob": "1/1/1975",
        "Page": 1,
        "ResultsPerPage": 10
    }
    ```
4. Submit your search.

A complete list of JSON request properties follows:

    * `BusinessName` = null (optional, string) ... Business name.
    * `BusinessType` = null (optional, string) ... Business type.
    * `FirstName` = null (optional, string) ... First name.
    * `MiddleName` = null (optional, string) ... Middle name or middle initial.
    * `LastName` = null (optional, string) ... Last name.
    * `AddressLine1` = null (optional, string) ... Address line 1 (house number, street, state).
    * `HouseNumber` = null (optional, string) ... House number.
    * `Street` = null (optional, string) ... Street name.
    * `City` = null (optional, string) ... City.
    * `State` = null (optional, string) ... State (2-character code).
    * `Zip` = null (optional, string) ... Zip code (5-digit code).
    * `BusinessSearchId` (optional, string) ... Poseidon ID.
    * `Includes` (optional, string[]) ... Data to be included in the response.
        * Members
            * `DatabaseQueryInfo`
    * `Page` = 1 (optional, int) ... The page of data to return.
    * `ResultsPerPage` = 10 (optional, int) ... The number of results to return per page.

+ Request (application/json)

    + Headers

            galaxy-ap-name: Access Profile Name
            galaxy-ap-password: Access Profile Password
            galaxy-client-session-id: APIARY
            galaxy-client-type: Galaxy Client Type

    + Body

            {
                "BusinessName": "Hot dog stand",
                "Page": 1,
                "ResultsPerPage": 10
            }

+ Response 200 (application/json)

            {
                "PoseidonId" : "555557831",
                "SourceType" : "FBN",
                "SourceKey" : 102867831,
                "SourceGroupKey" : "55512_20090555",
                "MatchRank" : 1,
                "RecordType" : "Overview",
                "BusinessName" : "Hot dog stand",
                "BusinessDescription" : null,
                "OwningCompany" : null,
                "EmployeeSize" : null,
                "OwnerSize" : null,
                "LegalBusinessDescription" : "LIMITED LIABILITY COMPANY",
                "Comments" : null,
                "StateOfIncorporation" : null,
                "StateList" : null,
                "Url" : null,
                "IsHomeOffice" : false,
                "IsSolicitable" : true,
                "IsNonProfit" : false,
                "IsCorporation" : false,
                "IsNbe" : false,
                "IsFranchise" : false,
                "StartDate" : "20010110",
                "DbaName" : "",
                "RegistryNum" : "",
                "TaxId" : "",
                "CorpDesc" : "",
                "CorpType" : "",
                "CorpStatus" : "",
                "CorpStatusDate" : "",
                "LastReportDate" : "",
                "ExpireDate" : "",
                "BankruptDate" : "",
                "Sic" : "",
                "SicDescription" : "",
                "NonProfitType" : "",
                "Term" : "",
                "Capital" : "",
                "Purpose" : "",
                "HomeState" : "",
                "IncState" : "",
                "IncJurisdiction" : "",
                "IncStatute" : "",
                "Names" : [{
                        "SourceType" : "FBN",
                        "SourceKey" : 55552751,
                        "SourceGroupKey" : "55512_20010110",
                        "MatchRank" : 1,
                        "RecordType" : "Person",
                        "Firstname" : "JOE",
                        "MiddleName" : "",
                        "LastName" : "SMITH",
                        "Suffix" : "",
                        "ContactType" : "BUSINESS",
                        "OfficerType" : "CONTACT"
                    }
                ],
                "Addresses" : [{
                        "SourceType" : "FBN",
                        "SourceKey" : 55558236,
                        "SourceGroupKey" : "55552_20010110",
                        "MatchRank" : 1,
                        "RecordType" : "Address",
                        "AddressType" : "MAIL ADDRESS",
                        "AddressLine1" : "555 MAIN ST",
                        "AddressLine2" : "APT 1",
                        "City" : "SPRINGFIELD",
                        "State" : "MI",
                        "ZipCode" : "55555",
                        "Zip4" : "5555",
                        "County" : "SPRING",
                        "Country" : "",
                        "IsPoBox" : false,
                        "IsMailDeliverable" : false,
                        "IsCommercialLocation" : false,
                        "IsResidentialLocation" : false,
                        "Longitude" : "55.555500",
                        "Latitude" : "55.555500",
                        "TimeZone" : "EST"
                    }
                ],
                "PhoneNumbers" : [],
                "EmailAddresses" : [],
                "Mergers" : [],
                "Stocks" : []
            }
            
## Census Search [/CensusSearch]

Performs a census search, and returns a list of matching census records.

### Search [POST]
***Click on the grey search box above, to view sample request/response objects for the Census Search.***

Perform a search:
1. Add your Access Profile username and password to the request headers.
    * galaxy-ap-name: [Access Profile Name]
    * galaxy-ap-password: [Access Profile Password]
    * galaxy-client-session-id: (Optional) Session ID for logging
    * galaxy-client-type: [Galaxy Client Type] (required for Javascript clients)
    * galaxy-search-type: [Galaxy Search Type] (optional)
        * To auto-populate all includes and filter options in your requests, you may provide a search type value in your request header. A search type is required for all API Customers. Applicable search type values for this endpoint include: 
            1. Census
2. Add search criteria to your request:
    _Please note that at present we only support one relative in the search criteria. We expect to be able to support multiple relatives in the future._
    ```
    {
      "FirstName": "Andrew",
      "LastName": "Smith",
      "CensusDecades": [
        1930,
        1940
      ],
      "Addresses": [
        {
          "County": "Queens",
          "State": "NY"
        }
      ],
      "Relatives": [],
      "Includes": [],
      "FilterOptions": []
    }
    ```
3. Set the desired pagination rules:
    ```
    {
      "FirstName": "Andrew",
      "LastName": "Smith",
      "CensusDecades": [
        1930,
        1940
      ],
      "Addresses": [
        {
          "County": "Queens",
          "State": "NY"
        }
      ],
      "Relatives": [],
      "Includes": [],
      "FilterOptions": [],
      "Page": 1,
      "ResultsPerPage": 20
    }
    ```
4. Submit your search.

A complete list of JSON request properties follows:

* `FirstName` = null (optional, string) ... First name.
* `MiddleName` = null (optional, string) ... Middle name or middle initial.
* `LastName` = null (optional, string) ... Last name.
* `DOB` = null (optional, string)
* `Age` = null (optional, string)
* `AgeRange` = null (optional, string)... i.e. "70-90"
* `Addresss` = null (optional, object[])
    * `City` = null (optional, string) ... City.
    * `County` = null (optional, string) ... County.
    * `State` = null (optional, string) ... State (2-characters code) (State is required, if City or County is provided).
    * `ZipCode` = null (optional, string) ... Zip code (5-characters code).
* `Relatives` (optional, object[])
    * `FirstName` = null (optional, string)
    * `MiddleName` = null (optional, string)
    * `LastName` = null (optional, string)
* `CensusDecades` (optional, int[]) ... Census decades.
    * Valid Years
        * `1780`
        * `1790`
        * `1800`
        * `1810`
        * `1820`
        * `1830`
        * `1840`
        * `1850`
        * `1860`
        * `1870`
        * `1880`
        * `1890`
        * `1900`
        * `1910`
        * `1920`
        * `1930`
        * `1940`
* `Includes` (optional, string[]) ... Data to be included in the response.
    * Members
        * `DatabaseQueryInfo`
        * `ExecutionTimeInfo`
* `FilterOptions` (optional, string[]) ... Data filtering options.
    * Members (N/A)
* `Page` = 1 (optional, int) ... The page of data to return.
* `ResultsPerPage` = 10 (optional, int) ... The number of results to return per page.

+ Request (application/json)

    + Headers

            galaxy-ap-name: Access Profile Name
            galaxy-ap-password: Access Profile Password
            galaxy-client-session-id: APIARY
            galaxy-client-type: Galaxy Client Type

    + Body

            {
                "FirstName": "John",
                "LastName": "Smith",
                "Dob": "1/1/1975",
                "Page": 1,
                "ResultsPerPage": 10
            }

+ Response 200 (application/json)

            {
              "censusRecords": [
                {
                  "censusId": 155136,
                  "censusYear": 1940,
                  "matchQuality": 0,
                  "firstNameIsExactMatch": 1,
                  "householdId": 114,
                  "dob": "0",
                  "gender": "M",
                  "maritalStatus": "S",
                  "ethnicityId": 0,
                  "raceId": 0,
                  "firstName": "ANDREW",
                  "middleName": "",
                  "lastName": "SMITH",
                  "nameSuffix": "",
                  "namePrefix": "",
                  "extraInfo": {
                    "ageFormatted": "8",
                    "canRead": null,
                    "canWrite": null,
                    "citizenshipStatus": null,
                    "cityResidedIn1935": null,
                    "citySameHouse": "SAME HOUSE",
                    "deathDateStd": null,
                    "dwelling": null,
                    "enumerationDist": null,
                    "enumerationDistrict": "1-17",
                    "estimatedMarriageYear": null,
                    "ethnicity": "W",
                    "eventDistrict": null,
                    "familyNumber": null,
                    "famNew": null,
                    "freeOrSlave": null,
                    "fullName": "ANDREW SMITH",
                    "idSuffix": null,
                    "immigrationYearOrig": null,
                    "immigrationYearStd": null,
                    "incorporatedPlace": null,
                    "institutions": null,
                    "language": null,
                    "minorCivilDivision": null,
                    "mthrHowManyChildren": null,
                    "newFamNew": null,
                    "newDwell": null,
                    "numberLivingChildren": null,
                    "ownRent": null,
                    "prAgeMonths": null,
                    "prOccupation": null,
                    "race": "W",
                    "regionKode": null,
                    "relationshipGroup": null,
                    "relMerge": null,
                    "respondent": null,
                    "scheduleType": null,
                    "stateResidedIn1935": "\r",
                    "temporarilyAbsent": null,
                    "tgnRecordId": null,
                    "tgnRelId": null,
                    "townCodeHex": null,
                    "townIsolated": null,
                    "unincorporatedPlace": null,
                    "ward": null
                  },
                  "imageInfo": {
                    "batchName": "m-t0627-02456",
                    "dgsImage": null,
                    "digitalGsNumber": null,
                    "entryChar": null,
                    "entryNumber": null,
                    "filmNumber": null,
                    "gsuFilmNumber": null,
                    "imageName": "00542",
                    "imageNbr": null,
                    "imageType": null,
                    "lineNumber": "72",
                    "naraFilm": null,
                    "naraPublicationNumber": null,
                    "naraRoll": null,
                    "naraRollNumber": null,
                    "naraSeries": null,
                    "numericImageNbr": null,
                    "orderOnPage": null,
                    "packet": null,
                    "packetLtr": null,
                    "page": null,
                    "pageChar": null,
                    "pageOrig": null,
                    "pid": null,
                    "pidNumber": null,
                    "recNbr": null,
                    "recNbrPadded": null,
                    "recNumber": null,
                    "recordGroup": null,
                    "recordId": null,
                    "recordNbr": null,
                    "recordNumber": null,
                    "refId": null,
                    "sequenceOrder": null,
                    "sequenceOrderSuffix": null,
                    "sheetLtr": null,
                    "sheetNumber": null,
                    "sheetNumberLetter": null,
                    "udeBatchNumber": null,
                    "batchId": null,
                    "dgsImageId": null,
                    "lineNbr": null,
                    "imageId": null,
                    "pageNumber": "5B"
                  },
                  "addressInfo": {
                    "city": "",
                    "state": "NY",
                    "county": "ALBANY",
                    "birthLocation": "NY",
                    "birthLocationFather": null,
                    "birthLocationMother": null,
                    "birthLocationSpouse": null
                  },
                  "relatives": [
                    {
                      "censusYear": 1940,
                      "householdId": 114,
                      "relativeRelationship": "Daughter",
                      "extraInfo": {
                            "ageFormatted": "8",
                            "canRead": null,
                            "canWrite": null,
                            "citizenshipStatus": null,
                            "cityResidedIn1935": null,
                            "citySameHouse": "SAME HOUSE",
                            "deathDateStd": null,
                            "dwelling": null,
                            "enumerationDist": null,
                            "enumerationDistrict": "1-17",
                            "estimatedMarriageYear": null,
                            "ethnicity": "W",
                            "eventDistrict": null,
                            "familyNumber": null,
                            "famNew": null,
                            "freeOrSlave": null,
                            "fullName": "ANDREW SMITH",
                            "idSuffix": null,
                            "immigrationYearOrig": null,
                            "immigrationYearStd": null,
                            "incorporatedPlace": null,
                            "institutions": null,
                            "language": null,
                            "minorCivilDivision": null,
                            "mthrHowManyChildren": null,
                            "newFamNew": null,
                            "newDwell": null,
                            "numberLivingChildren": null,
                            "ownRent": null,
                            "prAgeMonths": null,
                            "prOccupation": null,
                            "race": "W",
                            "regionKode": null,
                            "relationshipGroup": null,
                            "relMerge": null,
                            "respondent": null,
                            "scheduleType": null,
                            "stateResidedIn1935": "\r",
                            "temporarilyAbsent": null,
                            "tgnRecordId": null,
                            "tgnRelId": null,
                            "townCodeHex": null,
                            "townIsolated": null,
                            "unincorporatedPlace": null,
                            "ward": null
                            }
                        }
                    ]
                }

## Criminal Search V2 [/CriminalSearch/V2]

Performs a criteria search, and returns a list of matching criminal records.

### Search [POST]
***Click on the grey search box above, to view sample request/response objects for the Criminal Search***

Perform a search:
1. Add your Access Profile username and password to the request headers.
    * galaxy-ap-name: [Access Profile Name]
    * galaxy-ap-password: [Access Profile Password]
    * galaxy-client-session-id: (Optional) Session ID for logging
    * galaxy-client-type: [Galaxy Client Type] (required for Javascript clients)
    * galaxy-search-type: [Galaxy Search Type] (optional)
        * To auto-populate all includes and filter options in your requests, you may provide a search type value in your request header. A search type is required for all API Customers. Applicable search type values for this endpoint include: 
            1. CriminalV2
2. Add search criteria to your request:
    ```
    {
        "BusinessName": "",
        "LastName": "Simpson",
        "FirstName": "Orenthal",
        "MiddleName": "",
        "Suffix": "",
        "AddressLine1": "",
        "AddressLine2": "",
        "Dob": "07/09/1947",
        "DobTo": "",
        "Age": 0,
        "OffenseCity": "",
        "OffenseCounty": "",
        "OffenseState": "",
        "PersonCity": "",
        "PersonState": "",
        "CategoryTypes": "ARR,CRI"
    }
    ```
    
3. Set the desired pagination rules:
    ```
    {
        "BusinessName": "",
        "LastName": "Simpson",
        "FirstName": "Orenthal",
        "MiddleName": "",
        "Suffix": "",
        "Dob": "07/09/1947",
        "DobTo": "",
        "Age": ,
        "OffenseCity": "",
        "OffenseCounty": "",
        "OffenseState": "",
        "CategoryTypes": "ARR,CRI",
        "Page": 1,
        "ResultsPerPage": 20
    }
    ```
4. Submit your search.

A complete list of JSON request properties follows:

* `CaseNumber` = null (optional, string) ... Case Number.
* `TahoeId` = null (optional, string) ... Tahoe Person ID.
* `PoseidonId` = null (optional, string) ... Unique criminal record ID.
* `BusinessName` = null (optional, string) ... Business name.
* `LastName` = null (optional, string) ... Last name.
* `FirstName` = null (optional, string) ... First name.
* `MiddleName` = null (optional, string) ... Middle name or middle initial.
* `Suffix` = null (optional, string) ... Name suffix.
* `Dob` = null (optional, string) ... Date of birth from (format: MM/DD/YYYY).
* `DobTo` = null (optional, string) ... Date of birth to (format: MM/DD/YYYY).
* `Age` = null (optional, int) ... Age).
* `OffenseCity` = null (optional, string ... Offense city).
* `OffenseState` = null (optional, string ... Offense state).
* `PersonCity` = null (optional, string ... Person city).
* `CategoryTypes` = null (optional, string ... Category types ... These can be pass in combination with each other by seperating the values with a comma. i.e.  `ARR,CRI,TRA`).
    * `ALL` - (All categories)
    * `ARR` - (Arrest records)
    * `CRI` - (Criminal records)
    * `TRA` - (Traffic Infractions)
    * `WAN` - (Wants and Warrants)
    * `SEX` - (Sex Offender records)
* `Includes` (optional, string[]) ... Data to be included in the response.
    * Members
        * `DatabaseQueryInfo`
        * `ExecutionTimeInfo`
        * `SocialSecurityNumbers`
* `FilterOptions` (optional, string[]) ... Data filtering options.
    * Members
        * `IncludeOptOutData`
        * `IncludeFullSsnValues`
        * `DisableFirstNameSynonymMatching`
* `Page` = 1 (optional, int) ... The page of data to return.
* `ResultsPerPage` = 10 (optional, int) ... The number of results to return per page.

+ Request (application/json)

    + Headers

            galaxy-ap-name: Access Profile Name
            galaxy-ap-password: Access Profile Password
            galaxy-client-session-id: APIARY
            galaxy-client-type: Galaxy Client Type

    + Body

            {
                "FirstName": "John",
                "LastName": "Smith",
                "Dob": "1/1/1975",
                "Page": 1,
                "ResultsPerPage": 10
            }

+ Response 200 (application/json)

        {"criminalRecords":[{"poseidonId":284133067705372131,"shortCat":"TRA","names":[{"firstName":"Orenthal","middleName":"J","lastName":"Simpson","suffix":null,"tahoeId":"G2132292532481985608","ssn":null,"nameHash":3095858141145503349,"nameScore":1001008.3333333334,"sourceMap":null,"fullName":"Orenthal J Simpson"}],"offenderAttributes":[{"dob":"7/9/1947","age":null,"birthState":null,"hair":null,"eye":null,"height":null,"weight":null,"race":null,"sex":null,"skinTone":null,"militaryService":null,"scarsMarks":null,"sourceMap":null,"nameHashes":[3095858141145503349]}],"photos":[],"addresses":[],"caseDetails":[{"caseNumber":"13-2001-CF-004445-0001-XX","caseType":"CRIMINAL FELONY","rawCategory":"CRIMINAL","mappedCategory":"TRAFFIC & INFRACTION","nciCcode":null,"source":"FLORIDA DADE COUNTY WEB","courtType":null,"court":"REGJB - JUSTICE BUILDING, ROOM NO.:","courtCounty":"MIAMI-DADE","fees":null,"fines":null,"caseDate":null,"sourceMap":"HYG"}],"offenses":[{"offenseCodes":null,"photos":null,"offenseDescription":["BATTERY"],"offenseDate":null,"chargesFiledDate":"2/12/2001","sourceCounty":null,"sourceState":"FL","convictionDate":null,"convictionPlace":null,"disposition":"ACQUITTED BY JURY","dispositionDate":null,"sentenced":null,"probationDate":null,"sourceMap":"HYG","classificationCodeDescription":"Misdemeanor","classificationSubCodeDescription":null}],"others":[{"sourceMap":"hyg","columns":{"sourcetype":"HYG","classificationcode":"M","sourcename":"FLORIDA DADE COUNTY WEB","rawCategory":"CRIMINAL","status":"CLOSED; BOND STATUS: DISCHARGED; BOND ISSUE DATE: 20010209","comments":"COURT CASE #: F-01-004445 COURT ADDRESS: 1351 N.W. 12 ST; B FILE SECTION: F017; FILE LOCATION: RECORD CENTER; BOX #: 63-49","casetypeClassification":"MISDEMEANOR"}}],"images":[]},{"poseidonId":6834540554752805195,"shortCat":"TRA","names":[{"firstName":"Orenthal","middleName":"James","lastName":"Simpson","suffix":null,"tahoeId":"G2132292532481985608","ssn":null,"nameHash":-180909923821732275,"nameScore":1001010.6666666666,"sourceMap":null,"fullName":"Orenthal James Simpson"},{"firstName":"Orenthal","middleName":"J","lastName":"Simpson","suffix":null,"tahoeId":"G2132292532481985608","ssn":null,"nameHash":3095858141145503349,"nameScore":1008.3333333333334,"sourceMap":null,"fullName":"Orenthal J Simpson"},{"firstName":"O","middleName":"J Juice","lastName":"Simpson","suffix":null,"tahoeId":"G2132292532481985608","ssn":null,"nameHash":1761306363277606290,"nameScore":1008.0,"sourceMap":null,"fullName":"O J Juice Simpson"},{"firstName":"O","middleName":"J","lastName":"Simpson","suffix":null,"tahoeId":"G2132292532481985608","ssn":null,"nameHash":6359454639443648661,"nameScore":1005.0,"sourceMap":null,"fullName":"O J Simpson"},{"firstName":null,"middleName":null,"lastName":null,"suffix":null,"tahoeId":null,"ssn":null,"nameHash":null,"nameScore":1003.0,"sourceMap":null,"fullName":""}],"offenderAttributes":[{"dob":"7/9/1947","age":null,"birthState":null,"hair":"BLACK","eye":"BROWN","height":"6'02\"","weight":"235 LBS","race":null,"sex":"MALE","skinTone":"DARK","militaryService":null,"scarsMarks":null,"sourceMap":null,"nameHashes":[3095858141145503349,6359454639443648661,1761306363277606290,-180909923821732275]}],"photos":[],"addresses":[],"caseDetails":[{"caseNumber":"","caseType":null,"rawCategory":"CRIMINAL","mappedCategory":"TRAFFIC & INFRACTION","nciCcode":null,"source":"NV_DOC","courtType":null,"court":null,"courtCounty":null,"fees":null,"fines":null,"caseDate":null,"sourceMap":"HYG"}],"offenses":[{"offenseCodes":["466"],"photos":null,"offenseDescription":["COERCION"],"offenseDate":null,"chargesFiledDate":null,"sourceCounty":null,"sourceState":"NV","convictionDate":null,"convictionPlace":null,"disposition":null,"dispositionDate":null,"sentenced":null,"probationDate":null,"sourceMap":"HYG","classificationCodeDescription":"Misdemeanor","classificationSubCodeDescription":null}],"others":[{"sourceMap":"hyg","columns":{"sourcetype":"HYG","classificationcode":"M","commitmentdate":"20081205","sourcename":"NV_DOC","rawCategory":"CRIMINAL"}}],"images":[]},{"poseidonId":-8027969834842343199,"shortCat":"TRA","names":[{"firstName":"Orenthal","middleName":"James","lastName":"Simpson","suffix":null,"tahoeId":"G2132292532481985608","ssn":null,"nameHash":-180909923821732275,"nameScore":1001010.6666666666,"sourceMap":null,"fullName":"Orenthal James Simpson"}],"offenderAttributes":[{"dob":"7/9/1947","age":null,"birthState":null,"hair":null,"eye":null,"height":null,"weight":null,"race":null,"sex":null,"skinTone":null,"militaryService":null,"scarsMarks":null,"sourceMap":null,"nameHashes":[-180909923821732275]}],"photos":[],"addresses":[],"caseDetails":[{"caseNumber":"13-2002-IN-040232-0001-XX","caseType":"INFRACTION","rawCategory":"CRIMINAL","mappedCategory":"TRAFFIC & INFRACTION","nciCcode":null,"source":"FLORIDA DADE COUNTY WEB","courtType":null,"court":"REGJB - JUSTICE BUILDING, ROOM NO.:","courtCounty":"MIAMI-DADE","fees":null,"fines":null,"caseDate":null,"sourceMap":"HYG"}],"offenses":[{"offenseCodes":null,"photos":null,"offenseDescription":["MANATEE/SPD ZONE"],"offenseDate":null,"chargesFiledDate":"7/19/2002","sourceCounty":null,"sourceState":"FL","convictionDate":null,"convictionPlace":null,"disposition":"NOLLE PROS","dispositionDate":null,"sentenced":null,"probationDate":null,"sourceMap":"HYG","classificationCodeDescription":"Infraction","classificationSubCodeDescription":null},{"offenseCodes":null,"photos":null,"offenseDescription":["BOAT/REG/FAIL COMPLY"],"offenseDate":null,"chargesFiledDate":"7/19/2002","sourceCounty":null,"sourceState":"FL","convictionDate":null,"convictionPlace":null,"disposition":"NOLLE PROS","dispositionDate":null,"sentenced":null,"probationDate":null,"sourceMap":"HYG","classificationCodeDescription":"Misdemeanor","classificationSubCodeDescription":null}],"others":[{"sourceMap":"hyg","columns":{"sourcetype":"HYG","classificationcode":"I","sourcename":"FLORIDA DADE COUNTY WEB","rawCategory":"CRIMINAL","status":"CLOSED","comments":"COURT CASE #: M-02-040232 COURT ADDRESS: 1351 N.W. 12 ST; B FILE SECTION: M008; FILE LOCATION: DESTROYED; ALT SECTION: M008; ALT BACKUP JUDGE: ORTIZ, MARIA D","casetypeClassification":"MISDEMEANOR"}}],"images":[]},{"poseidonId":1060067805084598114,"shortCat":"TRA","names":[{"firstName":"Orenthal","middleName":"James","lastName":"Simpson","suffix":null,"tahoeId":"G2132292532481985608","ssn":null,"nameHash":-180909923821732275,"nameScore":1001010.6666666666,"sourceMap":null,"fullName":"Orenthal James Simpson"}],"offenderAttributes":[{"dob":"7/9/1947","age":null,"birthState":null,"hair":null,"eye":null,"height":null,"weight":null,"race":null,"sex":null,"skinTone":null,"militaryService":null,"scarsMarks":null,"sourceMap":null,"nameHashes":[-180909923821732275]},{"dob":"7/9/1947","age":null,"birthState":null,"hair":null,"eye":null,"height":null,"weight":null,"race":"BLACK","sex":"MALE","skinTone":null,"militaryService":null,"scarsMarks":null,"sourceMap":null,"nameHashes":[-180909923821732275]}],"photos":[],"addresses":[{"attention":"","houseNumber":"9450","streetDirection":"SW","streetName":"112th","streetType":"ST","streetPostDirection":"","unitType":"","unitNumber":"","city":"Miami","state":"FL","zipCode":"33176","zip4":"3619","county":"Miami-Dade","longitude":"-80.348342","latitude":"25.665093","rawVerificationCodes":"AS01","addressHash":null,"sourceMap":null,"nameHashes":[-180909923821732275],"fullAddress":"9450 SW 112th ST; Miami, FL 33176-3619"}],"caseDetails":[{"caseNumber":"M02040232","caseType":null,"rawCategory":"CRIMINAL","mappedCategory":"TRAFFIC & INFRACTION","nciCcode":null,"source":"FL_DADE_WB","courtType":null,"court":null,"courtCounty":"MIAMI-DADE","fees":null,"fines":null,"caseDate":"11/22/2002","sourceMap":"HYG"},{"caseNumber":"M-02-040232","caseType":null,"rawCategory":"CRIMINAL","mappedCategory":"TRAFFIC & INFRACTION","nciCcode":null,"source":"FL_DADE_WB","courtType":null,"court":null,"courtCounty":"MIAMI-DADE","fees":null,"fines":null,"caseDate":null,"sourceMap":"HYG"}],"offenses":[{"offenseCodes":["327.72"],"photos":null,"offenseDescription":["BOAT/REG/FAIL COMPLY"],"offenseDate":"11/22/2002","chargesFiledDate":"7/19/2002","sourceCounty":null,"sourceState":"FL","convictionDate":null,"convictionPlace":null,"disposition":"NOLLE PROS","dispositionDate":"11/22/2002","sentenced":null,"probationDate":null,"sourceMap":"HYG","classificationCodeDescription":"Misdemeanor","classificationSubCodeDescription":null},{"offenseCodes":["327.72"],"photos":null,"offenseDescription":["BOAT/REG/FAIL COMPLY"],"offenseDate":null,"chargesFiledDate":"7/19/2002","sourceCounty":null,"sourceState":"FL","convictionDate":null,"convictionPlace":null,"disposition":"NOLLE PROS","dispositionDate":null,"sentenced":null,"probationDate":null,"sourceMap":"HYG","classificationCodeDescription":"Misdemeanor","classificationSubCodeDescription":null}],"others":[{"sourceMap":"hyg","columns":{"arrestingagency":"064","sourcetype":"HYG","classificationcode":"M","sourcename":"FL_DADE_WB","status":"CLOSED","rawCategory":"CRIMINAL","arrestdate":"20020704"}}],"images":[]},{"poseidonId":5247249713456904349,"shortCat":"TRA","names":[{"firstName":"Orenthal","middleName":"J","lastName":"Simpson","suffix":null,"tahoeId":"G2132292532481985608","ssn":null,"nameHash":3095858141145503349,"nameScore":1001008.3333333334,"sourceMap":null,"fullName":"Orenthal J Simpson"}],"offenderAttributes":[{"dob":"7/9/1947","age":null,"birthState":null,"hair":null,"eye":null,"height":null,"weight":null,"race":null,"sex":null,"skinTone":null,"militaryService":null,"scarsMarks":null,"sourceMap":null,"nameHashes":[3095858141145503349]},{"dob":"7/9/1947","age":null,"birthState":null,"hair":null,"eye":null,"height":null,"weight":null,"race":"BLACK","sex":"MALE","skinTone":null,"militaryService":null,"scarsMarks":null,"sourceMap":null,"nameHashes":[3095858141145503349]}],"photos":[],"addresses":[{"attention":"","houseNumber":"9450","streetDirection":"SW","streetName":"112th","streetType":"ST","streetPostDirection":"","unitType":"","unitNumber":"","city":"Miami","state":"FL","zipCode":"33176","zip4":"3619","county":"Miami-Dade","longitude":"-80.348342","latitude":"25.665093","rawVerificationCodes":"AS01","addressHash":null,"sourceMap":null,"nameHashes":[3095858141145503349],"fullAddress":"9450 SW 112th ST; Miami, FL 33176-3619"}],"caseDetails":[{"caseNumber":"F-01-004445","caseType":null,"rawCategory":"CRIMINAL","mappedCategory":"TRAFFIC & INFRACTION","nciCcode":null,"source":"FL_DADE_WB","courtType":null,"court":null,"courtCounty":"MIAMI-DADE","fees":null,"fines":null,"caseDate":null,"sourceMap":"HYG"},{"caseNumber":"F01004445","caseType":null,"rawCategory":"CRIMINAL","mappedCategory":"TRAFFIC & INFRACTION","nciCcode":null,"source":"FL_DADE_WB","courtType":null,"court":null,"courtCounty":"MIAMI-DADE","fees":null,"fines":null,"caseDate":"10/24/2001","sourceMap":"HYG"}],"offenses":[{"offenseCodes":["784.03"],"photos":null,"offenseDescription":["BATTERY"],"offenseDate":"10/24/2001","chargesFiledDate":"2/12/2001","sourceCounty":null,"sourceState":"FL","convictionDate":null,"convictionPlace":null,"disposition":"ACQUITTED BY JURY","dispositionDate":"10/24/2001","sentenced":null,"probationDate":null,"sourceMap":"HYG","classificationCodeDescription":"Misdemeanor","classificationSubCodeDescription":null},{"offenseCodes":["784.03"],"photos":null,"offenseDescription":["BATTERY"],"offenseDate":null,"chargesFiledDate":"2/12/2001","sourceCounty":null,"sourceState":"FL","convictionDate":null,"convictionPlace":null,"disposition":"ACQUITTED BY JURY","dispositionDate":null,"sentenced":null,"probationDate":null,"sourceMap":"HYG","classificationCodeDescription":"Misdemeanor","classificationSubCodeDescription":null}],"others":[{"sourceMap":"hyg","columns":{"arrestingagency":"030","sourcetype":"HYG","classificationcode":"M","sourcename":"FL_DADE_WB","status":"CLOSED","rawCategory":"CRIMINAL","arrestdate":"20010209"}}],"images":[]}],"criminalRecordCounts":5,"pagination":{"currentPageNumber":1,"resultsPerPage":20,"totalPages":1},"searchCriteria":[],"totalRequestExecutionTimeMs":281,"requestId":"d069e529-2dc3-4bbc-a947-1023483f42f7","requestType":"Search","requestTime":"2019-04-26T10:14:27.7040880-07:00","isError":false}

            
## Debt Search v2 [/DebtSearch/V2]

Performs a criteria search, and returns a list of banckruptcy, lien, and judgement records.

### Search [POST]
***Click on the grey search box above, to view sample request/response objects for the Debt Search.***

Perform a search:
1. Add your Access Profile username and password to the request headers.
    * galaxy-ap-name: [Access Profile Name]
    * galaxy-ap-password: [Access Profile Password]
    * galaxy-client-session-id: (Optional) Session ID for logging
    * galaxy-client-type: [Galaxy Client Type] (required for Javascript clients)
    * galaxy-search-type: [Galaxy Search Type] (optional)
        * To auto-populate all includes and filter options in your requests, you may provide a search type value in your request header. A search type is required for all API Customers. Applicable search type values for this endpoint include: 
            1. DebtV2
2. Add search criteria to your request:
    ```
    {
        "FirstName": "John",
        "LastName": "Smith",
        "AddressLine2": "CA"
    }
    ```
3. Set the desired pagination rules:
    ```
    {
        "FirstName": "John",
        "LastName": "Smith",
        "AddressLine2": "CA"
        "Page": 1,
        "ResultsPerPage": 10
    }
    ```
4. Submit your search.

A complete list of JSON request properties follows:

(Note: Use AddressLine1/AddressLine2 OR the component address parts; not recommended to mix them)

* `BusinessName` = null (optional, string) ... Business name.
* `FirstName` = null (optional, string) ... First name.
* `MiddleName` = null (optional, string) ... Middle name or middle initial.
* `LastName` = null (optional, string) ... Last name.
* `AddressLine1` = null (optional, string) ... Address line 1 (house number, street).
* `AddressLine2` = null (optional, string) ... Address line 2 (city, state).
* `HouseNumber` = null (optional, string) ... Address house number.
* `Street` - null (optional, string) ... Address street name.
* `Unit` = null (optional, string) ... Address apt/unit number.
* `City` = null (optional, string) ... Address city.
* `State` = null (optional, string) ... Address state (2-char abbreviation).
* `Zip` = null (optional, string) ... Address ZIPcode
* `Ssn` = null (optional, string) ... Social security number (format: ###-##-####) (Note: not all Debt records contain SSN).
* `PoseidonId` = null (optional, string) ... Unique ID per debt record.
* `Includes` (optional, string[]) ... Data to be included in the response.
    * Members
        * `DatabaseQueryInfo`
        * `SocialSecurityNumbers`
* `FilterOptions`
    * Members
        * `IncludeFullSSNValues`
* `DebtType` (optional, string) ... one of: "0", "1", "2", or "3" = All, Bankruptcies, Liens, Judgments.
    * Members
        * `0 = All`
        * `1 = Bankruptcies`
        * `2 = Liens`
        * `3 = Judgments`
* `Page` = 1 (optional, int) ... The page of data to return.
* `ResultsPerPage` = 10 (optional, int) ... The number of results to return per page.

+ Request (application/json)

    + Headers

            galaxy-ap-name: Access Profile Name
            galaxy-ap-password: Access Profile Password
            galaxy-client-session-id: APIARY
            galaxy-client-type: Galaxy Client Type

    + Body

            {
                "FirstName": "John",
                "LastName": "Smith",
                "AddressLine2": "CA"
                "Page": 1,
                "ResultsPerPage": 10
            }

+ Response 200 (application/json)

            {
                "debtRecords": [
                    {
                        "poseidonId": null,
                        "debtType": "Judgment",
                        "filingDate": "1/1/2001",
                        "reportDate": "1/1/2001",
                        "names": [
                            {
                                "type": "debtor",
                                "isBusiness": false,
                                "prefix": null,
                                "firstName": "John",
                                "middleName": null,
                                "lastName": "Smith",
                                "suffix": null,
                                "tahoeId": null,
                                "ssn": null,
                                "ein": null,
                                "nameHash": null,
                                "email": null,
                                "phone": null,
                                "addressHash": null,
                                "address": {
                                    "addressHash": null,
                                    "type": "debtoraddress",
                                    "houseNumber": "123",
                                    "streetDirection": null,
                                    "streetName": "MAIN",
                                    "streetType": "St",
                                    "streetPostDirection": null,
                                    "unitType": "#",
                                    "unitNumber": "1",
                                    "city": "New York City",
                                    "state": "NY",
                                    "zipCode": "00000",
                                    "zip4": "0000",
                                    "county": "New York",
                                    "longitude": "-55.555555",
                                    "latitude": "55.555555",
                                    "fullAddress": null,
                                    "rawVerificationCodes": null,
                                    "verificationCodes": [null]
                                },
                                "fullName": "John Smith",
                                "businessName": null
                            },
                            {
                                "type": "creditor",
                                "isBusiness": true,
                                "prefix": null,
                                "firstName": null,
                                "middleName": null,
                                "lastName": null,
                                "suffix": null,
                                "tahoeId": null,
                                "ssn": null,
                                "ein": null,
                                "nameHash": null,
                                "email": null,
                                "phone": null,
                                "addressHash": null,
                                "address": null,
                                "fullName": null,
                                "businessName": null
                            }
                        ],
                        "addresses": [
                            {
                                "addressHash": null,
                                "type": "debtoraddress",
                                "houseNumber": "123",
                                "streetDirection": null,
                                "streetName": "MAIN",
                                "streetType": "St",
                                "streetPostDirection": null,
                                "unitType": "#",
                                "unitNumber": "1",
                                "city": "New York City",
                                "state": "NY",
                                "zipCode": "00000",
                                "zip4": "0000",
                                "county": "New York",
                                "longitude": "-55.555555",
                                "latitude": "55.555555",
                                "fullAddress": null,
                                "rawVerificationCodes": null,
                                "verificationCodes": [null]
                            }
                        ],
                        "courts": [
                            {
                                "courtId": "MANORD4",
                                "division": null,
                                "district": null,
                                "name": null,
                                "phone": null,
                                "email": null,
                                "url": null,
                                "addressHash": null,
                                "address": null,
                                "judge": null
                            }
                        ],
                        "caseDetails": [
                            {
                                "caseNumber": "200101CV000000",
                                "filingDate": "1/1/2001",
                                "assets": null,
                                "unlawfulDetainer": "N",
                                "entity": "I",
                                "reportDate": "10/28/2010",
                                "book": null,
                                "page": null,
                                "originalDepartment": null,
                                "originalBook": null,
                                "originalPage": null,
                                "schedule341Time": null,
                                "filingType": "CJ",
                                "filingTypeDescription": "CIVIL JUDGMENT",
                                "fileState": "NY",
                                "releaseDate": null,
                                "otherCaseNumber": null,
                                "generationCode": null,
                                "actionType": "04",
                                "actionTypeDescription": "CIVIL JUDGMENT",
                                "courtState": null,
                                "bankruptcyType": null,
                                "lawFirm": null,
                                "dischargeDate": null,
                                "dismissalDate": null,
                                "convertedDate": null,
                                "closedDate": null,
                                "reopenedDate": null,
                                "transferredDate": null,
                                "withdrawnDate": null,
                                "claimDate": null,
                                "objectionDate": null,
                                "assetsAvailable": null,
                                "assetValue": null,
                                "chapter": null,
                                "noticeDate": null,
                                "caseNumber2": null,
                                "amountOrLiability": null,
                                "originalCase": null,
                                "schedule341Date": null,
                                "plaintiffLawFirm": null,
                                "attorney": null,
                                "attorneyZipCode": null,
                                "primaryIndustryBusiness": null,
                                "secondaryIndustryBusiness": null,
                                "associationCode": null,
                                "liabilityAmount": null,
                                "originalCaseNumber": null,
                                "judgesInitials": null,
                                "associateCode": "1",
                                "liability": "9641.0",
                                "assetsAvailableFlag": null,
                                "bankruptcyDismissalFlag": null
                            }
                        ]
                    }
                ],
                "debtRecordCounts": 1,
                "bankruptcyRecordCounts": 0,
                "lienRecordCounts": 0,
                "judgmentRecordCounts": 1,
                "pagination": {
                    "currentPageNumber": 1,
                    "resultsPerPage": 10,
                    "totalPages": 1
                },
                "searchCriteria": [],
                "totalRequestExecutionTimeMs": 0,
                "requestId": "00000000-0000-0000-0000-000000000000",
                "requestType": "Search",
                "requestTime": "2018-08-01T00:00:00.0000000-00:00",
                "isError": false
            }
            
## Domain Search [/DomainSearch]

Performs a domain search, and returns a list of domains matching the search criteria.

### Search [POST]
***Click on the grey search box above, to view sample request/response objects for the Domain Search.***

Perform a search:
1. Add your Access Profile username and password to the request headers.
    * galaxy-ap-name: [Access Profile Name]
    * galaxy-ap-password: [Access Profile Password]
    * galaxy-client-session-id: (Optional) Session ID for logging
    * galaxy-client-type: [Galaxy Client Type] (required for Javascript clients)
    * galaxy-search-type: [Galaxy Search Type] (optional)
        * To auto-populate all includes and filter options in your requests, you may provide a search type value in your request header. A search type is required for all API Customers. Applicable search type values for this endpoint include: 
            1. Domain
2. Add search criteria to your request:
    ```
    {
        "FreeFormSearch": "Acme Corp"
    }
    OR
    {
        "TahoeId": "G-123123123123"
    }
    OR
    {
        "BusinessName": "Acme Corp",
        "FirstName": "John",
        "MiddleName": "D",
        "LastName": "Smith",
        "HouseNumber": "1234",
        "Unit": "123",
        "Country": "US",
        "City": "Sacramento",
        "State": "CA",
        "Zip": "12345"
    }
    Note: FreeFormSearch parameter can't be combine with other parameters.
    ```
3. Select the data types you would like to receive in the output (i.e. the Includes):
    ```
    {
        "FreeFormSearch": "Acme Corp",
        "Includes": ["DatabaseQueryInfo", "ExecutionTimeInfo"]
    }
    ```
4. Select any desired data filters:
    ```
    {
        "FreeFormSearch": "Acme Corp",
        "Includes": ["DatabaseQueryInfo", "ExecutionTimeInfo"],
        "FilterOptions": ["DisableFirstNameSynonymMatching"]
    }
    ```
5. Set the desired pagination rules:
    ```
    {
        "FreeFormSearch": "Acme Corp",
        "Includes": ["DatabaseQueryInfo", "ExecutionTimeInfo"],
        "FilterOptions": ["DisableFirstNameSynonymMatching"],
        "Page": 1,
        "ResultsPerPage": 10
    }
    ```
6. Submit your search.

A complete list of JSON request properties follows:

* `FreeFormSearch` = Acme Corp (optional, string)
* `BusinessName  ` = ""            (optional, string)
* `FirstName     ` = ""            (optional, string)
* `MiddleName    ` = ""            (optional, string)
* `LastName      ` = ""            (optional, string)
* `HouseNumber   ` = ""            (optional, string)
* `Unit          ` = ""            (optional, string)
* `Country       ` = US            (optional, string) ... Country (format: 2 charcters long string, i.e.: US for USA, CA for Canada)
* `City          ` = Sacramento    (optional, string)
* `State         ` = CA            (optional, string) ... State (format: 2 characters long string, i.e.: CA, TX)
* `Zip           ` = ""            (optional, string)
* `Includes` (optional, string[]) .. Data to be included in the response.
    * Members
        * `DatabaseQueryInfo`
        * `ExecutionTimeInfo`
* `FilterOptions` (optional, string[]) .. Data filtering options.
    * Members
        * `DisableFirstNameSynonymMatching`
* `Page` = 1 (optional, int) ... The page of data to return.
* `ResultsPerPage` = 10 (optional, int) ... The number of results to return per page.

+ Request (application/json)
    + Headers
        
            galaxy-ap-name: Access Profile Name
            galaxy-ap-password: Access Profile Password
            galaxy-client-session-id: APIARY
            galaxy-client-type: Galaxy Client Type

    + Body
    
            {
                "FullFormSearch": "Acme Corp",
                "Includes": ["DatabaseQueryInfo", "ExecutionTimeInfo"],
                "FilterOptions": ["DisableFirstNameSynonymMatching"],
                "Page": 1,
                "ResultsPerPage": 10
            }

+ Response 200 (application/json)

            {
                "domainRecords": [{
                        "domainId": 1234567890,
                        "domainName": "SomeName",
                        "contacts": [{
                                "contactId": 123456789012,
                                "contactType": "Contact",
                                "businessName": "",
                                "businessNameShort": "",
                                "businessType": "1",
                                "businessTypeDesc": "Contact",
                                "salutation": "",
                                "gender": "M",
                                "firstName": "JOHN",
                                "middleName": "",
                                "lastName": "SMITH",
                                "nameSuffix": "",
                                "addressTypeDesc": "Street Address",
                                "addressAttn": "",
                                "houseNumber": "1234",
                                "streetPreDirection": "S",
                                "streetName": "Some Street",
                                "streetType": "ST",
                                "streetPostDirection": "",
                                "unitType": "",
                                "unitNbr": "",
                                "addressBuilding": "",
                                "city": "Some City",
                                "state": "CA",
                                "zip": "12345",
                                "zip4": "1234",
                                "carrierRoute": "",
                                "deliveryPoint": "12",
                                "county": "Sacramento",
                                "country": "US",
                                "emails": [],
                                "phones": [],
                                "faxes": [],
                                "dates": [{
                                        "creationDate": "01/01/2002",
                                        "lastUpdated": ""
                                    }
                                ]
                            }
                        ]
                    }
                ],
                "counts": {
                    "searchResults": 18
                },
                "pagination": {
                    "currentPageNumber": 1,
                    "resultsPerPage": 100,
                    "totalPages": 1
                },
                "databaseQueryInfo": [{
                        "searchType": null,
                        "hasIntermediateSort": null,
                        "retryCount": null,
                        "idCount": null,
                        "matchRecordCount": null,
                        "databaseQueries": [{
                                "databaseConnectionTimeInMs": 24,
                                "databaseQuery": "CALL search_domain(@p_business_name := null, @p_first_name := null, @p_middle_name := null, @p_last_name := null, @p_freeform_name := 'acme corp', @p_gender := null, @p_street_address := null, @p_house_number := null, @p_street_name := null, @p_unit := null, @p_country := null, @p_city := null, @p_state := null, @p_zip_code := null, @p_phone_or_fax := null, @p_email := null, @p_domain_name := null, @p_apply_fn_syn := True, @p_record_limit := 1000);",
                                "executionTimeInMs": 31
                            }
                        ]
                    }
                ],
                "executionStatistics": [{
                            "description": "Domain SP Client Search",
                            "startTime": 31,
                            "executionTimeInMs": 55
                        }, {
                            "description": "CALL search_domain",
                            "startTime": 31,
                            "executionTimeInMs": 55
                    }
                ],
                "searchCriteria": [],
                "totalRequestExecutionTimeMs": 89,
                "requestId": "bb014839-ff1f-4ede-a021-df96242ee1ef",
                "requestType": "DomainSearch",
                "requestTime": "2017-01-16T09:22:21.3300849-08:00",
                "isError": false
            }
            
## Eviction Search [/EvictionSearch]

Performs a Eviction search, and returns a list of Eviction records matching the search criteria.

### Search [POST]
***Click on the grey search box above, to view sample request/response objects for the Eviction Search.***

Perform a search:
1. Add your Access Profile username and password to the request headers.
    * galaxy-ap-name: [Access Profile Name]
    * galaxy-ap-password: [Access Profile Password]
    * galaxy-client-session-id: (Optional) Session ID for logging
    * galaxy-client-type: [Galaxy Client Type] (required for Javascript clients)
    * galaxy-search-type: [Galaxy Search Type] (optional)
        * To auto-populate all includes and filter options in your requests, you may provide a search type value in your request header. A search type is required for all API Customers. Applicable search type values for this endpoint include: 
            1. Eviction
2. Add search criteria to your request:
    ```
    {
        "BusinessName": "walmart"
    }
    Or
    {
        "TahoeId": "GXXXXXXXXXXXXXXXXXXX",
        "PoseidonIds": [
            "12345678912345678912",
            "12345678912345678912"
        ],
        "SSN": "XXX-XX-XXXX",
        "DefendantFirstName": "John",
        "DefendantMiddleName": "",
        "DefendantLastName": "Smith",
        "DefendantNameSuffix": "",
        "PlaintiffFirstName": "",
        "PlaintiffMiddleName": "",
        "PlaintiffLastName": "",
        "PlaintiffNameSuffix": "",
        "HouseNumber": "",
        "StreetName": "",
        "Unit": "",
        "City": "",
        "State": "",
        "ZipCode": "XXXXX"
    }
    Or
    {
        "TahoeId": "GXXXXXXXXXXXXXXXXXXX",
        "PoseidonIds": [
            "12345678912345678912",
            "12345678912345678912"
        ],
        "SSN": "XXX-XX-XXXX",
        "DefendantFirstName": "John",
        "DefendantMiddleName": "",
        "DefendantLastName": "Smith",
        "DefendantNameSuffix": "",
        "PlaintiffFirstName": "",
        "PlaintiffMiddleName": "",
        "PlaintiffLastName": "",
        "PlaintiffNameSuffix": "",
        "StreetAddress": "",
        "City": "",
        "State": "",
        "ZipCode": "XXXXX"
    }
    ```
3. Select the data types you would like to receive in the output (i.e. the Includes):
    ```
    {
        "BusinessName": "walmart",
        "Includes": [
            "DatabaseQueryInfo", 
            "ExecutionTimeInfo"
        ]
    }
    Please note, includes do not apply to API partners. Includes are configured at the access profile level and will autmotically be applied.
    ```
4. Set the desired pagination rules:
    ```
    {
        "BusinessName": "dulaney",
        "Includes": [
            "DatabaseQueryInfo", 
            "ExecutionTimeInfo"
        ],
        "Page": 1,
        "ResultsPerPage": 20
    }
    ```
6. Submit your search.

A complete list of JSON request properties follows:

* `PoseidonIds` = null (optional, string[]) ... Poseidon Ids (batch record retrival).
* `TahoeId` = null (optional, string) ... Tahoe Id (individual record retrival).
* `SSN` = null (optional, string) ... Social Security Number (format: ###-##-####).
* `BusinessName` = null (optional, string) ... Business name.
* `DefendantFirstName` = null (optional, string) ... Defendant First name.
* `DefendantMiddleName` = null (optional, string) ... Defendant Middle name or middle initial.
* `DefendantLastName` = null (optional, string) ... Defendant Last name.
* `DefendantNameSuffix` = null (optional, string) ... Defendant Name suffix.
* `PlaintiffFirstName` = null (optional, string) ... Plaintiff First name.
* `PlaintiffMiddleName` = null (optional, string) ... Plaintiff Middle name or middle initial.
* `PlaintiffLastName` = null (optional, string) ... Plaintiff Last name.
* `PlaintiffNameSuffix` = null (optional, string) ... Plaintiff Name suffix.
* `StreetAddress` = null (optional, string) ... Street Address. State is required if StreetAddress is provided. Either StreetAddress or HouseNumber, Street and Unit can be included in search.
* `HouseNumber` = null (optional, string) ... House number cannot be provided without including Street.
* `StreetName` = null (optional, string) ... Street name cannot be provided without including either the City and State, or the City and Zip Code.
* `Unit` = null (optional, string) ... Unit number cannot be provided without including Street.
* `City` = null (optional, string) ... State/Zip is required if city is provided.
* `State` = null (optional, string) ... Two character long state name.
* `ZipCode` = null (optional, string) ... Zip code.

<i><strong>If you are an API partner</strong> and are missing any include/members listed below, then please contact our revenue department so we can adjust your access profile configuration.</i>

* `Includes` (optional, string[]) ... Data to be included in the response.
    * Members
        * `DatabaseQueryInfo`
        * `ExecutionTimeInfo`
* `Page` = 1 (optional, int) ... The page of data to return.
* `ResultsPerPage` = 20 (optional, int) ... The number of results to return per page.

+ Request (application/json)

    + Headers
            
                galaxy-ap-name: Access Profile Name
                galaxy-ap-password: Access Profile Password
                galaxy-client-session-id: APIARY
                galaxy-client-type: Galaxy Client Type

    + Body

            {
                "BusinessName": "walmart",
                "Includes": ["DatabaseQueryInfo", "ExecutionTimeInfo"]
                "Page": 1,
                "ResultsPerPage": 20
            }

+ Response 200 (application/json)

            {
                "evictionRecords": [{
                        "evictionId": -1234567891234567891,
                        "bridge": [{
                            "poseidonId": -1234567891234567891,
                            "tahoeId": "Gxxxxxxxxxxxxxxxxxxx"
                        }, {
                            "poseidonId": -1234567891234567891,
                            "tahoeId": "G-xxxxxxxxxxxxxxxxxxx"
                        }, {
                            "poseidonId": -1234567891234567891,
                            "tahoeId": "Gxxxxxxxxxxxxxxxxxxx"
                        }
                    ],
                    "defendantNames": [{
                        "isBusiness": false,
                        "prefix": "",
                        "firstName": "firstname",
                        "middleName": "",
                        "lastName": "lastname",
                        "suffix": "",
                        "gender": "M",
                        "fullName": "firstname lastname"
                    }],
                    "plaintiffNames": [{
                        "isOwner": false,
                        "prefix": "",
                        "firstName": "firstname",
                        "middleName": "",
                        "lastName": "lastname",
                        "suffix": "",
                        "gender": "M",
                        "fullName": "firstname lastname"
                    }],
                    "addresses": [{
                        "addressType": "Defendant Address",
                        "houseNumber": "1234",
                        "streetDirection": "",
                        "streetName": "StreetName",
                        "streetType": "ST",
                        "streetPostDirection": "",
                        "unitType": "",
                        "unitNumber": "",
                        "city": "Sacramento",
                        "state": "CA",
                        "zipCode": "12345",
                        "zip4": "1234",
                        "longitude": "-121.451962",
                        "latitude": "38.608252",
                        "verificationCodes": ["AS01"],
                        "fullAddress": "1234 StreetName ST; Sacramento, CA 12345-1234"
                    }],
                    "evictionDetails": [{
                        "courtId": "CAxxxxx",
                        "caseNumber": "0xUD0xxxx",
                        "fileDate": "20050928",
                        "liabilityAmount": "000002126",
                        "reportDate": "20051105",
                        "fileType": "CJ",
                        "state": "CA",
                        "unlawfulDetainer": "Y",
                        "assetsInDollar": "000000000",
                        "updateDate": ""
                    }]
                }],
                "counts": {
                    "searchResults": 1
                },
                "pagination": {
                    "currentPageNumber": 1,
                    "resultsPerPage": 20,
                    "totalPages": 1
                },
                "databaseQueryInfo": [{
                    "searchType": null,
                    "hasIntermediateSort": null,
                    "retryCount": null,
                    "idCount": null,
                    "matchRecordCount": null,
                    "databaseQueries": [{
                        "databaseConnectionTimeInMs": 3,
                        "databaseQuery": "",
                        "executionTimeInMs": 1286
                    }]
                }],
                "executionStatistics": [{
                    "description": "Eviction SP Client Search",
                    "startTime": 90,
                    "executionTimeInMs": 1291
                }, {
                    "description": "CALL search_eviction_v2",
                    "startTime": 90,
                    "executionTimeInMs": 1289
                }],
                "searchCriteria": [],
                "totalRequestExecutionTimeMs": 1403,
                "requestId": "601aa9ba-f7f5-4c87-9638-d00e50d36ccb",
                "requestType": "EvictionSearch",
                "requestTime": "2017-09-13T12:42:26.2023305-07:00",
                "isError": false
            }

            
## Foreclosure Search [/ForeclosureSearch]

Performs a Foreclosure search, and returns a list of Foreclosure records matching the search criteria.

### Search [POST]
***Click on the grey search box above, to view sample request/response objects for the Foreclosure Search.***

Perform a search:
1. Add your Access Profile username and password to the request headers.
    * galaxy-ap-name: [Access Profile Name]
    * galaxy-ap-password: [Access Profile Password]
    * galaxy-client-session-id: (Optional) Session ID for logging
    * galaxy-client-type: [Galaxy Client Type] (required for Javascript clients)
    * galaxy-search-type: [Galaxy Search Type] (optional)
        * To auto-populate all includes and filter options in your requests, you may provide a search type value in your request header. A search type is required for all API Customers. Applicable search type values for this endpoint include: 
            1. Foreclosure
2. Add search criteria to your request:
    ```
    {
        "BusinessName": "walmart"
    }
    Or
    {
        "TahoeId": "GXXXXXXXXXXXXXXXXXXX",
        "PoseidonIds": [
            "12345678912345678912",
            "12345678912345678912"
        ],
        "SSN": "XXX-XX-XXXX",
        "FirstName": "John",
        "MiddleName": "",
        "LastName": "Smith",
        "HouseNumber": "",
        "StreetName": "",
        "Unit": "",
        "City": "",
        "State": "",
        "ZipCode": "XXXXX"
    }
    Or
    {
        "TahoeId": "GXXXXXXXXXXXXXXXXXXX",
        "PoseidonIds": [
            "12345678912345678912",
            "12345678912345678912"
        ],
        "SSN": "XXX-XX-XXXX",
        "FirstName": "John",
        "MiddleName": "",
        "LastName": "Smith",
        "StreetAddress": "",
        "City": "",
        "State": "",
        "ZipCode": "XXXXX"
    }
    ```
3. Select the data types you would like to receive in the output (i.e. the Includes):
    ```
    {
        "BusinessName": "walmart",
        "Includes": [
            "DatabaseQueryInfo", 
            "ExecutionTimeInfo"
        ]
    }
    Please note, includes do not apply to API partners. Includes are configured at the access profile level and will autmotically be applied.
    ```
4. Set the desired pagination rules:
    ```
    {
        "BusinessName": "walmart",
        "Includes": [
            "DatabaseQueryInfo", 
            "ExecutionTimeInfo"
        ],
        "Page": 1,
        "ResultsPerPage": 20
    }
    ```
5. Submit your search.

A complete list of JSON request properties follows:

* `PoseidonIds` = null (optional, string[]) ... Poseidon Ids (batch record retrival).
* `TahoeId` = null (optional, string) ... Tahoe Id (individual record retrival).
* `SSN` = null (optional, string) ... Social Security Number (format: ###-##-####).
* `BusinessName` = null (optional, string) ... Business name.
* `FirstName` = null (optional, string) ... First name.
* `MiddleName` = null (optional, string) ... Middle name or middle initial.
* `LastName` = null (optional, string) ... Last name.
* `StreetAddress` = null (optional, string) ... Street Address. State is required if StreetAddress is provided. Either StreetAddress or HouseNumber, Street and Unit can be included in search.
* `HouseNumber` = null (optional, string) ... House number cannot be provided without including Street.
* `StreetName` = null (optional, string) ... Street name cannot be provided without including either the City and State, or the City and Zip Code.
* `Unit` = null (optional, string) ... Unit number cannot be provided without including Street.
* `City` = null (optional, string) ... State/Zip is required if city is provided.
* `State` = null (optional, string) ... Two character long state name.
* `ZipCode` = null (optional, string) ... Zip code.

<i><strong>If you are an API partner</strong> and are missing any include/members listed below, then please contact our revenue department so we can adjust your access profile configuration.</i>

* `Includes` (optional, string[]) ... Data to be included in the response.
    * Members
        * `DatabaseQueryInfo`
        * `ExecutionTimeInfo`
* `Page` = 1 (optional, int) ... The page of data to return.
* `ResultsPerPage` = 20 (optional, int) ... The number of results to return per page.

+ Request (application/json)

    + Headers
            
                galaxy-ap-name: Access Profile Name
                galaxy-ap-password: Access Profile Password
                galaxy-client-session-id: APIARY
                galaxy-client-type: Galaxy Client Type

    + Body

            {
                "BusinessName": "walmart",
                "Includes": ["DatabaseQueryInfo", "ExecutionTimeInfo"]
                "Page": 1,
                "ResultsPerPage": 20
            }

+ Response 200 (application/json)

            {
                "foreclosureRecords": [{
                    "foreclosureId": "-1234567891234567891",
                    "bridge": [{
                        "poseidonId": -1234567891234567891,
                        "tahoeId": "G-xxxxxxxxxxxxxxxxxxx"
                        }, {
                        "poseidonId": -1234567891234567891,
                        "tahoeId": "Gxxxxxxxxxxxxxxxxxxx"
                        }, {
                        "poseidonId": -1234567891234567891,
                        "tahoeId": "Gxxxxxxxxxxxxxxxxxxx"
                    }],
                    "names": [{
                        "isOwner": "",
                        "prefix": "",
                        "firstName": "firstname",
                        "middleName": "",
                        "lastName": "lastname",
                        "suffix": "",
                        "fullName": "firstname lastname"
                    }],
                    "addresses": [{
                        "addrtype": "siteaddr",
                        "houseNumber": "1234",
                        "streetDirection": "",
                        "streetName": "Some",
                        "streetType": "WAY",
                        "streetPostDirection": "",
                        "unitType": "",
                        "unitNumber": "",
                        "city": "Hanford",
                        "state": "CA",
                        "zipCode": "12345",
                        "zip4": "1234",
                        "longitude": "-123.671453",
                        "latitude": "12.337331",
                        "verificationcodes": "AS01",
                        "fullAddress": "1234 Some WAY; Hanford, CA 12345-1234"
                    }],
                    "beneficiaries": [{
                        "beneficiaryFullname": ""
                    }],
                    "foreclosureDetails": [{
                        "sapropertyid": "12345678",
                        "scmId": "48",
                        "fipscounty": "KINGS",
                        "statecode": "CA",
                        "muniname": "KINGS",
                        "sruniqueid": "12345678",
                        "recordtype": "T",
                        "parcelnbrraw": "010 320 086 000",
                        "recordingdate": "20090929",
                        "documentno": "0000017138",
                        "documenttype": "N",
                        "dateorigloan": "19980227",
                        "docnbrorigloan": "0000003789",
                        "origloanamt": "0",
                        "istrustorortrusteebusiness": "Y",
                        "trusteephone": "7147302727",
                        "trusteesalenbr": "74-33695-2",
                        "titlecompanycode": "3342",
                        "titlecompanyname": "TITLE COURT SERVICE",
                        "processid": "123226",
                        "delinquentdate": "",
                        "delinquentamt": "",
                        "balanceprincipal": "95000",
                        "beneficiaryphone": "",
                        "noticeofdefaultauctiondate": "",
                        "noticeofdefaultsaletime": "",
                        "noticeofdefaulttimetype": "",
                        "noticeofdefaultauctionstreetno": "",
                        "noticeofdefaultauctionstreetname": "",
                        "noticeofdefaultauctioncity": "",
                        "amountofdefault": "0",
                        "noticeofsaledate": "20091019",
                        "noticeofsaletime": "12:30",
                        "noticeoftimetype": "P",
                        "noticeofsalestreetno": "1400",
                        "noticeofsalestreetname": "W LACEY BLVD",
                        "noticeofsalecity": "HANFORD",
                        "ntdsauctionbidamount": "0",
                        "receiveddate": "20131004"
                    }]
                }],
                "counts": {
                    "searchResults": 1
                },
                "pagination": {
                    "currentPageNumber": 1,
                    "resultsPerPage": 20,
                    "totalPages": 1
                },
                "databaseQueryInfo": [{
                    "searchType": null,
                    "hasIntermediateSort": null,
                    "retryCount": null,
                    "idCount": null,
                    "matchRecordCount": null,
                    "databaseQueries": [{
                        "databaseConnectionTimeInMs": 3,
                        "databaseQuery": "",
                        "executionTimeInMs": 22
                    }]
                }],
                "executionStatistics": [{
                    "description": "Foreclosure SP Client Search",
                    "startTime": 6,
                    "executionTimeInMs": 26
                }, {
                    "description": "CALL search_foreclosure_criteria_v1_1",
                    "startTime": 6,
                    "executionTimeInMs": 25
                }],
                "searchCriteria": [],
                "totalRequestExecutionTimeMs": 33,
                "requestId": "b00f114a-0731-4aa4-9c48-a56cf28eba85",
                "requestType": "ForeclosureSearch",
                "requestTime": "2017-09-13T15:11:26.6095180-07:00",
                "isError": false
            }

## Property Search [/PropertySearch]
***Click on the grey search box above, to view sample request/response objects for the Property Search.***

Performs a criteria search, and returns a list of matching Assessor and Recorder records.

### Search [POST]

Perform a search:
1. Add your Access Profile username and password to the request headers.
    * galaxy-ap-name: [Access Profile Name]
    * galaxy-ap-password: [Access Profile Password]
    * galaxy-client-session-id: (Optional) Session ID for logging
    * galaxy-client-type: [Galaxy Client Type] (required for Javascript clients)
    * galaxy-search-type: [Galaxy Search Type] (optional)
        * To auto-populate all includes and filter options in your requests, you may provide a search type value in your request header. A search type is required for all API Customers. Applicable search type values for this endpoint include: 
            1. Property
2. Add search criteria to your request:
    ```
    {
        "FirstName": "John",
        "LastName": "Smith",
        "City": "Sacramento",
        "State": "CA"
    }
    ```
3. Set the desired pagination rules:
    ```
    {
        "FirstName": "John",
        "LastName": "Smith",
        "City": "Sacramento",
        "State": "CA",
        "Page": 1,
        "ResultsPerPage": 10
    }
    ```
4. Submit your search.

A complete list of JSON request properties follows:

* `BusinessName` = null (optional, string) ... Business name.
* `FirstName` = null (optional, string) ... First name.
* `MiddleName` = null (optional, string) ... Middle name or middle initial.
* `LastName` = null (optional, string) ... Last name.
* `AddressLine1` = null (optional, string) ... Address line 1 (house number, street, state).
* `HouseNumber` = null (optional, string) ... House number.
* `Street` = null (optional, string) ... Street name.
* `Unit` = null (optional, string) ... Unit number.
* `City` = null (optional, string) ... City.
* `State` = null (optional, string) ... State (2-character code).
* `Zip` = null (optional, string) ... Zip code (5-digit code).
* `Apn` = null (optional, string) ... Assessor Parcel Number.
* `PropertyId` = null (optional, string) ... Unique ID per property record.
* `Includes` (optional, string[]) ... Data to be included in the response.
    * Members
        * `Assessor`
        * `DatabaseQueryInfo`
        * `Recorder`
* `Page` = 1 (optional, int) ... The page of data to return.
* `ResultsPerPage` = 10 (optional, int) ... The number of results to return per page.

+ Request (application/json)

    + Headers

            galaxy-ap-name: Access Profile Name
            galaxy-ap-password: Access Profile Password
            galaxy-client-session-id: APIARY
            galaxy-client-type: Galaxy Client Type

    + Body

            {
                "FirstName": "John",
                "LastName": "Smith",
                "City": "Sacramento",
                "State": "CA"
                "Page": 1,
                "ResultsPerPage": 10
            }

+ Response 200 (application/json)

            {
                "PropertyId" : 5555567555515120000,
                "Apn" : "555 5555 555 5555",
                "RecordType" : "Recorder",
                "StateCode" : "CA",
                "FilingDate" : "1/1/2001",
                "RawData" : "",
                "Names" : [{
                        "IsOwner" : false,
                        "TahoeId" : null,
                        "Prefix" : "",
                        "FirstName" : "",
                        "MiddleName" : "",
                        "LastName" : "SUDER HOLDINGS INC",
                        "Suffix" : "",
                        "FullName" : "SUDER HOLDINGS INC"
                    }
                ],
                "Addresses" : [{
                        "AddressType" : "Mail",
                        "HouseNumber" : "555",
                        "StreetDirection" : "",
                        "StreetName" : "Main",
                        "StreetType" : "ST",
                        "StreetPostDirection" : "",
                        "UnitType" : "",
                        "UnitNumber" : "",
                        "City" : "Sacramento",
                        "State" : "CA",
                        "ZipCode" : "55555",
                        "Zip4" : "5555",
                        "Longitude" : "-55.555555",
                        "Latitude" : "55.555555",
                        "VerificationCodes" : [
                            "AS01"
                        ],
                        "FullAddress" : "555 Main ST; Sacramento, CA 555555-5555"
                    }
                ],
                "AssessorData" : null,
                "RecorderData" : {
                    "maxSrDateTransfer" : "20010101",
                    "mmFipsMuniCode" : "555",
                    "mmFipsStateCode" : "55",
                    "mmMuniCode" : "SA",
                    "mmMuniName" : "SACRAMENTO",
                    "mmStateCode" : "CA",
                    "reoFlag" : null,
                    "srArmsLengthFlagDfs" : "Y",
                    "srDateFiling" : "20010101",
                    "srDateTransfer" : "20010101",
                    "srDoctType" : "G",
                    "srFullPartCode" : "F",
                    "srLndrSellerFlag" : null,
                    "srMultApnFlagKeyed" : null,
                    "srParcelNbrRaw" : "555 5555 555 5555",
                    "srQuitclaim" : null,
                    "srTranType" : "R",
                    "srValTransfer" : "555000",
                    "maxSrDateTransferFormatted" : "1/1/2001",
                    "srDateFilingFormatted" : "1/1/2001",
                    "srDateTransferFormatted" : "1/1/2001"
                },
                "Warnings" : null,
                "ApnFormatted" : null
            }
            
## Reverse Phone Search [/ReversePhoneSearch]

Performs a reverse phone search, and returs a list of people matching the search criteria.

### Search [POST]
***Click on the grey search box above, to view sample request/response objects for the Reverse Phone Search.***

Perform a search:
1. Add your Access Profile username and password to the request headers.
    * galaxy-ap-name: [Access Profile Name]
    * galaxy-ap-password: [Access Profile Password]
    * galaxy-client-session-id: (Optional) Session ID for logging
    * galaxy-client-type: [Galaxy Client Type] (required for Javascript clients)
    * galaxy-search-type: [Galaxy Search Type] (optional)
        * To auto-populate all includes and filter options in your requests, you may provide a search type value in your request header. A search type is required for all API Customers. Applicable search type values for this endpoint include: 
            1. ReversePhone
2. Add search criteria to your request:
    ```
    {
        "Phone": "123-456-7890"
    }
    ```
3. Select the data types you would like to receive in the output (i.e. the Includes):
    ```
    {
        "Phone": "123-456-7890",
        "Includes": ["FullRecord", "DatabaseQueryInfo", "Sources"]
    }
    ```
4. Select any desired data filters:
    ```
    {
        "Phone": "123-456-7890",
        "Includes": ["FullRecord", "DatabaseQueryInfo", "Sources"],
        "FilterOptions": ["IncludePrivateData", 
                          "IncludeOptOutData", 
                          "IncludeAllDataSources", 
                          "IncludeResultsWithMissingNames", 
                          "DisplayNpaResults", 
                          "EnableThirdPartyDataSourceLookup"
                         ]
    }
    ```
5. Set the desired pagination rules:
    ```
    {
        "Phone": "123-456-7890",
        "Includes": ["FullRecord", "DatabaseQueryInfo", "Sources"],
        "FilterOptions": ["IncludePrivateData", 
                          "IncludeOptOutData", 
                          "IncludeAllDataSources", 
                          "IncludeResultsWithMissingNames", 
                          "DisplayNpaResults", 
                          "EnableThirdPartyDataSourceLookup"
                         ],
        "Page": 1,
        "ResultsPerPage": 10
    }
    ```
6. Submit your search.

A complete list of JSON request properties follows:

* `Phone` = 123-456-7890 (required, string) ... Phone number (format: ###-###-####, ##########, (###) ###-####)
* `Includes` (optional, string[]) .. Data to be included in the response.
    * Members
        * `FullRecord`
        * `DatabaseQueryInfo`
        * `Sources`
* `FilterOptions` (optional, string[]) .. Data filtering options.
    * Members
        * `IncludePrivateData`
        * `IncludeOptOutData`
        * `IncludeAllDataSources`
        * `IncludeResultsWithMissingNames`
        * `DisplayNpaResults`
        * `EnableThirdPartyDataSourceLookup`
* `Page` = 1 (optional, int) ... The page of data to return.
* `ResultsPerPage` = 10 (optional, int) ... The number of results to return per page.
* `TahoeBlobRetrievalLimit` = null (optional, int) ... The number of Tahoe results to consider.

+ Request (application/json)
    + Headers
        
            galaxy-ap-name: Access Profile Name
            galaxy-ap-password: Access Profile Password
            galaxy-client-session-id: APIARY
            galaxy-client-type: Galaxy Client Type

    + Body
    
            {
                "Phone": "123-456-7890",
                "Includes": ["FullRecord", "DatabaseQueryInfo", "Sources"],
                "FilterOptions": ["IncludePrivateData", 
                                  "IncludeOptOutData", 
                                  "IncludeAllDataSources", 
                                  "IncludeResultsWithMissingNames", 
                                  "DisplayNpaResults", 
                                  "EnableThirdPartyDataSourceLookup"
                                 ],
                "Page": 1,
                "ResultsPerPage": 10
            }

+ Response 200 (application/json)

        {
           "PhoneNumber": "(123) 456-7890",
           "Addresses": [
              {
                 "HouseNumber": "5555",
                 "StreetPreDirection": "",
                 "StreetName": "Some Street",
                 "StreetPostDirection": "",
                 "StreetType": "",
                 "Unit": "",
                 "UnitType": null,
                 "City": "Some City",
                 "State": "CA",
                 "Zip": "12345",
                 "Zip4": "1234",
                 "FullAddress": "5555 Some Steet; Some City, CA 12345-1234"
              }
           ],
           "Names": [
              {
                 "Prefix": "Mr",
                 "FirstName": "XYZ",
                 "MiddleName": "ABC",
                 "LastName": "PQR",
                 "Suffix": ""
              }
           ],
           "Carrier": "POWERTEL ATLANTA LICENSES, INC.",
           "PhoneType": "Cell",
           "TimeZone": "Eastern",
           "Latitude": "55.5555",
           "Longitude": "-55.5555",
           "RecordId": "G1234567890123456789",
           "DataSource": "Tahoe",
           "SecondaryDataSource": null,
           "FirstReportedDate": "2/7/2010",
           "LastReportedDate": "12/5/2016",
           "FullRecord": null
        }

## Work Place Search [/WorkplaceSearch]

Performs a criteria search, and returns a list of matching businesses.

### Search [POST]
***Click on the grey search box above, to view sample request/response objects for the Work Place Search.***

Perform a search:
1. Add your Access Profile username and password to the request headers.
    * galaxy-ap-name: [Access Profile Name]
    * galaxy-ap-password: [Access Profile Password]
    * galaxy-client-session-id: (Optional) Session ID for logging
    * galaxy-client-type: [Galaxy Client Type] (required for Javascript clients)
    * galaxy-search-type: [Galaxy Search Type] (optional)
        * To auto-populate all includes and filter options in your requests, you may provide a search type value in your request header. A search type is required for all API Customers. Applicable search type values for this endpoint include: 
            1. Workplace
2. Add search criteria to your request:
    ```
    {
        "BusinessName": '',
    }
    Or
    {
      "FirstName": '',
      "MiddleName": '',
      "LastName": '',
      "Dob": '',
      "AddressLine1": '',
      "HouseNumber": '',
      "Street": '',
      "Unit": '',
      "City": '',
      "State": '',
      "Zip": '',
      "Phone": '',
      "Page": '',
      "ResultsPerPage": ''
    }
    Or
    {
        "TahoeId": '',
    }
    Or
    {
        "WorkplaceSearchId": '',
    }
    ```
3. Set the desired pagination rules:
    ```
    {
        "FirstName": "John",
        "LastName": "Doe",
        "City": "Sacramento",
        "State": "CA",
        "Page": 1,
        "ResultsPerPage": 20,
        "OriginatingIpAddress": "1.2.3.4",
        "Includes": [
            "DatabaseQueryInfo",
            "ExecutionTimeInfo"
        ],
        "FilterOptions": []
    }
    ```
4. Submit your search.

A complete list of JSON request properties follows:

* `BusinessName` = null (optional, string) ... Business name.
* `FirstName` = null (optional, string) ... First name.
* `MiddleName` = null (optional, string) ... Middle name or middle initial.
* `LastName` = null (optional, string) ... Last name.
* `AddressLine1` = null (optional, string) ... Address line 1 (house number, street, state).
* `HouseNumber` = null (optional, string) ... House number.
* `Street` = null (optional, string) ... Street name.
* `City` = null (optional, string) ... City.
* `State` = null (optional, string) ... State (2-character code).
* `Zip` = null (optional, string) ... Zip code (5-digit code).
* `Includes` (optional, string[]) ... Data to be included in the response.
    * Members
        * `DatabaseQueryInfo`
        * `ExecutionTimeInfo`
* `Page` = 1 (optional, int) ... The page of data to return.
* `ResultsPerPage` = 10 (optional, int) ... The number of results to return per page.

+ Request (application/json)

    + Headers

            galaxy-ap-name: Access Profile Name
            galaxy-ap-password: Access Profile Password
            galaxy-client-session-id: APIARY
            galaxy-client-type: Galaxy Client Type

    + Body

            {
                "BusinessName": "Hot dog stand",
                "Page": 1,
                "ResultsPerPage": 10
            }

+ Response 200 (application/json)

            {
                "workplaceRecords": [
                    {
                      "requestId": 70262849,
                      "fullName": "John",
                      "salutation": "",
                      "firstName": "John",
                      "middleName": "",
                      "lastName": "Doe",
                      "suffix": "",
                      "professionalTitles": "",
                      "addresses": [
                        {
                          "location": "",
                          "addressLine1": "",
                          "city": "New york",
                          "state": "NY",
                          "zip": ""
                        }
                      ],
                      "phoneNumbers": [],
                      "emailAddresses": [],
                      "education": [
                        {
                          "school": "",
                          "schoolMatch": "",
                          "degree": "",
                          "degreeMatch": "",
                          "major": "",
                          "schoolStartDate": "1980-01-01T00:00:00",
                          "schoolEndDate": "1982-01-01T00:00:00"
                        }
                      ],
                      "workExperience": [
                        {
                          "expJobTitle": "",
                          "expCompanyProfileURL": "",
                          "expCompany": "",
                          "expCompanyDetails": "",
                          "expStartDate": "",
                          "expEndDate": "",
                          "expDuration": "",
                          "company": {
                            "companyId": "",
                            "companyName": "",
                            "companyAddress1": "",
                            "companyAddress2": "",
                            "companyCity": "",
                            "companyState": "",
                            "companyZipCode": "",
                            "companyCountry": "United States",
                            "companyIndustry": "",
                            "companyType": "",
                            "companyStatus": "",
                            "companySize": "",
                            "companyFounded": "",
                            "companyWebSite": "",
                            "companyMedianAge": "",
                            "companyMedianTenure": "",
                            "companyMalePercentage": "",
                            "companyFemalePercentage": "",
                            "companyEmail": "",
                            "companyHeadQuarters": "",
                            "companyRoles": []
                          }
                        }
                      ],
                      "impliedInfo": [],
                      "miscInfo": [
                        {
                          "attributeName": "Groups",
                          "attributeValue": "Skip Tracing - Auto Finance Industry"
                        },
                        {
                          "attributeName": "Websites",
                          "attributeValue": "http://Www.somewebsite.com"
                        }
                      ]
                    }
                  ],
                  "counts": {
                    "searchResults": 1
                  },
                  "pagination": {
                    "currentPageNumber": 1,
                    "resultsPerPage": 20,
                    "totalPages": 1
                  },
                  "databaseQueryInfo": [
                    {
                      "searchType": null,
                      "hasIntermediateSort": null,
                      "retryCount": null,
                      "idCount": null,
                      "matchRecordCount": null,
                      "databaseQueries": [
                        {
                          "databaseConnectionTimeInMs": 0,
                          "databaseQuery": "CALL search_workplace_v1_1(@p_output_type := null, @p_business_name := null, @p_first_name := 'x', @p_middle_name := null, @p_last_name := 'xx', @p_street_address := null, @p_house_number := null, @p_street_name := null, @p_unit := null, @p_city := 'x', @p_state := 'x', @p_zip_code := null, @p_phone := null, @p_dob := null, @p_use_fuzzy_search := null, @p_apply_fn_syn := True, @p_pro_flag := null, @p_record_key_list := '123', @p_tahoe_id := 0, @p_surprise_me := False, @p_record_limit := 20);",
                          "executionTimeInMs": 62
                        }
                      ]
                    }
                  ],
                  "executionStatistics": [
                    {
                      "description": "Workplace SP Client Search",
                      "startTime": 0,
                      "executionTimeInMs": 62
                    },
                    {
                      "description": "CALL search_workplace_v1_1",
                      "startTime": 0,
                      "executionTimeInMs": 62
                    }
                  ],
                  "searchCriteria": [],
                  "totalRequestExecutionTimeMs": 63,
                  "requestId": "978d8c22-2f3e-4402-867f-704ad430c6db",
                  "requestType": "WorkplaceSearch",
                  "requestTime": "2017-02-09T15:17:14.6250652-08:00",
                  "isError": false
            }
            
## Marriage Search [/MarriageSearch]

Performs a marriage search, and returns a list of marriage records matching search criteria.

### Search [POST]
***Click on the grey search box above, to view sample request/response objects for the Marriage Search.***

Perform a search:
1. Add your Access Profile username and password to the request headers.
    * galaxy-ap-name: [Access Profile Name]
    * galaxy-ap-password: [Access Profile Password]
    * galaxy-client-session-id: (Optional) Session ID for logging
    * galaxy-client-type: [Galaxy Client Type] (required for Javascript clients)
    * galaxy-search-type: [Galaxy Search Type] (optional)
        * To auto-populate all includes and filter options in your requests, you may provide a search type value in your request header. A search type is required for all API Customers. Applicable search type values for this endpoint include: 
            1. Marriage
2. Add search criteria to your request:
    ```
    {
        "FirstName": "John",
        "MiddleName": "",
        "LastName": "Smith",
        "NameSuffix": "",
        "MaidenName": "",
        "SpouseFirstName": "",
        "SpouseMiddleName": "",
        "SpouseLastName":"",
        "SpouseNameSuffix": "",
        "MarriageDate": "",
        "City": "Sacramento",
        "County": "",
        "State": "CA",
        "PosiedonIds": [
            "XXXXXXXX",
            "XXXXXXXX"
        ],
        "TahoeId": "G-XXXXXXXXXXXXXXXXXXX",
        "SSN": "xxxxxxxxx"
    }
    ```
3. Set the desired pagination rules:
    ```
    {
        "FirstName": "John",
        "MiddleName": "",
        "LastName": "Smith",
        "NameSuffix": "",
        "MaidenName": "",
        "SpouseFirstName": "",
        "SpouseMiddleName": "",
        "SpouseLastName":"",
        "SpouseNameSuffix": "",
        "MarriageDate": "MM/DD/YYYY",
        "City": "Sacramento",
        "County": "",
        "State": "CA",
        "PosiedonIds": [
            "XXXXXXXX",
            "XXXXXXXX"
        ],
        "TahoeId": "G-XXXXXXXXXXXXXXXXXXX",
        "SSN": "XXXXXXXXX",
        "Page": 1,
        "ResultsPerPage": 10
    }
    ```
4. Submit your search.

A complete list of JSON request properties follows:

* `FirstName` = null (optional, string) ... First name.
* `MiddleName` = null (optional, string) ... Middle name.
* `LastName` = null (optional, string) ... Last name.
* `NameSuffix` = null (optional, string) ... Name suffix (Maximum 4 characters long).
* `MaidenName` = null (optional, string) ... Maiden name.
* `SpouseFirstName` = null (optional, string) ... Spouse first name.
* `SpouseMiddleName` = null (optional, string) ... Spouse middle name.
* `SpouseLastName` = null (optional, string) ... Spouse last name.
* `SpouseNameSuffix` = null (optional, string) ... Spouse name suffix (Maximum 4 characters long).
* `MarriageDate` = null (optional, string) ... Marriage date. (MM/DD/YYYY).
* `City` = null (optional, string) ... City.
* `County` = null (optional, string) ... County.
* `State` = null (optional, string) ... State (2-character code) (State is required when City is provided).
* `PosiedonIds` = null (optional, string[]) ... Posiedon Ids.
* `TahoeId` = null (optional, string) ... Tahoe Id (Format: G-XXXXXXXXXXXXXXXXXXX or GXXXXXXXXXXXXXXXXXXX).
* `SSN` = null (optional, string) ... Social Security Number (Format: XXXXXXXXX).
* `Includes` (optional, string[]) ... Data to be included in the response.
    * Members
        * `DatabaseQueryInfo`
        * `ExecutionTimeInfo`
* `Page` = 1 (optional, int) ... The page of data to return.
* `ResultsPerPage` = 10 (optional, int) ... The number of results to return per page.

+ Request (application/json)

    + Headers

            galaxy-ap-name: Access Profile Name
            galaxy-ap-password: Access Profile Password
            galaxy-client-session-id: APIARY
            galaxy-client-type: Galaxy Client Type

    + Body

            {
                "FirstName": "John",
                "LastName": "Smith",
                "State": "CA",
                "Page": 1,
                "ResultsPerPage": 10,
                "Includes": [
                  "DatabaseQueryInfo",
                  "ExecutionTimeInfo"
                ],
                "FilterOptions": []
            }

+ Response 200 (application/json)

            {
              "records": [
                {
                  "posiedonId": "XXXXXXXX",
                  "spouseKey": "SpouseKey",
                  "spouseGender": "Male",
                  "spouseFirstName": "FirstName",
                  "spouseMiddleName": "MiddleName",
                  "spouseLastName": "LastName",
                  "spouseNameSuffix": "",
                  "spouseMaidenName": "",
                  "spouseAge": 25,
                  "otherSpouseFirstName": "FirstName",
                  "otherSpouseMiddleName": "MiddleName",
                  "otherSpouseLastName": "LastName",
                  "otherSpouseNameSuffix": "",
                  "otherSpouseAge": 24,
                  "otherSpouseFullName": "FirstName MiddleName LastName",
                  "marriageDate": "M/DD/YYYY",
                  "divorceDate": "0",
                  "certificatNo": "UNKNOWN",
                  "recordType": "M",
                  "state": "Ca",
                  "county": "Sacramento",
                  "recordSubType": "",
                  "decree": "0",
                  "fileId": "",
                  "caseBookId": ""
                }
              ]
            }
            
## Divorce Search [/DivorceSearch]

Performs a divorce search, and returns a list of divorce records matching search criteria.

### Search [POST]
***Click on the grey search box above, to view sample request/response objects for the Divorce search.***

Perform a search:
1. Add your Access Profile username and password to the request headers.
    * galaxy-ap-name: [Access Profile Name]
    * galaxy-ap-password: [Access Profile Password]
    * galaxy-client-session-id: (Optional) Session ID for logging
    * galaxy-client-type: [Galaxy Client Type] (required for Javascript clients)
    * galaxy-search-type: [Galaxy Search Type] (optional)
        * To auto-populate all includes and filter options in your requests, you may provide a search type value in your request header. A search type is required for all API Customers. Applicable search type values for this endpoint include: 
            1. Divorce
2. Add search criteria to your request:
    ```
    {
        "FirstName": "John",
        "MiddleName": "",
        "LastName": "Smith",
        "NameSuffix": "",
        "MaidenName": "",
        "SpouseFirstName": "",
        "SpouseMiddleName": "",
        "SpouseLastName":"",
        "SpouseNameSuffix": "",
        "MarriageDate": "",
        "DivorceDate: "",
        "City": "Sacramento",
        "County": "",
        "State": "CA",
        "PosiedonIds": [
            "XXXXXXXX",
            "XXXXXXXX"
        ],
        "TahoeId": "G-XXXXXXXXXXXXXXXXXXX",
        "SSN": "xxxxxxxxx"
    }
    ```
3. Set the desired pagination rules:
    ```
    {
        "FirstName": "John",
        "MiddleName": "",
        "LastName": "Smith",
        "NameSuffix": "",
        "MaidenName": "",
        "SpouseFirstName": "",
        "SpouseMiddleName": "",
        "SpouseLastName":"",
        "SpouseNameSuffix": "",
        "MarriageDate": "MM/DD/YYYY",
        "DivorceDate: "MM/DD/YYYY",
        "City": "Sacramento",
        "County": "",
        "State": "CA",
        "PosiedonIds": [
            "XXXXXXXX",
            "XXXXXXXX"
        ],
        "TahoeId": "G-XXXXXXXXXXXXXXXXXXX",
        "SSN": "XXXXXXXXX",
        "Page": 1,
        "ResultsPerPage": 10
    }
    ```
4. Submit your search.

A complete list of JSON request properties follows:

* `FirstName` = null (optional, string) ... First name.
* `MiddleName` = null (optional, string) ... Middle name.
* `LastName` = null (optional, string) ... Last name.
* `NameSuffix` = null (optional, string) ... Name suffix (Maximum 4 characters long).
* `MaidenName` = null (optional, string) ... Maiden name.
* `SpouseFirstName` = null (optional, string) ... Spouse first name.
* `SpouseMiddleName` = null (optional, string) ... Spouse middle name.
* `SpouseLastName` = null (optional, string) ... Spouse last name.
* `SpouseNameSuffix` = null (optional, string) ... Spouse name suffix (Maximum 4 characters long).
* `MarriageDate` = null (optional, string) ... Marriage date. (MM/DD/YYYY).
* `DivorceDate` = null (optional, string) ... Divorce date. (MM/DD/YYYY).
* `City` = null (optional, string) ... City.
* `County` = null (optional, string) ... County.
* `State` = null (optional, string) ... State (2-character code) (State is required when City is provided).
* `PosiedonIds` = null (optional, string[]) ... Posiedon Ids.
* `TahoeId` = null (optional, string) ... Tahoe Id (Format: G-XXXXXXXXXXXXXXXXXXX or GXXXXXXXXXXXXXXXXXXX).
* `SSN` = null (optional, string) ... Social Security Number (Format: XXXXXXXXX).
* `Includes` (optional, string[]) ... Data to be included in the response.
    * Members
        * `DatabaseQueryInfo`
        * `ExecutionTimeInfo`
* `Page` = 1 (optional, int) ... The page of data to return.
* `ResultsPerPage` = 10 (optional, int) ... The number of results to return per page.

+ Request (application/json)

    + Headers

            galaxy-ap-name: Access Profile Name
            galaxy-ap-password: Access Profile Password
            galaxy-client-session-id: APIARY
            galaxy-client-type: Galaxy Client Type

    + Body

            {
                "DivorceDate": "02/07/1983"
                "Page": 1,
                "ResultsPerPage": 10,
                "Includes": [
                  "DatabaseQueryInfo",
                  "ExecutionTimeInfo"
                ],
                "FilterOptions": []
            }

+ Response 200 (application/json)

            {
              "records": [
                {
                  "posiedonId": "XXXXXXXX",
                  "spouseKey": "SouseKey",
                  "spouseGender": "",
                  "spouseFirstName": "FirstName",
                  "spouseMiddleName": "MiddleName",
                  "spouseLastName": "LastName",
                  "spouseNameSuffix": "",
                  "spouseMaidenName": "",
                  "spouseAge": 0,
                  "otherSpouseFirstName": "FirstName",
                  "otherSpouseMiddleName": "MiddleName",
                  "otherSpouseLastName": "LastName",
                  "otherSpouseNameSuffix": "",
                  "otherSpouseAge": 0,
                  "otherSpouseFullName": "FirstName MiddleName LastName",
                  "marriageDate": "0",
                  "divorceDate": "2/7/1983",
                  "certificatNo": "XXXXXXX",
                  "recordType": "D",
                  "state": "Nv",
                  "county": "Unknown",
                  "recordSubType": "",
                  "decree": "1",
                  "fileId": "XXXXXXX",
                  "caseBookId": ""
                }
              ]
            }
            
## ProLicense Search [/ProLicenseSearch]

Performs a ProLicense search, and returns a list of ProLicense records matching the search criteria.

### Search [POST]
***Click on the grey search box above, to view sample request/response objects for the ProLicense Search.***

Perform a search:
1. Add your Access Profile username and password to the request headers.
    * galaxy-ap-name: [Access Profile Name]
    * galaxy-ap-password: [Access Profile Password]
    * galaxy-client-session-id: (Optional) Session ID for logging
    * galaxy-client-type: [Galaxy Client Type] (required for Javascript clients)
    * galaxy-search-type: [Galaxy Search Type] (optional)
        * To auto-populate all includes and filter options in your requests, you may provide a search type value in your request header. A search type is required for all API Customers. Applicable search type values for this endpoint include: 
            1. ProLicense
2. Add search criteria to your request:
    ```
    {
        "BusinessName": "dulaney"
    }
    Or
    {
        "TahoeId": "GXXXXXXXXXXXXXXXXXXX",
        "PoseidonIds": [
            "CB2B#XXXXXX",
            "CB2B#XXXXXXXX"
        ],
        "SSN": "XXX-XX-XXXX",
        "FirstName": "John",
        "MiddleName": "",
        "LastName": "Smith",
        "LicenseType": "",
        "LicenseNumber": ""
        "HouseNumber": "",
        "StreetName": "",
        "Unit": "",
        "City": "",
        "State": "",
        "ZipCode": "XXXXX"
    }
    Or
    {
        "TahoeId": "GXXXXXXXXXXXXXXXXXXX",
        "PoseidonIds": [
            "CB2B#XXXXXX",
            "CB2B#XXXXXXXX"
        ],
        "SSN": "XXX-XX-XXXX",
        "FirstName": "John",
        "MiddleName": "",
        "LastName": "Smith",
        "LicenseType": "",
        "LicenseNumber": ""
        "HouseNumber": "",
        "StreetName": "",
        "Unit": "",
        "City": "",
        "State": "",
        "ZipCode": "XXXXX"
    }
    ```
3. Select the data types you would like to receive in the output (i.e. the Includes):
    ```
    {
        "BusinessName": "dulaney",
        "Includes": [
            "IncludeFullSsnValues", 
            "DatabaseQueryInfo", 
            "ExecutionTimeInfo"
        ]
    }
    Please note, includes do not apply to API partners. Includes are configured at the access profile level and will autmotically be applied.
    ```
4. Set the desired pagination rules:
    ```
    {
        "BusinessName": "dulaney",
        "Includes": [
            "IncludeFullSsnValues", 
            "DatabaseQueryInfo", 
            "ExecutionTimeInfo"
        ]
        "Page": 1,
        "ResultsPerPage": 20
    }
    ```
5. Submit your search.

A complete list of JSON request properties follows:

* `PoseidonIds` = null (optional, string[]) ... Poseidon Ids (batch record retrival).
* `TahoeId` = null (optional, string) ... Tahoe Id (individual record retrival).
* `SSN` = null (optional, string) ... Social Security Number (format: ###-##-####).
* `BusinessName` = null (optional, string) ... Business name.
* `FirstName` = null (optional, string) ... First name.
* `MiddleName` = null (optional, string) ... Middle name or middle initial.
* `LastName` = null (optional, string) ... Last name.
* `LicenseType` = null (optional, string) ... LicenseType.
* `LicenseNumber` = null (optional, string) ... LicenseNumber.
* `AddressLine1` = null (optional, string) ... Address line one. State is required if AddressLine1 is provided. Either AddressLine1 or HouseNumber, Street and Unit can be included in search.
* `HouseNumber` = null (optional, string) ... House number cannot be provided without including Street.
* `StreetName` = null (optional, string) ... Street name cannot be provided without including either the City and State, or the City and Zip Code.
* `Unit` = null (optional, string) ... Unit number cannot be provided without including Street.
* `City` = null (optional, string) ... State/Zip is required if city is provided.
* `State` = null (optional, string) ... Two character long state name.
* `ZipCode` = null (optional, string) ... Zip code.


<i><strong>If you are an API partner</strong> and are missing any include/members listed below, then please contact our revenue department so we can adjust your access profile configuration.</i>

* `Includes` (optional, string[]) ... Data to be included in the response.
    * Members
        * `IncludeFullSsnValues`
        * `DatabaseQueryInfo`
        * `ExecutionTimeInfo`
        
* `Page` = 1 (optional, int) ... The page of data to return.
* `ResultsPerPage` = 20 (optional, int) ... The number of results to return per page.

+ Request (application/json)

    + Headers
            
                galaxy-ap-name: Access Profile Name
                galaxy-ap-password: Access Profile Password
                galaxy-client-session-id: APIARY
                galaxy-client-type: Galaxy Client Type

    + Body
            
            {
            "BusinessName": "smith",
            "Page": 1,
            "ResultsPerPage": 20,
            "Includes": [
            "DatabaseQueryInfo",
            "ExecutionTimeInfo"
            ]
            }

+ Response 200 (application/json)

         {
        "proLicenseRecords": [
        {
            "proLicensesId": "-5317284065384629492",
            "bridge": [],
            "names": [
                {
                    "prefix": "",
                    "firstName": "Google",
                    "middleName": "",
                    "lastName": "Financial Services Inc",
                    "suffix": "",
                    "tahoeId": null,
                    "gender": "U",
                    "ssn": "",
                    "fullName": "Google Financial Services Inc",
                    "individualId": 5743948404294657512
                }
            ],
            "addresses": [
                {
                    "houseNumber": "1910",
                    "streetDirection": "W",
                    "streetName": "Lagoon",
                    "streetType": "RD",
                    "streetPostDirection": "",
                    "unitType": "",
                    "unitNumber": "",
                    "city": "Pleasanton",
                    "state": "CA",
                    "zipCode": "94566",
                    "zip4": "3402",
                    "longitude": "-121.899057",
                    "latitude": "37.652399",
                    "verificationCodes": [
                        "AS01"
                    ],
                    "maxExpiredate": "6/9/2008",
                    "minExpireDate": "6/9/2008",
                    "maxIssuedate": "",
                    "minIssuedate": ""
                },
                {
                    "houseNumber": "844",
                    "streetDirection": "",
                    "streetName": "Saint Lucia",
                    "streetType": "CT",
                    "streetPostDirection": "",
                    "unitType": "",
                    "unitNumber": "",
                    "city": "San Jose",
                    "state": "CA",
                    "zipCode": "95127",
                    "zip4": "1036",
                    "longitude": "-121.844555",
                    "latitude": "37.388244",
                    "verificationCodes": [
                        "AS01"
                    ],
                    "maxExpiredate": "6/9/2008",
                    "minExpireDate": "6/9/2008",
                    "maxIssuedate": "",
                    "minIssuedate": ""
                }
            ],
            "attributes": [
                {
                    "licenseNumber": "01430804",
                    "licenseStatus": "N",
                    "originalIssuedate": "6/10/2004",
                    "minIssuedate": "6/10/2004",
                    "maxIssuedate": "6/10/2004",
                    "minExpiredate": "6/9/2008",
                    "maxExpiredate": "6/9/2008",
                    "licenseState": "CA",
                    "licenseCategory": "",
                    "licenseType": "C"
                }
            ],
            "phone": null,
            "businessNames": [
                {
                    "businessId": -5317284065384629492,
                    "businessName": "GOOGLE FINANCIAL SERVICES INC"
                }
            ],
            "ownerName": null
        },
        {
            "proLicensesId": "-3080467525499269631",
            "bridge": [],
            "names": [
                {
                    "prefix": "",
                    "firstName": "Google",
                    "middleName": "",
                    "lastName": "Inc Financial Services",
                    "suffix": "",
                    "tahoeId": null,
                    "gender": "U",
                    "ssn": "",
                    "fullName": "Google Inc Financial Services",
                    "individualId": 7888000710532425935
                }
            ],
            "addresses": [
                {
                    "houseNumber": "",
                    "streetDirection": "",
                    "streetName": "",
                    "streetType": "",
                    "streetPostDirection": "",
                    "unitType": "",
                    "unitNumber": "",
                    "city": "844 Saint Lucia",
                    "state": "CT",
                    "zipCode": "",
                    "zip4": "",
                    "longitude": "",
                    "latitude": "",
                    "verificationCodes": [
                        "AE01",
                        "AE07"
                    ],
                    "maxExpiredate": "7/13/2004",
                    "minExpireDate": "7/13/2004",
                    "maxIssuedate": "6/10/2004",
                    "minIssuedate": "6/10/2004"
                }
            ],
            "attributes": [
                {
                    "licenseNumber": "01430804",
                    "licenseStatus": "Expired",
                    "originalIssuedate": "6/10/2004",
                    "minIssuedate": "6/10/2004",
                    "maxIssuedate": "6/10/2004",
                    "minExpiredate": "7/13/2004",
                    "maxExpiredate": "7/13/2004",
                    "licenseState": "CA",
                    "licenseCategory": "REALTORS",
                    "licenseType": "C"
                }
            ],
            "phone": null,
            "businessNames": null,
            "ownerName": null
        },
        {
            "proLicensesId": "-2877903308561621501",
            "bridge": [],
            "names": [
                {
                    "prefix": "",
                    "firstName": "Google",
                    "middleName": "",
                    "lastName": "Inc Financial Services",
                    "suffix": "",
                    "tahoeId": null,
                    "gender": "U",
                    "ssn": "",
                    "fullName": "Google Inc Financial Services",
                    "individualId": -8420864180640764165
                }
            ],
            "addresses": null,
            "attributes": [
                {
                    "licenseNumber": "01430804",
                    "licenseStatus": "Expired",
                    "licenseState": "CA",
                    "licenseCategory": "REALTORS",
                    "licenseType": "C"
                }
            ],
            "phone": null,
            "businessNames": null,
            "ownerName": null
        },
        {
            "proLicensesId": "-891519381889567160",
            "bridge": [],
            "names": [
                {
                    "prefix": "",
                    "firstName": "Google",
                    "middleName": "",
                    "lastName": "Inc Financial Services",
                    "suffix": "",
                    "tahoeId": null,
                    "gender": "U",
                    "ssn": "",
                    "fullName": "Google Inc Financial Services",
                    "individualId": 8666910347028148770
                }
            ],
            "addresses": [
                {
                    "houseNumber": "",
                    "streetDirection": "",
                    "streetName": "",
                    "streetType": "",
                    "streetPostDirection": "",
                    "unitType": "",
                    "unitNumber": "",
                    "city": "844 Saint Lucia",
                    "state": "CT",
                    "zipCode": "",
                    "zip4": "",
                    "longitude": "",
                    "latitude": "",
                    "verificationCodes": [
                        "AE01",
                        "AE07"
                    ],
                    "maxExpiredate": "",
                    "minExpireDate": "",
                    "maxIssuedate": "",
                    "minIssuedate": ""
                }
            ],
            "attributes": [
                {
                    "licenseNumber": "01430804",
                    "licenseStatus": "Expired",
                    "licenseState": "CA",
                    "licenseCategory": "REALTORS",
                    "licenseType": "C"
                }
            ],
            "phone": null,
            "businessNames": null,
            "ownerName": null
        },
        {
            "proLicensesId": "2933257562954159364",
            "bridge": [],
            "names": [
                {
                    "prefix": "",
                    "firstName": "Google",
                    "middleName": "",
                    "lastName": "Inc Financial Services",
                    "suffix": "",
                    "tahoeId": null,
                    "gender": "U",
                    "ssn": "",
                    "fullName": "Google Inc Financial Services",
                    "individualId": 3432209059547503869
                }
            ],
            "addresses": null,
            "attributes": [
                {
                    "licenseNumber": "01430804",
                    "licenseStatus": "Expired",
                    "originalIssuedate": "6/10/2004",
                    "minIssuedate": "6/10/2004",
                    "maxIssuedate": "6/10/2004",
                    "minExpiredate": "5/16/2006",
                    "maxExpiredate": "5/16/2006",
                    "licenseState": "CA",
                    "licenseCategory": "REALTORS",
                    "licenseType": "C"
                }
            ],
            "phone": null,
            "businessNames": null,
            "ownerName": null
        },
        {
            "proLicensesId": "3492857278978083145",
            "bridge": [],
            "names": [
                {
                    "prefix": "",
                    "firstName": "Google",
                    "middleName": "",
                    "lastName": "Inc Financial Services",
                    "suffix": "",
                    "tahoeId": null,
                    "gender": "U",
                    "ssn": "",
                    "fullName": "Google Inc Financial Services",
                    "individualId": 659339160851390335
                }
            ],
            "addresses": null,
            "attributes": [
                {
                    "licenseNumber": "01430804",
                    "licenseStatus": "Active",
                    "originalIssuedate": "6/10/2004",
                    "minIssuedate": "6/10/2004",
                    "maxIssuedate": "6/10/2004",
                    "minExpiredate": "5/16/2006",
                    "maxExpiredate": "5/16/2006",
                    "licenseState": "CA",
                    "licenseCategory": "",
                    "licenseType": "C"
                }
            ],
            "phone": null,
            "businessNames": null,
            "ownerName": null
        },
        {
            "proLicensesId": "4841067337194872938",
            "bridge": [],
            "names": [
                {
                    "prefix": "",
                    "firstName": "Chao-jung",
                    "middleName": "",
                    "lastName": "Li",
                    "suffix": "",
                    "tahoeId": null,
                    "gender": "U",
                    "ssn": "",
                    "fullName": "Chao-jung Li",
                    "individualId": -3830304358883656968
                }
            ],
            "addresses": [
                {
                    "houseNumber": "1910",
                    "streetDirection": "W",
                    "streetName": "Lagoon",
                    "streetType": "RD",
                    "streetPostDirection": "",
                    "unitType": "",
                    "unitNumber": "",
                    "city": "Pleasanton",
                    "state": "CA",
                    "zipCode": "94566",
                    "zip4": "3402",
                    "longitude": "-121.899057",
                    "latitude": "37.652399",
                    "verificationCodes": [
                        "AS01"
                    ],
                    "maxExpiredate": "",
                    "minExpireDate": "",
                    "maxIssuedate": "",
                    "minIssuedate": ""
                }
            ],
            "attributes": [
                {
                    "licenseNumber": "0",
                    "licenseStatus": "",
                    "licenseState": "",
                    "licenseCategory": "Real Estate",
                    "licenseType": "Realtor"
                }
            ],
            "phone": [
                "8886884108"
            ],
            "businessNames": [
                {
                    "businessId": 4841067337194872938,
                    "businessName": "Google Financial Srvcs Inc"
                }
            ],
            "ownerName": null
        },
        {
            "proLicensesId": "7755375781128766218",
            "bridge": [],
            "names": [
                {
                    "prefix": "",
                    "firstName": "Chao-jung",
                    "middleName": "",
                    "lastName": "Li",
                    "suffix": "",
                    "tahoeId": null,
                    "gender": "U",
                    "ssn": "",
                    "fullName": "Chao-jung Li",
                    "individualId": -5066731274543755266
                }
            ],
            "addresses": [
                {
                    "houseNumber": "1910",
                    "streetDirection": "W",
                    "streetName": "Lagoon",
                    "streetType": "RD",
                    "streetPostDirection": "",
                    "unitType": "",
                    "unitNumber": "",
                    "city": "Pleasanton",
                    "state": "CA",
                    "zipCode": "94566",
                    "zip4": "3402",
                    "longitude": "-121.899057",
                    "latitude": "37.652399",
                    "verificationCodes": [
                        "AS01"
                    ],
                    "maxExpiredate": "",
                    "minExpireDate": "",
                    "maxIssuedate": "",
                    "minIssuedate": ""
                }
            ],
            "attributes": [
                {
                    "licenseNumber": "1301535",
                    "licenseStatus": "",
                    "licenseState": "",
                    "licenseCategory": "Real Estate",
                    "licenseType": "Realtor"
                }
            ],
            "phone": [
                "8886884108"
            ],
            "businessNames": [
                {
                    "businessId": 7755375781128766218,
                    "businessName": "Google Financial Srvcs Inc"
                }
            ],
            "ownerName": null
        }
        ],
        "counts": {
        "searchResults": 8
        },
        "pagination": {
        "currentPageNumber": 1,
        "resultsPerPage": 20,
        "totalPages": 1
        },
        "databaseQueryInfo": [
        {
            "searchType": null,
            "hasIntermediateSort": null,
            "retryCount": null,
            "idCount": null,
            "matchRecordCount": null,
            "databaseQueries": [
                {
                    "databaseConnectionTimeInMs": 1,
                    "databaseQuery": "CALL search_license_criteria(@p_business_name := 'google f', @p_last_name := null, @p_first_name := null, @p_middle_name := null, @p_license_type := null, @p_license_number := null, @p_street_address := null, @p_house_number := null, @p_street_name := null, @p_unit := null, @p_city := null, @p_state := null, @p_zip_code := null, @p_poseidon_id_list := '', @p_tahoe_id := 0, @p_ssn := null, @p_retry_level := null, @p_uncompress := False, @p_record_limit := 20);",
                    "executionTimeInMs": 9
                }
            ]
        }
        ],
        "executionStatistics": [
        {
            "description": "ProLicense SP Client Search",
            "startTime": 3,
            "executionTimeInMs": 13
        },
        {
            "description": "CALL search_license_criteria",
            "startTime": 3,
            "executionTimeInMs": 10
        }
        ],
        "searchCriteria": [],
        "totalRequestExecutionTimeMs": 17,
        "requestId": "4b0d9e1a-607d-4ff7-86e7-e79eb1804ab8",
        "requestType": "ProLicenseSearch",
        "requestTime": "2017-08-24T17:07:50.1469582-07:00",
        "isError": false
        }        
        
## DEA License [/deasearch]

Performs a DEA License search, and returns a list of DEA License records matching the search criteria.

### Search [POST]
***Click on the grey search box above, to view sample request/response objects for the ProLicense Search.***

Perform a search:
1. Add your Access Profile username and password to the request headers.
    * galaxy-ap-name: [Access Profile Name]
    * galaxy-ap-password: [Access Profile Password]
    * galaxy-client-session-id: (Optional) Session ID for logging
    * galaxy-client-type: [Galaxy Client Type] (required for Javascript clients)
2. Add search criteria to your request:
    ```
    {
        "BusinessName": "dulaney"
    }
    Or
    {
        "TahoeId": "GXXXXXXXXXXXXXXXXXXX",
        "PoseidonIds": [
            "CB2B#XXXXXX",
            "CB2B#XXXXXXXX"
        ],
        "SSN": "XXX-XX-XXXX",
        "FirstName": "John",
        "MiddleName": "",
        "LastName": "Smith",
        "LicenseType": "",
        "LicenseNumber": ""
        "HouseNumber": "",
        "StreetName": "",
        "Unit": "",
        "City": "",
        "State": "",
        "ZipCode": "XXXXX"
    }
    Or
    {
        "TahoeId": "GXXXXXXXXXXXXXXXXXXX",
        "PoseidonIds": [
            "CB2B#XXXXXX",
            "CB2B#XXXXXXXX"
        ],
        "SSN": "XXX-XX-XXXX",
        "FirstName": "John",
        "MiddleName": "",
        "LastName": "Smith",
        "LicenseType": "",
        "LicenseNumber": ""
        "HouseNumber": "",
        "StreetName": "",
        "Unit": "",
        "City": "",
        "State": "",
        "ZipCode": "XXXXX"
    }
    ```
3. Select the data types you would like to receive in the output (i.e. the Includes):
    ```
    {
        "BusinessName": "dulaney",
        "Includes": [
            "IncludeFullSsnValues", 
            "DatabaseQueryInfo", 
            "ExecutionTimeInfo"
        ]
    }
    Please note, includes do not apply to API partners. Includes are configured at the access profile level and will autmotically be applied.
    ```
4. Set the desired pagination rules:
    ```
    {
        "BusinessName": "dulaney",
        "Includes": [
            "IncludeFullSsnValues", 
            "DatabaseQueryInfo", 
            "ExecutionTimeInfo"
        ]
        "Page": 1,
        "ResultsPerPage": 20
    }
    ```
5. Submit your search.

A complete list of JSON request properties follows:

* `PoseidonIds` = null (optional, string[]) ... Poseidon Ids (batch record retrival).
* `TahoeId` = null (optional, string) ... Tahoe Id (individual record retrival).
* `SSN` = null (optional, string) ... Social Security Number (format: ###-##-####).
* `BusinessName` = null (optional, string) ... Business name.
* `FirstName` = null (optional, string) ... First name.
* `MiddleName` = null (optional, string) ... Middle name or middle initial.
* `LastName` = null (optional, string) ... Last name.
* `HouseNumber` = null (optional, string) ... House number cannot be provided without including Street.
* `StreetName` = null (optional, string) ... Street name cannot be provided without including either the City and State, or the City and Zip Code.
* `City` = null (optional, string) ... State/Zip is required if city is provided.
* `State` = null (optional, string) ... Two character long state name.
* `ZipCode` = null (optional, string) ... Zip code.


<i><strong>If you are an API partner</strong> and are missing any include/members listed below, then please contact our revenue department so we can adjust your access profile configuration.</i>

* `Includes` (optional, string[]) ... Data to be included in the response.
    * Members
        * `IncludeFullSsnValues`
        * `DatabaseQueryInfo`
        * `ExecutionTimeInfo`
        
* `Page` = 1 (optional, int) ... The page of data to return.
* `ResultsPerPage` = 20 (optional, int) ... The number of results to return per page.

+ Request (application/json)

    + Headers
            
                galaxy-ap-name: Access Profile Name
                galaxy-ap-password: Access Profile Password
                galaxy-client-session-id: APIARY
                galaxy-client-type: Galaxy Client Type

    + Body
    
            {
                "FirstName": "James"
                "LastName":  "Smith"
                "City": "st petersburg"
                "State: "fl"
            }
+ Response 200 (application/json)
    + Body
    
            {
              "DeaRecords": [
                {
                  "DeaId": -5317254453914399940,
                  "Name": {
                    "PersonId": -672643292779098319,
                    "Prefix": "",
                    "LastName": "Smith",
                    "MiddleName": "W",
                    "FirstName": "James",
                    "Suffix": "JR",
                    "TahoeId": "G-7277067792241873458",
                    "Ssn": "266-50-xxxx",
                    "FullName": "James W Smith JR"
                  },
                  "Address": {
                    "StreetDirection": "",
                    "HouseNumber": "1249",
                    "UnitType": "",
                    "StreetName": "Snell Isle",
                    "StreetType": "BLVD",
                    "UnitNumber": "",
                    "StreetPostDirection": "NE",
                    "City": "St Petersburg",
                    "State": "FL",
                    "ZipCode": "33704",
                    "Zip4": "3035",
                    "Latitude": "27.79672100",
                    "Longitude": "-82.61035600",
                    "FullAddress": "1249 Snell Isle NE BLVD; St Petersburg, FL 33704-3035"
                  },
                  "MailingAddress": {
                    "HouseNumber": "",
                    "StreetName": "",
                    "Latitude": null,
                    "Longitude": null,
                    "FullAddress": ""
                  },
                  "Details": {
                    "DeaRegistrationNumber": "AS0132718",
                    "BusinessActivityCode": "C",
                    "BusinessActivitySubCode": "0",
                    "BusinessDescription": "Practitioner",
                    "DrugSchedules": "22N 33N 4 5",
                    "MappedDrugSchedules": [
                      "Schedule 2 Narcotic Controlled Substances",
                      "Schedule 2N Non-Narcotic Controlled Substances",
                      "Schedule 3 Narcotic Controlled Substances",
                      "Schedule 3N Non-Narcotic Controlled Substances",
                      "Schedule 4 Controlled Substances",
                      "Schedule 5 Controlled Substances"
                    ],
                    "ExpDate": "2/29/2020",
                    "BusinessName": "",
                    "AdditionalInfo": "CENTRAL ANIMAL CORP.",
                    "PaymentInd": "P",
                    "Activity": "A"
                  }
                }
              ],
              "DeaRecordCounts": 1,
              "Pagination": {
                "CurrentPageNumber": 1,
                "ResultsPerPage": 500,
                "TotalPages": 1
              },
              "DatabaseQueryInfo": [
                {
                  "SearchType": null,
                  "HasIntermediateSort": null,
                  "RetryCount": null,
                  "IdCount": null,
                  "MatchRecordCount": null,
                  "DatabaseQueries": [
                    {
                      "Host": "smf3-posmysql-int-vip.pfnetwork.net",
                      "Database": "dea_20180503",
                      "DatabaseConnectionTimeInMs": 17,
                      "DatabaseQuery": "CALL search_dea_v2_1(@p_business_name := null, @p_first_name := 'James', @p_middle_name := null, @p_last_name := 'Smith', @p_suffix_name := null, @p_house_number := null, @p_street_name := null, @p_unit := null, @p_city := 'st petersburg', @p_state := 'FL', @p_zip_code := null, @p_dea_id_list := null, @p_tahoe_id_list := null, @p_ssn := null, @p_output_bridge := True, @p_match_key_list := null, @p_apply_fn_syn := True, @p_record_limit := 500);",
                      "ExecutionTimeInMs": 103
                    }
                  ]
                }
              ],
              "ExecutionStatistics": [
                {
                  "Description": "Dea SP Client Search",
                  "StartTime": 92,
                  "ExecutionTimeInMs": 120
                },
                {
                  "Description": "CALL search_dea_v2_1",
                  "StartTime": 92,
                  "ExecutionTimeInMs": 120
                }
              ],
              "SearchCriteria": [],
              "TotalRequestExecutionTimeMs": 220,
              "RequestId": "d5234896-ae33-47cd-9060-c077198e71dd",
              "RequestType": "Search",
              "RequestTime": "2020-04-10T10:28:39.5408297-07:00",
              "IsError": false,
              "Error": {
                "InputErrors": [],
                "Warnings": []
              }
            }

## OFAC Search [/OfacSearch]

Performs an OFAC search, and returns a list of records matching the search criteria.

### Search [POST]
***Click on the grey search box above, to view sample request/response objects for the OFAC Search.***

Perform a search:
1. Add your Access Profile username and password to the request headers.
    * galaxy-ap-name: [Access Profile Name]
    * galaxy-ap-password: [Access Profile Password]
    * galaxy-client-session-id: (Optional) Session ID for logging
    * galaxy-client-type: [Galaxy Client Type] (required for Javascript clients)
    * galaxy-search-type: [Galaxy Search Type] (optional)
        * To auto-populate all includes and filter options in your requests, you may provide a search type value in your request header. A search type is required for all API Customers. Applicable search type values for this endpoint include: 
            1. Ofac
2. Add search criteria to your request:
    ```
    {
        "EntityName": "",
        "PersonName": "Eugene Palmer"
    }
    Please note: Supply a value for one, or the other, but not both.
    ```
3. Select the data types you would like to receive in the output (i.e. the Includes):
    ```
    {
        "EntityName": "",
        "PersonName": "Eugene Palmer"
        "Includes": [
            "SocialSecurityNumbers", 
            "DatabaseQueryInfo", 
            "ExecutionTimeInfo"
        ]
    }
    Please note, includes do not apply to API partners. Includes are configured at the access profile level and will autmotically be applied.
    ```
4. Set the desired pagination rules:
    ```
    {
        "EntityName": "",
        "PersonName": "Eugene Palmer"
        "Includes": [
            "SocialSecurityNumbers", 
            "DatabaseQueryInfo", 
            "ExecutionTimeInfo"
        ]
        "Page": 1,
        "ResultsPerPage": 20
    }
    ```
5. Submit your search.

A complete list of JSON request properties follows:

* `EntityName` = null (optional, string) ... Business name.
* `PersonName` = null (optional, string) ... Individual's full name.

    Please note: You must supply a value to one of the above criteria, but not both.

<i><strong>If you are an API partner</strong> and are missing any include/members listed below, then please contact our revenue department so we can adjust your access profile configuration.</i>

* `Includes` (optional, string[]) ... Data to be included in the response.
    * Members
        * `SocialSecurityNumbers`
        * `DatabaseQueryInfo`
        * `ExecutionTimeInfo`

* `Page` = 1 (optional, int) ... The page of data to return.

* `ResultsPerPage` = 20 (optional, int) ... The number of results to return per page.

+ Request (application/json)

    + Headers
            
            galaxy-ap-name: Access Profile Name
            galaxy-ap-password: Access Profile Password
            galaxy-client-session-id: APIARY
            galaxy-client-type: Galaxy Client Type

    + Body
            
            {
              "EntityName": "",
              "PersonName": "Eugene Palmer",
              "Page": 1,
              "ResultsPerPage": 10,
              "AuthorizedForUse": false,
              "Includes": [
                "SocialSecurityNumbers",
                "DatabaseQueryInfo",
                "ExecutionTimeInfo"
              ],
              "FilterOptions": []
            }
            
+ Response 200 (application/json)
            
            {
              "OfacRecords": [
                {
                  "RecordId": "USFBIVIOLENTMURDERS284",
                  "Main": {
                    "ResultsetNumber": 1,
                    "RecordId": "USFBIVIOLENTMURDERS284",
                    "SourceName": "US FEDERAL BUREAU OF INVESTIGATION VIOLENT MURDERS",
                    "SourceType": "",
                    "RecordUploadDate": 20190123,
                    "Name": "PALMER, EUGENE",
                    "LastName": "PALMER",
                    "FirstName": "EUGENE",
                    "MiddleName": "",
                    "Suffix": "",
                    "NameType": "INDIVIDUAL",
                    "CountryOfBirth": "",
                    "Ssn": null,
                    "Dobs": "19390404",
                    "Pobs": "NEW YORK",
                    "Fax": "",
                    "Phones": "",
                    "Nationalities": "AMERICAN",
                    "Deceased": "",
                    "DeceasedNotes": "",
                    "Gender": "MALE",
                    "Title": "",
                    "TitleRole": "",
                    "Positions": "",
                    "Height": "5'10",
                    "Weight": "220 LBS",
                    "WeightInfo": "",
                    "Eyecolor": "BROWN",
                    "HairColor": "GRAY - BALDING",
                    "Age": "",
                    "Complexion": "",
                    "Build": "",
                    "Marks": "PALMER'S LEFT THUMB IS DEFORMED.",
                    "Citizenship": "",
                    "UsCitizenFlag": "",
                    "Languages": "",
                    "Race": "WHITE",
                    "Email": "",
                    "Website": "",
                    "LinkedPerson": "",
                    "Spouse": "",
                    "MaritalStatus": "",
                    "Profession": "",
                    "Specialty": "",
                    "Occupations": "",
                    "FbiNumber": "",
                    "NcicNumber": "",
                    "StateCriminalNumber": "",
                    "PassportNumber": "",
                    "NationalIdNumber": "",
                    "FidNumber": "",
                    "Fingerprint": "",
                    "DriversLicense": "",
                    "StateIdNumber": "",
                    "OriginalId": "",
                    "OriginalIdSource": ""
                  },
                  "Addresses": [],
                  "Aliases": [
                    {
                      "ResultsetNumber": 0,
                      "RecordId": "USFBIVIOLENTMURDERS284",
                      "AliasName": "PALMER, EUGENE KEVIN",
                      "AliasFirstName": "EUGENE",
                      "AliasLastName": "PALMER",
                      "AliasMiddleName": "KEVIN",
                      "AliasSuffix": "",
                      "AliasType": "",
                      "AliasRemarks": "",
                      "OriginalAliasId": ""
                    },
                    {
                      "ResultsetNumber": 0,
                      "RecordId": "USFBIVIOLENTMURDERS284",
                      "AliasName": "PALMER, EUGENE KENNETH",
                      "AliasFirstName": "EUGENE",
                      "AliasLastName": "PALMER",
                      "AliasMiddleName": "KENNETH",
                      "AliasSuffix": "",
                      "AliasType": "",
                      "AliasRemarks": "",
                      "OriginalAliasId": ""
                    },
                    {
                      "ResultsetNumber": 0,
                      "RecordId": "USFBIVIOLENTMURDERS284",
                      "AliasName": "PALMER, EUGENE K",
                      "AliasFirstName": "EUGENE",
                      "AliasLastName": "PALMER",
                      "AliasMiddleName": "K",
                      "AliasSuffix": "",
                      "AliasType": "",
                      "AliasRemarks": "",
                      "OriginalAliasId": ""
                    },
                    {
                      "ResultsetNumber": 0,
                      "RecordId": "USFBIVIOLENTMURDERS284",
                      "AliasName": "PALMER, EUGENE KEVIN",
                      "AliasFirstName": "EUGENE",
                      "AliasLastName": "PALMER",
                      "AliasMiddleName": "KEVIN",
                      "AliasSuffix": "",
                      "AliasType": "",
                      "AliasRemarks": "",
                      "OriginalAliasId": ""
                    },
                    {
                      "ResultsetNumber": 0,
                      "RecordId": "USFBIVIOLENTMURDERS284",
                      "AliasName": "PALMER, EUGENE KENNETH",
                      "AliasFirstName": "EUGENE",
                      "AliasLastName": "PALMER",
                      "AliasMiddleName": "KENNETH",
                      "AliasSuffix": "",
                      "AliasType": "",
                      "AliasRemarks": "",
                      "OriginalAliasId": ""
                    },
                    {
                      "ResultsetNumber": 0,
                      "RecordId": "USFBIVIOLENTMURDERS284",
                      "AliasName": "PALMER, EUGENE K",
                      "AliasFirstName": "EUGENE",
                      "AliasLastName": "PALMER",
                      "AliasMiddleName": "K",
                      "AliasSuffix": "",
                      "AliasType": "",
                      "AliasRemarks": "",
                      "OriginalAliasId": ""
                    },
                    {
                      "ResultsetNumber": 0,
                      "RecordId": "USFBIVIOLENTMURDERS284",
                      "AliasName": "PALMER, EUGENE KEVIN",
                      "AliasFirstName": "EUGENE",
                      "AliasLastName": "PALMER",
                      "AliasMiddleName": "KEVIN",
                      "AliasSuffix": "",
                      "AliasType": "",
                      "AliasRemarks": "",
                      "OriginalAliasId": ""
                    },
                    {
                      "ResultsetNumber": 0,
                      "RecordId": "USFBIVIOLENTMURDERS284",
                      "AliasName": "PALMER, EUGENE KENNETH",
                      "AliasFirstName": "EUGENE",
                      "AliasLastName": "PALMER",
                      "AliasMiddleName": "KENNETH",
                      "AliasSuffix": "",
                      "AliasType": "",
                      "AliasRemarks": "",
                      "OriginalAliasId": ""
                    },
                    {
                      "ResultsetNumber": 0,
                      "RecordId": "USFBIVIOLENTMURDERS284",
                      "AliasName": "PALMER, EUGENE K",
                      "AliasFirstName": "EUGENE",
                      "AliasLastName": "PALMER",
                      "AliasMiddleName": "K",
                      "AliasSuffix": "",
                      "AliasType": "",
                      "AliasRemarks": "",
                      "OriginalAliasId": ""
                    },
                    {
                      "ResultsetNumber": 0,
                      "RecordId": "USFBIVIOLENTMURDERS284",
                      "AliasName": "PALMER, EUGENE KEVIN",
                      "AliasFirstName": "EUGENE",
                      "AliasLastName": "PALMER",
                      "AliasMiddleName": "KEVIN",
                      "AliasSuffix": "",
                      "AliasType": "",
                      "AliasRemarks": "",
                      "OriginalAliasId": ""
                    },
                    {
                      "ResultsetNumber": 0,
                      "RecordId": "USFBIVIOLENTMURDERS284",
                      "AliasName": "PALMER, EUGENE KENNETH",
                      "AliasFirstName": "EUGENE",
                      "AliasLastName": "PALMER",
                      "AliasMiddleName": "KENNETH",
                      "AliasSuffix": "",
                      "AliasType": "",
                      "AliasRemarks": "",
                      "OriginalAliasId": ""
                    },
                    {
                      "ResultsetNumber": 0,
                      "RecordId": "USFBIVIOLENTMURDERS284",
                      "AliasName": "PALMER, EUGENE K",
                      "AliasFirstName": "EUGENE",
                      "AliasLastName": "PALMER",
                      "AliasMiddleName": "K",
                      "AliasSuffix": "",
                      "AliasType": "",
                      "AliasRemarks": "",
                      "OriginalAliasId": ""
                    }
                  ],
                  "Details": [
                    {
                      "ResultsetNumber": 4,
                      "RecordId": "USFBIVIOLENTMURDERS284",
                      "CaseNumber": "",
                      "DocketNumber": "",
                      "PermReferenceNumber": "",
                      "FederalRegCitation": "",
                      "DocAssociation": "",
                      "Violations": "",
                      "OriginalCharge": "",
                      "PrimaryCharge": "",
                      "Charge": "UNLAWFUL FLIGHT TO AVOID PROSECUTION - MURDER",
                      "Remarks": "PALMER IS KNOWN TO BE INTERESTED IN AUTO RACING AND IS A CAR ENTHUSIAST.&#160; HE IS ALSO AN EXPERIENCED HUNTER AND OUTDOORSMAN.",
                      "OtherInfo": "SHOULD BE CONSIDERED ARMED AND DANGEROUS",
                      "Details": "EUGENE PALMER&#160;IS WANTED FOR ALLEGEDLY SHOOTING AND KILLING HIS DAUGHTER-IN-LAW ON SEPTEMBER 24, 2012,&#160;IN STONY POINT, NEW YORK.&#160; AFTER A LOCAL ARREST WARRANT WAS ISSUED FOR PALMER&#160;IN ROCKLAND COUNTY AND HE WAS CHARGED WITH MURDER, A FEDERAL ARREST WARRANT WAS ISSUED ON JUNE 10, 2013,&#160;BY THE UNITED STATES COURT FOR THE SOUTHERN DISTRICT OF NEW YORK AFTER PALMER WAS CHARGED WITH UNLAWFUL FLIGHT TO AVOID PROSECUTION.&#160; &#160; THIS INVESTIGATION IS BEING CONDUCTED BY THE FBI&#8217;S WESTCHESTER SAFE STREETS/VIOLENT CRIMES TASK FORCE, THE HAVERSTRAW POLICE DEPARTMENT, AND THE UNITED STATES MARSHALS SERVICE. &#160;",
                      "InstitutionId": "",
                      "InstitutionAffliation": "",
                      "WarrantIssued": "",
                      "DateOfWarrant": "",
                      "WarrantNumber": "",
                      "Reward": "THE FBI IS OFFERING A REWARD OF UP TO $20,000 FOR INFORMATION LEADING TO THE ARREST AND CONVICTION OF EUGENE PALMER. ADDITIONAL REWARD MONEY MAY BE OFFERED BY OTHER LAW ENFORCEMENT AGENCIES.",
                      "Program": "",
                      "ProgramCode": "",
                      "IssueDate": "",
                      "TypeCode": "",
                      "TypeDescription": "",
                      "OrderNumber": "",
                      "TypeOfOrder": "",
                      "StandardOrder": "",
                      "VesselRegistration": "",
                      "VesselCallSign": "",
                      "VesselType": "",
                      "VesselTonnage": "",
                      "GrossRegisteredTonnage": "",
                      "VesselFlag": "",
                      "VesselOwner": "",
                      "BusinessRegDoc": "",
                      "EffectiveDate": "",
                      "ExpirationDate": "",
                      "EnforcementAction": "",
                      "Caution": "",
                      "Grp": "",
                      "Rolee": "",
                      "PassportNum": "",
                      "PassportInfo": "",
                      "DateOfDissertion": "",
                      "GangAffiliation": "",
                      "Type": "",
                      "ControlDate": "",
                      "Regime": "",
                      "FederalRegNum": "",
                      "FederalRegDate": "",
                      "DisqualifiedFrom": "",
                      "DisqualifiedTo": ""
                    },
                    {
                      "ResultsetNumber": 4,
                      "RecordId": "USFBIVIOLENTMURDERS284",
                      "CaseNumber": "",
                      "DocketNumber": "",
                      "PermReferenceNumber": "",
                      "FederalRegCitation": "",
                      "DocAssociation": "",
                      "Violations": "",
                      "OriginalCharge": "",
                      "PrimaryCharge": "",
                      "Charge": "UNLAWFUL FLIGHT TO AVOID PROSECUTION - MURDER",
                      "Remarks": "PALMER IS KNOWN TO BE INTERESTED IN AUTO RACING AND IS A CAR ENTHUSIAST.&#160; HE IS ALSO AN EXPERIENCED HUNTER AND OUTDOORSMAN.",
                      "OtherInfo": "SHOULD BE CONSIDERED ARMED AND DANGEROUS",
                      "Details": "EUGENE PALMER&#160;IS WANTED FOR ALLEGEDLY SHOOTING AND KILLING HIS DAUGHTER-IN-LAW ON SEPTEMBER 24, 2012,&#160;IN STONY POINT, NEW YORK.&#160; AFTER A LOCAL ARREST WARRANT WAS ISSUED FOR PALMER&#160;IN ROCKLAND COUNTY AND HE WAS CHARGED WITH MURDER, A FEDERAL ARREST WARRANT WAS ISSUED ON JUNE 10, 2013,&#160;BY THE UNITED STATES COURT FOR THE SOUTHERN DISTRICT OF NEW YORK AFTER PALMER WAS CHARGED WITH UNLAWFUL FLIGHT TO AVOID PROSECUTION.&#160; &#160; THIS INVESTIGATION IS BEING CONDUCTED BY THE FBI&#8217;S WESTCHESTER SAFE STREETS/VIOLENT CRIMES TASK FORCE, THE HAVERSTRAW POLICE DEPARTMENT, AND THE UNITED STATES MARSHALS SERVICE. &#160;",
                      "InstitutionId": "",
                      "InstitutionAffliation": "",
                      "WarrantIssued": "",
                      "DateOfWarrant": "",
                      "WarrantNumber": "",
                      "Reward": "THE FBI IS OFFERING A REWARD OF UP TO $20,000 FOR INFORMATION LEADING TO THE ARREST AND CONVICTION OF EUGENE PALMER. ADDITIONAL REWARD MONEY MAY BE OFFERED BY OTHER LAW ENFORCEMENT AGENCIES.",
                      "Program": "",
                      "ProgramCode": "",
                      "IssueDate": "",
                      "TypeCode": "",
                      "TypeDescription": "",
                      "OrderNumber": "",
                      "TypeOfOrder": "",
                      "StandardOrder": "",
                      "VesselRegistration": "",
                      "VesselCallSign": "",
                      "VesselType": "",
                      "VesselTonnage": "",
                      "GrossRegisteredTonnage": "",
                      "VesselFlag": "",
                      "VesselOwner": "",
                      "BusinessRegDoc": "",
                      "EffectiveDate": "",
                      "ExpirationDate": "",
                      "EnforcementAction": "",
                      "Caution": "",
                      "Grp": "",
                      "Rolee": "",
                      "PassportNum": "",
                      "PassportInfo": "",
                      "DateOfDissertion": "",
                      "GangAffiliation": "",
                      "Type": "",
                      "ControlDate": "",
                      "Regime": "",
                      "FederalRegNum": "",
                      "FederalRegDate": "",
                      "DisqualifiedFrom": "",
                      "DisqualifiedTo": ""
                    },
                    {
                      "ResultsetNumber": 4,
                      "RecordId": "USFBIVIOLENTMURDERS284",
                      "CaseNumber": "",
                      "DocketNumber": "",
                      "PermReferenceNumber": "",
                      "FederalRegCitation": "",
                      "DocAssociation": "",
                      "Violations": "",
                      "OriginalCharge": "",
                      "PrimaryCharge": "",
                      "Charge": "UNLAWFUL FLIGHT TO AVOID PROSECUTION - MURDER",
                      "Remarks": "PALMER IS KNOWN TO BE INTERESTED IN AUTO RACING AND IS A CAR ENTHUSIAST.&#160; HE IS ALSO AN EXPERIENCED HUNTER AND OUTDOORSMAN.",
                      "OtherInfo": "SHOULD BE CONSIDERED ARMED AND DANGEROUS",
                      "Details": "EUGENE PALMER&#160;IS WANTED FOR ALLEGEDLY SHOOTING AND KILLING HIS DAUGHTER-IN-LAW ON SEPTEMBER 24, 2012,&#160;IN STONY POINT, NEW YORK.&#160; AFTER A LOCAL ARREST WARRANT WAS ISSUED FOR PALMER&#160;IN ROCKLAND COUNTY AND HE WAS CHARGED WITH MURDER, A FEDERAL ARREST WARRANT WAS ISSUED ON JUNE 10, 2013,&#160;BY THE UNITED STATES COURT FOR THE SOUTHERN DISTRICT OF NEW YORK AFTER PALMER WAS CHARGED WITH UNLAWFUL FLIGHT TO AVOID PROSECUTION.&#160; &#160; THIS INVESTIGATION IS BEING CONDUCTED BY THE FBI&#8217;S WESTCHESTER SAFE STREETS/VIOLENT CRIMES TASK FORCE, THE HAVERSTRAW POLICE DEPARTMENT, AND THE UNITED STATES MARSHALS SERVICE. &#160;",
                      "InstitutionId": "",
                      "InstitutionAffliation": "",
                      "WarrantIssued": "",
                      "DateOfWarrant": "",
                      "WarrantNumber": "",
                      "Reward": "THE FBI IS OFFERING A REWARD OF UP TO $20,000 FOR INFORMATION LEADING TO THE ARREST AND CONVICTION OF EUGENE PALMER. ADDITIONAL REWARD MONEY MAY BE OFFERED BY OTHER LAW ENFORCEMENT AGENCIES.",
                      "Program": "",
                      "ProgramCode": "",
                      "IssueDate": "",
                      "TypeCode": "",
                      "TypeDescription": "",
                      "OrderNumber": "",
                      "TypeOfOrder": "",
                      "StandardOrder": "",
                      "VesselRegistration": "",
                      "VesselCallSign": "",
                      "VesselType": "",
                      "VesselTonnage": "",
                      "GrossRegisteredTonnage": "",
                      "VesselFlag": "",
                      "VesselOwner": "",
                      "BusinessRegDoc": "",
                      "EffectiveDate": "",
                      "ExpirationDate": "",
                      "EnforcementAction": "",
                      "Caution": "",
                      "Grp": "",
                      "Rolee": "",
                      "PassportNum": "",
                      "PassportInfo": "",
                      "DateOfDissertion": "",
                      "GangAffiliation": "",
                      "Type": "",
                      "ControlDate": "",
                      "Regime": "",
                      "FederalRegNum": "",
                      "FederalRegDate": "",
                      "DisqualifiedFrom": "",
                      "DisqualifiedTo": ""
                    },
                    {
                      "ResultsetNumber": 4,
                      "RecordId": "USFBIVIOLENTMURDERS284",
                      "CaseNumber": "",
                      "DocketNumber": "",
                      "PermReferenceNumber": "",
                      "FederalRegCitation": "",
                      "DocAssociation": "",
                      "Violations": "",
                      "OriginalCharge": "",
                      "PrimaryCharge": "",
                      "Charge": "UNLAWFUL FLIGHT TO AVOID PROSECUTION - MURDER",
                      "Remarks": "PALMER IS KNOWN TO BE INTERESTED IN AUTO RACING AND IS A CAR ENTHUSIAST.&#160; HE IS ALSO AN EXPERIENCED HUNTER AND OUTDOORSMAN.",
                      "OtherInfo": "SHOULD BE CONSIDERED ARMED AND DANGEROUS",
                      "Details": "EUGENE PALMER&#160;IS WANTED FOR ALLEGEDLY SHOOTING AND KILLING HIS DAUGHTER-IN-LAW ON SEPTEMBER 24, 2012,&#160;IN STONY POINT, NEW YORK.&#160; AFTER A LOCAL ARREST WARRANT WAS ISSUED FOR PALMER&#160;IN ROCKLAND COUNTY AND HE WAS CHARGED WITH MURDER, A FEDERAL ARREST WARRANT WAS ISSUED ON JUNE 10, 2013,&#160;BY THE UNITED STATES COURT FOR THE SOUTHERN DISTRICT OF NEW YORK AFTER PALMER WAS CHARGED WITH UNLAWFUL FLIGHT TO AVOID PROSECUTION.&#160; &#160; THIS INVESTIGATION IS BEING CONDUCTED BY THE FBI&#8217;S WESTCHESTER SAFE STREETS/VIOLENT CRIMES TASK FORCE, THE HAVERSTRAW POLICE DEPARTMENT, AND THE UNITED STATES MARSHALS SERVICE. &#160;",
                      "InstitutionId": "",
                      "InstitutionAffliation": "",
                      "WarrantIssued": "",
                      "DateOfWarrant": "",
                      "WarrantNumber": "",
                      "Reward": "THE FBI IS OFFERING A REWARD OF UP TO $20,000 FOR INFORMATION LEADING TO THE ARREST AND CONVICTION OF EUGENE PALMER. ADDITIONAL REWARD MONEY MAY BE OFFERED BY OTHER LAW ENFORCEMENT AGENCIES.",
                      "Program": "",
                      "ProgramCode": "",
                      "IssueDate": "",
                      "TypeCode": "",
                      "TypeDescription": "",
                      "OrderNumber": "",
                      "TypeOfOrder": "",
                      "StandardOrder": "",
                      "VesselRegistration": "",
                      "VesselCallSign": "",
                      "VesselType": "",
                      "VesselTonnage": "",
                      "GrossRegisteredTonnage": "",
                      "VesselFlag": "",
                      "VesselOwner": "",
                      "BusinessRegDoc": "",
                      "EffectiveDate": "",
                      "ExpirationDate": "",
                      "EnforcementAction": "",
                      "Caution": "",
                      "Grp": "",
                      "Rolee": "",
                      "PassportNum": "",
                      "PassportInfo": "",
                      "DateOfDissertion": "",
                      "GangAffiliation": "",
                      "Type": "",
                      "ControlDate": "",
                      "Regime": "",
                      "FederalRegNum": "",
                      "FederalRegDate": "",
                      "DisqualifiedFrom": "",
                      "DisqualifiedTo": ""
                    }
                  ]
                },
                {
                  "RecordId": "USFBIVIOLENTMURDERS284",
                  "Main": {
                    "ResultsetNumber": 1,
                    "RecordId": "USFBIVIOLENTMURDERS284",
                    "SourceName": "US FEDERAL BUREAU OF INVESTIGATION VIOLENT MURDERS",
                    "SourceType": "",
                    "RecordUploadDate": 20190123,
                    "Name": "PALMER, EUGENE",
                    "LastName": "PALMER",
                    "FirstName": "EUGENE",
                    "MiddleName": "",
                    "Suffix": "",
                    "NameType": "INDIVIDUAL",
                    "CountryOfBirth": "",
                    "Ssn": null,
                    "Dobs": "19390404",
                    "Pobs": "NEW YORK",
                    "Fax": "",
                    "Phones": "",
                    "Nationalities": "AMERICAN",
                    "Deceased": "",
                    "DeceasedNotes": "",
                    "Gender": "MALE",
                    "Title": "",
                    "TitleRole": "",
                    "Positions": "",
                    "Height": "5'10",
                    "Weight": "220 LBS",
                    "WeightInfo": "",
                    "Eyecolor": "BROWN",
                    "HairColor": "GRAY - BALDING",
                    "Age": "",
                    "Complexion": "",
                    "Build": "",
                    "Marks": "PALMER'S LEFT THUMB IS DEFORMED.",
                    "Citizenship": "",
                    "UsCitizenFlag": "",
                    "Languages": "",
                    "Race": "WHITE",
                    "Email": "",
                    "Website": "",
                    "LinkedPerson": "",
                    "Spouse": "",
                    "MaritalStatus": "",
                    "Profession": "",
                    "Specialty": "",
                    "Occupations": "",
                    "FbiNumber": "",
                    "NcicNumber": "",
                    "StateCriminalNumber": "",
                    "PassportNumber": "",
                    "NationalIdNumber": "",
                    "FidNumber": "",
                    "Fingerprint": "",
                    "DriversLicense": "",
                    "StateIdNumber": "",
                    "OriginalId": "",
                    "OriginalIdSource": ""
                  },
                  "Addresses": [],
                  "Aliases": [
                    {
                      "ResultsetNumber": 0,
                      "RecordId": "USFBIVIOLENTMURDERS284",
                      "AliasName": "PALMER, EUGENE KEVIN",
                      "AliasFirstName": "EUGENE",
                      "AliasLastName": "PALMER",
                      "AliasMiddleName": "KEVIN",
                      "AliasSuffix": "",
                      "AliasType": "",
                      "AliasRemarks": "",
                      "OriginalAliasId": ""
                    },
                    {
                      "ResultsetNumber": 0,
                      "RecordId": "USFBIVIOLENTMURDERS284",
                      "AliasName": "PALMER, EUGENE KENNETH",
                      "AliasFirstName": "EUGENE",
                      "AliasLastName": "PALMER",
                      "AliasMiddleName": "KENNETH",
                      "AliasSuffix": "",
                      "AliasType": "",
                      "AliasRemarks": "",
                      "OriginalAliasId": ""
                    },
                    {
                      "ResultsetNumber": 0,
                      "RecordId": "USFBIVIOLENTMURDERS284",
                      "AliasName": "PALMER, EUGENE K",
                      "AliasFirstName": "EUGENE",
                      "AliasLastName": "PALMER",
                      "AliasMiddleName": "K",
                      "AliasSuffix": "",
                      "AliasType": "",
                      "AliasRemarks": "",
                      "OriginalAliasId": ""
                    },
                    {
                      "ResultsetNumber": 0,
                      "RecordId": "USFBIVIOLENTMURDERS284",
                      "AliasName": "PALMER, EUGENE KEVIN",
                      "AliasFirstName": "EUGENE",
                      "AliasLastName": "PALMER",
                      "AliasMiddleName": "KEVIN",
                      "AliasSuffix": "",
                      "AliasType": "",
                      "AliasRemarks": "",
                      "OriginalAliasId": ""
                    },
                    {
                      "ResultsetNumber": 0,
                      "RecordId": "USFBIVIOLENTMURDERS284",
                      "AliasName": "PALMER, EUGENE KENNETH",
                      "AliasFirstName": "EUGENE",
                      "AliasLastName": "PALMER",
                      "AliasMiddleName": "KENNETH",
                      "AliasSuffix": "",
                      "AliasType": "",
                      "AliasRemarks": "",
                      "OriginalAliasId": ""
                    },
                    {
                      "ResultsetNumber": 0,
                      "RecordId": "USFBIVIOLENTMURDERS284",
                      "AliasName": "PALMER, EUGENE K",
                      "AliasFirstName": "EUGENE",
                      "AliasLastName": "PALMER",
                      "AliasMiddleName": "K",
                      "AliasSuffix": "",
                      "AliasType": "",
                      "AliasRemarks": "",
                      "OriginalAliasId": ""
                    },
                    {
                      "ResultsetNumber": 0,
                      "RecordId": "USFBIVIOLENTMURDERS284",
                      "AliasName": "PALMER, EUGENE KEVIN",
                      "AliasFirstName": "EUGENE",
                      "AliasLastName": "PALMER",
                      "AliasMiddleName": "KEVIN",
                      "AliasSuffix": "",
                      "AliasType": "",
                      "AliasRemarks": "",
                      "OriginalAliasId": ""
                    },
                    {
                      "ResultsetNumber": 0,
                      "RecordId": "USFBIVIOLENTMURDERS284",
                      "AliasName": "PALMER, EUGENE KENNETH",
                      "AliasFirstName": "EUGENE",
                      "AliasLastName": "PALMER",
                      "AliasMiddleName": "KENNETH",
                      "AliasSuffix": "",
                      "AliasType": "",
                      "AliasRemarks": "",
                      "OriginalAliasId": ""
                    },
                    {
                      "ResultsetNumber": 0,
                      "RecordId": "USFBIVIOLENTMURDERS284",
                      "AliasName": "PALMER, EUGENE K",
                      "AliasFirstName": "EUGENE",
                      "AliasLastName": "PALMER",
                      "AliasMiddleName": "K",
                      "AliasSuffix": "",
                      "AliasType": "",
                      "AliasRemarks": "",
                      "OriginalAliasId": ""
                    },
                    {
                      "ResultsetNumber": 0,
                      "RecordId": "USFBIVIOLENTMURDERS284",
                      "AliasName": "PALMER, EUGENE KEVIN",
                      "AliasFirstName": "EUGENE",
                      "AliasLastName": "PALMER",
                      "AliasMiddleName": "KEVIN",
                      "AliasSuffix": "",
                      "AliasType": "",
                      "AliasRemarks": "",
                      "OriginalAliasId": ""
                    },
                    {
                      "ResultsetNumber": 0,
                      "RecordId": "USFBIVIOLENTMURDERS284",
                      "AliasName": "PALMER, EUGENE KENNETH",
                      "AliasFirstName": "EUGENE",
                      "AliasLastName": "PALMER",
                      "AliasMiddleName": "KENNETH",
                      "AliasSuffix": "",
                      "AliasType": "",
                      "AliasRemarks": "",
                      "OriginalAliasId": ""
                    },
                    {
                      "ResultsetNumber": 0,
                      "RecordId": "USFBIVIOLENTMURDERS284",
                      "AliasName": "PALMER, EUGENE K",
                      "AliasFirstName": "EUGENE",
                      "AliasLastName": "PALMER",
                      "AliasMiddleName": "K",
                      "AliasSuffix": "",
                      "AliasType": "",
                      "AliasRemarks": "",
                      "OriginalAliasId": ""
                    }
                  ],
                  "Details": [
                    {
                      "ResultsetNumber": 4,
                      "RecordId": "USFBIVIOLENTMURDERS284",
                      "CaseNumber": "",
                      "DocketNumber": "",
                      "PermReferenceNumber": "",
                      "FederalRegCitation": "",
                      "DocAssociation": "",
                      "Violations": "",
                      "OriginalCharge": "",
                      "PrimaryCharge": "",
                      "Charge": "UNLAWFUL FLIGHT TO AVOID PROSECUTION - MURDER",
                      "Remarks": "PALMER IS KNOWN TO BE INTERESTED IN AUTO RACING AND IS A CAR ENTHUSIAST.&#160; HE IS ALSO AN EXPERIENCED HUNTER AND OUTDOORSMAN.",
                      "OtherInfo": "SHOULD BE CONSIDERED ARMED AND DANGEROUS",
                      "Details": "EUGENE PALMER&#160;IS WANTED FOR ALLEGEDLY SHOOTING AND KILLING HIS DAUGHTER-IN-LAW ON SEPTEMBER 24, 2012,&#160;IN STONY POINT, NEW YORK.&#160; AFTER A LOCAL ARREST WARRANT WAS ISSUED FOR PALMER&#160;IN ROCKLAND COUNTY AND HE WAS CHARGED WITH MURDER, A FEDERAL ARREST WARRANT WAS ISSUED ON JUNE 10, 2013,&#160;BY THE UNITED STATES COURT FOR THE SOUTHERN DISTRICT OF NEW YORK AFTER PALMER WAS CHARGED WITH UNLAWFUL FLIGHT TO AVOID PROSECUTION.&#160; &#160; THIS INVESTIGATION IS BEING CONDUCTED BY THE FBI&#8217;S WESTCHESTER SAFE STREETS/VIOLENT CRIMES TASK FORCE, THE HAVERSTRAW POLICE DEPARTMENT, AND THE UNITED STATES MARSHALS SERVICE. &#160;",
                      "InstitutionId": "",
                      "InstitutionAffliation": "",
                      "WarrantIssued": "",
                      "DateOfWarrant": "",
                      "WarrantNumber": "",
                      "Reward": "THE FBI IS OFFERING A REWARD OF UP TO $20,000 FOR INFORMATION LEADING TO THE ARREST AND CONVICTION OF EUGENE PALMER. ADDITIONAL REWARD MONEY MAY BE OFFERED BY OTHER LAW ENFORCEMENT AGENCIES.",
                      "Program": "",
                      "ProgramCode": "",
                      "IssueDate": "",
                      "TypeCode": "",
                      "TypeDescription": "",
                      "OrderNumber": "",
                      "TypeOfOrder": "",
                      "StandardOrder": "",
                      "VesselRegistration": "",
                      "VesselCallSign": "",
                      "VesselType": "",
                      "VesselTonnage": "",
                      "GrossRegisteredTonnage": "",
                      "VesselFlag": "",
                      "VesselOwner": "",
                      "BusinessRegDoc": "",
                      "EffectiveDate": "",
                      "ExpirationDate": "",
                      "EnforcementAction": "",
                      "Caution": "",
                      "Grp": "",
                      "Rolee": "",
                      "PassportNum": "",
                      "PassportInfo": "",
                      "DateOfDissertion": "",
                      "GangAffiliation": "",
                      "Type": "",
                      "ControlDate": "",
                      "Regime": "",
                      "FederalRegNum": "",
                      "FederalRegDate": "",
                      "DisqualifiedFrom": "",
                      "DisqualifiedTo": ""
                    },
                    {
                      "ResultsetNumber": 4,
                      "RecordId": "USFBIVIOLENTMURDERS284",
                      "CaseNumber": "",
                      "DocketNumber": "",
                      "PermReferenceNumber": "",
                      "FederalRegCitation": "",
                      "DocAssociation": "",
                      "Violations": "",
                      "OriginalCharge": "",
                      "PrimaryCharge": "",
                      "Charge": "UNLAWFUL FLIGHT TO AVOID PROSECUTION - MURDER",
                      "Remarks": "PALMER IS KNOWN TO BE INTERESTED IN AUTO RACING AND IS A CAR ENTHUSIAST.&#160; HE IS ALSO AN EXPERIENCED HUNTER AND OUTDOORSMAN.",
                      "OtherInfo": "SHOULD BE CONSIDERED ARMED AND DANGEROUS",
                      "Details": "EUGENE PALMER&#160;IS WANTED FOR ALLEGEDLY SHOOTING AND KILLING HIS DAUGHTER-IN-LAW ON SEPTEMBER 24, 2012,&#160;IN STONY POINT, NEW YORK.&#160; AFTER A LOCAL ARREST WARRANT WAS ISSUED FOR PALMER&#160;IN ROCKLAND COUNTY AND HE WAS CHARGED WITH MURDER, A FEDERAL ARREST WARRANT WAS ISSUED ON JUNE 10, 2013,&#160;BY THE UNITED STATES COURT FOR THE SOUTHERN DISTRICT OF NEW YORK AFTER PALMER WAS CHARGED WITH UNLAWFUL FLIGHT TO AVOID PROSECUTION.&#160; &#160; THIS INVESTIGATION IS BEING CONDUCTED BY THE FBI&#8217;S WESTCHESTER SAFE STREETS/VIOLENT CRIMES TASK FORCE, THE HAVERSTRAW POLICE DEPARTMENT, AND THE UNITED STATES MARSHALS SERVICE. &#160;",
                      "InstitutionId": "",
                      "InstitutionAffliation": "",
                      "WarrantIssued": "",
                      "DateOfWarrant": "",
                      "WarrantNumber": "",
                      "Reward": "THE FBI IS OFFERING A REWARD OF UP TO $20,000 FOR INFORMATION LEADING TO THE ARREST AND CONVICTION OF EUGENE PALMER. ADDITIONAL REWARD MONEY MAY BE OFFERED BY OTHER LAW ENFORCEMENT AGENCIES.",
                      "Program": "",
                      "ProgramCode": "",
                      "IssueDate": "",
                      "TypeCode": "",
                      "TypeDescription": "",
                      "OrderNumber": "",
                      "TypeOfOrder": "",
                      "StandardOrder": "",
                      "VesselRegistration": "",
                      "VesselCallSign": "",
                      "VesselType": "",
                      "VesselTonnage": "",
                      "GrossRegisteredTonnage": "",
                      "VesselFlag": "",
                      "VesselOwner": "",
                      "BusinessRegDoc": "",
                      "EffectiveDate": "",
                      "ExpirationDate": "",
                      "EnforcementAction": "",
                      "Caution": "",
                      "Grp": "",
                      "Rolee": "",
                      "PassportNum": "",
                      "PassportInfo": "",
                      "DateOfDissertion": "",
                      "GangAffiliation": "",
                      "Type": "",
                      "ControlDate": "",
                      "Regime": "",
                      "FederalRegNum": "",
                      "FederalRegDate": "",
                      "DisqualifiedFrom": "",
                      "DisqualifiedTo": ""
                    },
                    {
                      "ResultsetNumber": 4,
                      "RecordId": "USFBIVIOLENTMURDERS284",
                      "CaseNumber": "",
                      "DocketNumber": "",
                      "PermReferenceNumber": "",
                      "FederalRegCitation": "",
                      "DocAssociation": "",
                      "Violations": "",
                      "OriginalCharge": "",
                      "PrimaryCharge": "",
                      "Charge": "UNLAWFUL FLIGHT TO AVOID PROSECUTION - MURDER",
                      "Remarks": "PALMER IS KNOWN TO BE INTERESTED IN AUTO RACING AND IS A CAR ENTHUSIAST.&#160; HE IS ALSO AN EXPERIENCED HUNTER AND OUTDOORSMAN.",
                      "OtherInfo": "SHOULD BE CONSIDERED ARMED AND DANGEROUS",
                      "Details": "EUGENE PALMER&#160;IS WANTED FOR ALLEGEDLY SHOOTING AND KILLING HIS DAUGHTER-IN-LAW ON SEPTEMBER 24, 2012,&#160;IN STONY POINT, NEW YORK.&#160; AFTER A LOCAL ARREST WARRANT WAS ISSUED FOR PALMER&#160;IN ROCKLAND COUNTY AND HE WAS CHARGED WITH MURDER, A FEDERAL ARREST WARRANT WAS ISSUED ON JUNE 10, 2013,&#160;BY THE UNITED STATES COURT FOR THE SOUTHERN DISTRICT OF NEW YORK AFTER PALMER WAS CHARGED WITH UNLAWFUL FLIGHT TO AVOID PROSECUTION.&#160; &#160; THIS INVESTIGATION IS BEING CONDUCTED BY THE FBI&#8217;S WESTCHESTER SAFE STREETS/VIOLENT CRIMES TASK FORCE, THE HAVERSTRAW POLICE DEPARTMENT, AND THE UNITED STATES MARSHALS SERVICE. &#160;",
                      "InstitutionId": "",
                      "InstitutionAffliation": "",
                      "WarrantIssued": "",
                      "DateOfWarrant": "",
                      "WarrantNumber": "",
                      "Reward": "THE FBI IS OFFERING A REWARD OF UP TO $20,000 FOR INFORMATION LEADING TO THE ARREST AND CONVICTION OF EUGENE PALMER. ADDITIONAL REWARD MONEY MAY BE OFFERED BY OTHER LAW ENFORCEMENT AGENCIES.",
                      "Program": "",
                      "ProgramCode": "",
                      "IssueDate": "",
                      "TypeCode": "",
                      "TypeDescription": "",
                      "OrderNumber": "",
                      "TypeOfOrder": "",
                      "StandardOrder": "",
                      "VesselRegistration": "",
                      "VesselCallSign": "",
                      "VesselType": "",
                      "VesselTonnage": "",
                      "GrossRegisteredTonnage": "",
                      "VesselFlag": "",
                      "VesselOwner": "",
                      "BusinessRegDoc": "",
                      "EffectiveDate": "",
                      "ExpirationDate": "",
                      "EnforcementAction": "",
                      "Caution": "",
                      "Grp": "",
                      "Rolee": "",
                      "PassportNum": "",
                      "PassportInfo": "",
                      "DateOfDissertion": "",
                      "GangAffiliation": "",
                      "Type": "",
                      "ControlDate": "",
                      "Regime": "",
                      "FederalRegNum": "",
                      "FederalRegDate": "",
                      "DisqualifiedFrom": "",
                      "DisqualifiedTo": ""
                    },
                    {
                      "ResultsetNumber": 4,
                      "RecordId": "USFBIVIOLENTMURDERS284",
                      "CaseNumber": "",
                      "DocketNumber": "",
                      "PermReferenceNumber": "",
                      "FederalRegCitation": "",
                      "DocAssociation": "",
                      "Violations": "",
                      "OriginalCharge": "",
                      "PrimaryCharge": "",
                      "Charge": "UNLAWFUL FLIGHT TO AVOID PROSECUTION - MURDER",
                      "Remarks": "PALMER IS KNOWN TO BE INTERESTED IN AUTO RACING AND IS A CAR ENTHUSIAST.&#160; HE IS ALSO AN EXPERIENCED HUNTER AND OUTDOORSMAN.",
                      "OtherInfo": "SHOULD BE CONSIDERED ARMED AND DANGEROUS",
                      "Details": "EUGENE PALMER&#160;IS WANTED FOR ALLEGEDLY SHOOTING AND KILLING HIS DAUGHTER-IN-LAW ON SEPTEMBER 24, 2012,&#160;IN STONY POINT, NEW YORK.&#160; AFTER A LOCAL ARREST WARRANT WAS ISSUED FOR PALMER&#160;IN ROCKLAND COUNTY AND HE WAS CHARGED WITH MURDER, A FEDERAL ARREST WARRANT WAS ISSUED ON JUNE 10, 2013,&#160;BY THE UNITED STATES COURT FOR THE SOUTHERN DISTRICT OF NEW YORK AFTER PALMER WAS CHARGED WITH UNLAWFUL FLIGHT TO AVOID PROSECUTION.&#160; &#160; THIS INVESTIGATION IS BEING CONDUCTED BY THE FBI&#8217;S WESTCHESTER SAFE STREETS/VIOLENT CRIMES TASK FORCE, THE HAVERSTRAW POLICE DEPARTMENT, AND THE UNITED STATES MARSHALS SERVICE. &#160;",
                      "InstitutionId": "",
                      "InstitutionAffliation": "",
                      "WarrantIssued": "",
                      "DateOfWarrant": "",
                      "WarrantNumber": "",
                      "Reward": "THE FBI IS OFFERING A REWARD OF UP TO $20,000 FOR INFORMATION LEADING TO THE ARREST AND CONVICTION OF EUGENE PALMER. ADDITIONAL REWARD MONEY MAY BE OFFERED BY OTHER LAW ENFORCEMENT AGENCIES.",
                      "Program": "",
                      "ProgramCode": "",
                      "IssueDate": "",
                      "TypeCode": "",
                      "TypeDescription": "",
                      "OrderNumber": "",
                      "TypeOfOrder": "",
                      "StandardOrder": "",
                      "VesselRegistration": "",
                      "VesselCallSign": "",
                      "VesselType": "",
                      "VesselTonnage": "",
                      "GrossRegisteredTonnage": "",
                      "VesselFlag": "",
                      "VesselOwner": "",
                      "BusinessRegDoc": "",
                      "EffectiveDate": "",
                      "ExpirationDate": "",
                      "EnforcementAction": "",
                      "Caution": "",
                      "Grp": "",
                      "Rolee": "",
                      "PassportNum": "",
                      "PassportInfo": "",
                      "DateOfDissertion": "",
                      "GangAffiliation": "",
                      "Type": "",
                      "ControlDate": "",
                      "Regime": "",
                      "FederalRegNum": "",
                      "FederalRegDate": "",
                      "DisqualifiedFrom": "",
                      "DisqualifiedTo": ""
                    }
                  ]
                },
                {
                  "RecordId": "USFBIVIOLENTMURDERS284",
                  "Main": {
                    "ResultsetNumber": 1,
                    "RecordId": "USFBIVIOLENTMURDERS284",
                    "SourceName": "US FEDERAL BUREAU OF INVESTIGATION VIOLENT MURDERS",
                    "SourceType": "",
                    "RecordUploadDate": 20190123,
                    "Name": "PALMER, EUGENE",
                    "LastName": "PALMER",
                    "FirstName": "EUGENE",
                    "MiddleName": "",
                    "Suffix": "",
                    "NameType": "INDIVIDUAL",
                    "CountryOfBirth": "",
                    "Ssn": null,
                    "Dobs": "19390404",
                    "Pobs": "NEW YORK",
                    "Fax": "",
                    "Phones": "",
                    "Nationalities": "AMERICAN",
                    "Deceased": "",
                    "DeceasedNotes": "",
                    "Gender": "MALE",
                    "Title": "",
                    "TitleRole": "",
                    "Positions": "",
                    "Height": "5'10",
                    "Weight": "220 LBS",
                    "WeightInfo": "",
                    "Eyecolor": "BROWN",
                    "HairColor": "GRAY - BALDING",
                    "Age": "",
                    "Complexion": "",
                    "Build": "",
                    "Marks": "PALMER'S LEFT THUMB IS DEFORMED.",
                    "Citizenship": "",
                    "UsCitizenFlag": "",
                    "Languages": "",
                    "Race": "WHITE",
                    "Email": "",
                    "Website": "",
                    "LinkedPerson": "",
                    "Spouse": "",
                    "MaritalStatus": "",
                    "Profession": "",
                    "Specialty": "",
                    "Occupations": "",
                    "FbiNumber": "",
                    "NcicNumber": "",
                    "StateCriminalNumber": "",
                    "PassportNumber": "",
                    "NationalIdNumber": "",
                    "FidNumber": "",
                    "Fingerprint": "",
                    "DriversLicense": "",
                    "StateIdNumber": "",
                    "OriginalId": "",
                    "OriginalIdSource": ""
                  },
                  "Addresses": [],
                  "Aliases": [
                    {
                      "ResultsetNumber": 0,
                      "RecordId": "USFBIVIOLENTMURDERS284",
                      "AliasName": "PALMER, EUGENE KEVIN",
                      "AliasFirstName": "EUGENE",
                      "AliasLastName": "PALMER",
                      "AliasMiddleName": "KEVIN",
                      "AliasSuffix": "",
                      "AliasType": "",
                      "AliasRemarks": "",
                      "OriginalAliasId": ""
                    },
                    {
                      "ResultsetNumber": 0,
                      "RecordId": "USFBIVIOLENTMURDERS284",
                      "AliasName": "PALMER, EUGENE KENNETH",
                      "AliasFirstName": "EUGENE",
                      "AliasLastName": "PALMER",
                      "AliasMiddleName": "KENNETH",
                      "AliasSuffix": "",
                      "AliasType": "",
                      "AliasRemarks": "",
                      "OriginalAliasId": ""
                    },
                    {
                      "ResultsetNumber": 0,
                      "RecordId": "USFBIVIOLENTMURDERS284",
                      "AliasName": "PALMER, EUGENE K",
                      "AliasFirstName": "EUGENE",
                      "AliasLastName": "PALMER",
                      "AliasMiddleName": "K",
                      "AliasSuffix": "",
                      "AliasType": "",
                      "AliasRemarks": "",
                      "OriginalAliasId": ""
                    },
                    {
                      "ResultsetNumber": 0,
                      "RecordId": "USFBIVIOLENTMURDERS284",
                      "AliasName": "PALMER, EUGENE KEVIN",
                      "AliasFirstName": "EUGENE",
                      "AliasLastName": "PALMER",
                      "AliasMiddleName": "KEVIN",
                      "AliasSuffix": "",
                      "AliasType": "",
                      "AliasRemarks": "",
                      "OriginalAliasId": ""
                    },
                    {
                      "ResultsetNumber": 0,
                      "RecordId": "USFBIVIOLENTMURDERS284",
                      "AliasName": "PALMER, EUGENE KENNETH",
                      "AliasFirstName": "EUGENE",
                      "AliasLastName": "PALMER",
                      "AliasMiddleName": "KENNETH",
                      "AliasSuffix": "",
                      "AliasType": "",
                      "AliasRemarks": "",
                      "OriginalAliasId": ""
                    },
                    {
                      "ResultsetNumber": 0,
                      "RecordId": "USFBIVIOLENTMURDERS284",
                      "AliasName": "PALMER, EUGENE K",
                      "AliasFirstName": "EUGENE",
                      "AliasLastName": "PALMER",
                      "AliasMiddleName": "K",
                      "AliasSuffix": "",
                      "AliasType": "",
                      "AliasRemarks": "",
                      "OriginalAliasId": ""
                    },
                    {
                      "ResultsetNumber": 0,
                      "RecordId": "USFBIVIOLENTMURDERS284",
                      "AliasName": "PALMER, EUGENE KEVIN",
                      "AliasFirstName": "EUGENE",
                      "AliasLastName": "PALMER",
                      "AliasMiddleName": "KEVIN",
                      "AliasSuffix": "",
                      "AliasType": "",
                      "AliasRemarks": "",
                      "OriginalAliasId": ""
                    },
                    {
                      "ResultsetNumber": 0,
                      "RecordId": "USFBIVIOLENTMURDERS284",
                      "AliasName": "PALMER, EUGENE KENNETH",
                      "AliasFirstName": "EUGENE",
                      "AliasLastName": "PALMER",
                      "AliasMiddleName": "KENNETH",
                      "AliasSuffix": "",
                      "AliasType": "",
                      "AliasRemarks": "",
                      "OriginalAliasId": ""
                    },
                    {
                      "ResultsetNumber": 0,
                      "RecordId": "USFBIVIOLENTMURDERS284",
                      "AliasName": "PALMER, EUGENE K",
                      "AliasFirstName": "EUGENE",
                      "AliasLastName": "PALMER",
                      "AliasMiddleName": "K",
                      "AliasSuffix": "",
                      "AliasType": "",
                      "AliasRemarks": "",
                      "OriginalAliasId": ""
                    },
                    {
                      "ResultsetNumber": 0,
                      "RecordId": "USFBIVIOLENTMURDERS284",
                      "AliasName": "PALMER, EUGENE KEVIN",
                      "AliasFirstName": "EUGENE",
                      "AliasLastName": "PALMER",
                      "AliasMiddleName": "KEVIN",
                      "AliasSuffix": "",
                      "AliasType": "",
                      "AliasRemarks": "",
                      "OriginalAliasId": ""
                    },
                    {
                      "ResultsetNumber": 0,
                      "RecordId": "USFBIVIOLENTMURDERS284",
                      "AliasName": "PALMER, EUGENE KENNETH",
                      "AliasFirstName": "EUGENE",
                      "AliasLastName": "PALMER",
                      "AliasMiddleName": "KENNETH",
                      "AliasSuffix": "",
                      "AliasType": "",
                      "AliasRemarks": "",
                      "OriginalAliasId": ""
                    },
                    {
                      "ResultsetNumber": 0,
                      "RecordId": "USFBIVIOLENTMURDERS284",
                      "AliasName": "PALMER, EUGENE K",
                      "AliasFirstName": "EUGENE",
                      "AliasLastName": "PALMER",
                      "AliasMiddleName": "K",
                      "AliasSuffix": "",
                      "AliasType": "",
                      "AliasRemarks": "",
                      "OriginalAliasId": ""
                    }
                  ],
                  "Details": [
                    {
                      "ResultsetNumber": 4,
                      "RecordId": "USFBIVIOLENTMURDERS284",
                      "CaseNumber": "",
                      "DocketNumber": "",
                      "PermReferenceNumber": "",
                      "FederalRegCitation": "",
                      "DocAssociation": "",
                      "Violations": "",
                      "OriginalCharge": "",
                      "PrimaryCharge": "",
                      "Charge": "UNLAWFUL FLIGHT TO AVOID PROSECUTION - MURDER",
                      "Remarks": "PALMER IS KNOWN TO BE INTERESTED IN AUTO RACING AND IS A CAR ENTHUSIAST.&#160; HE IS ALSO AN EXPERIENCED HUNTER AND OUTDOORSMAN.",
                      "OtherInfo": "SHOULD BE CONSIDERED ARMED AND DANGEROUS",
                      "Details": "EUGENE PALMER&#160;IS WANTED FOR ALLEGEDLY SHOOTING AND KILLING HIS DAUGHTER-IN-LAW ON SEPTEMBER 24, 2012,&#160;IN STONY POINT, NEW YORK.&#160; AFTER A LOCAL ARREST WARRANT WAS ISSUED FOR PALMER&#160;IN ROCKLAND COUNTY AND HE WAS CHARGED WITH MURDER, A FEDERAL ARREST WARRANT WAS ISSUED ON JUNE 10, 2013,&#160;BY THE UNITED STATES COURT FOR THE SOUTHERN DISTRICT OF NEW YORK AFTER PALMER WAS CHARGED WITH UNLAWFUL FLIGHT TO AVOID PROSECUTION.&#160; &#160; THIS INVESTIGATION IS BEING CONDUCTED BY THE FBI&#8217;S WESTCHESTER SAFE STREETS/VIOLENT CRIMES TASK FORCE, THE HAVERSTRAW POLICE DEPARTMENT, AND THE UNITED STATES MARSHALS SERVICE. &#160;",
                      "InstitutionId": "",
                      "InstitutionAffliation": "",
                      "WarrantIssued": "",
                      "DateOfWarrant": "",
                      "WarrantNumber": "",
                      "Reward": "THE FBI IS OFFERING A REWARD OF UP TO $20,000 FOR INFORMATION LEADING TO THE ARREST AND CONVICTION OF EUGENE PALMER. ADDITIONAL REWARD MONEY MAY BE OFFERED BY OTHER LAW ENFORCEMENT AGENCIES.",
                      "Program": "",
                      "ProgramCode": "",
                      "IssueDate": "",
                      "TypeCode": "",
                      "TypeDescription": "",
                      "OrderNumber": "",
                      "TypeOfOrder": "",
                      "StandardOrder": "",
                      "VesselRegistration": "",
                      "VesselCallSign": "",
                      "VesselType": "",
                      "VesselTonnage": "",
                      "GrossRegisteredTonnage": "",
                      "VesselFlag": "",
                      "VesselOwner": "",
                      "BusinessRegDoc": "",
                      "EffectiveDate": "",
                      "ExpirationDate": "",
                      "EnforcementAction": "",
                      "Caution": "",
                      "Grp": "",
                      "Rolee": "",
                      "PassportNum": "",
                      "PassportInfo": "",
                      "DateOfDissertion": "",
                      "GangAffiliation": "",
                      "Type": "",
                      "ControlDate": "",
                      "Regime": "",
                      "FederalRegNum": "",
                      "FederalRegDate": "",
                      "DisqualifiedFrom": "",
                      "DisqualifiedTo": ""
                    },
                    {
                      "ResultsetNumber": 4,
                      "RecordId": "USFBIVIOLENTMURDERS284",
                      "CaseNumber": "",
                      "DocketNumber": "",
                      "PermReferenceNumber": "",
                      "FederalRegCitation": "",
                      "DocAssociation": "",
                      "Violations": "",
                      "OriginalCharge": "",
                      "PrimaryCharge": "",
                      "Charge": "UNLAWFUL FLIGHT TO AVOID PROSECUTION - MURDER",
                      "Remarks": "PALMER IS KNOWN TO BE INTERESTED IN AUTO RACING AND IS A CAR ENTHUSIAST.&#160; HE IS ALSO AN EXPERIENCED HUNTER AND OUTDOORSMAN.",
                      "OtherInfo": "SHOULD BE CONSIDERED ARMED AND DANGEROUS",
                      "Details": "EUGENE PALMER&#160;IS WANTED FOR ALLEGEDLY SHOOTING AND KILLING HIS DAUGHTER-IN-LAW ON SEPTEMBER 24, 2012,&#160;IN STONY POINT, NEW YORK.&#160; AFTER A LOCAL ARREST WARRANT WAS ISSUED FOR PALMER&#160;IN ROCKLAND COUNTY AND HE WAS CHARGED WITH MURDER, A FEDERAL ARREST WARRANT WAS ISSUED ON JUNE 10, 2013,&#160;BY THE UNITED STATES COURT FOR THE SOUTHERN DISTRICT OF NEW YORK AFTER PALMER WAS CHARGED WITH UNLAWFUL FLIGHT TO AVOID PROSECUTION.&#160; &#160; THIS INVESTIGATION IS BEING CONDUCTED BY THE FBI&#8217;S WESTCHESTER SAFE STREETS/VIOLENT CRIMES TASK FORCE, THE HAVERSTRAW POLICE DEPARTMENT, AND THE UNITED STATES MARSHALS SERVICE. &#160;",
                      "InstitutionId": "",
                      "InstitutionAffliation": "",
                      "WarrantIssued": "",
                      "DateOfWarrant": "",
                      "WarrantNumber": "",
                      "Reward": "THE FBI IS OFFERING A REWARD OF UP TO $20,000 FOR INFORMATION LEADING TO THE ARREST AND CONVICTION OF EUGENE PALMER. ADDITIONAL REWARD MONEY MAY BE OFFERED BY OTHER LAW ENFORCEMENT AGENCIES.",
                      "Program": "",
                      "ProgramCode": "",
                      "IssueDate": "",
                      "TypeCode": "",
                      "TypeDescription": "",
                      "OrderNumber": "",
                      "TypeOfOrder": "",
                      "StandardOrder": "",
                      "VesselRegistration": "",
                      "VesselCallSign": "",
                      "VesselType": "",
                      "VesselTonnage": "",
                      "GrossRegisteredTonnage": "",
                      "VesselFlag": "",
                      "VesselOwner": "",
                      "BusinessRegDoc": "",
                      "EffectiveDate": "",
                      "ExpirationDate": "",
                      "EnforcementAction": "",
                      "Caution": "",
                      "Grp": "",
                      "Rolee": "",
                      "PassportNum": "",
                      "PassportInfo": "",
                      "DateOfDissertion": "",
                      "GangAffiliation": "",
                      "Type": "",
                      "ControlDate": "",
                      "Regime": "",
                      "FederalRegNum": "",
                      "FederalRegDate": "",
                      "DisqualifiedFrom": "",
                      "DisqualifiedTo": ""
                    },
                    {
                      "ResultsetNumber": 4,
                      "RecordId": "USFBIVIOLENTMURDERS284",
                      "CaseNumber": "",
                      "DocketNumber": "",
                      "PermReferenceNumber": "",
                      "FederalRegCitation": "",
                      "DocAssociation": "",
                      "Violations": "",
                      "OriginalCharge": "",
                      "PrimaryCharge": "",
                      "Charge": "UNLAWFUL FLIGHT TO AVOID PROSECUTION - MURDER",
                      "Remarks": "PALMER IS KNOWN TO BE INTERESTED IN AUTO RACING AND IS A CAR ENTHUSIAST.&#160; HE IS ALSO AN EXPERIENCED HUNTER AND OUTDOORSMAN.",
                      "OtherInfo": "SHOULD BE CONSIDERED ARMED AND DANGEROUS",
                      "Details": "EUGENE PALMER&#160;IS WANTED FOR ALLEGEDLY SHOOTING AND KILLING HIS DAUGHTER-IN-LAW ON SEPTEMBER 24, 2012,&#160;IN STONY POINT, NEW YORK.&#160; AFTER A LOCAL ARREST WARRANT WAS ISSUED FOR PALMER&#160;IN ROCKLAND COUNTY AND HE WAS CHARGED WITH MURDER, A FEDERAL ARREST WARRANT WAS ISSUED ON JUNE 10, 2013,&#160;BY THE UNITED STATES COURT FOR THE SOUTHERN DISTRICT OF NEW YORK AFTER PALMER WAS CHARGED WITH UNLAWFUL FLIGHT TO AVOID PROSECUTION.&#160; &#160; THIS INVESTIGATION IS BEING CONDUCTED BY THE FBI&#8217;S WESTCHESTER SAFE STREETS/VIOLENT CRIMES TASK FORCE, THE HAVERSTRAW POLICE DEPARTMENT, AND THE UNITED STATES MARSHALS SERVICE. &#160;",
                      "InstitutionId": "",
                      "InstitutionAffliation": "",
                      "WarrantIssued": "",
                      "DateOfWarrant": "",
                      "WarrantNumber": "",
                      "Reward": "THE FBI IS OFFERING A REWARD OF UP TO $20,000 FOR INFORMATION LEADING TO THE ARREST AND CONVICTION OF EUGENE PALMER. ADDITIONAL REWARD MONEY MAY BE OFFERED BY OTHER LAW ENFORCEMENT AGENCIES.",
                      "Program": "",
                      "ProgramCode": "",
                      "IssueDate": "",
                      "TypeCode": "",
                      "TypeDescription": "",
                      "OrderNumber": "",
                      "TypeOfOrder": "",
                      "StandardOrder": "",
                      "VesselRegistration": "",
                      "VesselCallSign": "",
                      "VesselType": "",
                      "VesselTonnage": "",
                      "GrossRegisteredTonnage": "",
                      "VesselFlag": "",
                      "VesselOwner": "",
                      "BusinessRegDoc": "",
                      "EffectiveDate": "",
                      "ExpirationDate": "",
                      "EnforcementAction": "",
                      "Caution": "",
                      "Grp": "",
                      "Rolee": "",
                      "PassportNum": "",
                      "PassportInfo": "",
                      "DateOfDissertion": "",
                      "GangAffiliation": "",
                      "Type": "",
                      "ControlDate": "",
                      "Regime": "",
                      "FederalRegNum": "",
                      "FederalRegDate": "",
                      "DisqualifiedFrom": "",
                      "DisqualifiedTo": ""
                    },
                    {
                      "ResultsetNumber": 4,
                      "RecordId": "USFBIVIOLENTMURDERS284",
                      "CaseNumber": "",
                      "DocketNumber": "",
                      "PermReferenceNumber": "",
                      "FederalRegCitation": "",
                      "DocAssociation": "",
                      "Violations": "",
                      "OriginalCharge": "",
                      "PrimaryCharge": "",
                      "Charge": "UNLAWFUL FLIGHT TO AVOID PROSECUTION - MURDER",
                      "Remarks": "PALMER IS KNOWN TO BE INTERESTED IN AUTO RACING AND IS A CAR ENTHUSIAST.&#160; HE IS ALSO AN EXPERIENCED HUNTER AND OUTDOORSMAN.",
                      "OtherInfo": "SHOULD BE CONSIDERED ARMED AND DANGEROUS",
                      "Details": "EUGENE PALMER&#160;IS WANTED FOR ALLEGEDLY SHOOTING AND KILLING HIS DAUGHTER-IN-LAW ON SEPTEMBER 24, 2012,&#160;IN STONY POINT, NEW YORK.&#160; AFTER A LOCAL ARREST WARRANT WAS ISSUED FOR PALMER&#160;IN ROCKLAND COUNTY AND HE WAS CHARGED WITH MURDER, A FEDERAL ARREST WARRANT WAS ISSUED ON JUNE 10, 2013,&#160;BY THE UNITED STATES COURT FOR THE SOUTHERN DISTRICT OF NEW YORK AFTER PALMER WAS CHARGED WITH UNLAWFUL FLIGHT TO AVOID PROSECUTION.&#160; &#160; THIS INVESTIGATION IS BEING CONDUCTED BY THE FBI&#8217;S WESTCHESTER SAFE STREETS/VIOLENT CRIMES TASK FORCE, THE HAVERSTRAW POLICE DEPARTMENT, AND THE UNITED STATES MARSHALS SERVICE. &#160;",
                      "InstitutionId": "",
                      "InstitutionAffliation": "",
                      "WarrantIssued": "",
                      "DateOfWarrant": "",
                      "WarrantNumber": "",
                      "Reward": "THE FBI IS OFFERING A REWARD OF UP TO $20,000 FOR INFORMATION LEADING TO THE ARREST AND CONVICTION OF EUGENE PALMER. ADDITIONAL REWARD MONEY MAY BE OFFERED BY OTHER LAW ENFORCEMENT AGENCIES.",
                      "Program": "",
                      "ProgramCode": "",
                      "IssueDate": "",
                      "TypeCode": "",
                      "TypeDescription": "",
                      "OrderNumber": "",
                      "TypeOfOrder": "",
                      "StandardOrder": "",
                      "VesselRegistration": "",
                      "VesselCallSign": "",
                      "VesselType": "",
                      "VesselTonnage": "",
                      "GrossRegisteredTonnage": "",
                      "VesselFlag": "",
                      "VesselOwner": "",
                      "BusinessRegDoc": "",
                      "EffectiveDate": "",
                      "ExpirationDate": "",
                      "EnforcementAction": "",
                      "Caution": "",
                      "Grp": "",
                      "Rolee": "",
                      "PassportNum": "",
                      "PassportInfo": "",
                      "DateOfDissertion": "",
                      "GangAffiliation": "",
                      "Type": "",
                      "ControlDate": "",
                      "Regime": "",
                      "FederalRegNum": "",
                      "FederalRegDate": "",
                      "DisqualifiedFrom": "",
                      "DisqualifiedTo": ""
                    }
                  ]
                },
                {
                  "RecordId": "USFBIVIOLENTMURDERS284",
                  "Main": {
                    "ResultsetNumber": 1,
                    "RecordId": "USFBIVIOLENTMURDERS284",
                    "SourceName": "US FEDERAL BUREAU OF INVESTIGATION VIOLENT MURDERS",
                    "SourceType": "",
                    "RecordUploadDate": 20190123,
                    "Name": "PALMER, EUGENE",
                    "LastName": "PALMER",
                    "FirstName": "EUGENE",
                    "MiddleName": "",
                    "Suffix": "",
                    "NameType": "INDIVIDUAL",
                    "CountryOfBirth": "",
                    "Ssn": null,
                    "Dobs": "19390404",
                    "Pobs": "NEW YORK",
                    "Fax": "",
                    "Phones": "",
                    "Nationalities": "AMERICAN",
                    "Deceased": "",
                    "DeceasedNotes": "",
                    "Gender": "MALE",
                    "Title": "",
                    "TitleRole": "",
                    "Positions": "",
                    "Height": "5'10",
                    "Weight": "220 LBS",
                    "WeightInfo": "",
                    "Eyecolor": "BROWN",
                    "HairColor": "GRAY - BALDING",
                    "Age": "",
                    "Complexion": "",
                    "Build": "",
                    "Marks": "PALMER'S LEFT THUMB IS DEFORMED.",
                    "Citizenship": "",
                    "UsCitizenFlag": "",
                    "Languages": "",
                    "Race": "WHITE",
                    "Email": "",
                    "Website": "",
                    "LinkedPerson": "",
                    "Spouse": "",
                    "MaritalStatus": "",
                    "Profession": "",
                    "Specialty": "",
                    "Occupations": "",
                    "FbiNumber": "",
                    "NcicNumber": "",
                    "StateCriminalNumber": "",
                    "PassportNumber": "",
                    "NationalIdNumber": "",
                    "FidNumber": "",
                    "Fingerprint": "",
                    "DriversLicense": "",
                    "StateIdNumber": "",
                    "OriginalId": "",
                    "OriginalIdSource": ""
                  },
                  "Addresses": [],
                  "Aliases": [
                    {
                      "ResultsetNumber": 0,
                      "RecordId": "USFBIVIOLENTMURDERS284",
                      "AliasName": "PALMER, EUGENE KEVIN",
                      "AliasFirstName": "EUGENE",
                      "AliasLastName": "PALMER",
                      "AliasMiddleName": "KEVIN",
                      "AliasSuffix": "",
                      "AliasType": "",
                      "AliasRemarks": "",
                      "OriginalAliasId": ""
                    },
                    {
                      "ResultsetNumber": 0,
                      "RecordId": "USFBIVIOLENTMURDERS284",
                      "AliasName": "PALMER, EUGENE KENNETH",
                      "AliasFirstName": "EUGENE",
                      "AliasLastName": "PALMER",
                      "AliasMiddleName": "KENNETH",
                      "AliasSuffix": "",
                      "AliasType": "",
                      "AliasRemarks": "",
                      "OriginalAliasId": ""
                    },
                    {
                      "ResultsetNumber": 0,
                      "RecordId": "USFBIVIOLENTMURDERS284",
                      "AliasName": "PALMER, EUGENE K",
                      "AliasFirstName": "EUGENE",
                      "AliasLastName": "PALMER",
                      "AliasMiddleName": "K",
                      "AliasSuffix": "",
                      "AliasType": "",
                      "AliasRemarks": "",
                      "OriginalAliasId": ""
                    },
                    {
                      "ResultsetNumber": 0,
                      "RecordId": "USFBIVIOLENTMURDERS284",
                      "AliasName": "PALMER, EUGENE KEVIN",
                      "AliasFirstName": "EUGENE",
                      "AliasLastName": "PALMER",
                      "AliasMiddleName": "KEVIN",
                      "AliasSuffix": "",
                      "AliasType": "",
                      "AliasRemarks": "",
                      "OriginalAliasId": ""
                    },
                    {
                      "ResultsetNumber": 0,
                      "RecordId": "USFBIVIOLENTMURDERS284",
                      "AliasName": "PALMER, EUGENE KENNETH",
                      "AliasFirstName": "EUGENE",
                      "AliasLastName": "PALMER",
                      "AliasMiddleName": "KENNETH",
                      "AliasSuffix": "",
                      "AliasType": "",
                      "AliasRemarks": "",
                      "OriginalAliasId": ""
                    },
                    {
                      "ResultsetNumber": 0,
                      "RecordId": "USFBIVIOLENTMURDERS284",
                      "AliasName": "PALMER, EUGENE K",
                      "AliasFirstName": "EUGENE",
                      "AliasLastName": "PALMER",
                      "AliasMiddleName": "K",
                      "AliasSuffix": "",
                      "AliasType": "",
                      "AliasRemarks": "",
                      "OriginalAliasId": ""
                    },
                    {
                      "ResultsetNumber": 0,
                      "RecordId": "USFBIVIOLENTMURDERS284",
                      "AliasName": "PALMER, EUGENE KEVIN",
                      "AliasFirstName": "EUGENE",
                      "AliasLastName": "PALMER",
                      "AliasMiddleName": "KEVIN",
                      "AliasSuffix": "",
                      "AliasType": "",
                      "AliasRemarks": "",
                      "OriginalAliasId": ""
                    },
                    {
                      "ResultsetNumber": 0,
                      "RecordId": "USFBIVIOLENTMURDERS284",
                      "AliasName": "PALMER, EUGENE KENNETH",
                      "AliasFirstName": "EUGENE",
                      "AliasLastName": "PALMER",
                      "AliasMiddleName": "KENNETH",
                      "AliasSuffix": "",
                      "AliasType": "",
                      "AliasRemarks": "",
                      "OriginalAliasId": ""
                    },
                    {
                      "ResultsetNumber": 0,
                      "RecordId": "USFBIVIOLENTMURDERS284",
                      "AliasName": "PALMER, EUGENE K",
                      "AliasFirstName": "EUGENE",
                      "AliasLastName": "PALMER",
                      "AliasMiddleName": "K",
                      "AliasSuffix": "",
                      "AliasType": "",
                      "AliasRemarks": "",
                      "OriginalAliasId": ""
                    },
                    {
                      "ResultsetNumber": 0,
                      "RecordId": "USFBIVIOLENTMURDERS284",
                      "AliasName": "PALMER, EUGENE KEVIN",
                      "AliasFirstName": "EUGENE",
                      "AliasLastName": "PALMER",
                      "AliasMiddleName": "KEVIN",
                      "AliasSuffix": "",
                      "AliasType": "",
                      "AliasRemarks": "",
                      "OriginalAliasId": ""
                    },
                    {
                      "ResultsetNumber": 0,
                      "RecordId": "USFBIVIOLENTMURDERS284",
                      "AliasName": "PALMER, EUGENE KENNETH",
                      "AliasFirstName": "EUGENE",
                      "AliasLastName": "PALMER",
                      "AliasMiddleName": "KENNETH",
                      "AliasSuffix": "",
                      "AliasType": "",
                      "AliasRemarks": "",
                      "OriginalAliasId": ""
                    },
                    {
                      "ResultsetNumber": 0,
                      "RecordId": "USFBIVIOLENTMURDERS284",
                      "AliasName": "PALMER, EUGENE K",
                      "AliasFirstName": "EUGENE",
                      "AliasLastName": "PALMER",
                      "AliasMiddleName": "K",
                      "AliasSuffix": "",
                      "AliasType": "",
                      "AliasRemarks": "",
                      "OriginalAliasId": ""
                    }
                  ],
                  "Details": [
                    {
                      "ResultsetNumber": 4,
                      "RecordId": "USFBIVIOLENTMURDERS284",
                      "CaseNumber": "",
                      "DocketNumber": "",
                      "PermReferenceNumber": "",
                      "FederalRegCitation": "",
                      "DocAssociation": "",
                      "Violations": "",
                      "OriginalCharge": "",
                      "PrimaryCharge": "",
                      "Charge": "UNLAWFUL FLIGHT TO AVOID PROSECUTION - MURDER",
                      "Remarks": "PALMER IS KNOWN TO BE INTERESTED IN AUTO RACING AND IS A CAR ENTHUSIAST.&#160; HE IS ALSO AN EXPERIENCED HUNTER AND OUTDOORSMAN.",
                      "OtherInfo": "SHOULD BE CONSIDERED ARMED AND DANGEROUS",
                      "Details": "EUGENE PALMER&#160;IS WANTED FOR ALLEGEDLY SHOOTING AND KILLING HIS DAUGHTER-IN-LAW ON SEPTEMBER 24, 2012,&#160;IN STONY POINT, NEW YORK.&#160; AFTER A LOCAL ARREST WARRANT WAS ISSUED FOR PALMER&#160;IN ROCKLAND COUNTY AND HE WAS CHARGED WITH MURDER, A FEDERAL ARREST WARRANT WAS ISSUED ON JUNE 10, 2013,&#160;BY THE UNITED STATES COURT FOR THE SOUTHERN DISTRICT OF NEW YORK AFTER PALMER WAS CHARGED WITH UNLAWFUL FLIGHT TO AVOID PROSECUTION.&#160; &#160; THIS INVESTIGATION IS BEING CONDUCTED BY THE FBI&#8217;S WESTCHESTER SAFE STREETS/VIOLENT CRIMES TASK FORCE, THE HAVERSTRAW POLICE DEPARTMENT, AND THE UNITED STATES MARSHALS SERVICE. &#160;",
                      "InstitutionId": "",
                      "InstitutionAffliation": "",
                      "WarrantIssued": "",
                      "DateOfWarrant": "",
                      "WarrantNumber": "",
                      "Reward": "THE FBI IS OFFERING A REWARD OF UP TO $20,000 FOR INFORMATION LEADING TO THE ARREST AND CONVICTION OF EUGENE PALMER. ADDITIONAL REWARD MONEY MAY BE OFFERED BY OTHER LAW ENFORCEMENT AGENCIES.",
                      "Program": "",
                      "ProgramCode": "",
                      "IssueDate": "",
                      "TypeCode": "",
                      "TypeDescription": "",
                      "OrderNumber": "",
                      "TypeOfOrder": "",
                      "StandardOrder": "",
                      "VesselRegistration": "",
                      "VesselCallSign": "",
                      "VesselType": "",
                      "VesselTonnage": "",
                      "GrossRegisteredTonnage": "",
                      "VesselFlag": "",
                      "VesselOwner": "",
                      "BusinessRegDoc": "",
                      "EffectiveDate": "",
                      "ExpirationDate": "",
                      "EnforcementAction": "",
                      "Caution": "",
                      "Grp": "",
                      "Rolee": "",
                      "PassportNum": "",
                      "PassportInfo": "",
                      "DateOfDissertion": "",
                      "GangAffiliation": "",
                      "Type": "",
                      "ControlDate": "",
                      "Regime": "",
                      "FederalRegNum": "",
                      "FederalRegDate": "",
                      "DisqualifiedFrom": "",
                      "DisqualifiedTo": ""
                    },
                    {
                      "ResultsetNumber": 4,
                      "RecordId": "USFBIVIOLENTMURDERS284",
                      "CaseNumber": "",
                      "DocketNumber": "",
                      "PermReferenceNumber": "",
                      "FederalRegCitation": "",
                      "DocAssociation": "",
                      "Violations": "",
                      "OriginalCharge": "",
                      "PrimaryCharge": "",
                      "Charge": "UNLAWFUL FLIGHT TO AVOID PROSECUTION - MURDER",
                      "Remarks": "PALMER IS KNOWN TO BE INTERESTED IN AUTO RACING AND IS A CAR ENTHUSIAST.&#160; HE IS ALSO AN EXPERIENCED HUNTER AND OUTDOORSMAN.",
                      "OtherInfo": "SHOULD BE CONSIDERED ARMED AND DANGEROUS",
                      "Details": "EUGENE PALMER&#160;IS WANTED FOR ALLEGEDLY SHOOTING AND KILLING HIS DAUGHTER-IN-LAW ON SEPTEMBER 24, 2012,&#160;IN STONY POINT, NEW YORK.&#160; AFTER A LOCAL ARREST WARRANT WAS ISSUED FOR PALMER&#160;IN ROCKLAND COUNTY AND HE WAS CHARGED WITH MURDER, A FEDERAL ARREST WARRANT WAS ISSUED ON JUNE 10, 2013,&#160;BY THE UNITED STATES COURT FOR THE SOUTHERN DISTRICT OF NEW YORK AFTER PALMER WAS CHARGED WITH UNLAWFUL FLIGHT TO AVOID PROSECUTION.&#160; &#160; THIS INVESTIGATION IS BEING CONDUCTED BY THE FBI&#8217;S WESTCHESTER SAFE STREETS/VIOLENT CRIMES TASK FORCE, THE HAVERSTRAW POLICE DEPARTMENT, AND THE UNITED STATES MARSHALS SERVICE. &#160;",
                      "InstitutionId": "",
                      "InstitutionAffliation": "",
                      "WarrantIssued": "",
                      "DateOfWarrant": "",
                      "WarrantNumber": "",
                      "Reward": "THE FBI IS OFFERING A REWARD OF UP TO $20,000 FOR INFORMATION LEADING TO THE ARREST AND CONVICTION OF EUGENE PALMER. ADDITIONAL REWARD MONEY MAY BE OFFERED BY OTHER LAW ENFORCEMENT AGENCIES.",
                      "Program": "",
                      "ProgramCode": "",
                      "IssueDate": "",
                      "TypeCode": "",
                      "TypeDescription": "",
                      "OrderNumber": "",
                      "TypeOfOrder": "",
                      "StandardOrder": "",
                      "VesselRegistration": "",
                      "VesselCallSign": "",
                      "VesselType": "",
                      "VesselTonnage": "",
                      "GrossRegisteredTonnage": "",
                      "VesselFlag": "",
                      "VesselOwner": "",
                      "BusinessRegDoc": "",
                      "EffectiveDate": "",
                      "ExpirationDate": "",
                      "EnforcementAction": "",
                      "Caution": "",
                      "Grp": "",
                      "Rolee": "",
                      "PassportNum": "",
                      "PassportInfo": "",
                      "DateOfDissertion": "",
                      "GangAffiliation": "",
                      "Type": "",
                      "ControlDate": "",
                      "Regime": "",
                      "FederalRegNum": "",
                      "FederalRegDate": "",
                      "DisqualifiedFrom": "",
                      "DisqualifiedTo": ""
                    },
                    {
                      "ResultsetNumber": 4,
                      "RecordId": "USFBIVIOLENTMURDERS284",
                      "CaseNumber": "",
                      "DocketNumber": "",
                      "PermReferenceNumber": "",
                      "FederalRegCitation": "",
                      "DocAssociation": "",
                      "Violations": "",
                      "OriginalCharge": "",
                      "PrimaryCharge": "",
                      "Charge": "UNLAWFUL FLIGHT TO AVOID PROSECUTION - MURDER",
                      "Remarks": "PALMER IS KNOWN TO BE INTERESTED IN AUTO RACING AND IS A CAR ENTHUSIAST.&#160; HE IS ALSO AN EXPERIENCED HUNTER AND OUTDOORSMAN.",
                      "OtherInfo": "SHOULD BE CONSIDERED ARMED AND DANGEROUS",
                      "Details": "EUGENE PALMER&#160;IS WANTED FOR ALLEGEDLY SHOOTING AND KILLING HIS DAUGHTER-IN-LAW ON SEPTEMBER 24, 2012,&#160;IN STONY POINT, NEW YORK.&#160; AFTER A LOCAL ARREST WARRANT WAS ISSUED FOR PALMER&#160;IN ROCKLAND COUNTY AND HE WAS CHARGED WITH MURDER, A FEDERAL ARREST WARRANT WAS ISSUED ON JUNE 10, 2013,&#160;BY THE UNITED STATES COURT FOR THE SOUTHERN DISTRICT OF NEW YORK AFTER PALMER WAS CHARGED WITH UNLAWFUL FLIGHT TO AVOID PROSECUTION.&#160; &#160; THIS INVESTIGATION IS BEING CONDUCTED BY THE FBI&#8217;S WESTCHESTER SAFE STREETS/VIOLENT CRIMES TASK FORCE, THE HAVERSTRAW POLICE DEPARTMENT, AND THE UNITED STATES MARSHALS SERVICE. &#160;",
                      "InstitutionId": "",
                      "InstitutionAffliation": "",
                      "WarrantIssued": "",
                      "DateOfWarrant": "",
                      "WarrantNumber": "",
                      "Reward": "THE FBI IS OFFERING A REWARD OF UP TO $20,000 FOR INFORMATION LEADING TO THE ARREST AND CONVICTION OF EUGENE PALMER. ADDITIONAL REWARD MONEY MAY BE OFFERED BY OTHER LAW ENFORCEMENT AGENCIES.",
                      "Program": "",
                      "ProgramCode": "",
                      "IssueDate": "",
                      "TypeCode": "",
                      "TypeDescription": "",
                      "OrderNumber": "",
                      "TypeOfOrder": "",
                      "StandardOrder": "",
                      "VesselRegistration": "",
                      "VesselCallSign": "",
                      "VesselType": "",
                      "VesselTonnage": "",
                      "GrossRegisteredTonnage": "",
                      "VesselFlag": "",
                      "VesselOwner": "",
                      "BusinessRegDoc": "",
                      "EffectiveDate": "",
                      "ExpirationDate": "",
                      "EnforcementAction": "",
                      "Caution": "",
                      "Grp": "",
                      "Rolee": "",
                      "PassportNum": "",
                      "PassportInfo": "",
                      "DateOfDissertion": "",
                      "GangAffiliation": "",
                      "Type": "",
                      "ControlDate": "",
                      "Regime": "",
                      "FederalRegNum": "",
                      "FederalRegDate": "",
                      "DisqualifiedFrom": "",
                      "DisqualifiedTo": ""
                    },
                    {
                      "ResultsetNumber": 4,
                      "RecordId": "USFBIVIOLENTMURDERS284",
                      "CaseNumber": "",
                      "DocketNumber": "",
                      "PermReferenceNumber": "",
                      "FederalRegCitation": "",
                      "DocAssociation": "",
                      "Violations": "",
                      "OriginalCharge": "",
                      "PrimaryCharge": "",
                      "Charge": "UNLAWFUL FLIGHT TO AVOID PROSECUTION - MURDER",
                      "Remarks": "PALMER IS KNOWN TO BE INTERESTED IN AUTO RACING AND IS A CAR ENTHUSIAST.&#160; HE IS ALSO AN EXPERIENCED HUNTER AND OUTDOORSMAN.",
                      "OtherInfo": "SHOULD BE CONSIDERED ARMED AND DANGEROUS",
                      "Details": "EUGENE PALMER&#160;IS WANTED FOR ALLEGEDLY SHOOTING AND KILLING HIS DAUGHTER-IN-LAW ON SEPTEMBER 24, 2012,&#160;IN STONY POINT, NEW YORK.&#160; AFTER A LOCAL ARREST WARRANT WAS ISSUED FOR PALMER&#160;IN ROCKLAND COUNTY AND HE WAS CHARGED WITH MURDER, A FEDERAL ARREST WARRANT WAS ISSUED ON JUNE 10, 2013,&#160;BY THE UNITED STATES COURT FOR THE SOUTHERN DISTRICT OF NEW YORK AFTER PALMER WAS CHARGED WITH UNLAWFUL FLIGHT TO AVOID PROSECUTION.&#160; &#160; THIS INVESTIGATION IS BEING CONDUCTED BY THE FBI&#8217;S WESTCHESTER SAFE STREETS/VIOLENT CRIMES TASK FORCE, THE HAVERSTRAW POLICE DEPARTMENT, AND THE UNITED STATES MARSHALS SERVICE. &#160;",
                      "InstitutionId": "",
                      "InstitutionAffliation": "",
                      "WarrantIssued": "",
                      "DateOfWarrant": "",
                      "WarrantNumber": "",
                      "Reward": "THE FBI IS OFFERING A REWARD OF UP TO $20,000 FOR INFORMATION LEADING TO THE ARREST AND CONVICTION OF EUGENE PALMER. ADDITIONAL REWARD MONEY MAY BE OFFERED BY OTHER LAW ENFORCEMENT AGENCIES.",
                      "Program": "",
                      "ProgramCode": "",
                      "IssueDate": "",
                      "TypeCode": "",
                      "TypeDescription": "",
                      "OrderNumber": "",
                      "TypeOfOrder": "",
                      "StandardOrder": "",
                      "VesselRegistration": "",
                      "VesselCallSign": "",
                      "VesselType": "",
                      "VesselTonnage": "",
                      "GrossRegisteredTonnage": "",
                      "VesselFlag": "",
                      "VesselOwner": "",
                      "BusinessRegDoc": "",
                      "EffectiveDate": "",
                      "ExpirationDate": "",
                      "EnforcementAction": "",
                      "Caution": "",
                      "Grp": "",
                      "Rolee": "",
                      "PassportNum": "",
                      "PassportInfo": "",
                      "DateOfDissertion": "",
                      "GangAffiliation": "",
                      "Type": "",
                      "ControlDate": "",
                      "Regime": "",
                      "FederalRegNum": "",
                      "FederalRegDate": "",
                      "DisqualifiedFrom": "",
                      "DisqualifiedTo": ""
                    }
                  ]
                }
              ],
              "OfacRecordCounts": 4,
              "ResponseRecordCount": 4,
              "Pagination": {
                "CurrentPageNumber": 1,
                "ResultsPerPage": 10,
                "TotalPages": 1
              },
              "DatabaseQueryInfo": [
                {
                  "SearchType": "",
                  "HasIntermediateSort": false,
                  "RetryCount": 99,
                  "IdCount": 4,
                  "MatchRecordCount": 4,
                  "DatabaseQueries": [
                    {
                      "Host": "DevMySql03.cco",
                      "Database": "blacklist",
                      "DatabaseConnectionTimeInMs": 1,
                      "DatabaseQuery": "CALL search_blacklist(@p_entity_name := null, @p_name := 'Eugene Palmer', @p_record_limit := 10);",
                      "ExecutionTimeInMs": 34
                    }
                  ]
                }
              ],
              "ExecutionStatistics": [
                {
                  "Description": "Ofac SP Client Search",
                  "StartTime": 1,
                  "ExecutionTimeInMs": 35
                },
                {
                  "Description": "CALL search_blacklist",
                  "StartTime": 1,
                  "ExecutionTimeInMs": 35
                }
              ],
              "SearchCriteria": [],
              "TotalRequestExecutionTimeMs": 39,
              "RequestId": "e343d07c-300f-440a-a214-00b7d9abc23e",
              "RequestType": "Search",
              "RequestTime": "2019-06-24T07:22:16.1372087-07:00",
              "IsError": false,
              "Error": {
                "InputErrors": [],
                "Warnings": []
              }
            }
        }
        
## Identity Verification [/IdVerificationScoreSearch]

Performs an identity verification search, and returns a list of people matching the search criteria.
+ Each person result match will have an <code>identityScore</code> out of 100. 
+ The <code>identityVerified</code> flag indicates whether identity was verified.

### Search  [POST]

###### *Click on the grey search box above, to view sample request/response objects for the Identity Verification Search*

Perform a search:

1. Add your Access Profile username and password to the request headers.
    * galaxy-ap-name: [Access Profile Name]
    * galaxy-ap-password: [Access Profile Password]
    * galaxy-client-session-id: (Optional) Session ID for logging
    
2.  Add search criteria to your request.  At least two are required: SSN, Name, Phone, Address or Email.
    ~~~html
            {
                "SSN": "",
                "Last4SSN": "",
                "FirstName": "John",
                "MiddleName": "T",
                "LastName": "Lawrence",
                "Dob":"",
                "Age": 0,
                "Address": {
                    "addressLine1":"",
                    "addressLine2":""
                },
                "PhoneNumber":"",
                "Email":""
            }
    ~~~
3. Select any desired data filters:
    ```
    {
        "Includes": ["SocialSecurityNumbers"],
        "FilterOptions": [
            "IncludeFullSsnValues", 
            "IncludePrivateData", 
            "IncludeOptOutData"
        ]
    }
    
4.  Submit your search




A complete list of JSON request properties follows.
* `SSN              ` = null (optional, string) ... Social security number (format: ###-##-####).
* `Last4SSN         ` = null (optional, string) ... Last 4 digits of a Social security number (format:####). 
                        It will not be used for searching but for scoring only.
* `FirstName        `= null (optional, string) ... First name.
* `MiddleName       ` = null (optional, string) ... Middle name or middle initial.
* `LastName         ` = null (optional, string) ... Last name.
* `Dob              ` = null (optional, string) ... Date of birth (format: MM/DD/YYYY).
* `Age              ` = null (optional, int) ... Age.
* `Addresses        ` = null (optional, Addresses[]) ... List of addresses.
    * Members
        * AddressLine1 = null (optional, string) ... House number, street name and Unit number (i.e. 123 Q Street, Unit 102) or PO Box (i.e. 1821 Q Street).
        * AddressLine2 = null (optional, string) ... State or City and State or Zip (i.e. Sacramento, CA).
* `Phones           ` = null (optional, string) ... Phone number (formats: ###-###-####, (###) ###-####).
* `Emails           ` = null (optional, string) ... E-mail address.

<i><strong>If you are an API partner</strong> and are missing any include/members listed below, then please contact our revenue department so we can adjust your access profile configuration.</i>

* `Includes` (optional, string[]) ... Data to be included in the response.
    * Members
        * `SocialSecurityNumbers`
        
<i><strong>If you are an API partner</strong> you <strong>DO NOT</strong> need to pass these includes or filters. These items are pre-configured on your access profile. If you are missing one of these data elements or would like to enable or disable a filter, then please contact our revenue department so we can adjust your access profile configuration.</i>
        
* `FilterOptions` (optional, string[]) ... Data filtering options.
    * Members
        * `IncludePrivateData`
        * `IncludeOptOutData`

+ Request (application/json)

    + Headers
            
            galaxy-ap-name: Access Profile Name
            galaxy-ap-password: Access Profile Password
            galaxy-client-session-id: APIARY
            
    + Body

            {
                "SSN": "",
                "Last4SSN": "1234",
                "FirstName": "",
                "MiddleName": "",
                "LastName": "",
                "Dob":"",
                "Age": 0,
                "Address": {
                    "addressLine1":"",
                    "addressLine2":""
                },
                "PhoneNumber":"",
                "Email":""
            }

+ Response 200 (application/json)

    + Headers
          

    + Body

            {
                "verifiedPeople": [
                    {
                        "identityScore": 90,
                        "tahoeId": "G-12345678912345678978",
                        "firstName": {
                            "value": "firstname",
                            "matchTypeCode": "Match"
                        },
                        "middleName": {
                            "value": "middlename",
                            "matchTypeCode": "Match"
                        },
                        "lastName": {
                            "value": "lastname",
                            "matchTypeCode": "Match"
                        },
                         "ssn": {
                            "value": "123-45-6789",
                            "matchTypeCode": "Mismatch"
                        },
                        "dob": {
                            "month": {
                                "value": "month",
                                "matchTypeCode": "NA"
                            },
                            "day": {
                                "value": "day",
                                "matchTypeCode": "NA"
                            },
                            "year": {
                                "value": "year",
                                "matchTypeCode": "NA"
                            }
                        },
                        "age": {
                            "value": "age",
                            "matchTypeCode": "NA"
                        },
                        "addresses": [
                            {
                                "value": "address",
                                "matchTypeCode": "Match"
                            }
                        ],
                        "emails": [
                            {
                                "value": "email",
                                "matchTypeCode": "NA"
                            }
                        ],
                        "phones": [
                            {
                                "value": "phone",
                                "matchTypeCode": "NA"
                            }
                        ],
                        "dateofDeath": null,
                        "indicators": {}
                    }
                ],
                "fraudAlerts": [],
                "identityVerified": true
            }
