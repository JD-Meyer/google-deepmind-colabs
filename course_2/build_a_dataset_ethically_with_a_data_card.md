# Build a Dataset Ethically with a Data Card

### The Task: Revisit the problem statement from Chapter 1.
The gap between teaching and learning causes many children to become marginalized adults.
Critics of our education system complain that students become disinterested because the material is
1. Irrelevant to the student's needs
2. Poorly presented
3. Inappropriate for students with disabilities
4. Prioritizes metrics over learning

What dataset would I need for my model to work effectively?
1. Detailed histories of specific geographical regions during specific eras including.
   - Politics
   - Religion
   - Economics
   - Social mechanics
   - Architecture
   - Maps
   - Education

The LLM needs to be knowledgeable about all aspects of life in a given period.
I use the example of Elizabethan England in my problem statement.
The model needs to be an expert in the 
- history of the royal court, 
- quotidian matters of daily life
- economics, including trade and the effects of political events

## Data card
| Type                  | Problem                                                           | Response                                                                                     |
|-----------------------|-------------------------------------------------------------------|----------------------------------------------------------------------------------------------|
| Input                 | What is the user input?                                           | Users will input audio and text.                                                             |
| Output                | What outputs/labels will the model generate?                      | Text, images, video                                                                          |
| Classification        | What classification tasks are involved?                           | Classifying information based on relevance to the current topic                              |
|                       | What categories of classes am I working with?                     | Social/economic effects, gender, military engagements, political manuevering                 |
|                       | Why?                                                              | In order to understand how events are related.                                               |
| Labeling              | Where do labels come from?                                        | Domain experts, history books, historical fiction, Ai-generated sources                      |
|                       | How do I check for consistency and accuracy?                      | Crowdsource/beta test.                                                                       |
| Data Creation         | How do I collect the data?                                        | Using the same data sources used to train commercial LLMs                                    |
|                       | Will it come from direct sources?                                 | No.                                                                                          |
| Web collection ethics | Will I source data from the web?                                  | No.                                                                                          |
|                       | Which sites/platforms?                                            | NA                                                                                           |
|                       | What tools will I use?                                            | NA                                                                                           |
|                       | Have I addressed issues of consent, copyright, and privacy?       | Copyright issues need to be addressed.                                                       |
| Bias & Representation | Who might be left out?                                            | Women, the lower social classes, and other marginalized groups.                              |
|                       | How will I ensure that the dataset reflects the diversity of      | Histories are frequently written by and about the wealthy and powerful.                      |
|                       | the community and includes underrepresented voices?               | I may need to resort to creative fiction to tell the story.                                  |
| Values & Community    | How does the dataset reflect the values I identified in Course 1? | The dataset provides a more immersive experience for students than history books provide.    |
| Alignment             | How will my community benefit from it?                            | Engaged children grow up to become engaged, productive adults.                               |
|                       |                                                                   | They will have more tools to address current social needs.                                   |



