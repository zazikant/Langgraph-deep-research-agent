1. Place the "Deep Research Agent.yaml" file in path like so: /home/zazikant/.factory/droids/deep-research-agent.yaml
2. cd to a folder if you want the agent to look for files having some base research or output already
3. Run command **@.factory/droids/Deep Research Agent.yaml "Research on trending ai models from china "** it will do thorough research mimmicking the python code base that i gave a reference.

    PLAN   Updated: 5 total (4 pending, 1 in progress, 0 completed)

 ○ Research trending AI models from China using web search
 ○ Fetch and analyze primary sources from Chinese AI companies
 ○ Verify claims and cross-reference information across multiple sources
 ○ Synthesize findings into a comprehensive report with citations
 ○ Evaluate research quality and iterate if needed

This yaml file is not a direct agent but the bash comamnd allows the agentic behaviour to follow  prompt to complete task.


Very important: whenever you wnat to get web data, do this search **@.factory/droids/Deep Research Agent.yaml "Research on xxx "** understood?

so every prompt you write with "research" keyword. rsearch on what is the latest article on gemengserv.com it will run the yaml instructions.

Then, 

1. ask for show all urls you used to get this summary.
2. Then ask to use FetchUrl tool to make summary of all those urls.
3. use claude code to pass learning.md and reiterate to droid chat for final learning.md
