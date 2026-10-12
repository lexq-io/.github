Your service sends the facts of a request, such as an order total or a customer's plan, to LexQ's Execution API and gets a decision back. The decision comes from rules your team writes in LexQ, so you can change a rule without waiting for a release and try the change on past requests first. A rule can change some of those values, for example taking a discount off an order total, or mark the request as rejected. Each kind of decision, like whether a plan allows another seat, has its own group of rules. The request names the group.

LexQ stores each group's rules as a series of versions. You can deploy a new version or roll back without redeploying your service, as long as the new rules use only facts that are already in the request. An A/B test splits live traffic by customer ID or another key in the request and sends part of it to a second version. Every decision leaves a trace of which rules matched and which facts they changed. Each trace also names the version that made the decision, so you can filter traces by version. How long traces are kept depends on your LexQ plan.

Impact Simulation runs the new version alongside another one, usually the live version, on past requests or an uploaded file. It compares the two on how many requests matched a rule and on a number you choose from the results, such as the total discount. Decision Replay instead compares the new version with the decisions LexQ actually returned. Those may have come from several versions, if the period had deploys or an A/B test. Replay reruns the stored inputs of past requests and counts how many decisions would come out differently. Rules read only the request, never a database or the clock, so a rerun differs from the original only in the rules.

The LexQ CLI (`npm install -g @lexq/cli`) can also run as a local Model Context Protocol (MCP) server, using the API key you saved with `lexq auth login`. Agents in Cursor or Claude Desktop can then call its commands as tools, including deploys. The same tools are hosted at `https://mcp.lexq.io` for Claude.ai and other clients that support remote MCP servers. When a client connects, you sign in to LexQ and pick the API key the agent will use.

Your service makes a network call to LexQ for every decision, so a rule that changes once a year is simpler to keep in your code.

## Start here

- [Quickstart](https://docs.lexq.io/quickstart)
- [Console](https://console.lexq.io): sign up and write rules in the browser
- [lexq-cli](https://github.com/lexq-io/lexq-cli): the CLI and the MCP server
- [Connect an AI agent over MCP](https://docs.lexq.io/cli/mcp-server)
- [lexq-examples](https://github.com/lexq-io/lexq-examples): what you send and get back, with runnable TypeScript and Spring Boot services
- [Pricing and the free plan](https://lexq.io/en#pricing)
