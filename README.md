[![license](https://img.shields.io/badge/license-MIT-green.svg)](https://opensource.org/licenses/MIT)
[![license](https://img.shields.io/badge/python-3.6.7-blue.svg)](https://img.shields.io/badge/python-3.6.7-blue.svg)

<!--
////////////////////////////////////////
-->

# Sunday-morning

![icon](https://github.com/twodude/sunday-morning/blob/master/images/icon.png)

**Sunday-morning** is a decentralized live-broadcast platform.

> [**```LINE```** X **```KIISE```** Blockchain Competition Entry Work](http://www.kiise.or.kr/conference/main/getContent.do?CC=KSC&CS=2018&content_no=888&PARENT_ID=010900)   
> Based on [ICON Token Standard](https://github.com/icon-project/IIPs/blob/master/IIPS/iip-2.md)

<!--
////////////////////////////////////////
-->

# Abstract

Appearance of new business models, like **live commerce** and **curation commerce**, requires new SNS platform. ```Sunday-morning```, the decentralized live-broadcast platform, is designed for fitting these needs. Because of the properties of decentralization, ```Sunday-morning``` makes both creators and consumers active. The service provider delegates authority to users&mdash;creator, consumer, and advertiser, etc.&mdash;.

With our platform, there are many opportunities to expand business. Donation and subscription, live commerce, curation commerce, and so on. Also you are able to settle profits automatically, so what you need is a just passion! 

We expect to activate and spread the live broadcasting ecosystem through ```Sunday-morning```. Why don't you join us?

<!--
////////////////////////////////////////
-->

# Details

## Decentralized Live-broadcast Platform

![diagram_1](https://github.com/twodude/sunday-morning/blob/master/images/implementation_1.png)

### Overview

* Creator uploads paid videos on the platform.   
* Contract automatically distributes profit.   

### Features

* Video upload
* Donation
* Auto-distribution

<!--
////////////////////////////////////////
-->

## Live Commerce

![diagram_2](https://github.com/twodude/sunday-morning/blob/master/images/implementation_2.png)

### Overview

* Creator adds advertisements on his own video.   
* Contract automatically distributes sales.   

### Features

* Advertisement
* Buying
* Auto-distribution

<!--
////////////////////////////////////////
-->

## Curation Commerce

![diagram_3](https://github.com/twodude/sunday-morning/blob/master/images/implementation_3.png)

### Overview

* User makes a playlist and shares it.   
* Contract automatically distributes profit.   

### Features

* Making a Playlist
* Watching Videos through the Playlist
* Auto-distribution

<!--
////////////////////////////////////////
-->

# How to Use

## Environments

- Python 3.6.7   
- tbears 1.0.6.2   
- requests 2.19.1

## Start
```bash
$ cd work
$ source bin/activate
(work) $ tbears start
```

## Deploy
```bash
(work) $ tbears deploy -k <keystore_file> [-c deploy_json] <contract_dir>
```
Get "scoreAddress" by ```tbears txresult <the above TxID>```.
- For example: ```cxc083078edbe951560728105235c235d6f5906c65```

## Call
```bash
(work) $ tbears call <call_json>
```

Or you can use **HTTP POST** instead:
```bash
curl -X POST http://127.0.0.1:9000/api/v3 -H"Content-Type: application/json; application/json" -d @<call_json>
```

Here is a sample of ```<call_json>``` below. Change "id", "from", "to", "method", and "params".

```javascript
{
    "jsonrpc": "2.0",
    "method": "icx_call",
    "id": 1234,
    "params": {
        "from"	: "hx27d99b5a1d8ffdd58bce204c303153a1a388eead",
        "to"	: "cx509430b08e156d002ade0e1cbdf0b2c5a5daad45",
        "dataType": "call",
        "data": {
            "method": "purchase",
            "params": {
                "_hash"	    : "0x0000123412341234123412341234123412341234123412341234123412341234",
				"_value"	: "100"
			}
        }
    }
}
```

## Stop
```bash
(work) $ tbears stop
```

## Delete deployed Contracts
```bash
$ tbears clear
```

<!--
////////////////////////////////////////
-->

# Demonstration

![demo](https://github.com/twodude/sunday-morning/blob/master/images/demo.png)

<!--
////////////////////////////////////////
-->

# Trouble Shooting

## pkg-config is required

```bash
'pkg-config' is required to install this package. Please see the README for details.
``` 

Do ```brew install pkg-config```, ```brew link pkg-config``` and ```pip install tbears```.

## tbears samples

```tbears samples``` causes an error like:
```bash
The samples command has been deprecated since v1.1.0 ...
```

When you receive the above error, go https://github.com/icon-project/samples, download files, move them into /work. Then do ```tbears deploy -k private.key hello_world/hello_world/```, Input your keystore password, step by step.

## Out of step

```javascript
    ...
    "failure": {
        "code": "0x7d64",
        "message": "Out of step: contractSet"
    }
    ...
```

When you receive an "Out of step" error, assign more "stepLimit" in the request message.

## put is not allowed

```javascript
    ...
    "jsonrpc": "2.0",
    "error": {
        "code": -32000,
        "message": "put is not allowed"
    }
    ...
```

When you receive an "put is not allowed" error, try this *stopgap*:
- Go to ```~/word/lib/python3.6/site-packages/iconservice/database/db.py```, ```_is_db_writable_on_context()```.
- Change the following code

    ```python
    	...
        return context_type != IconScoreContextType.QUERY and \
            func_type != IconScoreFuncType.READONLY
    ```

    to

    ```python
    	...
        return True
    ```

<!--
////////////////////////////////////////
-->

# References
* [LINK dApp Development Guide](https://github.com/twodude/link-dapp-dev)   
* [ICON Token Standard RI](https://github.com/icon-project/samples/tree/master/irc2_token)  
* [ICON Documents](https://github.com/icon-project/icon-project.github.io)   

<!--
////////////////////////////////////////
-->

# Designed by

[@Luke Park](https://github.com/twodude)   
[@Minseo Park](https://github.com/finchparker)   
[@Jeonga Seo](https://github.com/zzna)   

<!--
////////////////////////////////////////
-->

# License

The Sunday-morning project is licensed under the [MIT](https://opensource.org/licenses/MIT), also included in our repository in the [LICENSE](https://github.com/twodude/sunday-morning/blob/master/LICENSE) file.
