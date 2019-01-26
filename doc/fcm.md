### Go-fcm 

**Firebase Cloud Messaging (FCM)** Library using Golang (Go). This library uses HTTP/JSON Firebase Cloud Messaging connection server protocol. Its main features are: send messages to a topic, send messages to a device list, message can be a notification or data payload, supports condition attribute (fcm only), instance Id Features

**Firebase-server-sdk-go** – This is the Server SDK written in Golang for the newly announced Firebase suite of services. This SDK, like its Java and Node counterparts, supports the following functions needed on the application server: Authentication, Real-time Database, Cloud Messaging (FCM)


### Send to A topic

```golang
package main

import (
	"fmt"
    "github.com/NaySoftware/go-fcm"
)

const (
	 serverKey = "YOUR-KEY"
     topic = "/topics/someTopic"
)

func main() {

	data := map[string]string{
		"msg": "Hello World1",
		"sum": "Happy Day",
	}

	c := fcm.NewFcmClient(serverKey)
	c.NewFcmMsgTo(topic, data)


	status, err := c.Send()


	if err == nil {
    status.PrintResults()
	} else {
		fmt.Println(err)
	}

}
```


### Send to a list of Devices (tokens)

```golang
package main

import (
	"fmt"
    "github.com/NaySoftware/go-fcm"
)

const (
	 serverKey = "YOUR-KEY"
)

func main() {

	data := map[string]string{
		"msg": "Hello World1",
		"sum": "Happy Day",
	}

  ids := []string{
      "token1",
  }


  xds := []string{
      "token5",
      "token6",
      "token7",
  }

	c := fcm.NewFcmClient(serverKey)
    c.NewFcmRegIdsMsg(ids, data)
    c.AppendDevices(xds)

	status, err := c.Send()


	if err == nil {
    status.PrintResults()
	} else {
		fmt.Println(err)
	}

}
```


### Create Custom Tokens


Чтобы создать собственный токен, передайте уникальный идентификатор пользователя, 
используемый вашей системой аутентификации,
методу CreateCustomToken ():

```golang
auth, _ := firebase.GetAuth()
token, err := auth.CreateCustomToken(userId, nil)
```

Вы также можете при желании указать дополнительные претензии, которые будут включены в пользовательский токен. 
Эти утверждения будут доступны в объектах auth / request.auth в ваших Правилах безопасности. 
Например:

```golang
auth, _ := firebase.GetAuth()
developerClaims = make(firebase.Claims)
developerClaims["premium_account"] = true
token, err := auth.CreateCustomToken(userId, &amp;developerClaims)
```

### Verify ID Tokens

Чтобы проверить и декодировать ID-токен с помощью SDK, передайте ID-токен методу 
VerifyIDToken. 
Если идентификатор токена не истек и подписан должным образом, метод декодирует идентификатор токена.

```golang
auth, _ := firebase.GetAuth()
decodedToken, err := auth.VerifyIDToken(idTokenString)
if err == nil {
	uid, found := decodedToken.Uid()
}
```

## Links
[A Firebase token generator written in Go](https://github.com/zabawaba99/fireauth)  
[This a library for invoking the Firebase REST API.](https://github.com/cosn/firebase)   




















