# Recipe

Documentation for a foundational understanding of what comprises a recipe.

## Table of Contents

- [Recipe](#recipe)
	- [Table of Contents](#table-of-contents)
	- [What is a Recipe?](#what-is-a-recipe)
	- [Actions](#actions)
	- [Recipe State](#recipe-state)
	- [Environments](#environments)
	- [Processes](#processes)
		- [Temperature](#temperature)
			- [Ramping Temperature](#ramping-temperature)
		- [Concurrent Processes/Actions](#concurrent-processesactions)
	- [To Do](#to-do)

## What is a Recipe?

- A recipe is a **series of action steps** with input, actions and output. 
- Actions are **sequential** and feed into one another.
- A recipe will have a single final output, may be an aggregation of multiple components

## Actions

We define a fixed number of generalized actions:

1. `PROCESS`
2. `TRANSFER`
3. `PLATE`

## Recipe State

- A **partially processed component (PPC) resolves/expands to a series of action steps** performed on a set of base ingredients.
- PPCs are **never explicitly extracted** into nodes/objects in the action graph, until the final output - the output of a processing step feeds directly into another action.
- The current "state" of a PPC is **implicit in the structure of the subgraph** rooted at a given point.

## Environments

An environment is described by:

> An (optional) **container** (eg. pan, mixing bowl, baking tray) and a **location** (eg. counter, cutting board, stovetop)

- An ingredient is not associated with an environment by default.
- An ingredient or PPC is assigned an environment by a `TRANSFER` action, and implicitly continues to be associated with this environment through any processing steps.

## Processes

A process can generally be broken down like so:

> (Context $\xrightarrow{\text{describes}}$ **Technique** $\xrightarrow{\text{applied to}}$ **Item** $\xrightarrow{\text{using}}$ Tool) $\xrightarrow{\text{at}}$ Temperature $\xrightarrow{\text{until}}$ Time Elapsed / Outcome Achieved

### Temperature

#### Ramping Temperature

We may introduce an additional temperature component that defines a `START_TEMP`, `END_TEMP`, and a `TEMP_CURVE`, which interpolates between the given endpoints within the time frame defined by the parent process.

### Concurrent Processes/Actions

Concurrent processes on the same item (ie. "milk in pot" undergoes "gradually add flour while stirring slowly at 60°C") are handled by branching / parallel edges that are immediately resolved and merged upon completion of both processes.

- Interjections or periodic parallel actions (eg. "sauté onions and add garlic halfway through") are handled similarly, with relative times (halfway through) inherited from named processes

## To Do

- (?) Heating actions are simply (optional) performing some action at a certain temperature in a container. Thus, things like "cook" and "fry" aren't necessarily actions on their own.
- Alternatively, should the processing be implicit in the definition of the heating action?
- How do we represent interjections (frying sausage, add garlic halfway through)?