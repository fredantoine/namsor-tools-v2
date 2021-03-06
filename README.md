# namsor-tools-v2
NamSor command line tools, to append gender, origin, diaspora or us 'race'/ethnicity to a CSV file.

## Installation

Please install https://github.com/namsor/namsor-java-sdk2 first, then use Maven to build the executable JAR file

```bash
mvn package
```
NB: we use Unix conventions for file paths, ex. samples/some_fnln.txt but on MS Windows that would be samples\some_fnln.txt

## Usage

```bash
java -jar target/NamSorToolsV2-1.0-SNAPSHOT.jar

usage: NamSorTools -apiKey <apiKey> [-countryIso2 <countryIso2>] [-e
       <encoding>] -f <inputDataFormat> [-h] [-header] -i <inputFile> [-o
       <outputFile>] [-r] -service <service> [-uid] [-w]
 -apiKey,--apiKey <apiKey>                  NamSor API Key
 -countryIso2,--countryIso2 <countryIso2>   countryIso2 default
 -e,--encoding <encoding>                   encoding : UTF-8 by default
 -f,--inputDataFormat <inputDataFormat>     input data format : first
                                            name, last name (fnln) / first
                                            name, last name, geo country
                                            iso2 (fnlngeo) / full name
                                            (name) / full name, geo
                                            country iso2 (namegeo)
 -h,--help                                  get help
 -header,--header                           output header
 -i,--inputFile <inputFile>                 input file name
 -o,--outputFile <outputFile>               output file name
 -r,--recover                               continue from a job (requires
                                            uid)
 -service,--endpoint <service>              service : parse / gender /
                                            origin / diaspora /
                                            usraceethnicity
 -uid,--uid                                 input data has an ID prefix
 -w,--overwrite                             overwrite existing output file
```

## Examples

To append gender to a list of first and last names : John|Smith

```bash
java -jar target/NamSorToolsV2-1.0-SNAPSHOT.jar -apiKey <yourAPIKey> -w -header -f fnln -i samples/some_fnln.txt -service gender
```

To append origin to a list of first and last names : John|Smith

```bash
java -jar target/NamSorToolsV2-1.0-SNAPSHOT.jar -apiKey <yourAPIKey> -w -header -f fnln -i samples/some_fnln.txt -service origin
```

To parse names into first and last name components (John Smith or Smith, John -> John|Smith)

```bash
java -jar target/NamSorToolsV2-1.0-SNAPSHOT.jar -apiKey <yourAPIKey> -w -header -f name -i samples/some_name.txt -service parse
```

The recommended input format is to specify a unique ID and a geographic context (if known) as a countryIso2 code. 

To append gender to a list of id, first and last names, geographic context : id12|John|Smith|US

```bash
java -jar target/NamSorToolsV2-1.0-SNAPSHOT.jar -apiKey <yourAPIKey> -w -header -uid -f fnlngeo -i samples/some_idfnlngeo.txt -service gender
```
To parse name into first and last name components, a geographic context is recommended (esp. for Latam names) : id12|John Smith|US

```bash
java -jar target/NamSorToolsV2-1.0-SNAPSHOT.jar -apiKey <yourAPIKey> -w -header -uid -f namegeo -i samples/some_idnamegeo.txt -service parse
```
On large input files with a unique ID, it is possible to recover from where the process crashed and append to the existint output file, for example :

```bash
java -jar target/NamSorToolsV2-1.0-SNAPSHOT.jar -apiKey <yourAPIKey> -r -header -uid -f fnlngeo -i samples/some_idfnlngeo.txt -service gender
```
## Understanding output
Please read and contribute to the WIKI
https://github.com/namsor/namsor-tools-v2/wiki/NamSor-Tools-V2

## Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

Please make sure to update tests as appropriate.

