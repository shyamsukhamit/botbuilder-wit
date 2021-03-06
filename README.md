# botbuilder-wit
Node.js module that provides [Wit.ai](https://wit.ai) NLP integration for the [Microsoft Bot Framework](https://dev.botframework.com/).

## Installation

`npm install --save botbuilder-wit`

## Usage
This package does **not** work with Wit.ai's *Story* feature. This is by design. That doesn't mean you can't use it entirely, just not in combination with the IntentDialog that uses the WitRecognizer.
```
const { IntentDialog } = require('botbuilder');
const WitRecognizer = require('botbuilder-wit');
const recognizer = new WitRecognizer('Wit.ai_access_token');
const intents = new IntentDialog({recognizers: [recognizer]});

intents.matches('intent.name', (session, args) => {...});
intents.onDefault(session => {...});

bot.dialog('/', intents)
```

## Using Entities

You can use the utility class [EntityRecognizer](https://docs.botframework.com/en-us/node/builder/chat-reference/classes/_botbuilder_d_.entityrecognizer.html) to parse & resolve common entities.
```
// Inside your dialog handler that receives the session and arguments object
const { EntityRecognizer } = require('botbuilder');
const location = EntityRecognizer.findEntity(args.entities, 'location')
```

## Using the Wit.ai client
You can still use the Wit.ai client directly by accessing the ```witClient``` property of the instantiated WitRecognizer.
```
const recognizer = new WitRecognizer('Wit.ai_access_token');
const witClient = recognizer.witClient;
```
## Recompiling the TypeScript source
If you want to recompile the source, you will need to make sure the ```node-wit``` dependency has a type definitions file in its root directory. At the moment, they're not yet available in the DefinitelyTyped repository. However, in the resources directory you'll find a minimalistic version that will do the job.

## License

MIT