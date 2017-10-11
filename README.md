# how-to-flow
You want to setup the flow engine? This might tell you how to do it.

## Flow Deploy Service
- Converts from designer flow json to the nanocyte engine
- Designer format is easy for the UI to render
- Nanocyte format is easy for the engine to read and execute
- Converts nodes into "nanocytes" - simple components that can be executed in series or parallel that represent a node in the flow.
  - also obfuscates data
- Once the flow deploy service translates the json, it writes it to redis, where the engine reads it.
- It also saves the configuration to mongo in case the redis server gets restarted
- Finally, it sends a start command to the flow engine, which causes the engine to run the flow-start nodes, as well as other startup-related actions.

## Running Flows
This requires a few different services

#### nanocyte-engine-http
  Takes http messages, converts them into the internal nanocyte message format, and dumps them into a message queue in redis

#### nanocyte-engine-simple
- reads messages from a redis queue
-  executes nanocytes, feeding the input of one into the output of the other based on the flow in the nanocyte format
- has "engine-output" and "engine-input" nodes, which are the only parts of the flow engine that are specific to meshblu - just replace these nodes to point the flow engine at a different service!
