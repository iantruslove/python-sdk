# Koodous Python SDK
This is the Python SDK developed by our team to use Koodous easily.

# SHA-256

Koodous works with many different hashing functions, but we prefer sha256 to 
manage all samples in the better way.

# Installation

Latest published release from PyPi:
```
$ pip install koodous-py
```

Development snapshot from Github:
```bash
$ pip install 'git+https://github.com/Koodous/python-sdk.git#egg=koodous_py'
```

# Library Usage

The only thing that you need is your API token that you can obtain after 
registering to [koodous.com](https://koodous.com) for free!

Go to your [profile](https://koodous.com/settings/profile) and there it is.

## Upload a file

```python
import koodous
koodous_obj = koodous.Koodous(token)
koodous_obj.upload(filepath)
```

## Search for APKs
```python
apks = obj.search('whatsapp and package_name:"com.whatsapp" and size:2MB+ and rating:2+')
```

This returns contains a list object with the details of the found APKs.
```
[   
    ...,
    {
        "size": 16674795,
        "rating": 2,
        "sha1": "8b0b907fb72d6284d22ccacb40df1b497a361ad1",
        "corrupted": false,
        "package_name": "com.whatsapp",
        "tags": [
            "googleplay"
        ],
        "image": "https://koodous.com/media/apk_images/tmpRdiC7v",
        "detected": false,
        "repo": "googleplay",
        "created_on": 1426302935,
        "stored": true,
        "displayed_version": "2.12.5",
        "analyzed": true,
        "sha256": "f149b135f86ce2dbaa6a0efb332fb0309d39dd692100172b4aff3f95ce5c43b4",
        "company": "WhatsApp Inc.",
        "app": "WhatsApp",
        "trusted": false,
        "md5": "3b7991ee09db22db6de8e1d5d58e2885"
    },
    ...
]
```

## Download an analysis
```python
analysis = koodous_obj.get_analysis(sha256)
```

If analysis raise an Exception this means that the analysis is not ready. You
 can require an analysis, wait 2 minutes approximately and request it again.

If something strange happends, this call returns ```None```.
 
```python
koodous_obj.analyze(apk) #Wait 2 minutes and retry get_analysis(sha256)
```

And then you can access to analysis information (JSON format):

```python
print analysis
{
    "androguard": {
        "app_name": "图表",
        "package_name": "dfkldsfdgjhdfg.fdgjndfkgirg.fghsdiuogh",
        "providers": [],
        "new_permissions": [],
        "filters": [
            "android.app.action.DEVICE_ADMIN_ENABLED",
            "android.intent.action.MAIN",
            "android.provider.Telephony.SMS_RECEIVED"
        ],
        "max_sdk_version": null,
        "certificate": {
            "sha1": "7750A347F871CF2C9753A6958E87ABE2358AA9B0",
            "not_after": "Feb 23 07:41:48 2045 GMT",
            "issuerDN": "/C=US/O=Android/CN=Android Debug",
            "subjectDN": "/C=US/O=Android/CN=Android Debug",
            "serial": "54F565BC",
            "not_before": "Mar 3 07:41:48 2015 GMT"
        },
        "min_sdk_version": "8",
        "version_code": "2",
        "libraries": [],
        "target_sdk_version": "20",
        "cordova": null,
        "activities": [
            "dfkldsfdgjhdfg.fdgjndfkgirg.fghsdiuogh.MainActivity"
        ],
        "main_activity": "dfkldsfdgjhdfg.fdgjndfkgirg.fghsdiuogh.MainActivity",
        "receivers": [
            "dfkldsfdgjhdfg.fdgjndfkgirg.fghsdiuogh.DevicesReceiver2",
            "dfkldsfdgjhdfg.fdgjndfkgirg.fghsdiuogh.laixinxis"
        ],
        "signature_name": "META-INF/CERT.RSA",
        "dexes": {
            "classes": {
                "ssdeep": "384:lrmS/xLyL7zIQ9CIBLlCRWAodycJ2NWhWYORsynlvGO61EP4T:lSwxLInI3IBLntnhPOR2O6Y4T",
                "sha256": "17e213420ee4d5c78fb9fcd0e0af668922aaf7ff0c98d0ace3c21e58f19be8dd"
            }
        },
        "displayed_version": "2.0",
        "services": [
            "dfkldsfdgjhdfg.fdgjndfkgirg.fghsdiuogh.MyServers1"
        ],
        "permissions": [
            "android.permission.SEND_SMS",
            "android.permission.KILL_BACKGROUND_PROCESSES",
            "android.permission.WRITE_SMS",
            ...
        ],
        "functionalities": {
            "dynamicbroadcastreceiver": [
                {
                    "code": "invoke-virtual v7, v1, v0, v2, v6, Ldfkldsfdgjhdfg/fdgjndfkgirg/fghsdiuogh/MyServers1;->registerReceiver(Landroid/content/BroadcastReceiver; Landroid/content/IntentFilter; Ljava/lang/String; Landroid/os/Handler;)Landroid/content/Intent;",
                    "class": "Ldfkldsfdgjhdfg/fdgjndfkgirg/fghsdiuogh/MyServers1;",
                    "method": "onCreate"
                },
                {
                    "code": "invoke-virtual v3, v1, Ldfkldsfdgjhdfg/fdgjndfkgirg/fghsdiuogh/MyServers1;->unregisterReceiver(Landroid/content/BroadcastReceiver;)V",
                    "class": "Ldfkldsfdgjhdfg/fdgjndfkgirg/fghsdiuogh/MyServers1;",
                    "method": "onDestroy"
                }
            ]
        },
        "urls": [
            "http://60.8.229.158:8002/sj.asp"
        ]
    },
    "cuckoo": {
        "network": {
            "http": [],
            "smtp": [],
            "hosts": [],
            "dns": [],
            "domains": [],
            "irc": []
        },
        "target": {
            "category": "file",
            "file": {
                "size": 54477,
                "sha1": "4bac63842c26957190ae1722647c1f0fc6828f1d",
                "crc32": "4339AE28",
                "ssdeep": "768:XyDIt03WP8fPyKC4rCHkHu7rnQJ1KRPJEOdLt74Hz9DncM5WYxwiGM4ywEHfXl+5:ENzPKkO7rIKRPJFdxcBp5X8rEvMjy0r",
                "sha256": "88ddda0977d8af07d5b04979736e713a950767f7270658ead6781e6464631f8a",
                "sha512": "f6761c060b4bd80a9dd456f498a48d0dbd20056e33936fbb05e789cbea6f250c3debeafe2e1923df884b90aa793a5842814c7c30ea79f48666c4618f536a7db5",
                "md5": "4be0093ac136b39ec33021f7b55452a9"
            }
        }
    },
    "droidbox": {
        "fileswritten": [],
        "dns": [],
        "cryptousage": [],
        "filesread": [
            {
                "name": "/data/app/dfkldsfdgjhdfg.fdgjndfkgirg.fghsdiuogh-1.apk",
                "pid": 846,
                "processname": "dfkldsfdgjhdfg.fdgjndfkgirg.fghsdiuogh",
                "time": 1.813291,
                "tid": 1073870640,
                "data": "504b0506000000000b..."
            }
        ],
        "sendsms": [],
        "servicestart": [
            {
                "tid": 1073870640,
                "processname": "dfkldsfdgjhdfg.fdgjndfkgirg.fghsdiuogh",
                "pid": 846,
                "name": "dfkldsfdgjhdfg.fdgjndfkgirg.fghsdiuogh.MyServers1",
                "time": 3.314782
            }
        ],
        "sendnet": [],
        "libraries": [],
        "phonecalls": [],
        "recvnet": [],
        "dexclass": [
            {
                "tid": 1073870640,
                "processname": "dfkldsfdgjhdfg.fdgjndfkgirg.fghsdiuogh",
                "time": 1.752926,
                "pid": 846,
                "path": "/data/app/dfkldsfdgjhdfg.fdgjndfkgirg.fghsdiuogh-1.apk"
            },
            ...
        ]
    }
}
```

## Downloading a sample
You can use two methods, first download to a file directly:

```python
koodous_obj.download_to_file(sha256, "/home/name/filename")
```

Or you can obtain the download URL to use as you want:

```python
url = koodous_obj.get_download_url(sha256)
print url
```

## Analyze a sample
```python
koodous_obj.analyze(sha256) 
#Wait 2 minutes and try:
analysis = koodous_obj.get_analysis(sha256)
```
# Rulesets
## Get matches
It must be used as iterator in python, for example:
```python
for val in koodous_obj.get_ruleset_matches(1337):
    print val
```

**val** will be a python dictionary with the following format:

```json
{
    "count": 3,
    "results": [{
        "created_on": 1498041142,
        "rating": 0,
        "image": "https://cdn1.koodous.com/apk_images/2017/06/21/75d1a1e52070ff02e46dd9580c6ad96364a26d2714e802f8786bf285e390098a",
        "tags": [],
        "md5": "81b3f1c54330e3ca727b270f2a454354",
        "sha1": "d5d9f14f00c96b48acb8ac57960c6ca557cf5433",
        "sha256": "304202910418375c030472c31c8f588f9f6f6269a869d24e592b521d584031c4",
        "app": "搜狗浏览器",
        "package_name": "sogou.mobile.explorer",
        "company": "Sogou-inc",
        "displayed_version": "5.7.0",
        "size": 11659573,
        "stored": true,
        "analyzed": true,
        "is_apk": true,
        "trusted": false,
        "detected": false,
        "corrupted": false,
        "repo": "",
        "on_devices": false
    },
    {...},
    {...}
    ]
}
```

# Comments
## Posting a comment
```python
text_posted = koodous_obj.post_comment(sha256, comment_text)
```

## See APK comments

```python
>>> koodous_obj.get_comments(sha256)
[{
    'author': {
        'username': 'OpenAntivirus', 'total_public_rulesets': 1, 'first_name': '', 'last_name': '', 'total_comments': 669323, 'bio': None, 'following': [], 'twitter_user': None, 'is_superuser': True, 'avatar_url': 'https://cdn1.koodous.com/avatars/f743de5a3e28c8e0a513b73845dff589c7a3fab03eee46ed933a8ea8c7800540', 'last_login': 1440422421, 'total_following': 0, 'latest_24h_social_detections': 5, 'total_social_detections': 589, 'total_followers': 22, 'occupation': None, 'total_votes': 686908, 'date_joined': 1431507752
    }, 'text': '#sms-fraud  This application sends SMS messages that costs you money', 'apk': 'b499cb515e5b6086c7b993c529e602b190b4a031534ec887d8dcaf7ec4d6a489', 'created_on': 1452908630, 'ruleset': None, 'modified_on': 1452908630, 'id': 637165
}]
```

## Delete a comment
```python
koodous_obj.delete_comment(comment_id)
```
#Votes
## Vote a sample positive (goodware)
```python
>>> koodous_obj.vote_apk(sha256, koodous.POSITIVE)
{'kind': 'positive'}
```

## Vote a sample negative (malware)
```python
>>> koodous_obj.vote_apk(sha256, koodous.NEGATIVE)
{'kind': 'negative'}
```

## Get votes for an APK
```python
>>> koodous_obj.votes(sha256)
{
    'count': 3,
    'previous': None,
    'results': [{
        'kind': 'negative',
        'analyst': 'Incentoll'
    }, {
        'kind': 'negative',
        'analyst': 'OpenAntivirus'
    }, {
        'kind': 'negative',
        'analyst': 'Forits'
    }],
    'next': None
}
```

# Command Line Interface (CLI)
The SDK comes with a basic CLI that gets installed automatically and linked
as an executable script by setuptools.

```bash
Usage: koocli [OPTIONS] COMMAND [ARGS]...

  A simple command line interface (CLI) to the Koodous API.

  In order to use this CLI, you need an account at koodous.com and you need
  to grab your API token at https://koodous.com/settings/profile

  You can pass the API token both as a command line option, or set it as an
  environment variable (TOKEN).

  To get help for each individual command, just type

  $ koocli <command_name> --help

Options:
  --quiet / --no-quiet            Suppress output (logging is configured
                                  separately)
  --wdir PATH                     Working directory  [required]
  --loglevel [info|warning|critical|error|debug|notset]
  --token TEXT                    Koodous API token  [required]
  --help                          Show this message and exit.

Commands:
  get_matches_public_ruleset  Get the APKs that match a public ruleset by...
  get_public_ruleset          Get a public ruleset by its RULESET_ID
```

## Get a public ruleset metadata and download the first three matches
```bash
$ TOKEN='<your API token>' koocli --wdir /tmp/ \
    get_matches_public_ruleset  --download --save --limit 3 666
    
2015-12-08 13:29:42 yummy-ng.local koocli[19989] INFO Attempting to fetch ruleset 666
2015-12-08 13:29:42 yummy-ng.local requests.packages.urllib3.connectionpool[19989] INFO Starting new HTTPS connection (1): koodous.com
2015-12-08 13:29:43 yummy-ng.local koocli[19989] INFO Saving ruleset to /tmp/ruleset-666.json
2015-12-08 13:29:43 yummy-ng.local koocli[19989] INFO Ruleset saved successfully
2015-12-08 13:29:43 yummy-ng.local requests.packages.urllib3.connectionpool[19989] INFO Starting new HTTPS connection (1): koodous.com
{
    "analyzed": true, 
    "app": "Lucky Patcher", 
    "company": "pitorroman", 
    "corrupted": false, 
    "created_on": 1448478971, 
    "detected": true, 
    "displayed_version": "4.0", 
    "image": "https://cdn1.koodous.com/apk_images/647cb4313025b161a15e36c3270889a4bb556639f5d7aed8e2193f6904915bc7", 
    "is_apk": true, 
    "md5": "036d66d86911ed1bfb75c19f55a4b435", 
    "on_devices": false, 
    "package_name": "com.forpda.lp", 
    "rating": 0, 
    "repo": "", 
    "sha1": "e16af16b743bfb4ac3fc54b6f90f7995805b58a0", 
    "sha256": "01739acdf16999cabf147e679419c9dd7d910663d51e9e9ad9be95526f5cc770", 
    "size": 789528, 
    "stored": true, 
    "tags": [], 
    "trusted": false
}

2015-12-08 13:29:44 yummy-ng.local koocli[19989] INFO Saving metadata of 01739acdf16999cabf147e679419c9dd7d910663d51e9e9ad9be95526f5cc770 to /tmp/01739acdf16999cabf147e679419c9dd7d910663d51e9e9ad9be95526f5cc770.json
2015-12-08 13:29:44 yummy-ng.local koocli[19989] INFO Downloading 01739acdf16999cabf147e679419c9dd7d910663d51e9e9ad9be95526f5cc770 to /tmp/01739acdf16999cabf147e679419c9dd7d910663d51e9e9ad9be95526f5cc770.apk
2015-12-08 13:29:44 yummy-ng.local requests.packages.urllib3.connectionpool[19989] INFO Starting new HTTPS connection (1): koodous.com
2015-12-08 13:29:45 yummy-ng.local requests.packages.urllib3.connectionpool[19989] INFO Starting new HTTPS connection (1): lmcn4.koodous.com
2015-12-08 13:29:47 yummy-ng.local koocli[19989] INFO APK downloaded successfully
{
    "analyzed": true, 
    "app": "Lucky Patcher", 
    "company": "tengyhman", 
    "corrupted": false, 
    "created_on": 1448468963, 
    "detected": true, 
    "displayed_version": "2.7", 
    "image": "https://cdn1.koodous.com/apk_images/647cb4313025b161a15e36c3270889a4bb556639f5d7aed8e2193f6904915bc7", 
    "is_apk": true, 
    "md5": "ec92e27ba0dcaed9150bb711e13bc817", 
    "on_devices": false, 
    "package_name": "com.wLuckyPatcherFree", 
    "rating": 0, 
    "repo": "", 
    "sha1": "e1d8a51197afd5b0149504be17ccc0a29328da87", 
    "sha256": "04d0dffc667e0f68a619deaf580eaa63227c7dd7ba1d63f47a6b616d9a275970", 
    "size": 789362, 
    "stored": true, 
    "tags": [], 
    "trusted": false
}

2015-12-08 13:29:47 yummy-ng.local koocli[19989] INFO Saving metadata of 04d0dffc667e0f68a619deaf580eaa63227c7dd7ba1d63f47a6b616d9a275970 to /tmp/04d0dffc667e0f68a619deaf580eaa63227c7dd7ba1d63f47a6b616d9a275970.json
2015-12-08 13:29:47 yummy-ng.local koocli[19989] INFO Downloading 04d0dffc667e0f68a619deaf580eaa63227c7dd7ba1d63f47a6b616d9a275970 to /tmp/04d0dffc667e0f68a619deaf580eaa63227c7dd7ba1d63f47a6b616d9a275970.apk
2015-12-08 13:29:47 yummy-ng.local requests.packages.urllib3.connectionpool[19989] INFO Starting new HTTPS connection (1): koodous.com
2015-12-08 13:29:48 yummy-ng.local requests.packages.urllib3.connectionpool[19989] INFO Starting new HTTPS connection (1): lmcn4.koodous.com
2015-12-08 13:29:49 yummy-ng.local koocli[19989] INFO APK downloaded successfully
{
    "analyzed": true, 
    "app": "Puffin Web Browser", 
    "company": "tegyhmans", 
    "corrupted": false, 
    "created_on": 1448466542, 
    "detected": true, 
    "displayed_version": "3.8.1.0", 
    "image": "https://cdn1.koodous.com/apk_images/ca1310bc1ae8dc8795588bf894b9c01c43f00d4ff7b48f6ad7cc5130f33e573e", 
    "is_apk": true, 
    "md5": "82c6684ba4478d99111dd7f5e4edc6b9", 
    "on_devices": false, 
    "package_name": "com.cloudmosa.puffin", 
    "rating": 0, 
    "repo": "", 
    "sha1": "e22a7ed086b9008d86aa5801868b096af30bd087", 
    "sha256": "4b004d99816a6c777319e9abfb1c4c9b259da68cd8de65558e2596ba18ed9e86", 
    "size": 761235, 
    "stored": true, 
    "tags": [], 
    "trusted": false
}

2015-12-08 13:29:49 yummy-ng.local koocli[19989] INFO Saving metadata of 4b004d99816a6c777319e9abfb1c4c9b259da68cd8de65558e2596ba18ed9e86 to /tmp/4b004d99816a6c777319e9abfb1c4c9b259da68cd8de65558e2596ba18ed9e86.json
2015-12-08 13:29:49 yummy-ng.local koocli[19989] INFO Downloading 4b004d99816a6c777319e9abfb1c4c9b259da68cd8de65558e2596ba18ed9e86 to /tmp/4b004d99816a6c777319e9abfb1c4c9b259da68cd8de65558e2596ba18ed9e86.apk
2015-12-08 13:29:49 yummy-ng.local requests.packages.urllib3.connectionpool[19989] INFO Starting new HTTPS connection (1): koodous.com
2015-12-08 13:29:50 yummy-ng.local requests.packages.urllib3.connectionpool[19989] INFO Starting new HTTPS connection (1): lmcn4.koodous.com
2015-12-08 13:29:52 yummy-ng.local koocli[19989] INFO APK downloaded successfully
2015-12-08 13:29:52 yummy-ng.local koocli[19989] INFO Limit of 3 matches reached: stopping!
```
In this case 666 is the public ruleset identifier that you can get from the
URL (e.g., `https://koodous.com/rulesets/666`)

You can play with the options to suppress logging, verbosity and avoid saving
the metadata, if you're not interested in. Just saying.

# Utils
We implemented some tools to interact with APKs and not related explicitly with
 Koodous:
 
## SHA256 file
```python
>>> import koodous
>>> koodous.utils.sha256('/home/user/file.apk')
'133ee989293f92736301280c6f14c89d521200c17dcdcecca30cd20705332d44'
```

## Unpack file
Unpack an APK and generate one file with all content uncompressed.
```python
>>> import koodous
>>> koodous.utils.unpack('sample_test.apk', 'destination_file')
```
