# Module 05 — OpenAI Responses API and Agents SDK Basics

<p align="center">
  <img src="https://img.shields.io/badge/Module-05-blue"/>
  <img src="https://img.shields.io/badge/Status-Completed-success"/>
  <img src="https://img.shields.io/badge/Skill%20Check-80%25-success"/>
</p>

---

## 📌 Module Overview

This module introduces the practical foundations of building AI agents using the **OpenAI Responses API** and the **OpenAI Agents SDK**.

It explores the OpenAI agent stack, the Responses API, agent creation using the Agents SDK, tool and function calling, multi-agent systems with handoffs, and safety mechanisms such as guardrails.

The module also demonstrates how these components can be combined to build practical agentic applications, including a **Customer Support Agent**.

---

# 🎯 Learning Objectives

By completing this module, I developed an understanding of:

* The OpenAI agent stack.
* The OpenAI Responses API.
* The OpenAI Agents SDK.
* Creating and configuring AI agents.
* Tools and function calling.
* Multi-agent systems.
* Agent handoffs.
* Guardrails and safety mechanisms.
* Combining multiple agent components into a complete system.
* Building practical customer support agent workflows.

---

# 📚 Module Contents

| # | Topic                                      | Duration | Status |
| - | ------------------------------------------ | -------: | ------ |
| 1 | Module Intro                               |    3 min | ✅ |
| 2 | OpenAI Agent Stack                         |    8 min | ✅ |
| 3 | OpenAI Responses API                       |   11 min | ✅ |
| 4 | OpenAI Agents SDK                          |    7 min | ✅ |
| 5 | Demo: Responses API and Agents SDK         |    4 min | ✅ |
| 6 | Tools and Function Calling                 |   10 min | ✅ |
| 7 | Multi Agent System with Handoffs           |    5 min | ✅ |
| 8 | Guardrails and Safety                      |    7 min | ✅ |
| 9 | Putting it All Together                    |   10 min | ✅ |
| 10 | Demo: Customer Support Agent              |    9 min | ✅ |
| 11 | Summary                                   |    4 min | ✅ |
| 12 | Skill Check: OpenAI Responses API and Agents SDK | — | ✅ |

---

# 🧠 Core Concepts

## 1. OpenAI Agent Stack

The OpenAI agent stack provides the building blocks required to develop applications that can reason, use tools, interact with external systems and coordinate multiple agents.

A simplified representation is:

```text
                    AI AGENT APPLICATION
                            │
                            ↓
                  ┌───────────────────┐
                  │   OpenAI Models   │
                  └─────────┬─────────┘
                            ↓
                  ┌───────────────────┐
                  │ Responses API     │
                  └─────────┬─────────┘
                            ↓
                  ┌───────────────────┐
                  │   Agents SDK      │
                  └─────────┬─────────┘
                            ↓
             ┌──────────────┼──────────────┐
             ↓              ↓              ↓
           Tools        Handoffs       Guardrails
             │              │              │
             └──────────────┼──────────────┘
                            ↓
                       Agent Workflow
                            ↓
                          Result
