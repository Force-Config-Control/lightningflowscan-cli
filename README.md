Lightning Flow Scanner (sfdx plug-in)
=====================

![screenshot results(https://raw.githubusercontent.com/RubenHalman/Force-Flow-Control/master/docs/scanresults.png)](https://raw.githubusercontent.com/Force-Config-Control/lightning-flow-scanner-sfdx/master/.images/results.png)

## Installation:

NPM:
```sh-session
$ npm install -g lightning-flow-scanner
```

SFDX:
```sh-session
$ sfdx plugins:install lightning-flow-scanner
```

## Usage:

```
  $ sfdx flow:scan [-c <path>] [-d <directory>] [-e] [-p <path>][-u <targetusername>] [--json] [--loglevel <level>]
```

### Options
```
  -c, --config <path>                                               provide a path to the configuration file.

  -d, --directory <directory>                                       provide a directory to scan for flows.

  -e, --throwerrors                                                 set scan to throw an error if a violation is found.

  -p, --sourcepath <path>                                           provide a comma-separated list of source flow paths to scan.

  -u, --targetusername <username>                                   retrieve the latest metadata from the target before the scan.

  --json                                                            set output format as json.

  --loglevel=(trace|debug|info|warn|error|fatal)                    [default: warn] logging level.
```

## Configuration file:
Use a _.flowscanignore_ file to:

 - activeRules
 
 select a limited set of rules to run.
    
 - overrides
 
 specify results to ignore. Specify by ruleName and result(if applicable), like shown in the example.

#### Example .flowscanignore:
```
{
  "activeRules": [
    "DMLStatementInLoop",
    "DuplicateDMLOperationsByNavigation",
    "MissingFlowDescription",
    "HardcodedIds"
  ],
  "overrides": [
    {
      "flowName": "Create Property",
      "results": [
        {
          "ruleName": "DuplicateDMLOperationsByNavigation",
          "result": "error_creating_records"
        },
        {
          "ruleName": "DuplicateDMLOperationsByNavigation",
          "result": "upload_picture"
        }
      ]
    },
    {
      "flowName": "mainflow",
      "results": [
        {
          "ruleName": "MissingFlowDescription"
        }
      ]
    }
  ]
}
```

See code: [src/commands/flow/scan.ts](https://github.com/Force-Config-Control/lightning-flow-scanner-sfdx/blob/v0.0.18/src/commands/flow/scan.ts)
