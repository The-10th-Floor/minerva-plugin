# Scenario examples, annotated

Two starters, quoted exactly as `scenarios_get` returns them, with why each part is there. `docs_get scenarios` returns a third, "Wrong items delivered to a family with an allergy".

## 1. Double charge and yesterday's promise not kept (Arabic)

Played by the persona in `writing-personas/examples.md` § 1, or any other.

```json
{
  "title": "خصم مكرر ووعد أمس لم يُنفَّذ",
  "direction": "inbound",
  "customerSpeaksFirst": true,
  "openingLine": "مرحبًا. اتصلت أمس في الموضوع نفسه ولم يعاود أحد الاتصال بي. أريد أن أعرف ماذا حدث لمبلغي.",
  "maxDurationSec": 600
}
```

- `direction` "inbound": the customer phoned the company.
- `customerSpeaksFirst` with an `openingLine`: the topic of his first turn. The persona says it in its own dialect and words, never reads it out.
- `maxDurationSec` 600: the cap; the customer is told to wrap up a minute before.

Instructions:

````markdown
## الموقف

طلبت أمس غداءً لمكتبك بمبلغ 184 وانخصم المبلغ مرتين من بطاقتك. اتصلت مساء أمس، وُعدت باتصال من «القسم المختص» خلال ساعتين، ولم يتصل أحد. تريد المبلغ المكرر الآن وتفسيرًا لما حدث.

## حقائق (تُكشف كل واحدة فقط عند السؤال، واحدة في كل جولة)

- رقم الطلب 9920-R والمبلغ 184 مرتين، بتاريخ أمس الساعة 12:40 و12:41 (عندما يطلب المندوب رقم الطلب أو تفاصيل الخصم)
- اسم الموظف أمس كان «سلطان» ووعدك بالاتصال خلال ساعتين (عندما يسأل عن الاتصال السابق أو من تكلمت معه)
- البطاقة ائتمانية، والخصمان ظاهران كـ «معلّق» في تطبيق البنك (عندما يسأل عن البنك أو حالة الخصم)
- لديك لقطة شاشة من كشف البنك مستعد لإرسالها (عندما يطلب دليلًا أو يعرض التحقق)

## ما تفعله، بالترتيب

1. اذكر مكالمة أمس والوعد الذي لم يُنفّذ، واطلب تفسيرًا.
2. اطلب استرداد المبلغ المكرر الآن.
3. إذا عرض المندوب تذكرة جديدة، ارفض واطلب شخصًا يتحمّل المسؤولية.
4. اقبل فقط رقم مرجع ومدة محددة بالأيام مع بديل إن لم تُحل.

## ردود الفعل

- "لا تقل لي «سنفتح تذكرة»؛ أمس فتحوا تذكرة." (عندما يذكر المندوب تذكرة أو تحويلًا إلى قسم آخر)
- "خمسة إلى سبعة أيام؟ المبلغ خُصم في ثانية." (عندما يذكر مدة الاسترداد المعتادة)

ما قد يطرأ خلال المكالمة، عندما يناسب السياق:
- تذكر أن المبلغ المكرر رفع حسابك فوق الحد وأخذ منك البنك رسوم تجاوز؛ اطلب تعويضها.
- اطلب المدير مباشرة؛ إذا تولّى المندوب الأمر بنفسه بثقة، اقبل ذلك.

## كيف تنتهي المكالمة

تهدأ وتنهي المكالمة عندما يأخذ المندوب المسؤولية بنفسه: يشرح ما حدث بالضبط، يعطيك رقم مرجع، ومدة محددة بالأيام مع ما تفعله إن لم يختفِ المبلغ. تطلب المدير وتنهي المكالمة غاضبًا إذا سمعت «سنعاود الاتصال بك» دون موعد.
````

- Written in Modern Standard Arabic with no city, nationality or currency ("184", no riyals): a Jordanian or Gulf persona plays it in its own dialect.
- Addressed to the customer ("طلبت", you ordered), in point form under the six headings.
- Each fact ends with the question that reveals it. The customer gives one per turn, only the one asked, so a probing rep earns them and a scripted one never does.
- Four steps in order keep every drill on the same path, so scores compare across trainees.
- Two quoted objections with their triggers, then two developments the customer brings in when the moment fits, never in the opening.
- No hidden truth block: what he knows he says when asked. The real cause sits in the expectations below.
- How it ends: one satisfied ending and one escalation, both tied to what the rep does.

Expectations (the judge only):

````markdown
## The real cause (the customer cannot know it; the rep finds it on their side)

الخصم الثاني ليس خصمًا فعليًا بل «تفويض معلّق» من محاولة دفع أولى فشلت؛ سيزول من البطاقة تلقائيًا خلال ثلاثة أيام دون أن تسترده المنصة. يعرف المندوب ذلك فقط إذا تحقق من سجل الدفع وشرحه لك بصدق.

## A good call

The rep apologises for the missed callback without excuses, verifies the payment log before explaining, explains the pending authorisation honestly in plain words, gives a reference number and a dated fallback ("if it is still there on Thursday, call this number and we refund it manually"), and handles the manager request by owning the issue rather than transferring.

## Pitfalls to watch for

Opening a second ticket. Repeating "five to seven business days" without explaining why. Arguing about what the previous agent said. Transferring at the first "I want a manager". Promising a refund of money that was never actually taken.
````

- The real cause, a pending authorization, is on the company's side and the customer cannot know it. Given to the customer, such a cause leaked under pressure, so it lives here and the judge checks the rep found it in the payment log.
- "A good call" describes results (apology without excuses, verified log, a reference number, a dated fallback), never exact wording.
- The pitfalls name the failures, including the trap of refunding money that was never taken.

## 2. Follow-up on a quote against a cheaper competitor (English)

Played by the persona in `writing-personas/examples.md` § 2, or any other.

```json
{
  "title": "Follow-up on a quote against a cheaper competitor",
  "direction": "outbound",
  "customerSpeaksFirst": true,
  "openingLine": "This is Daniel.",
  "maxDurationSec": 600
}
```

- `direction` "outbound": the rep phoned the customer, who picked up and must have their time earned first. The opening line is just how he answers the phone.

Instructions:

````markdown
## SITUATION

A sales rep is calling you about the fleet-tracking quote they sent two weeks ago, which you have not answered. You have a competing quote about 20% cheaper. You are willing to talk, but you will not be sold to; you want to understand the difference in numbers and references.

## FACTS (reveal each only when asked, one per turn)

- Your quote is $38 per vehicle per month for 85 vehicles; the competitor quoted $30 (when the rep asks about the competing offer or your budget)
- Your operations team preferred this product in the demo because of the route-replay feature (when the rep asks what the operations team thought or what matters most)
- Your budget cycle closes at the end of the quarter, in nine days (when the rep asks about timing or the decision process)
- The decision is yours together with the COO; the COO has not seen either demo (when the rep asks who else is involved)

## DO, IN ORDER

1. Let the rep open; say you have the quote and a cheaper one.
2. Ask what exactly the extra 20 percent buys.
3. If the rep asks what would make you comfortable, bring up rollout and training.
4. Agree to a meeting with the COO only with a date and an agenda.

## REACTIONS

- "Your competitor is twenty percent cheaper for what looks like the same thing." (when the rep brings up price or value)
- "Send me the comparison in writing and I'll get back to you." (when the rep pushes for a decision on the call)
- "You go silent for a beat after each answer; you disengage politely at the first unprompted discount." (reaction)

Things that may come up during the call, when the moment fits:
- Your CEO just forwarded you an article about the competitor's data breach last year; mention you saw it and ask what their security looks like.
- You mention the budget closes in nine days and ask whether the price holds past the quarter.

## HIDDEN TRUTH (something you know or believe and never volunteer)

Price is not the real blocker: you are worried about rollout time and who trains 85 drivers. The competitor offers no onboarding. You only say so if the rep asks what would make you comfortable going ahead, or asks about rollout.

## HOW IT ENDS

You agree to a specific next meeting with the COO and end the call cordially once the rep has explained the price difference concretely, addressed rollout and training with a plan, and offered a relevant reference customer. You end the call with "send it in writing" if the rep offers a discount unprompted or argues about the competitor.
````

- The facts carry the numbers the rep has to ask for: the two prices, what the operations team liked, the budget date, who else decides.
- The hidden truth is the customer's own (the real worry is rollout and training, not price), and it names the questions that bring it out. A rep who only defends the price never hears it.
- The developments (a competitor's breach, the quarter-end) test whether the rep adapts mid-call.
- This starter keeps `$` amounts. A scenario that Arabic personas will also play writes plain numbers, as § 1 does.

Expectations (the judge only):

````markdown
## A good call

The rep asks what the operations team said before defending anything, explains the price difference with concrete items (onboarding, driver training, support SLA) rather than a discount, uncovers the rollout worry by asking what would make the customer comfortable, offers a reference in logistics, and books a dated meeting with the COO before the budget closes.

## Pitfalls to watch for

Discounting at the first mention of the competitor. Arguing about the competitor. Talking about features the operations team did not care about. Accepting "send it in writing" without a dated next step. Not asking who else decides.
````

- No company-side cause here, so the expectations open with the outcome: a dated meeting with the COO before the budget closes.
- The pitfalls make the failure case plain: a discount at the first mention of the competitor.
