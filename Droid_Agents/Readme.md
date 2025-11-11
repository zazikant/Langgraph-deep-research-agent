1. Place the "Deep Research Agent.yaml" file in path like so: /home/zazikant/.factory/droids/deep-research-agent.yaml
2. cd to a folder if you want the agent to look for files having some base research or output already
3. Run bash command droid @deep-research-agent "Research figma mcp" it will do thorough research mimmicking the python code base that i gave a reference.

This yaml file is not a direct agent but the bash comamnd allows the agentic behaviour to follow  prompt to complete task.

Very Important: 

have a base prompt like: please note that if you dont have pre knowledge of subject and instead of doing  a regular web serach, you will always run bash command like droid @deep-research-agent "Research on xxxxxxxx". are you ready?

For every search it will do:
EXECUTE  (droid @deep-research-agent "What is the latest article published on gemengserv.com?", impact: low)

