# Dev Log

---

## 2026-05-11

**19:28** — I was toying around with ideas to help me learn cybersecurity concepts. Thought to create an SOC dashboard that monitors system logs, regardless of the type, and uses a classical ML approach for anomaly detection. When an anomaly is detected, Claude is invoked to give threat assessments and classify the alert as nothing of concern, a MITRE ATT&CK tactic, a threat category, and severity level. I realized that a lot of actual attack logs are either proprietary or counterproductive to use, so I had the idea to also have Claude generate my logs.

**19:39** — Because this is for the sake of my learning, and because eventually I may have to explain exactly how this works, this is going to be made by hand, save for UI elements.

**19:44** — Going to start with the log parsing code. This will be the heart of the project. I want my program to be able to parse logs from Windows, Linux, and whatever else, so I need to go study some damn logs.

---

## 2026-05-15

**17:48** — Haven't had a ton of time to work on things, but I had enough downtime at work today to write my attack log synthesizer and a real time streamer to play them with. Claude seems to be able to generate pretty accurate logs, even on Haiku. Added different params for operating systems (just Linux and Windows right now), different modes of attack, and duration. Pretty solid foundation for some anomaly detection engineering.

**18:00** — Trying to figure out how GitHub works so I can get my first commit on there lol.

**18:05** — Think I figured it out. Got the generator and the streamer up, probably going to add these logs too for posterity.

**18:43** — Someone dear to me made a very good point: anomalous activity is only anomalous compared against a baseline of unremarkability. So for every malicious log, I should also be generating inconsequential ones. To take it one step further, every log should have an accompanying network group. Going to see if I can bang that out before it gets too late. It's been a long ass week.

---

## 2026-05-17

**14:23** — Finished the network companion for the generator. Looking pretty nice. Using the Linux or Windows profiles now generates a complete network companion log. Two logs, one incident. Also added profiles to generate boring, unremarkable logs with authorized logins and normal lateral movement. A normal workday basically. Committing now.

**14:30** — Realized I hard coded the date I started in the prompts, so all logs are from May 14th lol. Fixing that now.

**14:49** — Now that that's done, the last thing I want to add before starting on the XGBoost classifier is a randomized or editable environment profile to accompany each log. With each log generated there will also come a complete network profile with a name, devices, and authorization schema.

**15:07** — Logs of the same OS and type were overwriting each other in the saved logs folder. Quick fix, added a timestamp system to distinguish them.

---

## 2026-05-18

**15:14** — Left work early today to job search like my life depends on it, and finish up the environment template for the generator. Now when you generate logs, you can generate a fictional corporate environment with subnets, devices, a name, and all. Can be generated randomly or with a parameter like "law office, 4 employees." Coming along very nicely. Committing now.