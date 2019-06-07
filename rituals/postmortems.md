# Incident Postmortems

Postmortem documents are a ritual designed to examine serious incidents or outages. Google’s [book on Site Reliability Engineering](https://landing.google.com/sre/book.html) says:

> A postmortem is a written record of an incident, its impact, the actions taken to mitigate or resolve it, the root cause(s), and the follow-up actions to prevent the incident from recurring.

## Purpose

We practice postmortems to ensure we understand and address the root cause of severe incidents such as outages, data loss, or serious production bugs.

> "Don't make the mistake of neglecting a post-mortem after an incident. Without a post-mortem you fail to recognize what you're doing right, where you could improve, and most importantly, how to avoid making the same exact mistakes next time around. A well-designed, blameless post-mortem allows teams to continuously learn, and serves as a way to iteratively improve your infrastructure and incident response process." — [PagerDuty](https://response.pagerduty.com/after/post_mortem_process/)

### What is a Postmortem?

A postmortem is a document that examines an incident in detail, including:

- An summary of what happened
- The incident's impact
- What caused the incident
- How the incident was resolved
- A detailed timeline
- What could have prevented the incident

### Why Do We Do Postmortems?

The goal of the postmortem is to gain a detailed understanding of the root causes of the incident to avoid it happening again in the future. A secondary goal can be to reassure the client, since the actions taken during an incident response may not be visible to them.

For postmortems to be effective at reducing repeat incidents, the review process has to incentivize teams to honestly identify root causes and fix them. For this reason, we practice **blameless postmortems** (see below).

### When is a Postmortem Needed?

It depends on the client or project. For applications or sites with an service-level agreement, postmortems are commonly carried out for high-severity incidents that violate the SLA. For client applications or site, a postmortem may only be called for following a major outage or quality-control problem.

> "Incidents in your organization should have clear and measurable severity levels. These severity levels can be used to trigger the post-mortem process. For example, any incident Sev-1 or higher triggers the postmortem process, while the postmortem can be optional for less severe incidents." — [Atlassian](https://www.atlassian.com/blog/statuspage/incident-postmortem-writing-tips)

The postmortem document should be produced within 24-48 hours of the incident's resolution, while it's still fresh in everyone's memory.

> "Despite how painful an outage may have been, the worst thing you can do is to bury it and never properly close the incident in a clear and transparent way. Most humans come together in times of crisis and communication around outage post-mortems, in my experience, has always been met with positive energy, understanding comments, constructive suggestions and numerous offers to help." — [Daniel Doubrovkine says](https://artsy.github.io/blog/2014/11/19/how-to-write-great-outage-post-mortems/)

### Who Completes the Postmortem?

In a small company like ours, the most senior engineer with direct knowledge should be writing an outage postmortem. It's their job and responsibility to acknowledge, understand and explain what happened. For particularly sensitive topics, it may make sense to escalate this responsibility to an engineering manager or founder.

> "Focusing attention away from the individual contributors allows the team to learn from the mistakes and address the root causes in time without the unnecessary stress or pressure during a crisis." — [Daniel Doubrovkine](https://artsy.github.io/blog/2014/11/19/how-to-write-great-outage-post-mortems/)

### Who is the Postmortem For?

The postmortem is intended for public consumption, especially by clients. It's a visible way to document not just the problem that happened, but how you addressed it and are ensuring it won't happen again. A properly written postmortem should increase your customer's faith in you.

> "The postmortem audience includes customers, direct reports, peers, the company's executive team and often investors. The document may be published on your website, and otherwise goes to the entire team. It's critical to bcc everyone. This is the equivalent of a locked thread, avoiding washing the laundry in public: one of the worst possible things to see is when a senior manager replies back pointing an individual who made a mistake, definitely not an email you want accidentally sent to the entire company." — [Daniel Doubrovkine](https://artsy.github.io/blog/2014/11/19/how-to-write-great-outage-post-mortems/)

### Running a Postmortem Meeting

Some teams hold a meeting after the postmortem document is produced. These meetings are generally short, only 15-30 minutes, and are intended to be a wrap-up of the postmortem process. We discuss what happened, what could have gone better, and any followup actions we need to take. The point of the meeting is to ensure there's no disagreement on the analysis, and spread a wider awareness of problems the team is facing.

## Blameless Postmortems

Many teams have adopted “blameless” postmortems, which focus on systemic problems and root causes without naming individuals or casting blame onto people or teams. Here's John Allspaw, from [Blameless Postmortems and a Just Culture](https://codeascraft.com/2012/05/22/blameless-postmortems/)

> Having a “blameless” Post-Mortem process means that engineers whose actions have contributed to an accident can give a detailed account of:

> - what actions they took at what time,
> - what effects they observed,
> - expectations they had,
> - assumptions they had made,
> - and their understanding of timeline of events as they occurred.

> …and that they can give this detailed account without fear of punishment or retribution.

> Why shouldn’t they be punished or reprimanded? Because an engineer who thinks they’re going to be reprimanded are disincentivized to give the details necessary to get an understanding of the mechanism, pathology, and operation of the failure. This lack of understanding of how the accident occurred all but guarantees that it will repeat. If not with the original engineer, another one in the future.

For a good example of why blameless postmortems matter, I strongly encourage you to watch [Who Destroyed Three Mile Island?](https://www.youtube.com/watch?v=hMk6rF4Tzsg), a talk by Nickolas Means from Lead Dev London 2018.

## Tips

- Make sure the timeline is an accurate representation of events.
- Use the [Five Whys](https://en.wikipedia.org/wiki/5_Whys) technique to traverse the causal chain until you find a good true root cause.
- Don't change details or events to make things "look better". We need to be honest in our post-mortems, even to ourselves, otherwise they lose their effectiveness.
- Don't name and shame someone. We keep our post-mortems blameless. If someone deployed a change that broke things, it's not their fault, it's our fault for having a system that allowed them to deploy a breaking change, etc.
- Avoid the concept of "human error". This is related to the point above about "naming and shaming", but there's a subtle difference - very rarely is the mistake "rooted" in a human performing an action, there are often several contributing factors (the script the human ran didn't have rate limiting, the documentation was out of date, etc...) that can and should be addressed.

## Resources

* [Postmortem Template](https://docs.google.com/document/d/12Prd33SDG1U0yE_gwXUgwa85Vn6dS_Qo5RdEWwFzFEo) document on Google Drive
* [Postmortem Handbook from Atlassian](https://www.atlassian.com/incident-management/handbook/postmortems)
* [Postmortem Process from PagerDuty](https://response.pagerduty.com/after/post_mortem_process/)
* [Effective Postmortem Tips from PagerDuty](https://response.pagerduty.com/after/effective_post_mortems/)
* [Blameless Postmortems and a Just Culture](https://codeascraft.com/2012/05/22/blameless-postmortems/)
* [How to Write Great Outage Postmortems](https://artsy.github.io/blog/2014/11/19/how-to-write-great-outage-post-mortems/)
