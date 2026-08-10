---
title: "Event 2 - FCAJ x Agentic AI Build Week"
date: 2026-07-25
weight: 2
chapter: false
pre: " <b> 4.2. </b> "
---

# FCAJ x Agentic AI Build Week: Show Up. Build. Pitch. WIN!

## Event information

| Item | Details |
| --- | --- |
| **Event** | FCAJ x Agentic AI Build Week: Show Up. Build. Pitch. WIN! |
| **Time** | 09:00–12:00, 25 July 2026 |
| **Location** | 26th Floor, Bitexco Tower, Ho Chi Minh City |
| **Organizer** | First Cloud AI Journey (FCAJ) / AWS Study Group |
| **My role** | Attendee listening to the sharing, pitches, demonstrations, and Q&A |

## Overview and purpose

This event reviewed the journeys of notable teams from **Agentic AI Build Week**, where participants built AI-agent products on AWS. Teams presented real problems, product ideas, AWS architectures, demonstrations, and lessons from developing under hackathon time pressure.

I attended to learn how teams transformed ideas into demonstrable products, defined pain points, controlled MVP scope, divided responsibilities, selected AWS services, and communicated business value. These lessons were directly relevant to my team's CampusMeet project.

![FCAJ x Agentic AI Build Week venue](/images/4-EventParticipated/agentic-ai-build-week/event-venue.jpg "FCAJ x Agentic AI Build Week at Bitexco Tower")

*The event space on the 26th floor of Bitexco Tower.*

## Key content

### Opening and lifelong learning

AWS representatives discussed the rapid development of AI, opportunities for young builders, the confidence to challenge old processes, and the importance of remaining a **lifelong learner**.

![Opening sharing session](/images/4-EventParticipated/agentic-ai-build-week/opening-sharing.jpg "A speaker sharing practical experience")

*A speaker sharing practical experience with the audience.*

### Solutions presented

- **One Team – KFC Chatbot Agent:** a conversational ordering agent that keeps users inside messaging applications, maintains context, and streamlines checkout.
- **Signal Scout:** a multi-agent system that gathers public corporate information and analyzes competitor strategies, benefits, and risks while optimizing AWS cost and data protection.
- **AI assistant for Solution Architects:** a tool that interprets natural-language requirements and documents, then assists with architecture diagrams, cost estimates, and Infrastructure as Code.
- **Sheper:** a computer-vision and AI-agent solution that monitors crowd flow, detects congestion risk, and recommends operational responses.
- **Six Pillars – Adaptive Workflow Engine:** a multi-agent workflow that investigates anti-money-laundering alerts and escalates suspicious cases to human reviewers with an explanatory report.

## Lessons learned

### Start with business impact

The strongest solutions addressed a specific pain point and demonstrated measurable value. Technology matters when it reduces time, cost, friction, or risk.

### Control MVP scope

Under strict time constraints, teams should prioritize one reliable, demonstrable core flow before adding features. This is relevant to CampusMeet because it spans meetings, content, AI, calendars, and tasks.

### Work as a team under pressure

Members need to set ego aside, agree on priorities, and separate backend, frontend, infrastructure, and pitching responsibilities. Frequent communication prevents the product from splitting into incompatible directions.

### Protect security and operations

Secrets, `.env` files, access permissions, observability, and infrastructure costs must be controlled even during a hackathon.

## Application to CampusMeet

- Define the user problem before choosing AWS services or AI features.
- Prioritize the core flow from groups and meetings to Google Meet, content, minutes, and tasks.
- Separate work through modules and API contracts.
- Keep secrets out of Git and use appropriate secret management.
- Use Step Functions, AIJob states, and idempotency for observable and recoverable AI processing.
- Demonstrate CampusMeet through a user journey rather than an isolated list of services.

## Reflection

The event showed me the gap between an idea and a product that can persuade an audience. In addition to architecture and code, teams had to understand users, manage time, present clearly, and demonstrate value. Honest stories about technical failures, disagreements, fatigue, and scope changes made the lessons especially practical.

The courage to participate before feeling completely prepared was particularly motivating. I left with a stronger commitment to complete CampusMeet as a coherent product with a clear demonstration flow and secure deployable infrastructure.

## Video evidence

{{< video src="videos/agentic-ai-build-week/event-clip.mp4" caption="A short clip documenting the atmosphere at FCAJ x Agentic AI Build Week." >}}

## Reference

- [Event recap video](https://www.youtube.com/watch?v=hz32VBrvW7M)
