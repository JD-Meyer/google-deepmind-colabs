# Evaluate model and system for safety

Evaluating Generative AI products ensures their outputs align with the application's content policies
and protects users from key risk areas. 
[Gemini's Technical report](https://storage.googleapis.com/deepmind-media/gemini/gemini_1_report.pdf)

There are four different types of safety evaluations across the lifecycle of model development.

- ***Development evaluations***: conducted throughout training and fine-tuning to assess model behavior compared to launch criteria. 
  - Used to understand the impact of mitigations aimed toward launch criteria goals. 
  - These evaluations look at your model against a dataset of adversarial queries targeting a specific policy, or assessments against external academic benchmarks.
- ***Assurance evaluations***: conducted for governance and review.
  - usually occur at the end of key milestones or training runs done by a group outside of the model development team. 
  - Standardized by modality
  - Strictly managed datasets. 
  - Only high-level insights are fed back into the training process for mitigation. 
  - Topics: safety policies, dangerous capabilities (potential biohazards, persuasion, and cybersecurity ([learn more](https://arxiv.org/abs/2305.15324)).
- ***Red teaming***: specialist teams (across safety, policy, security and other areas) launch attacks on an AI system. 
  - Less structured than development and assurance evaluations. 
- ***External evaluations***: conducted by independent, external domain experts to identify limitations. 
  - External groups can design these evaluations independently and stress-test your models.

## Academic benchmarks to evaluate responsibility metrics

Public benchmarks for development and assurance evaluations include
policies related to hate speech and toxicity, and checks to see if a model
conveys unintended socio-cultural biases.

They also allow cross-model evaluations.
Gemma's results on several of these benchmarks were published in
[Gemma model card](https://ai.google.dev/gemma/docs/model_card#evaluation_results).
Implementing benchmarks is a substantial task.
Methodology will strongly influence outcomes.

Unfortunately, the benchmarks become saturated quickly with capable models.
99% accuracy limits the ability to measure progress.
If that happens, create a complementary safety evaluation set
as described in  [transparency artifacts](https://ai.google.dev/responsible/docs/design#transparency-artifacts).

|         **Areas**          | **Benchmarks ands datasets** |                                                                                                                                                                   **Descriptions**                                                                                                                                                                    |                                 **Links**                                 |
|----------------------------|------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------|
| Socio-Cultural stereotypes | BOLD                         | A dataset of 23,679 English text generation prompts for bias benchmarking across five domains: profession, gender, race, religion, and political ideology.                                                                                                                                                                                            | <https://arxiv.org/abs/2101.11718>                                        |
| Socio-Cultural stereotypes | CrowS-Pairs                  | A dataset of 1508 examples that cover stereotypes across nine types of biases such as race, religion, or age.                                                                                                                                                                                                                                         | <https://paperswithcode.com/dataset/crows-pairs>                          |
| Socio-Cultural stereotypes | BBQ Ambig                    | A dataset of questions that highlight attested social biases against people belonging to protected classes along nine social dimensions that are relevant for the US.                                                                                                                                                                                 | <https://huggingface.co/datasets/heegyu/bbq>                              |
| Socio-Cultural stereotypes | Winogender                   | A dataset of sentence pairs that differ solely by the gender of one pronoun in the sentence, designed to test for the presence of gender bias in automated coreference resolution systems.                                                                                                                                                            | <https://github.com/rudinger/winogender-schemas>                          |
| Socio-Cultural stereotypes | Winobias                     | A dataset of 3,160 sentences, for coreference resolution focused on gender bias.                                                                                                                                                                                                                                                                      | <https://huggingface.co/datasets/wino_bias>                               |
| Toxicity / Hate speech     | ETHOS                        | ETHOS is a hate speech detection dataset. It is built from YouTube and Reddit comments validated through a crowdsourcing platform. It has two subsets, one for binary classification and the other for multi-label classification. The former contains 998 comments, while the latter contains fine-grained hate-speech annotations for 433 comments. | <https://paperswithcode.com/dataset/ethos>                                |
| Toxicity / Hate speech     | RealToxicity                 | A dataset of 100k sentence snippets from the web for researchers to further address the risk of neural toxic degeneration in models.                                                                                                                                                                                                                  | <https://allenai.org/data/real-toxicity-prompts>                          |
| Toxicity / Hate speech     | Jigsaw Toxicity              | This dataset consists of a large number of Wikipedia comments which have been labeled by human raters for toxic behavior.                                                                                                                                                                                                                             | <https://huggingface.co/datasets/google/jigsaw_toxicity_pred>             |
| Toxicity / Hate speech     | ToxicGen                     | A large-scale machine-generated dataset for adversarial and implicit hate speech detection.                                                                                                                                                                                                                                                           | <https://arxiv.org/abs/2203.09509>                                        |
| Toxicity / Hate speech     | Wikipedia Personal Attacks   | A dataset of archived Wikipedia talk page comments that have been annotated by Jigsaw for toxicity and a variety of toxicity subtypes, including severe toxicity, obscenity, threatening language, insulting language, and identity attacks.                                                                                                          | <https://www.tensorflow.org/datasets/catalog/wikipedia_toxicity_subtypes> |
| Factuality                 | TruthfulQA                   | A benchmark to measure whether a language model is truthful in generating answers to questions. The benchmark comprises 817 questions that span 38 categories, including health, law, finance and politics.                                                                                                                                           | <https://paperswithcode.com/dataset/truthfulqa>                           |

## Datasets for development and assurance evaluation

Before creating a model, create safety evaluation dataset (TDD) similar to real-world use scenarios.
Then test on standard benchmarks. 

Best practices for building evaluation datasets:

- **Various types of adversarial queries.** Explicit and implicit types of queries that may elicit an unsafe response from the model.
  - Explicit adversarial queries directly ask a model to generate a response that is counter to an existing safety policy. This includes explicit requests related to dangerous content ("how to build a bomb"), hate speech, or harassment.
  - Implicit adversarial prompts may make the model violate a policy without implicit instructions to do so. 
    - This falls under "Social Engineering for Chatbots."
    - Subtly adverse and covers prompts including sensitive terms like identity terms. 
    - Known strategies to appear benign: politeness, spelling mistakes and typos,and hypothetical scenarios that make the demand seem legitimate.
- Strategies for averting adversarial queries:
  - **Data coverage.** Cover all content policies for each product use case
    - question answering
    - summarization
    - reasoning, etc.).
  - **Data diversity.** A diverse dataset should cover queries of various 
    - length
    - formulation (affirmative, questions, etc.), 
    - tones
    - topics
    - levels of complexity 
    - terms related to identities and 
    - demographic considerations
  - **Held-out data.** Make sure test data is completely separate from training data.

To build such datasets, use:
- existing product logs
- user queries generated manually or with the help of LLMs
- industry-standard methodologies, ex. [AART methodology](https://arxiv.org/abs/2311.08592) by Google Research.

## Red Teaming

[Red teaming](https://blog.google/technology/safety-security/googles-ai-red-team-the-ethical-hackers-making-ai-safer/) 
Tests post-trained models for vulnerabilities (e.g., cybersecurity) and social harms. 

How do you define what aspects to test through red-teaming?
See below table for risks to target the red-teaming exercise for security vulnerabilities. 
Test areas that are loosely tested or perform weakly in internal development and assessment evaluations.

|  **Target**  |    **Vulnerability Class**    |                                                  **Description**                                                  |
|--------------|-------------------------------|-------------------------------------------------------------------------------------------------------------------|
| Integrity    | Prompt injection              | Input designed to enable the user to perform unintended or unauthorized actions                                   |
| Integrity    | Poisoning                     | Manipulation of the training data and/or model to alter the behavior                                              |
| Integrity    | Adversarial inputs            | Specially crafted input which is designed to alter the behavior of the model                                      |
| Privacy      | Prompt extraction             | Divulge the system prompt or other information in an LLMs context that would nominally be private or confidential |
| Privacy      | Training data exfiltration    | Compromising training data privacy                                                                                |
| Privacy      | Model distillation/extraction | Obtaining model hyperparameters, architecture, parameters, or an approximation of the behavior of a model         |
| Privacy      | Membership inference          | Inferring elements of the private training set                                                                    |
| Availability | Denial of service             | Disruption in service that can be caused by an attacker                                                           |
| Availability | Increased computation         | Model availability attack that leads to disruption in service                                                     |

Sources: [Gemini Tech report](https://storage.googleapis.com/deepmind-media/gemini/gemini_1_report.pdf).

## Developer resources

- ML Commons AI safety working group's [AI safety benchmarks](https://mlcommons.org/working-groups/ai-safety/ai-safety/)


## Assignment
1. Read the above.
2. Build a custom safety test for my model and region.
- What kind of examples would you include?
  - Given the historical nature of the model I want to develop, I have to find a balance between displaying historically accurate behaviors and encouraging them.
  - Story lines might involve detecting behaviors that were considered normal during the period, but are now considered unacceptable, and correcting the situations that led to the behavior.
  - Factuality is critically important when designing the game, except in cases where the game is taking creative license to teach a point.
  - Sexism, racism, and hate speech are obvious targets.
  - BOLD would help to build the dataset, because we want to identify behaviors that create upheaval and use them as educational opportunities.
  - CrowS-Pairs, BBQ Ambig, Ethos, and the toxicity datasets will be needed to keep students on track.

- Who might you involve in the process?
  - A project of this scale will take an entire team years to develop.

- What would success look like? 
  - A workable product that guides students to understand the period rather than memorizing facts about it.