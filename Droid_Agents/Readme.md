1. Place the "Deep Research Agent.yaml" file in path like so: /home/zazikant/.factory/droids/deep-research-agent.yaml
2. cd to a folder if you want the agent to look for files having some base research or output already
3. Run bash command droid @deep-research-agent "Research figma mcp" it will do thorough research mimmicking the python code base that i gave a reference.

This yaml file is not a direct agent but the bash comamnd allows the agentic behaviour to follow  prompt to complete task.


Very important: whenever you wnat to get web data, do this search @deep-research-agent "Research on xxxxxxxx" understood?

so every prompt you write with "research" keyword. rsearch on what is the latest article on gemengserv.com it will run the yaml instructions.

Then, 

1. ask for show all urls you used to get this summary.
2. Then ask to use FetchUrl tool to make summary of all those urls.
