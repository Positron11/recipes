# Recipe Grammar

## To Do...
- (?) Heating actions are simply (optional) performing some action at a certain temperature in a container. Thus, things like "cook" and "fry" aren't necessarily actions on their own.
- Alternatively, should the processing be implicit in the definition of the heating action?
- How do we represent interjections (frying sausage, add garlic halfway through)?

## What is a Recipe?

- Recipe is a **series of sub-processes** with input, actions and output. 
- Processes are **sequential** and feed into one another.
- Processes are standardized **actions** applied to one or more **ingredients** in a certain **manner** for a certain **duration** (with a certain specified termination condition/**outcome**).

### Ingredients

- A **processed item resolves/expands to a series of processing steps** performed on a set of base ingredients.
- Ingredients are therefore always leaf nodes.

## What is a Process?

A process can generally be broken down like so:

> (*Adverb* $\xrightarrow{\text{describes}}$ **Action** $\xrightarrow{\text{applied to}}$ **Item** $\xrightarrow{\text{using}}$ *Active Utensil* $\xrightarrow{\text{in}}$ *Environment / Passive Utensil*) $\xrightarrow{\text{at}}$ *Temperature* $\xrightarrow{\text{until}}$ *Time Elapsed / Outcome Achieved*

### Concurrent Processes

Concurrent processes on the same item (ie. "milk in pot" undergoes "gradually add flour while stirring slowly at 60°C") are handled by branching / parallel edges that are immediately resolved upon completion of both processes. Processes with no defined time inherit from the longest sibling.

### Edge Cases

#### Ramping Temperature

We may introduce an additional temperature component that defines a `START_TEMP`, `END_TEMP`, and a `TEMP_CURVE`, which interpolates between the given endpoints within the time frame defined by the parent process.

## Recipe Procedure Graph

- The current "state" of something is implicit in the graph (following the subtree rooted at a given point)
