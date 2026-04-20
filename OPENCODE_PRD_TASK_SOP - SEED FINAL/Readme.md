
Very important - 

update keys in code for ai agent.py

NVIDIA_API_KEY      = ""
SERPER_API_KEY      = ""
BROWSERLESS_API_KEY = ""

1. The config for opencode in windows is at C:\Users\%USERPROFILE%\.config\opencode. in terminal, ask opencode to read all files in it.
2. To use this in windows, update the "seed-researcher" subagent to have path changed from "/home/zazikant/code for AI agent.py" to "C:\Users\Asus\.config\code for AI agent.py"   

3. To use temporal do this: Go to temporal.io and download temporal.exe from their website. Then place that temporal folder containing temporal.exe in C:\temporal location. Then, run cmd from windows -> cd "C:\temporal" -> temporal.exe server start-dev
This will enable you to use temporal UI. your app can in D drive , and temporal can be in C drive . No issues.


Do see https://github.com/zazikant/Adversarial-thinking-search-python-script as base source of this SEED research project
