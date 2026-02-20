# Model Evaluation

## Goal
Is the model good at the assigned task, in this case, generating coherent text?
- Is it fluent?
    - Grammar
    - Syntax
- Is it coherent?
    - Theme
    - Style
- Is it sensitive to context?
    - Does the prediction change based on changes to the context?
- What biases are present?
    - Harmful?
    - Helpful?

## Metrics
* Create automated metrics by using a test set.
* Abstract metrics, ex. loss.

## Human Evaluation
Slowest
**Rating scales**: Users rate a model's response on a scale (e.g., 1-5) for specific criteria like "Helpfulness" or "Factual accuracy."

**Side-by-side comparison**: A user is given the same prompt and two different responses (e.g., from Model A and Model B) and asked to choose which one is better and why. This is excellent for measuring relative improvements.

**Qualitative feedback**: Open-ended written feedback, explaining what they liked, what they disliked, and where the model failed. This can uncover unexpected problems or strengths.





