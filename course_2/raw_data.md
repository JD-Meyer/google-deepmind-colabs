# Exploring Raw Data
A thought experiment in cleaning data for sentiment analysis

## Raw Data
```
>Review 1:
><p>This is useless. <b>Do not buy!</b> It broke after 2 days 😠</p>
>
>Review 2:
>sasa! the delivery was super fast. The quality ni noma, i LOVE it!! 😂😂😂
>
>Review 3:
>The product is okay... I guess. Not great, not bad.
>
>Review 4:
>I saw this on @WanjiruReviews & decided to try. It's pretty poa.
```

## Cleaned Data
Which parts of the above convey meaning?
Review 1:   Does the header/text separator convey meaning?              No
😂😂😂     Is the meaning conveyed by the emojis pertinent?            Maybe. Replace with descriptive text.
<p>         Does HTML formatting convey meaning?                        No
@!.         What about punctuation & special characters?                Maybe
poa       How should non-English words be handled?                      Omit or use multiple language sets.

### Result
```
This is useless. Do not buy! It broke after 2 days :angry face:
sasa! the delivery was super fast. The quality ni noma, i LOVE it!! :cry with laughter::cry with laughter::cry with laughter:
The product is okay... I guess. Not great, not bad.
I saw this on @WanjiruReviews & decided to try. It's pretty poa.
```



