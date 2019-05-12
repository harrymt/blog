---
layout: post
title: Domain Driven Design
tags: [ddd]
---

<div class="message">
Domain Driven Design is about creating a contextual language to aid in software design.
</div>


## What is Domain Driven Design all about?

- Ubiquitious Language
- Bounded Context

#### Ubiquitious Language

A word can have different meanings depending on the context.
The word flight in Ryanair's iOS app, would have information such as the flight number, date of travel and price.
The word flight in an air traffic control system, would share some information, such as the flight number, but might contain the movements of the aircraft and probably won't include the price of the flight.

Domain Driven Design is about defining what words mean in the domain of the project.
It is also useful to define the bounds of this language.

#### Bounded Context

If a software team was tasked with building an air traffic control system and an iOS app, they would want to think hard about how to separate both projects.
They might group the parts of the system into multiple parts, label each of these parts and only refer to those parts in the context of the label.
This is the bounds of the project context.

If these labels get too cluttered or full with items, as they will over time, we should split up those parts into new contextual areas.

