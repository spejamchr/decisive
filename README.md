# Decisive

> A decision-modeling system

Stories are made up of decisions; many are made by thinking actors, and many are made purely by the
author, such as the choice to make a character get sick. _Decisive_ is a system for modeling these
interconnecting choices within and across a story.

## The Building Blocks

*Decisive* Uses a system of `Actors`, `Scopes`, and, `Events` to model a timeline. Each actor has
many scopes, and can cause events to occur within the constraints of those scopes.

### Actors

*Decisive* uses the term `Actor` to refer to a "thing" that needs to be tracked for the plot,
including: thinking characters, inanimate objects, diseases, emotional ties, locations, abstract
ideals held by characters, etc. An actor holds some information about the state of the world at some
point in time. Their interactions are recorded as `Events`, and are limited by their `Scopes`.

An actor holds state about what it is. That's it. It does not hold information about location,
emotions, capabilities, possessions, or anything else. All of that state is held in scopes attached
to the actor.

### Scopes

Each actor has a collection of scopes, which specify state & capabilities of the actor. An example
scope would be a physical range scope -- an actor's decisions can only directly affect other actors
within a range of influence. This scope can be limited to an inmate's jail cell, or can extend to a
superhero's planet.

Notice that scopes are not symmetrical generally -- a superhero might be able to travel instantly
and say "hi" to any random Joe, but the random Joe generally can't get the superhero's attention.

Also note that an actor's scopes can change:

- Actors can meet new people and/or become socially powerful
- Actors can travel to new places
- Actors can form emotional ties (which could be modeled as an "emotional tie" actor with a scope
  indicating which other actors are emotionally tied)
- Actors can get sick (which could be modeled within a "health" scope, for example)

An actor's scope can be affected by other actors' actions: if actor A dies or travels away, they may
leave actor B's physical range scope, and enter other actors' physical range scopes.

### Events

Keeping track of all the actors' changing scopes across a plot is not easy. Instead, establish an
initial set of scopes for all actors, and then keep track of the sequential events that change
those scopes. An event can:

1. change scopes,
2. create or destroy scopes (this is probably unusual, as it fundamentally changes the capabilities
   of an actor; like giving a human superpowers),
2. create or destroy actors.

Then, *Decisive* can calculate the scopes for any actor at any point in time, and verify whether the
chain of events is plausible (ie. whether all events occur within the bounds of the appropriate
scopes).

## Universes

Each collection of Actor/Scope/Events forms a universe with a single timeline. Subsets of one
universe can be copied to additional universes in order to simulate things like time travel or
parallel universes. Additionally, subsets of a universe can be copied within itself as long as the
copies enter the universe after the moment they are copied (duplication and forward time travel are
allowed, but not backward time travel).

## Influences

The Actor/Scopes/Events system has been heavily influenced by the
[Entity-Component-System](https://en.wikipedia.org/wiki/Entity_component_system) software
architectural pattern commonly used in video game development.

- An entity is similar to an actor - it holds only identifying information.
- A component is similar to a scope - it holds state information about the entity, which can be used
  to determine the entity's capabilities.
- A system is a set of code that runs a piece of the game logic continuously, like rendering all
  entities that are visible or doing collision detection between bullets and wound-able entities. It
  doesn't relate directly to events, but the way events are limited by scopes is similar to how
  systems are specific to certain components.
