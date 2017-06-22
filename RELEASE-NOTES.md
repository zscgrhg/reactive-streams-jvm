# Release notes for Reactive Streams

---

# Version 1.0.1 released on YYYY-MM-DD

## Highlights:

- Added Glossary to Specification
- Improved TCK.
- Clarified rules with Intent-sections
- Better documentation.
- No breaking semantical changes.
- No new methods.

## Spec alterations

## Publisher Rule 1

1.0.0: The total number of onNext signals sent by a Publisher to a Subscriber MUST be less than or equal to the total number of elements requested by that Subscriber´s Subscription at all times.

1.0.1: The total number of onNext´s signalled by a Publisher to a Subscriber MUST be less than or equal to the total number of elements requested by that Subscriber´s Subscription at all times.

### Comment: Minor spelling update.

## Publisher Rule 2

1.0.0: A Publisher MAY signal less onNext than requested and terminate the Subscription by calling onComplete or onError.

1.0.1: A Publisher MAY signal fewer onNext than requested and terminate the Subscription by calling onComplete or onError.

### Comment: Minor spelling update.

## Publisher Rule 3

1.0.0: onSubscribe, onNext, onError and onComplete signaled to a Subscriber MUST be signaled sequentially (no concurrent notifications).

1.0.1: onSubscribe, onNext, onError and onComplete signaled to a Subscriber MUST be signaled in a thread-safe manner—and if performed by multiple threads—use external synchronization.

### Comment: Reworded the part about sequential signal and its implications, for clarity.

## Subscriber Rule 6

1.0.0: A Subscriber MUST call Subscription.cancel() if it is no longer valid to the Publisher without the Publisher having signaled onError or onComplete.

1.0.1: A Subscriber MUST call Subscription.cancel() if the Subscription is no longer needed.

### Comment: Rule could be reworded since it now has an intent section describing desired effect.

## Subscriber Rule 11

1.0.0: A Subscriber MUST make sure that all calls on its onXXX methods happen-before [1] the processing of the respective signals. I.e. the Subscriber must take care of properly publishing the signal to its processing logic.

1.0.1: A Subscriber MUST make sure that all calls on its signal methods happen-before the processing of the respective signals. I.e. the Subscriber must take care of properly publishing the signal to its processing logic.

### Comment: Rule slightly reworded to use the glossary for `signal` instead of the more *ad-hoc* name "onXXX methods". And footnote was reworked into the Intent-section of the rule.

## Subscription Rule 1

1.0.0: Subscription.request and Subscription.cancel MUST only be called inside of its Subscriber context. A Subscription represents the unique relationship between a Subscriber and a Publisher [see 2.12].

1.0.1: Subscription.request and Subscription.cancel MUST only be called inside of its Subscriber context.

### Comment: Second part of rule moved into the Intent-section of the rule.

## Subscription Rule 3

1.0.0: Subscription.request MUST place an upper bound on possible synchronous recursion between Publisher and Subscriber[1].

1.0.1: Subscription.request MUST place an upper bound on possible synchronous recursion between Publisher and Subscriber.

### Comment: Footnote reworked into the Intent-section of the rule.

## Subscription Rule 4

1.0.0: Subscription.request SHOULD respect the responsivity of its caller by returning in a timely manner[2].

1.0.1: Subscription.request SHOULD respect the responsivity of its caller by returning in a timely manner.

### Comment: Footnote reworked into the Intent-section of the rule.

## Subscription Rule 5

1.0.0: Subscription.cancel MUST respect the responsivity of its caller by returning in a timely manner[2], MUST be idempotent and MUST be thread-safe.

1.0.1: Subscription.cancel MUST respect the responsivity of its caller by returning in a timely manner, MUST be idempotent and MUST be thread-safe.

### Comment: Footnote reworked into the Intent-section of the rule.

## Subscription Rule 13

1.0.0: While the Subscription is not cancelled, Subscription.cancel() MUST request the Publisher to eventually drop any references to the corresponding subscriber. Re-subscribing with the same Subscriber object is discouraged [see 2.12], but this specification does not mandate that it is disallowed since that would mean having to store previously cancelled subscriptions indefinitely.

1.0.1: While the Subscription is not cancelled, Subscription.cancel() MUST request the Publisher to eventually drop any references to the corresponding subscriber.

### Comment: Second part of rule reworked into the Intent-section of the rule.

## Subscription Rule 15

1.0.0: Calling Subscription.cancel MUST return normally. The only legal way to signal failure to a Subscriber is via the onError method.

1.0.1: Calling Subscription.cancel MUST return normally.

### Comment: Replaced second part of rule with a definition for `return normally` in the glossary.

## Subscription Rule 16

1.0.0: Calling Subscription.request MUST return normally. The only legal way to signal failure to a Subscriber is via the onError method.

1.0.1: Calling Subscription.request MUST return normally.

### Comment: Replaced second part of rule with a definition for `return normally` in the glossary.

## Subscription Rule 17

1.0.0: A Subscription MUST support an unbounded number of calls to request and MUST support a demand (sum requested - sum delivered) up to 2^63-1 (java.lang.Long.MAX_VALUE). A demand equal or greater than 2^63-1 (java.lang.Long.MAX_VALUE) MAY be considered by the Publisher as “effectively unbounded”[3].

1.0.1: A Subscription MUST support an unbounded number of calls to request and MUST support a demand up to 2^63-1 (java.lang.Long.MAX_VALUE). A demand equal or greater than 2^63-1 (java.lang.Long.MAX_VALUE) MAY be considered by the Publisher as “effectively unbounded”.

### Comment: Rule simplified by defining `demand` in the glossary, and footnote was reworked into the Intent-section of the rule.

---