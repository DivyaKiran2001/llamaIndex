###  Workflows

A Workflow in llamaindex is an event driven abstraction used to chain together several events.Workflows are made up of steps,with each
step responsible for handling certain event types and emitting new events

-> Workflow's in llamaindex work by decorating function with a @step decorator

