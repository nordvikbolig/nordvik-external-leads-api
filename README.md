# Nordvik External Leads API
Documentation on how to send a lead to Nordvik, for external partners and internal use.

URL | https://www.nordvikbolig.no
-- | --
Endpoint | /api/tips
Method | POST
Header | Content-Type: application/json
Output | JSON


## Request information
Body parameters for external partners

Navn | Beskrivelse | Type | Informasjon
-- | -- | -- | --
type | Referanse til opprinnelsestype | [OriginType](https://hub.megler.vitec.net/Help/ResourceModel?modelName=OriginType) | required
firstName | Fornavn | string | required
lastName | Etternavn | string | required
email | E-post | string | required
mobilePhone | Mobilnummer | string | required
postalCode | 4-sifret norsk postnummer | string | required
streetAddress | Gateadresse | string |  
comment | Kommentar | string |  
source | Kilde som naked domain | string | required
sourceUrl | Nettadresse til source | string | required
newsletter | Sender email til Nordvik nyhetsbrev | Boolean |  
externalReference | Ekstern referanse hos partner | string | max length: 63


## Other body parameters

Navn | Beskrivelse | Type | Informasjon
-- | -- | -- | --
departmentSlug | Et kontors slug fra nordvikbolig.no/kontorer/{slug} for å sende lead direkte til kontor. Kan brukes istedenfor departmentPostalCode. Kan ikke angis sammen med referanse til megler. | string |  
departmentPostalCode | Et kontors unike postnummer for å sende lead direkte til kontor. Kan brukes istedenfor deparmentSlug. Kan ikke angis sammen med referanse til megler. | string |  
employeeEmail | E-post for å sende lead direkte til megler. Kan ikke angis sammen med referanse til kontor. | string |  
employee | E-post eller employeeId fra Next for å sende lead direkte til megler. Kan brukes istedenfor employeeEmail. Kan ikke angis sammen med referanse til kontor. | string |  
estateId | Referanse til oppdrag i Next | string |  
streetAdress | Utgått. Erstattet av streetAddress med to D’er | string |  
debug | Sender respons data, men lagrer ikke i Next | Boolean |


## Examples
**Recommended body parameters example for external partners**

```
{
	"type": "2",
	"firstName": "Ola",
	"lastName": "Nordmann",
	"email": "ola@nordmann.no",
	"mobilePhone": "99999999",
	"postalCode": "9999",
	"streetAddress": "Nordmannsveien 9",
	"comment": "",
	"source": "tjenestetorget.no",
	"sourceUrl": "https://tjenestetorget.no/eiendom",
	"externalReference": "XXXXXXXXX"
}
```

**Direct lead to [employee](https://www.nordvikbolig.no/megler/thomas-granmo-kiligitto) example**
```
{
	"type": "2",
	"firstName": "Ola",
	"lastName": "Nordmann",
	"mobilePhone": "99999999",
	"postalCode": "9999",
	"source": "tjenestetorget.no",
	"sourceUrl": "https://tjenestetorget.no/eiendom",
	"employeeEmail": "t.kiligitto@nordvikbolig.no"
}
```

**Direct lead to [department](https://www.nordvikbolig.no/kontorer/frogner) example**
```
{
	"type": "2",
	"firstName": "Ola",
	"lastName": "Nordmann",
	"mobilePhone": "99999999",
	"postalCode": "9999",
	"source": "tjenestetorget.no",
	"sourceUrl": "https://tjenestetorget.no/eiendom",
	"departmentSlug": "frogner"
}
```


## Response information
### Success response
HTTP status code: 200

Navn | Beskrivelse | Type | Informasjon
-- | -- | -- | --
success | Alltid true | Boolean | required
postalCodeForVitec | Postnummer som ble sendt til Next | string | required
tipId | Referanse til ID for lead opprettet i Next | string | required

**Example**
```
{
	"success": true,
	"postalCodeForVitec": "XXXX",
	"tipId": "XXXXXXXXXXXX"
}
```


### Error response
HTTP status code: 500

Navn | Beskrivelse | Type | Informasjon
-- | -- | -- | --
error | Feilmelding | string | required


**Example**
```
{
	"error": "Error message"
}
```
