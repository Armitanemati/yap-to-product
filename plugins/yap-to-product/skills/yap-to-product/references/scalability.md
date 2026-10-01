# Scalability epic

Create one epic named "Scalability" with the lowest priority, in To Do, labeled `scalability`. Add the tasks below. Each task gets its **Start when** line and the filled-in prompt in a code block.

| Task | Start when | Focus line |
|---|---|---|
| Hosting and server capacity | Pages slow down at busy times, or a launch or campaign is coming | Where are the bottlenecks today, and do I need a bigger server, more servers, or neither? |
| CI/CD pipeline | More than one person changes the code, or manual deploys cause mistakes | What is the simplest pipeline that runs tests and deploys to staging, then to production after approval? |
| Database growth and migrations | Data grows quickly, or a schema change is needed on live data | Which tables grow fastest, what indexes or limits are missing, and how do I migrate safely with a rollback plan? |
| Monitoring and error alerts | Real users depend on the product | What must I be alerted about, through which channel, and what can wait for a weekly review? |
| Backups and recovery | The product holds data the user cannot afford to lose (do this early if so) | How often must data be backed up, where, and how do I prove a restore actually works? |
| Security review | Accounts, payments, or personal data at scale | Check authentication, permissions, secrets handling, dependencies, and data protection obligations for my users' locations. |
| Performance and caching | Measured slowness, not a hunch | Measure first. Which pages or queries are slow, and what is the cheapest fix? |

## Prompt template

```
I want to work on scalability for my product. Topic: [TASK NAME].
Before changing anything, interview me and inspect the project:
1. How many users do I have now, and how many use it at the same time at peak?
2. What is actually going wrong, or what growth do I expect (a launch, a campaign, a new market)?
3. What is my current stack and hosting? Check the repository to confirm my answer.
4. What monthly budget and how much downtime are acceptable?
Focus: [FOCUS LINE].
Then propose the smallest change that solves the real problem, explain the trade-offs
and costs, and wait for my approval before implementing. If my numbers do not justify
this work yet, tell me so and stop.
```
