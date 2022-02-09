## BiliBiliVideoToMusic
![counter](https://count.getloli.com/get/@sudoskys-github-BiliBiliVideoToMusic?theme=moebooru)

[![MIT License](https://img.shields.io/badge/LICENSE-MIT-ff69b4)](http://choosealicense.com/licenses/mit/)   ![u](https://img.shields.io/badge/USE-python-green)   [![s](https://img.shields.io/badge/Sponsor-Alipay-ff69b4)](https://azz.net/ly233)
![v](https://img.shields.io/badge/Version-220209-9cf)  

### [English](README.md)  | [中文](README-CN.md) 

## introduce

Bilibili video download and extract audio for wav and flac TG-RSS version video second-pass extraction and push.
This project allows you to synchronize the music of your favorite erchuang video to the specified TG group and also onedrive bussines, using RShub to provide data support.



## Features
🛠 MAIN can run on windows system, supports sticking music labels and optionally saving flv and wav files. (modify the file yourself...)

🚧 If you use action deployment, the function is only to extract flac. To configure this action, you need to add keys in the environment, one is token and the other is email. (Apply for github openapi token by yourself https://github.com/settings/tokens/new)

🎤 The sound quality should be the same as the video heard

## Notice
⚠ Execute up to 20 push tasks each time.

⚠ Do not push super long videos (>10min) to avoid risks

⚠ Liunx deploys RSS push see music.yml, the variables need to be configured manually.

## Start
### 1. Installation Requirements

 **Python 3.7 or higher**
````
python -m pip install --upgrade pip

pip install setuptools wheel twine bs4 requests tabulate mutagen pydub you_get moviepy pyTelegramBotAPI feedparser
````
- FFmpeg environment [ffmpeg](https://ffmpeg.org/download.html#get-packages).
(This repository Action uses https://github.com/marketplace/actions/setup-ffmpeg )
* Install necessary packages locally by running `pip install bs4 requests tabulate mutagen pydub you_get moviepy`
* Push service installation robot API library and RSS parsing library `pip install pyTelegramBotAPI feedparser`

### 2. Preparation

#### select file version
````
linuxdown_git.py --->RSS auto editon
mains.py --->win&linux edition
````
⚠ The ONEdrive synchronization function has been added since version 220209. If this function is not required for Rss deployment, please comment the parameters of lmain and the onedrive class in it.


#### RSS feed users
* source (linuxdown_git.py)
You need to build [Rsshub](https://docs.rsshub.app/) to get web sources, or use the services of public projects! See .

* Fork this repository and set secrets
Tips: If you use action deployment, it is recommended to only set extraction flac.
To configure this action, you need to add secrets to the environment, one is github token and the other is email. (Apply for [github openapi token](https://github.com/settings/tokens/new)

**Add Repository secrets**
````
>token
>objectID
>rssurl
>apptoken
>appid
>appkey
````
````
token = ***** # bot token, use tg@BotFather, google by yourself
objectID = ***** # channal id ,please use tg@getidsbot get this value!
rssurl = **** # rssurl, see https://docs.rsshub.app/

----
appid, appkey, and apptoken are synchronously used by Microsoft cloud disk. You need to obtain these quantities from Azure, and the token should be automatically generated by running test/tokensetup!
Comment out if this feature is not required!
````

**Add Environment secrets**
````
>token # github token, use https://github.com/settings/tokens/new
>email # your email address
````

⚠ Pay attention to distinguish between two tokens.

* run
Github action runs the process once a day at 6:20, and the repository owner plus stars will also trigger the process.

#### Standalone use
USE mains.py

Fill in data/userdata.yaml and run it.


## Implementation logic (linuxdown_git.py)

> For the specific code, see linuxdown_git.py (main.py is used in the windows environment)
Pull RSS-->Compare data + input data-->Calculate the updated data-->Incoming download extraction function-->Send file-->Delete file tree

RSSdata is an independent storage worker, associated with the main program by rssdata.yaml


![v](https://github.com/sudoskys/BiliBiliVideoToMusic/raw/main/docs/workflow.png)


````
mermaid
graph TB

A (pull RSS) ---Comparison input--> B[data]

B[data] --> C{Calculate updated entry?}

C{Calculate updated entry?} -- NEW --> D[Download Extract]

C{Compute updated entry?} -- NO new --> S

D[Download Extraction] --Push --> E[TG]
E -- delete data if successful --> B

E[TG] --> S[write report]
````

### Directory structure description
````
.
├── data
│ ├── public.cer //public key
│ ├── rssdata.yaml //automatically filled in
│ └── userdata.yaml // manually filled in
├── docs //documentation
│ └── workflow.png
├── err.txt //Local debugging error log
├── LICENSE //Protocol
├── LICENSE.txt
├── linuxdown_audio.py // rss test version, playlist download, because the api is limited
├── linuxdown_git.py // rss push version, github action run target
├── log.txt
├── main.py // Interactive download version available for both linux & win
├── mods
│
│ │
│ └── rsatool.py //rsa support
├── o365_token.txt //encrypted token, decrypted at runtime
├── README-CN.md
├── README.md
├── requirements.txt
├── targets.txt
└── test
    ├── err.txt
    ├── log.txt
    ├── tokensetup.py //token settings are automatically generated
    └── t_video.py

````

## TODO
- [x] Implement download function
- [x] Implement the function of fetching new entries
- [x] Implement push function
- [ ] Realize multi-source multi-target push


## contribute
🚧 See TODO for details

## Thanks

- [BV number to AV number](https://www.zhihu.com/question/381784377/answer/1099438784)|Youget Repair Algorithm Implementation|
- [O365](https://github.com/O365/python-o365) |Microsoft cloud disk synchronization implementation|
- [RSShub](https://docs.rsshub.app/) |Data Feed RSS|


## support
THIS link: https://azz.net/ly233
[![](https://static01.imgkr.com/temp/5808cb7e9e6340409bd07afc0e5ca723.png)](https://azz.net/ly233)

------------------------------

![a](https://tva1.sinaimg.cn/large/87c01ec7gy1fsnqqlbdzjj21kw0w07is.jpg)