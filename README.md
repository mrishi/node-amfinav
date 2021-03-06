node-amfinav
============

#### Fetches NAVs of Indian mutual funds published by AMFI and reformats data into JSON

DISCLAIMER/WARNING : Developer has nothing to do with [AMFI](http://www.amfiindia.com/ "Association of Mutual Funds in India") . If AMFI changes the way data is published or stops publishing the data, this code will not work as expected.

Data can be read as a JSON Array

Install

<pre>
npm install amfinav
</pre>

Usage
<pre>
amfi = require('amfi');
amfiNavs = new amfi(options);
</pre>

using with an event listener with refresh every 3600 seconds
<pre>
var amfiNavs = new amfi({refreshInterval : 3600});
amfiNavs.on('dataready', callback);
</pre>
using with a callback with refresh every 3600 seconds
<pre>
var amfiNavs = new amfi({callback: callback, refreshInterval : 3600});
</pre>
using with a callback and no refresh
<pre>
var amfiNavs = new amfi({callback: callback});
</pre>
using with a event listener and no refresh
<pre>
var amfiNavs = new amfi();
amfiNavs.on('dataready', listener);
</pre>

##### Options

- callback : function which handles NAV Data
- refreshInterval : Interval in seconds. Data is refreshed at this interval. 

##### Events

- dataready : Emitted after data is fetched and processed into JSON. 

##### Objects & properties
- amfi.status : String, 'Acquiring Data' or 'Data Ready'
- amfi.updateDate : Date, When last time data was updated
- amfi.data : Object, NAV Data 
<pre>
	{funds:[fund1, fund2...], fundManagers: [fundManager1, fundManager2..], 
	fundTypes: [fundType1, fundType2...], updateDate : Date}
</pre>
- fundManager : String, name of the fund manager
- fundType : String, fund type
- fund : Object
<pre>
{ 'Scheme Code': 'NNNNNNNN',
  'ISIN Div Payout/ ISIN Growth': 'Code1',
  'ISIN Div Reinvestment': 'Code2',
  'Scheme Name': 'Scheme XXXXXX',
  'Net Asset Value': '10.6113',
  'Repurchase Price': '10.5052',
  'Sale Price': '10.6113',
  'Date': '28-Mar-2013',
  'Type': 'Type1',
  'Manager': 'Manager1' }
</pre>
