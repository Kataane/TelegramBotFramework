Hey guys,

here we are. After some time and thoughts i give my Telegram Bot framework  to public.
It is based on C#.

It is module which is based on the original TelegramBotLibrary you will find in nuget.

It gives you features which will look/feel like WinForms or have a good way to create apps with actions and forms.

---

## How to start:

Within your empty App your need to put some initial lines including your APIKey to get things started. The "BotBase" Class will manage a lot of things for you, like system calls, action events and so on. "StartForm" is your first Formular which every user will get internally redirected to, like a start page, you could redirect from there later in code, so users won't recognize it. It needs to be a subclass of "FormBase" you will find in Namespace TelegramBotBase.Form.


```

//Prepare the System
BotBase<StartForm> bb = new BotBase<StartForm>("{YOUR API KEY}");

//Add Systemcommands if you like, you could catch them later
bb.SystemCalls.Add("/start");

//Start your Bot
bb.Start();

```

Every Form has some events which will get raised at specific times. On every form you are able to get notes about the "Remote Device" like ChatId and other stuff your carrying. From there you build up you apps:

```
public class StartForm : FormBase
{


        public override async Task PreLoad(MessageResult message)
        {

        }

        public override async Task Init(params object[] param)
        {
            
        }

        public override async Task Opened()
        {

        }

        public override async Task Closed()
        {

        }

        public override async Task Load(MessageResult message)
        {
            await this.Device.Send("Hello world!");
        }



        public override async Task Action(MessageResult message)
        {


        }


        public override async Task Render(MessageResult message)
        {

        }

}

```

For instance send a message after loading a specific form:

```
await this.Device.Send("Hello world!");
```

Or you want to goto a different form?
Go ahead, create it, initialize it and navigate to it:

```
var tf = new TestForm();

await tf.Init();

await this.NavigateTo(tf);
```

## Simple Message Handling

On every input the user is sending back to the bot Action event get raised. So here we could manage to send something back to him. For sure we could also manage different button inputs:

### Lets start with text messages



```
public class SimpleForm : FormBase
{


        public override async Task Load(MessageResult message)
        {
            await this.Device.Send("Hello world!");
        }



        public override async Task Action(MessageResult message)
        {
		//message.MessageText will work also, cause it is a string you could manage a lot different scenerios here

		var messageId = message.MessageId;

		switch (message.Command)
           	{
			case "hello":
			case "hi":

				//Send him a simple message
				await this.Device.Send("Hello you there !");
			break;

			case "maybe":

				//Send him a simple message and reply to the one of himself
				await this.Device.Send("Maybe what?", replyTo: messageId);

			break;
		
			case "bye":
			case "ciao":
		
				//Send him a simple message
				await this.Device.Send("Ok, take care !");
			break;
		}
        }


}

```





---

I will add more notes to it soon, so stay tuned.

Warm regards

Florian Dahn

