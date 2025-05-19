# SFDX Lens &nbsp; ![Visual Studio Marketplace Installs](https://img.shields.io/visual-studio-marketplace/i/PaoloCarrara.sfdxlens)

The quickest way to set up trace flags for a chosen active Salesforce user in any connected org.   
Or, to visualize Debug Logs.  
Or, to inspect Object Fields. 

Without leaving VSCode.
<br/>
<br/>

## Commands / Features

All features are accessible from the VS Code command palette using the shortcut `Ctrl+Shift+P` (Windows) or `Cmd+Shift+P` (Linux/MacOS) while in a SFDX Project

### Debug User

`SFDX Lens: Debug user` or `SFDX Lens: Debug user from Org`

Lets the current user to pick a name from a list of Salesforce active users in the current connected org, then creates a Trace Flag for that user.

In its variant, lets the current user to pick an Org name from a list of Connected Salesforce Orgs, then executes the same steps above on the chosen Org.

This feature is even available from the 🔎 button icon in VSCode's status bar on the left side.

Set up a trace flag and download the log:

![](https://github.com/pcarrara21/SFDXLens-Public/blob/main/gifs/sfdxlens.gif?raw=true)
<br/>
<br/>

### Log Analysis

`SFDX Lens: Log Analysis (Beta)`

When invoked on an Apex Log, it opens a new page tab showing the log's timeline, divided in each part proportional to its duration.
Every log section is clickable and upon clicking the corresponding code is displayed, up to the first 100000 characters for performance reasons.

You can search the code for a particular string through a fixed search bar displayed on the right side of the page.

Perform a log analysis:

![](https://github.com/pcarrara21/SFDXLens-Public/blob/main/gifs/sfdxlens_1.gif?raw=true)
<br/>
<br/>

### Object fields analysis

`SFDX Lens: Object fields analysis`

This command allows Objects field inspection to gain metrics about field usage and a suggestion about which field can potentially be safely deleted.

This functionality leverages both SOQL and tooling API to identify those fields and creates a graph using Chart.js to represent usage data.


![](https://github.com/pcarrara21/SFDXLens-Public/blob/main/gifs/sfdxlens_2.gif?raw=true)


The delicate part: ***what is being measured?***
1. Field references

2. How many record with those fields (not blank) were created in the past n months. Notice: created in the past n months. A record created 10 years ago and modified yesterday to set one of the inspected field won't be counted or show up in the charts.

e.g. 

Timeframe set to 12 months
Account created 3 years ago with customfield__c set and updated yesterday to the value 'ACME' -------> won't be counted despite having customfield__c set <br/><br/>
Account created 3 months ago with customfield__c set ----> will be counted<br/><br/>


### API Usage

Please be advised that this functionality uses API calls that counts towards your org limit. For each field inspected it uses 3 API calls so keep that in mind if you're short on those.<br/><br/>

### Settings

There are a few user settings you can play with (File > Preferences > Settings > Extensions > SFDX Lens):

**Number Of Apex Refences**<br/>
Maximum number of Apex code references to consider the field safe to delete. If blank, the check is skipped.

**Number Of Months**<br/>
Number of months to consider in the selected timeframe. If blank, the default value (12) is used.

**Number Of Records**<br/>
Maximum number of records with the field set to consider the field safe to delete. If blank, the check is skipped.

**Number Of Validation Refences**<br/>
Maximum number of Validation Rules references to consider the field safe to delete. If blank, the check is skipped.

## Requirements

- [Salesforce CLI](https://developer.salesforce.com/tools/sfdxcli) installed
- A Salesforce DX project
<br/>
<br/>

## Notes

- **Users** All active users are listed and can be traced

- **Scopes** Upon the first trace flags creation, this extension creates a *SFDX_Lens* Debug log level with all the scopes set to "Finest" to guarantee maximum logging debug level.

- **Trace Flags** Whenever a user is chosen, the extension checks if another trace flag is already created by extension and if so, it updates it to prevent trace flags littering

- **Log Colors** Log colors are chosen randomly

- **Log Labels** Generic Apex code (not linked to Validation Rules, Triggers, etc.) is labeled "Apex Code 1/2/3/etc."
<br/>
<br/>

## Release Notes

### 0.0.4

Initial release

### 0.0.5

Explicitly retargeted MAX_LIMIT_EXCEEDED error when setting up a trace flag in an org hitting the max debug log size limit

### 0.0.5

Explicitly retargeted MAX_LIMIT_EXCEEDED error when setting up a trace flag in an org hitting the max debug log size limit

### 1.0.0

Though in Beta, the SFDX Lens: Log Analysis command is released, giving the extension the  ability to set up and inspect logs

### 2.0.0

The SFDX Lens: Object fields analysis command is released, giving the extension the ability to gather and display field usage data

## Issues
You can report issues [here](https://github.com/pcarrara21/SFDXLens-Public/issues)
