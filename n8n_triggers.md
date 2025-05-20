# Trigger Nodes

When creating an automated workflow with n8n, a trigger node is your first building block. Think of a trigger node as the **initiator of your workflow** – it listens for specific events or conditions. When that event occurs, the trigger activates your workflow, supplying the initial data required for your automation.

In this page, we will cover:
- [Key features of a trigger node]()
- [Adding and configuring triggers]()
    - [Configuring multiple triggers]()
- [Types of triggers]()
- [Testing vs activating a trigger]()
    - [Testing]()
    - [Activating]()
- [Frequently asked questions]()
- [Additional resources]()

## Key features of a trigger node

1.  **The lightning bolt icon ⚡:** Most trigger nodes feature this icon, symbolizing their role in initiating the workflow.
2.  **Rouded left edge:** Unlike action nodes which have an input on their left hand side to receive data from preceding nodes, trigger nodes possess a smooth, rounded left edge. This signifies that they are the origin point of a workflow.

<center><img src= image-1.png width="200"></center> 

## Adding and configuring triggers

Incorporating a trigger into your workflow is straightforward:

- In a new, blank workflow:
    - Click the `+` icon with the caption `Add first step...`.
    - This opens the `What triggers this workflow?` panel. Here, you can click a trigger from common trigger categories (e.g., `Trigger manually`, `On app even`, `On a schedule`) or use the search bar to locate a specific trigger.

- Adding additional triggers to any Workflow:
    - Click the main `+` button (located in the top-right of the canvas).
    - From the general node selection panel that appears, click the `Add another trigger` option. This re-opens the `What triggers this workflow?` panel, enabling you to choose and configure your new trigger.

-  Managing a Existing Trigger
    * To re-configure a trigger's settings you can double-click it to open its settings page. 
    * To run, activate/deactivate, copy, duplicate, delete or otherwise manage a trigger, you can click the icons above it or click the `...` to open the trigger's menu.

    <center><img src = image-3.png width = "250"><center>

### Configuring multiple triggers

A single workflow can be initiated by multiple, distinct triggers. For instance, the same workflow logic could be executed:
*   When triggered by a `Schedule Trigger` (e.g., every Monday at 9 AM).
*   *AND* when triggered by a `Gmail Trigger` (e.g., upon a message being received).

> [!NOTE] 
> Each trigger is independent and triggers independent workflows. When `Trigger A` executes, it initiates one complete, self-contained run of the workflow using the data it received or generated. If `Trigger B` executes at a different time (or even concurrently), it starts an entirely new and separate run of the same workflow with its own specific data. 

## How workflows are triggered

To power your automations, n8n provides an extensive suite of trigger nodes. These triggers operate via a few core mechanisms, which are categorized by their grouping within the n8n application:

### 1. Trigger manually
This is the most straightforward way to start a workflow and is primarily for testing and development, or for tasks you want to execute on demand.
*   **How it works:** You directly initiate the workflow by clicking a button in the n8n workflow editor.
* **Read more:**
    - [Manual Trigger node](https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.manualworkflowtrigger/)

### 2. On app event
This trigger allows your workflow to react to events happening in external applications you use.
*   **How it works:** You click a specific application (e.g., Gmail, Shopify, Slack), and then choose a particular event within that app (e.g., `On message received`, `On order paid`, `On new message posted to channel`).
* **Read more:**
    - [n8n Triggers library](https://docs.n8n.io/integrations/builtin/trigger-nodes/)

> [!NOTE]
>App event triggers can operate in two main ways, which n8n manages for you:
>*   **Polling:** n8n periodically checks the external app for new events.
>*   **Webhook:** The external app sends a notification to n8n in near real-time as soon as the event occurs.

### 3. On a schedule
This category is for workflows that need to run at specific times or regular intervals.
*   **How it works:** You define a schedule (e.g., every hour, daily at 9:00 AM, the first Monday of every month). n8n's internal scheduler then initiates the workflow at these times.
* **Read more:**
    - [Schedule Trigger node](https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.scheduletrigger/)

### 4. On Webhook Call
This provides a generic, flexible way for almost any external system, application, or service to trigger your n8n workflow by sending an HTTP request.
*   **How it works:** n8n provides a unique URL. When an external service sends an HTTP request (e.g., POST, GET) to this URL, the workflow is triggered.
* **Read more:**
    - [Webhook node](https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.webhook/)

### 5. On form submission
Allows you to create simple web forms directly within n8n. The workflow starts when someone submits this form.
*   **How it works:** You design the form fields in the node and n8n hosts the form at a unique URL. A submission to this form triggers the workflow, passing the submitted data.
* **Read more:**
    - [n8n Form Trigger node](https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.formtrigger/)
    - [n8n Form node](https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.form/)

### 6. When called by another workflow
Enables you to create modular and interconnected automations where one n8n workflow can initiate another.
*   **How it works:** A parent workflow uses an `Execute A Sub Workflow` action node to trigger a child workflow. The child workflow must have a trigger that can accept this type of invocation such as a `When executed by Another Workflow` trigger.
* **Read more:**
    - [Execute Sub-workflow Trigger node](https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.executeworkflowtrigger/)
    - [Execute Sub-workflow](https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.executeworkflow/)

### 7. On chat message
Specifically designed for building conversational AI agents or chatbots within n8n.
*   **How it works:** The workflow is triggered when a message is received through an integrated chat interface or AI agent interaction point.
* **Read more:**
    - [Chat Trigger node](https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-langchain.chattrigger/) 
    - [Root nodes](https://docs.n8n.io/integrations/builtin/cluster-nodes/root-nodes/)

### 8. Other ways
This category serves as a collection point for more specialized trigger types that address unique system-level events, specific communication protocols, or advanced n8n meta-automation scenarios
*   **How it works:** These triggers enable workflows to be initiated by internal n8n instance activities, dedicated error occurrences in other workflows, or by subscribing to distinct data streams like email servers or real-time server-sent events.
* **Read more:**
    * [Email Trigger (IMAP) node](https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.emailimap/) 
    * [Error Trigger node](https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.errortrigger/)
    * [n8n Trigger node](https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.n8ntrigger/)
    * [SSE Trigger node](https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.ssetrigger/)
    * [MCP Server Trigger node](https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-langchain.mcptrigger/)

## Testing vs activating triggers

### Testing 
Use the `Test workflow` button (at the bottom of the canvas) or the individual play icon ▶️ on a node (including the trigger node) for manual execution.

To test a workflow with a webhook or event-based trigger, you can double-click the trigger node and in the parameters page click `Listen for Test Event` or `Fetch Sample Data` to capture a sample event or fetch recent data to use for testing.

The test data will then proceed through your workflow, and the output of each node is displayed. Use manual testing to check your setup, configuration, and for debugging.

<center><img src = image-4.png width = "450"></center>

### Activating your workflow
Once development and testing are complete, **activate** your workflow using the toggle switch at the top of the canvas. Your workflow is actively listening for real-world events based on its trigger configuration and should run when its trigger conditions are met.

Unlike manual tests, live workflow execution data and logs are not displayed directly on the canvas. To review them:
- Navigate to the `Executions` tab (next to the `Editor` tab) to view the history of all runs. Test executions are often marked with a test tube icon.

<center><img src = image-5.png width = "450"></center>

## Frequently asked questions

*   **"My webhook trigger isn't working after activation."**
    *   Verify that the external service is correctly configured to send events to the trigger's `Production URL`.
*   **"My trigger isn't firing as expected."**
    * Check the documentation to see if the issue is one of the common issues defined for that trigger node, for example:
        - [Schedule Trigger node common issues](https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.scheduletrigger/common-issues/)
        - [Chat Trigger node common issues](https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-langchain.chattrigger/common-issues/)
        - [Manual Trigger node common issues](https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.manualworkflowtrigger/#common-issues)
    * If you cannot find the right answer for your questions, ask the [n8n community](https://community.n8n.io/c/questions/12).

## Where to Go Next

This page provides a foundational understanding. To further enhance your expertise:

* Explore the [n8n Triggers library](https://docs.n8n.io/integrations/builtin/trigger-nodes/).
* Follow our tutorial on [How to create your first workflow](https://docs.n8n.io/try-it-out/tutorial-first-workflow/).
* Learn how to [Create your own nodes](https://docs.n8n.io/integrations/creating-nodes/overview/).