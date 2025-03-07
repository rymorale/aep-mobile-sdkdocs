---
title: Attach data to SDK events
description: A guide that explains how to attach data, using  Mobile Core, to your Mobile SDK events.
keywords:
- Attach data
- Guide
- Mobile Core
- Rules Engine
- Tutorial
---

import AttachingDataAnalytics from './tabs/attach-data/attaching-data/analytics.md'
import AttachingDataTarget from './tabs/attach-data/attaching-data/target.md'

# Attach data to SDK events

The attach data_rule action is supported in [Mobile Core](../mobile-core/index.md) starting from version 2.1.8 (Launch), 2.3.5 (iOS), and 1.4.5 (Android). This action is powerful, complex, and enables advanced use cases.

To use this action, you need to learn how events flow in the Adobe Experience Platform Mobile SDK and how they interact with the [rules engine](../mobile-core/rules-engine/index.md).

## Context

### What are SDK events?

In the Experience Platform Mobile SDK, events hold all the data that is required by other extensions to complete the necessary actions. Events have the following properties:

| Property | Description |
| :--- | :--- |
| Type | Describes the event. Examples include Adobe Analytics, Adobe Target, and Adobe Lifecycle. |
| Source | Indicates the cause or the directionality of the event. For example, a request or a response. |
| Event data | The data required to define the event. For example, context data on an Analytics event. |

Extensions that register with [Mobile Core](../mobile-core/index.md) will also register event listeners. A listener is defined by a combination of event type and source. When the SDK event hub processes an event, it notifies all listeners that match the provided combination.

### How are events created in the SDK?

Events are created by an extension and are dispatched to the SDK Event Hub. Each published rule that is created in the Data Collection UI is evaluated against the current event. Finally, the event is passed to each of the listeners for events with the submitted type / source combination.

<InlineAlert variant="info" slots="text"/>

Events are created and dispatched when an SDK public API is invoked. Attach data action use cases are meant to act on these types of events.

### What is the Rules Engine?

The Rules Engine lives in the SDK Event Hub. Before listeners are notified, the Rules Engine evaluates each tag rule for mobile properties against the triggering event. A rule is defined by the following properties:

| Property | Description |
| :--- | :--- |
| Event | Trigger for the rule. |
| Condition | Definition of the criteria to compare against the triggering event. |
| Action | The resulting action if the evaluation of the rule is positive. |

<InlineAlert variant="info" slots="text"/>

A rule might be read out in the following way: If the SDK **Event** occurs and **Condition(s)** are met, then perform the **Action(s)**.

## Using the attach data action

**Attach Data** is a type of rule action that lets you add event data to an SDK event. The modification of data happens in the Rules Engine before event listeners are notified of the event.

<InlineAlert variant="info" slots="text"/>

Attach data rule actions will only add data to the event. These actions never modify or remove data. <br/><br/> If there is a conflict between the data that is defined in your rule and the data in the event, the data in the event always has preference.

### Defining a payload for the attach data action

When defining a payload for the attach data action, the payload must match the format of the triggering event. For example, if you want to add context data to an Adobe Analytics event, you need to know where the context data is defined on that event and match the format in your rule.

As a result, it is highly recommended to enable verbose logging in the SDK and carefully study the format of the event to which you will attach the data. If the format does not match, most likely the expected results will not be received.

## Example - attaching data to an event

<TabsBlock orientation="horizontal" slots="heading, content" repeat="2"/>

Analytics

<AttachingDataAnalytics/>

Target

<AttachingDataTarget/>
