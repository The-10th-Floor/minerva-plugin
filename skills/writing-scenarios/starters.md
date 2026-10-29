# Starter scenarios

Nine starter calls ship with Minerva, three per starter set. `scenarios_list` shows the ones this workspace has (they carry a `templateId`); the others are added in the app (Library, New, from a template). Arabic titles are given in English here.

| Starter (set) | Direction | Tests |
| --- | --- | --- |
| Late order, customer on a short break (customer service) | inbound | Checking the live status, then a clear choice: wait with compensation, or cancel and refund to the card |
| Wrong items delivered to a family with an allergy (customer service) | inbound | Naming the allergy risk first, asking before deciding |
| Double charge and yesterday's promise not kept (customer service) | inbound | Explaining a pending charge honestly, owning the issue |
| Internet down for two days, customer already tried everything (technical support) | inbound | Not repeating what they tried; one diagnostic question; a dated repair and the outage credit |
| Internet down, her son video-calls tonight (technical support) | inbound | Simple steps for a novice, checking each one |
| Locked out of payroll software before the 5 pm deadline (technical support) | inbound | Identity checks without losing the deadline |
| Cold call to a salon that doesn't want cold calls (sales) | outbound | Earning time: who, why this number, is now good, one question before any pitch |
| Follow-up on a quote against a cheaper competitor (sales) | outbound | Explaining the price gap with concrete items instead of a discount |
| Renewal with upgrade for an undecided restaurant owner (sales) | outbound | Getting a dated commitment |

`docs_get scenarios` ends with one of these, "Wrong items delivered to a family with an allergy", in the exact shape `scenarios_save` takes.
