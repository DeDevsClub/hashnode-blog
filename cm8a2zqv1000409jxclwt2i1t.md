---
title: "Build with Mastra AI with our Starter Kit"
seoTitle: "Kickstart Your Project with Mastra AI Kit"
seoDescription: "Mastra AI's Starter Kit enables rapid AI agent development with a modular architecture, workflows, and tools for innovative applications."
datePublished: Sat Mar 15 2025 10:45:57 GMT+0000 (Coordinated Universal Time)
cuid: cm8a2zqv1000409jxclwt2i1t
slug: build-with-mastra-ai-with-our-starter-kit
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1742026898461/59cd545a-da24-412b-b29e-b3ab617de55d.png
tags: ai, artificial-intelligence, developer, devops, developer-tools, devrel, mastraai, mastra, dedevs

---

This article delves into the technical architecture, components, and implementation details of the Mastra Starter Kit, providing insights into how it facilitates the rapid development of AI agents and workflows.

![Mastra Banner](https://pbs.twimg.com/profile_banners/1861308613563949057/1732605740/1500x500 align="left")

## <mark>Our Final Product: What We’re Building</mark>

Our objective is to deliver a comprehensive and robust solution that empowers developers to swiftly and efficiently create AI agents and workflows. This final product is envisioned to be a versatile toolkit that not only simplifies the development process but also enhances the capabilities of AI-driven applications. By providing a well-structured framework, we aim to streamline the integration of various AI components, ensuring that developers can focus more on innovation and less on the complexities of setup and configuration.

<div data-node-type="callout">
<div data-node-type="callout-emoji">✨</div>
<div data-node-type="callout-text">We <em>really</em> want to make this toolkit accessible and user-friendly, catering to both novice developers who are just beginning their journey in AI, as well as seasoned professionals looking for a reliable and scalable solution.</div>
</div>

The final product will include detailed documentation, sample projects, and a supportive community to facilitate learning and collaboration. By achieving this, we hope to accelerate the adoption of AI technologies across different industries, ultimately contributing to the advancement of AI applications in solving real-world problems.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1742033787758/7fd2c1e6-e535-41c9-ab48-9368988a2fd6.png align="center")

By following this guided tutorial, you will be able to create a comprehensive final product that showcases the full potential of the Mastra Starter Kit.

> This tutorial will walk you through each step of the process, ensuring that you gain a deep understanding of how to effectively utilize the various components of the kit.

The final product will be a sophisticated AI application that leverages the power of Large Language Models (LLMs) to perform specific tasks through AI entities known as agents.

These agents will be enhanced by functional components, referred to as tools, which provide specialized functionalities to extend their capabilities.

Moreover, you will learn how to orchestrate these agents and tools into multi-step workflows, enabling them to work together seamlessly to accomplish complex tasks. This approach ensures a clear separation of concerns, allowing you to maintain a clean and organized code structure.

Throughout the tutorial, you will also gain insights into the implementation details and technical architecture of the Mastra Starter Kit. By the end, you will have a fully functional AI application that not only demonstrates the power of the kit but also adheres to best practices in code maintainability and type safety, thanks to the use of TypeScript.

## <mark>Mastra Framework and Template Design</mark>

#### The Mastra Starter Kit is thoughtfully designed with a modular architecture that revolves around three essential components: Agents, Tools, and Workflows.

#### Each component plays a crucial role in building robust AI applications, and together, they form the backbone of the Mastra framework. The starter template architecture is illustrated below.

```bash
mastra-starter/
├── src/
│   └── mastra/
│       ├── agents/           # AI agent definitions
│       ├── tools/            # Custom tools for agents
│       ├── workflows/        # Multi-step workflows
│       └── index.ts          # Main Mastra configuration
├── package.json              # Project dependencies
├── tsconfig.json             # TypeScript configuration
└── .env.example              # Environment variables template
```

# <mark>Mastra Framework Components</mark>

## <mark>Agents: Assistants with Special Abilities</mark>

Agents in Mastra are AI-powered entities that leverage LLMs to perform tasks. The starter kit includes a weather agent implementation, which configures agents with: a descriptive name, detailed instructions that guide its behavior, integration with OpenAI's GPT-4o model, and access to the custom weatherTool.

```typescript
// src/mastra/agents/index.ts
import { openai } from '@ai-sdk/openai';
import { Agent } from '@mastra/core/agent';
import { weatherTool } from '../tools';

export const weatherAgent = new Agent({
  name: 'Weather Agent',
  instructions: `
      You are a helpful weather assistant that provides accurate weather information.

      Your primary function is to help users get weather details for specific locations. When responding:
      - Always ask for a location if none is provided
      - If giving a location with multiple parts (e.g. "New York, NY"), use the most relevant part (e.g. "New York")
      - Include relevant details like humidity, wind conditions, and precipitation
      - Keep responses concise but informative

      Use the weatherTool to fetch current weather data.
  `,
  model: openai('gpt-4o'),
  tools: { weatherTool },
});
```

These are intelligent entities powered by advanced Large Language Models (LLMs). Agents are designed to perform specific tasks with precision and efficiency. They can process natural language inputs, make decisions, and execute actions based on the data they receive.

By leveraging the power of LLMs, these agents can handle a wide range of tasks, from simple queries to complex problem-solving scenarios. Developers can define and customize these agents to suit the unique needs of their applications, ensuring that each agent is tailored to perform its designated role effectively.

## <mark>Tools: Empower Agents with Skills and Knowledge</mark>

**Tools are the functional components that enhance the capabilities of the agents.** They provide specialized functionalities that agents can utilize to perform their tasks more effectively. The starter kit includes a weather tool that fetches data from an external API, but that is only one of many options.

Tools range from data processing utilities to integration modules that connect with external APIs or databases. *By incorporating tools, developers can extend the functionality of agents*, enabling them to interact with various systems and perform complex operations. This modular approach allows for easy scalability and adaptability, as new tools can be added or existing ones modified without disrupting the overall system.

**The implementation showcases**: schema validation using Zod for both input and output, structured error handling, integration with external APIs (Open-Meteo), and type safety throughout the execution flow.

```typescript
// src/mastra/tools/weather.ts
export const weatherTool = createTool({
  id: 'get-weather',
  description: 'Get current weather for a location',
  inputSchema: z.object({
    location: z.string().describe('City name'),
  }),
  outputSchema: z.object({
    temperature: z.number(),
    feelsLike: z.number(),
    humidity: z.number(),
    windSpeed: z.number(),
    windGust: z.number(),
    conditions: z.string(),
    location: z.string(),
  }),
  execute: async ({ context }) => {
    return await getWeather(context.location);
  },
});
```

## <mark>Workflows: Where the Magic Happens!</mark>

**Workflows orchestrate the interaction between agents and tools, facilitating the execution of multi-step processes.** Workflows define the sequence of actions that need to be performed to achieve a specific goal. They coordinate the activities of multiple agents and tools, ensuring that each step is executed in the correct order and that data flows seamlessly between components. This structured approach to process management allows developers to create sophisticated AI applications that can handle intricate tasks with ease. By using workflows, developers can break down complex problems into manageable steps, improving both the clarity and maintainability of their code.

Together, these key components enable developers to build powerful AI applications with a clear separation of concerns, maintainable code structure, and type safety through TypeScript.

### Starter Kit Workflow Example

The Mastra Starter Kit provides a solid foundation for developing AI-driven solutions that are both flexible and robust, making it an invaluable tool for developers looking to harness the power of artificial intelligence. We incorporate an example containing a weather workflow. This workflow takes a city `name` as input, fetches weather data using the `fetchWeather` step, generates activity recommendations based on the forecast using the `planActivities` step, and finalizes the workflow with `commit()`.

```typescript
// src/mastra/workflows/index.ts
const weatherWorkflow = new Workflow({
  name: 'weather-workflow',
  triggerSchema: z.object({
    city: z.string().describe('The city to get the weather for'),
  }),
})
  .step(fetchWeather)
  .then(planActivities);

weatherWorkflow.commit();
```

## <mark>Registration Component</mark>

Each step in the workflow is defined with its own input schema, execution logic, and error handling. This central registration: organize and centralizes components, integrates logging for debugging and monitoring, and enable easy access to all workflows and agents throughout the application.

```typescript
// Example of the fetchWeather step from workflows/index.ts
const fetchWeather = new Step({
  id: 'fetch-weather',
  description: 'Fetches weather forecast for a given city',
  inputSchema: z.object({
    city: z.string().describe('The city to get the weather for'),
  }),
  execute: async ({ context }) => {
    // Implementation details...
    return forecast;
  },
});

// src/mastra/index.ts
import { Mastra } from '@mastra/core/mastra';
import { createLogger } from '@mastra/core/logger';
import { weatherWorkflow } from './workflows';
import { weatherAgent } from './agents';

export const mastra = new Mastra({
  workflows: { weatherWorkflow },
  agents: { weatherAgent },
  logger: createLogger({
    name: 'Mastra',
    level: 'info',
  }),
});
```

## <mark>Technical Implementation Details</mark>

> #### **TypeScript Integration**

```json
// package.json (dependencies)
{
  "dependencies": {
    "@ai-sdk/openai": "^1.2.5",
    "@mastra/core": "^0.6.0",
    "mastra": "^0.3.1",
    "zod": "^3.24.2"
  },
  "devDependencies": {
    "@types/node": "^22",
    "tsx": "^4.19.3",
    "typescript": "^5.8.2"
  }
}
```

> #### Schema Validation with Zod

```typescript
// Example from workflows/index.ts
const forecastSchema = z.array(
  z.object({
    date: z.string(),
    maxTemp: z.number(),
    minTemp: z.number(),
    precipitationChance: z.number(),
    condition: z.string(),
    location: z.string(),
  }),
);
```

> #### Development Environment

```json
// package.json (scripts)
{
  "scripts": {
    "dev": "mastra dev"
  }
}
```

## <mark>Benefits and Practical Applications</mark>

#### <mark>Mastra’s Competitive Edge</mark>

* **Rapid Development**: Pre-configured components accelerate the development process.
    
* **Scalability**: Modular architecture supports growth from simple applications to complex systems.
    
* **Best Practices**: Encourages clean code organization and proper error handling.
    
* **Type Safety**: Comprehensive TypeScript integration prevents common runtime errors.
    
* **Modern Stack**: Built with current technologies (TypeScript, OpenAI, Zod).
    

#### <mark>Practical Applications and Use-Cases</mark>

* Conversational AI assistants
    
* Weather-based activity recommendation systems
    
* Data analysis tools with natural language interfaces
    
* Multi-step automation workflows
    

# <mark>Starter Template: Instructions Guide</mark>

%[https://github.com/BunsDev/mastra-starter] 

```bash
# Clones Template
git clone https://github.com/BunsDev/mastra-starter.git
cd mastra-starter
```

```bash
# Setup Environment Variables
cp .env.example .env
# Add your OpenAI API key to the .env file
```

```bash
# Installs Dependences
yarn

# Launches Dashboard
yarn dev
```

<div data-node-type="callout">
<div data-node-type="callout-emoji">🧠</div>
<div data-node-type="callout-text">Contains a chat interface for agent interaction, workflow visualization tools, debug information, logs, and performance metrics.</div>
</div>

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1742027303377/09656896-faab-4335-8827-47c4a91b3013.png align="center")

## <mark>Dashboard Tools and Features</mark>

The features and tools provided in this setup offer a comprehensive environment for developing and managing sophisticated applications. Hopefully you’re just as excited as we were when we discovered Mastra &lt;3

### Playground Interface [/](http://localhost:4111)

Serves as a versatile space for experimenting with new ideas and testing integrations. It is an essential feature for developers looking to innovate and push the boundaries of what the application can achiev

### Mastra API — [/api](http://localhost:4111/api)

Serves as the backbone, providing a robust interface for interacting with various components. The API allows developers to seamlessly integrate and extend functionalities.

### Open API Documentation — [/openapi.json](http://localhost:4111/openapi.json)

This documentation offers detailed insights into the API's capabilities, enabling developers to understand and utilize the available endpoints effectively. This documentation is crucial for ensuring that all team members are on the same page regarding the API's usage and potential.

### Swagger UI — [/swagger-ui](http://localhost:4111/swagger-ui)

For a more interactive experience, the **Swagger UI** provides a user-friendly interface to explore and test API endpoints. This tool is invaluable for developers who need to verify the behavior of the API in a controlled environment, allowing for quick iterations and debugging.

# <mark>Concluding Remarks</mark>

Congratulations! You have successfully setup your foundation for developing advanced applications with AI integration. We designed the template to offers flexibility and tools for your to build custom, innovative solutions. By integrating **LLMs** with structured **workflows** and custom **tools**, Mastra allows developers to build intelligent systems capable of understanding, reasoning, and responding to complex inputs.

As AI technology progresses, frameworks like Mastra deliver the architectural patterns and development tools necessary to effectively leverage these advancements. The starter kit acts as both an educational resource and a practical template for real-world applications. For further details, visit Mastra's official website or explore the documentation for in-depth guides and examples.

## <mark>Bonus Challenge: Extend the Template</mark>

%[https://github.com/BunsDev/mastra-starter] 

When it comes to extending the template, there are several avenues for customization and enhancement. Developers can create new agents with specialized capabilities, allowing the application to handle a wider range of tasks. Building custom tools that integrate with external APIs or services can significantly expand the application's functionality, making it more versatile and powerful.

Designing workflows for multi-step processes is another critical aspect, especially for applications that require complex task management. By creating detailed workflows, developers can ensure that tasks are executed efficiently and effectively.

Finally, enhancing the UI to meet specific application needs allows for a more tailored user experience. Customizing the dashboard and other interface elements ensures that users can interact with the application in a way that best suits their requirements.

#### **Do any of the following, then screenshot and share your code in a tweet and we will share it — just be sure to include @** [**DeDevsClub**](https://x.com/DeDevsClub) **in your tweet!**

* **Create New Agents**: Define additional agents with specialized capabilities.
    
* **Build Custom Tools**: Develop tools that integrate with external APIs or services.
    
* **Design Workflows**: Create multi-step processes for complex tasks.
    
* **Enhance the UI**: Customize the dashboard for specific application needs.
    
* **Submit an Issue on GitHub**: Details on how found in the [ISSUES\_TEMPLATE](https://github.com/BunsDev/mastra-starter/blob/main/.github/ISSUE_TEMPLATE/example-request.md)
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1742019262344/b2ca1ab5-2ae8-44a2-a038-bab047878245.png align="center")

# **<mark>About Valentina “Buns” Alexander &lt;3</mark>**

#### Valentina Alexander is a full-stack AI + Blockchain engineer with commits going back to ‘92 ([contributions](https://github.com/bunsdev)).

#### She is the founder of [DeDevs](https://dedevs.club), which is a community for professionals in AI and Blockchain. She also works full-time as a Developer Relations Engineer (DRE) at [Chainlink Labs](https://chain.link).

<div data-node-type="callout">
<div data-node-type="callout-emoji">💡</div>
<div data-node-type="callout-text"><a target="_self" rel="noopener noreferrer nofollow" href="https://chain.link" style="pointer-events: none">Chainlink</a> is a transformative platform that has unlocked trillions in transactional value on-chain with products ranging from price oracles, automation, external API calls via on-chain functions, non-deterministic random number generation, and so much more!</div>
</div>

## **Valentina Alexander**

**Follow** [**@0xBuns**](https://x.com/0xBuns) **on X (fka Twitter)**CoFounder of DeDevs • [@DeDevsClub](https://x.com/DeDevsClub)  
Developer Relations Engineer • [@Chainlink](https://x.com/chainlink)

---

# **<mark>Join DeDevs Club</mark>**

*In today’s tech-driven world, the fusion of blockchain and AI is not just a trend; it’s a revolution. As these technologies continue to reshape industries, the need for a dedicated space where developers can connect, share insights, and collaborate has never been more critical.*

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1742030986147/6a3d44e0-f4a3-4f29-88bc-010da56938a3.png align="center")

## **<mark>Community for Blockchain and AI Professionals</mark>**

We created a community dedicated to professionals working in the fields of Blockchain and Artificial Intelligence. Our platform is designed to bring together experts, enthusiasts, and newcomers who are passionate about these cutting-edge technologies. Here, members can engage in meaningful discussions, share insights, and collaborate on innovative projects that push the boundaries of what is possible.

We offer developer tools, forums, private Discord access, webinars hosted by industry leaders, and a library of educational materials to help you stay updated with the latest trends and advancements. Whether you are looking to network with like-minded individuals, seek advice on complex problems, or showcase your own projects, our community provides the perfect environment to grow and thrive.

> Join us today and become part of a dynamic network that is shaping the future of technology. Together, we can explore the endless possibilities of Blockchain and AI, driving innovation and creating solutions that have a lasting impact on the world.

%[https://dedevs.club]