# HC-SensitiveDataTypes
Microsoft 365 Sensitive Information Types created for the Dutch HealthCare sector. These Sensitive Information Types can be used in for example: Office 365 DLP, Microsoft Cloud App Security and AIP Scanner

The following Sensitive Information Types are included:
*	Custom - Netherlands Citizen's Service (BSN) Number
*	Custom - Dutch Passport number
*	Custom - Netherlands ZIP Code + City
* Custom - Email addresses
*	Custom - general Sensitive Keywords
*	Custom - healthcare cure set 1
*	Custom - healthcare cure set 2
*	Custom - healthcare care set 1 - Zorgplan
*	Custom - healthcare care set 2 - DVO
*	Custom - healthcare care set 3 - WMO
*	Custom - healthcare care set 4 - Algemeen
*	Custom - healthcare care set 5 - Zorg
*	Custom - healthcare care set 6 - Administratie

## Why these Sensitive Information Types
Microsoft 365 includes 100 sensitive Information Types up to now. While this a great numnber, it does not include localized Sensitive Information Types for the Dutch martket, besides BSN. This set is build to extend on the build-in types and allow you to faster implement services like DLP without the need of building sensitive information types from scratch yourself.

## Getting Started

### Prerequisites

### Installing


#####variable#####

$locatie="directory where files are located"

####create keywords#####

$fileData2 = Get-Content $locatie\termen_healthcare.txt -Encoding Byte -ReadCount 0
New-DlpKeywordDictionary -Name "termen_healthcare_cure1" -Description "healthcare cure termen" -FileData $fileData2

$fileData = Get-Content $locatie\Keyword_netherlands_zipcode_cities.txt -Encoding Byte -ReadCount 0
New-DlpKeywordDictionary -Name Keyword_netherlands_zipcode_cities -Description "list of all dutch cities" -FileData $fileData

Get-DlpKeywordDictionary | select name,identity

####inlezen sensitive information sets#####

New-DlpSensitiveInformationTypeRulePackage -FileData (Get-Content -Path $locatie\HealthCare.xml -Encoding Byte)

###update rulepack######

Set-DlpSensitiveInformationTypeRulePackage -FileData ([Byte[]]$(Get-Content -Path $locatie\HealthCare.xml -Encoding Byte -ReadCount 0))

### Usage


## Find us
* [Wortell](https://wortell.nl/)
* [Wortell Security](https://security.wortell.nl/)
* [GitHub](https://github.com/wortell/)

## Contributing

work in progress

## Thanks
Microsoft

## Authors

* **Ronnie van Buuren** - *Initial work* - [LinkedIn](https://www.linkedin.com/in/ronnievanbuuren/) / [GitHub](https://https://github.com/ronnievanbuuren)

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details
