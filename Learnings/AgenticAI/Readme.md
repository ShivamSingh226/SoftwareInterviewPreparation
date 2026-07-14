# Agentic AI

## Agents: An LLM that can use tools in a loop

- AI taking actions to achieve goal
- You give it a goal and it executes steps to achieve that goal
- AI takes multiple actions, runs feedback loop and ensure that the goal is achieved.
- Human only sets the goal.
- Multiple steps, multiple tools, context and state-ful applications, Pro-active compared to Re-active system of Gen AI

It has:
1. State - Memory
2. Persistence - Can be paused and removed
3. Control Flow - Can be branched, looped and coordinate
4. Tools at Scale
5. Human Oversight - Sensitive decisions can be delegated to Humans
6. Mult-Agent Orchestration - Multiple specialized agents working

## Why Langgraph

1. Langchain handle sequential workflows, loops become messy(`while` loops).  
2. Managing memory between multiple agents is manual.
3. Langchain expects workflow to run continuously, so scheduling tasks, waiting for execution becomes challenging while Langgraph supports persistent and resumable workflows.
4. Human in the loop (Approval workflows become complex) while in langgraph using graph noeds and edges.
5. Langgraph orchestrate intelligent systems(multi-agent systems) while Langchains call LLM.

## Sequential Workflow (Using State, Nodes and Edges)

1. 

