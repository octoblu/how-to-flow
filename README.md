# how-to-flow
You want to setup the flow engine? This might tell you how to do it.
* Flow Deploy Service
  - Converts from designer flow json to the nanocyte engine
  - Designer format is easy for the UI to render
  - Nanocyte format is easy for the engine to read and execute
    - also obfuscates data
  - Once the flow deploy service translates the json, it writes it to redis, where the engine reads it.
  - It also saves the configuration to mongo in case the redis server gets restarted
  - Finally, it sends a start command to the flow engine, which causes the engine to run the flow-start nodes, as well as other startup-related actions.
* 
