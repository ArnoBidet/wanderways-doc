# Project

This section is divided into 3 parts :

- Roadmap : 
    - Divided itself in parts, for each version
- Functional perimeter for V1
- The team

But first, let's explore the project organization

## Project cycle management

We opted for an agile like approach to manage our project.

This is due to the very nature of the project, whose goal is not to generate profits, does not have time boundaries, and whose only costs are human time and infrastucture cost. Thus, allowing us to be able to focus on quality.

But, we don't want this project to take years (which somehow it already took before the last months, due to the fact I was alone working on it) and fail miserably as do many projects.

Agile provides us an higher members implication due to it's forced regular meetings and ease to introduce change.

### Comitology (reunions planning)

1. The two main actors on the projet, Arthur and I, met every saturday morning to review the current/past sprint.

2. Once every two weeks, we met with graphic designer, Chloé, to guide her in her design decision by giving her hindsights upon our functionnal needs.

### Tools

![Jira icon](/assets/jira_logo.png){ align=right style=max-width:5rem }

To organize our work, we used Jira.<br>It was not always the case, and at first, we used the "Kanban" part of figma to try to organize ourselves. But due to obvious limitation, we switched to a tool that fits our needs in a better way.

We created 3 main epics :

- Backend : The rust API
- Frontend : The angular frontend
- Maquettes : The figma maquettes. It could have been merged with frontend Epic

Each of them includes functional and technical conception.

### Risk analysis

Priority is based on those criteria : Impact, probability and cost

|Label|Description|Risk|Found solution|
|-|-|-|-|
|Members loose faith in the project|This is about people getting bored of this project and tghus being less productive towards its completness.|<span style="color:red;">High</span>|Found solution : Agile project cycle, clearer objectives with reduced perimeter, increased CI/CD to have a quick feedback and the feeling of accomplishment.|
|Hacking|A hacker accesses the backend server by some mean or succesfully runs an SQLinjection by some unknowns vulnerability.|<span style="color:orange;">Medium</span>|For now there is no account, and the data is easily recoverable. But anyway, we will have to make saves of the database regularly. And if we begin to store user data (for users accounts) then we obviously will set appropriate hashing algorithm to mitigate risks.|
|Sudden increase in popularity|The website gains sudden popularity by some mean (exposure on social media) that would either break the site or increase server cost|<span style="color:orange;">Medium</span>|Setting a limit upon which the server would automatically stop. This could be achieved by having a host subscription plan that would symply stop when we go beyond current limit. Afterwards, if we want to be able to support such traffic, we would have to think about a way to earn monney to supports infrastucture costs.|
|A similar website exists or appears|-|<span style="color:green;">Low</span>|Not a real problem, we do not even wish to be seen as concurency for website or applications such as [Settera](https://www.seterra.com/) or [World Map Quizz](https://play.google.com/store/apps/details?id=com.qbis.guessthecountry)|


### Global perimeter
