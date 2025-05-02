### **1. Overview**

This document outlines my approach to designing and implementing an AI agent that helps users find and reserve meeting rooms in an office environment. The agent uses the **LangGraph** framework to manage conversational workflows, handle room selection, resolve scheduling conflicts, and interface with external APIs. While the full integration is not yet running 100% successfully, I’ve successfully studied and applied each core concept in isolated, functional code snippets. The final attempt to bring everything together revealed integration and logic issues, which I explain below.

---

### **2. Framework Justification: LangGraph**

I selected **LangGraph** for its ability to model complex multi-step agent workflows using a graph structure. Its **node-based architecture** allows for modular design and clear state transitions, which is ideal for problems like meeting room scheduling where multiple checks and decisions need to occur in sequence.

LangGraph’s features that supported my approach:

* Declarative node definitions and transitions
* Integrated support for memory and tools
* Built-in state tracking for user inputs, decisions, and API results

Although I explored AutoGen conceptually, LangGraph was a better fit for this deterministic, task-specific agent that depends more on structured logic than multiple dynamic roles.

---

### **3. Agent Roles and Workflow Design**

The main agent was structured with the following **functional nodes**:

1. **Input Parser**: Extracts meeting details such as time, required features (e.g., projector), and number of attendees.
2. **Room Lookup Tool**: Queries a (mocked) room database to retrieve available rooms with matching features.
3. **Conflict Checker**: Verifies availability by comparing user and room calendars.
4. **Decision Handler**: Resolves conflicts by suggesting alternatives or requesting user input.
5. **Reservation Agent**: Books the room via a simulated calendar API.
6. **Error Handler**: Captures failures (e.g., API failure, no available rooms) and logs errors for fallback messaging.
7. **Confirmation Generator**: Sends user a booking confirmation or an appropriate failure message.

Each of these was implemented as a **LangGraph state**, connected with transition logic based on the result of each step.

---

### **4. Data Structures and Parameters**

* User input is modeled as a dictionary storing:

  * `time`, `features`, `duration`, `attendees`
* Room data is mocked as a list of dictionaries with:

  * `room_id`, `features`, `capacity`, `availability`
* The state object passed between nodes carries keys like:

  * `parsed_input`, `available_rooms`, `selected_room`, `booking_status`

Sample parameter values:

```python
user_input = {
    "time": "2 PM",
    "features": ["projector"],
    "duration": "1h",
    "attendees": 6
}
```

---

### **5. Implementation Notes**

When I tested each component separately (e.g., room lookup, conflict resolution), everything worked correctly. These standalone versions helped me better understand the underlying mechanics of LangGraph, state transitions, and tool integration.

However, during the final phase—when I tried to merge all of them into a single graph—the code stopped running correctly. I encountered:

* Issues with how state objects were passed across multiple nodes
* Some asynchronous execution problems
* Conflicting assumptions between tools (e.g., expected structure of inputs/outputs)

These errors were difficult to debug in one go, and I plan to refactor the code by simplifying transitions and re-testing each integration point.

---

### **6. Evaluation Methodology**

Since the system wasn’t fully functional end-to-end, I evaluated each component independently:

* **Room lookup logic**: Verified against mock DB to return correct matches.
* **Conflict checker**: Passed sample calendar entries to ensure proper conflict detection.
* **State transitions**: Logged intermediate states to trace the flow between nodes.

For the complete system, my goal is to implement a unit-test style validation that covers:

* Valid booking cases
* Edge cases (e.g., no rooms available, time conflicts)
* API error responses

---

### **7. Conclusion and Future Work**

Although I wasn’t able to achieve a fully working prototype with everything combined, this project gave me a strong grasp of LangGraph and the structure of agent-based workflows. Going forward, I’ll continue debugging the integration and expand the system to use real calendar and database APIs. I also plan to include a more robust UI layer to support user interaction.
