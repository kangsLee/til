#Slack에 Heroku를 통해 Hubot을 만들자

##설치
```
$ npm install -g yo generator-hubot
```

##기본설정
```
$ mkdir bot-name
$ cd bot-name
$ yo hubot

                     _____________________________  
                    /                             \ 
   //\              |      Extracting input for    |
  ////\    _____    |   self-replication process   |
 //////\  /_____\   \                             / 
 ======= |[^_/\_]|   /----------------------------  
  |   | _|___@@__|__                                
  +===+/  ///     \_\                               
   | |_\ /// HUBOT/\\                             
   |___/\//      /  \\                            
         \      /   +---+                            
          \____/    |   |                            
           | //|    +===+                            
            \//      |xx|   
            
Owner xxxx <xxx@xxx.xxx>
Bot name bot-name
Description A simple helpful robot for your Company
Bot adapter slack
```
- 엔터를 치면 자동으로 기본 정보가 입력된다.
- Slack에서 사용할 예정이므로 adapter에는 slack을 입력한다.
- adapter를 입력하지 못했다면 Procfile의 내용에 `web: bin/hubot -a slack`를 추가한다.

##사용해보기
```
./bin/hubot --name bot-name
.
.
.
bot-name> ping
bot-name> PONG
```
- bot이 실행되면 ping을 입력해서 PONG을 응답받아보자 !

##Slack 연동
https://xxxxx.slack.com/apps/search?q=hubot

- 슬랙에서 hubot을 추가하여 API Token값을 발급받고 저장한다.
- 발급 된 토큰을 터미널에 입력한다.

```
$ HUBOT_SLACK_TOKEN=토큰값 ./bin/hubot --adapter slack
```

##Heroku 연동
```
$ heroku login
$ heroku create
Creating app... done, ⬢ xxxxxxxxx
https://xxxxxxxxx.herokuapp.com/ | https://git.heroku.com/xxxxxxxxx.git
```

##Heroku 배포 및 설정
```
$ heroku config:add HUBOT_URL=http://xxxxxxxxx.herokuapp.com
$ heroku config:add HUBOT_SLACK_TOKEN=토큰값
$ git add .
$ git commit -m "Hubot"
$ git push heroku master
$ heroku ps:scale web=1
```

- 이제 Slack에서 bot에게 ping을 보내고 PONG을 받으면 성공