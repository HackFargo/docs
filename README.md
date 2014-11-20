# HackFargo API Docs

## Notes
- All calls return a maximum of 10,000 records

## Basic API Usage
- Make requests to our API serving URL at `http://api.hackfagro.co/calls`


### Dispatch Data
HackFargo makes Dispatch Log data made available by the City of Fargo accessible via a simple HTTP call.


#### Structure
Criteria                    | Parameters                                     
---------------------------:|:----------
Last few days(15 by default)| `/calls`                                       
A data range                | `/calls?start=6-20-2013&end=6-21-2013`         
An incident Type            | `/calls/type/Party`                            
Date Range & Incident Type  | `/calls/type/Party?start=3-3-2014&end=3-4-2014`


Notes:
- The `date` attribute is returned in the [UNIX timestamp](http://www.epochconverter.com) format.
- Addresses are only accurate to block level . Example of returned address -
`314 Broadway becomes 300 Broadway.`

##### Example
Description:
Get noise related incidents filtered by the keyword `loud` for the date range
_2-30-2014_ to _3-30-2014_


Request URL:
    http://api.hackfargo.co/calls/type/loud/count?start=2-30-2014&end=3-30-2014

Response:
_Note that the following response is annotated with comments beginning
with `//` to indicate what those parts mean. Since the JSON format doesn't have
comments it should be considered as invalid._
```JSON
[
  {
    "DataSetID": "DispatchLogs",
    "Lat": 46.81618741541262,
    "Long": -96.88359341719978,
    "Date": 1394258006,                             // Unix timestamp
    "Description": "LOUD PEOPLE/MARIJUANA ODOR",    // Field to filter against. Supplied by you/user
    "Meta": {
      "id": 215986,
      "DateString": "3/7/2014 11:53:26 PM",
      "DateVal": 1394258006,
      "Address": "900 BLK 44 ST S",                 // Addresses are only accurate to block level
      "NatureOfCall": "LOUD PEOPLE/MARIJUANA ODOR",
      "CallType": "Loud Party/People",
      "IncidentNumber": "",
      "Duration": "",
      "AdditionalInfo": "",
      "CFSID": -5202747,
      "VenueName": "FGO",
      "VenueDescription": "Fargo",
      "Block": "900",                               // Addresses are only accurate to block level
      "StreetPrefix": "",
      "StreetPretype": "",
      "StreetName": "44",
      "StreetType": "ST",
      "StreetSuffix": "S",
      "Lat": 0,
      "Long": 0
    }
  },
  {
    "DataSetID": "DispatchLogs",
    "Lat": 46.830937295065304,
    "Long": -96.79115266298359,
    "Date": 1394164277,
    "Description": "LOUD TV",
    "Meta": {
      "id": 215829,
      "DateString": "3/6/2014 9:51:17 PM",
      "DateVal": 1394164277,
      "Address": "4200 BLK 9 AVENUE CIR S",
      "NatureOfCall": "LOUD TV",
      "CallType": "Loud Noise",
      "IncidentNumber": "2014-00013015",
      "Duration": "2326",
      "AdditionalInfo": "",
      "CFSID": -5202112,
      "VenueName": "FGO",
      "VenueDescription": "Fargo",
      "Block": "4200",
      "StreetPrefix": "",
      "StreetPretype": "",
      "StreetName": "9 AVENUE",
      "StreetType": "CIR",
      "StreetSuffix": "S",
      "Lat": 0,
      "Long": 0
    }
  }
]
```


#### Counts
If you just need the number of incidents, you may add `/count` towards the end
of your request path. You will receive the number of incidents instead of the
speceif incidents themselves. 

##### Example

Description:
Get count of noise related incidents filtered by the keyword `loud` for the date range
_6-20-12_ to _6-21-2013_

Request URL:
    http://api.hackfargo.co/calls/type/loud/count?start=6-20-2012&end=6-21-2013

Response:
```JSON
{
      "count": 1649
}
```

### Liability

The dispatch data provided via API by HackFargo is a service that repurposes
data made available for public usage by the City of Fargo who deserve all
credit for collection and assimilation of said data. The following is a
disclaimer to the usage of the same data to which you will agree to by using
HackFargo's services in any way, shape or manner - _The Fargo Police Department
allows access to its dispatch log online. The log is updated daily and is made
available in the public interest. The log does not represent all of the daily
activity of the department, nor does they always reflect what the officer found
at the scene of the call. These calls also do not reflect the self-initiated or
investigative activities of department officers._

