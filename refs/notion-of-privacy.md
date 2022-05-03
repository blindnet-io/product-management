> The purpose of this document is to list definitions of privacy and related notions, sourced from literature, and provide fundamental understanding about the key concepts of interests for blindnet. 
> 
> We are interested in privacy from a perspective of builders of computer systems, who have to account for the human, its psychology and relationships with other humans and with the machines. 
> 
> In this document, we are not interested in the general perspectives related to politics, democracy and justice other than those views and findings that directly impact the building of a software system made for humans.


## General Notion of Privacy

### Definition
Among the many definitions proposed in scientific literature, we use the following one:

> **“Privacy is the selective control of access to the self”** - *Irwin Altman[^1]*

This definition captures the essential fetures of the concept, in particular:
- Privacy is about the **self**.

The *self* is a very important element of human experience playing *"an integral part in human motivation, cognition, affect, and social identity"*[^2]. 

The self is not the same as identity. While the *self is the totality of the individual*[^3], the *identity is an individual’s sense of self defined by (a) a set of physical, psychological, and interpersonal characteristics that is not wholly shared with any other person and (b) a range of affiliations (e.g., ethnicity) and social roles*[^4].

Some scientists challenge the ability of an indifidual to know the *self*, under which view the self might be only intelligible through its manifestations or consequences. It is generally accepted that the self is developed. Also, undoubtably, in part *"the self emerges through interaction with others"*[^5].

Due to the relational provenance of the knowledge of the self, privacy is one of the key features of the relationship of oneself with the surrounding world (other humans and artefacts) through which the knoweledge of the self is formed. Privacy is a "factor of connection to oneself and to others"[^6].


- Privacy is about **control of access**.

As relationships play a key role in shaping the view on the self, it is of crucial importance for the individual to control the access to self, and thus maintain control over the change of the self. That is the function of Privacy.

- Privacy is **selective**.

It is not an absolute binary "come in" vs. "go away". It is a nuanced choice to control access to parts of the *self*.

### Genesis and Function

Privacy seems to trace its origins in biological processes, and "withdrawal from others is ubiquitous across the animal kingdom"[^7]. Researchers make an anlogy with cell membrane[^1] that seletively allows material inputs and outputs, similarly as privacy selectively regulates external stimulation to one's self or the flow of information to others[^7].

Biology research suggests that, in social species, privacy might have emerged as the cost-benefit balance between the advantages offered by the life in a group and the interest of the individual's competition over scarce resources. The practice of witholding information or actively sending deceiving signals might have have origins in a survival mechanism i.e. sending away the individuals competing for the same resources. *"By increasing another idividual's misinformation about the environment, an animal may increase its own fitness"*[^7].

In such primitive groups, privacy emerges as a strategy to establish **information asymmetry**[^8] and compensate for the power disbalance among individuals. It is thus possible that the need for privacy in modern society remains still linked to the power differential. Without privacy and the information asymmetry it creates, and individual is made vulnerable and its ability to ensure fitness for survival is diminished.

Compelling animals to remain inn contact contrary to their own privacy inclinations, in laboratory settings, has resulted in physiological changes, reproductive failure and adrenal dysfunction[^7].

Beyond the privacy of an individual, privacy also has a group-preserving function in the relationship between one group to another[^15].

### Privacy and Other Topics

#### Privacy and Information Asymmetry

Information asymmetry[^8] is clearly a key concept for privacy as identified by biological studies of privacy in animal societies. 

In the context of a power differential, where an individual interacts with a more powerful entity, the need for management of information asymmetry is twofold:
- reduce the information given by the less powerfull
- increase the transparency about about what the more powerful does with the information obtained. [^9]

Indeed, in order to selectively control the access to self, the individual has to know what the other party will do if given access to a part of the self. This two-way understanding of the information asymmetry that privacy seeks to create is the ground on which the legislation around *data minimization*, *transparency of treatment* and *consent* is formed.


#### Privacy vs Loneliness/Isolation
Humans are social species, hardwired for connection. 
>**"Connection is the energy that exists between people when they feel seen, heard and valued; when they can give and receive without judgement; and when they derive sustenance and strength from the relationship."** —*Brené Brown*
It is crucial to development; without it, social animals experience distress and face severe developmental consequences[^10].

Privacy is not a tool to reduce connection and favor isolation (which leads to loneliness - correlated with negative effects on health[^11]). On the contrary, privacy is a necessary element of connection making connection compatible with survival in the natural context of power differential and scarce resources.

#### Privacy and Trust
> **“Trust is choosing to make something important to you vulnerable to the actions of someone else.”** - *Charles Feldman*

Privacy is strongly linked with trust. Because privacy is about the access to *self*, and self is clearly of great importance, an individual is expected to choose a particular level of privacy in relation to the level of trust.

#### Privacy and Identity

As we derive the knoweledge of self from our relationships with others, the freedom to engage and disengage from those relationships and selectively allow access to self is crucial to our ability to keep our identity safe. At the psychological level, privacy supports social interaction which, in turn,
provides feedback on our competence to deal with the world which, in turn, affects our self-definition[^1][^16].

Inability to obtain privacy has important psychological consequences[^16].

#### Privacy Paradox
The privacy paradox is a phenomenon in which online users state that they are concerned about their privacy but behave as if they were not.[^12] Anecdotal and empirical evidence indicate that individuals are willing to trade their personal information for relatively small rewards[^14].

However, as we have seen, privacy regulates the conflic of the need for connection with the need for competition, survival and overcoming the power diferential. Habits, and other needs, indeniably play a role in the persons choice of privacy related behavior and may yeald behavior inconsistent with the persons beliefs and interests (as outlined by the *privacy paradox*).

The existance of the privacy paradox is not indicative of a false concern for privacy, but rather of the context not favoring behavior aligned with this concern, as is common with attitude-behavior gap[^13].

## Privacy in Software Systems


[^1]: Altman I (1975) The environment and social behavior. Wadsworth, Belmont
[^2]: Sedikides, C. & Spencer, S.J. (Eds.) (2007). The Self. New York: Psychology Press
[^3]: [Self in APA Dictionary](https://dictionary.apa.org/self)
[^4]: [Identity in APA Dictionary](https://dictionary.apa.org/identity)
[^5]: Colin Fraser, "Social Psychology" in Richard Gregory, The Oxford Companion to the Mind (Oxford 1987) p. 721-2
[^6]: Darhl M.Pedersen, [PSYCHOLOGICAL FUNCTIONS OF PRIVACY](https://www.sciencedirect.com/science/article/abs/pii/S0272494497900499)
[^7]: Peter H. Klopfer & Daniel I Rubenstein [The Concept Privacy and Its Biological Basis](https://www.researchgate.net/profile/Daniel-Rubenstein/publication/227655770_The_Concept_Privacy_and_Its_Biological_Basis/links/5ba4eb2045851574f7dbcb99/The-Concept-Privacy-and-Its-Biological-Basis.pdf)
[^8]: [Information Asymmetry](https://en.wikipedia.org/wiki/Information_asymmetry)
[^9]: [Mininal Information Asymmetry](https://privacypatterns.org/patterns/Minimal-Information-Asymmetry)
[^10]: Jaak, Panksepp (2004). Affective Neuroscience : the Foundations of Human and Animal Emotions. Oxford University Press. 
[^11]: [Loneliness](https://en.wikipedia.org/wiki/Loneliness)
[^12]: Bedrick, B., Lerner, B., Whitehead, B. "The privacy paradox: Introduction", "News Media and the Law", Washington, DC, Volume 22, Issue 2, Spring 1998, pp. P1–P3.
[^13]: [Attitude-behavior gap](https://en.wikipedia.org/wiki/Value-action_gap)
[^14]: Spyros Kokolakis [Privacy attitudes and privacy behaviour: A review of current research on the privacy paradox phenomenon] (https://www.researchgate.net/profile/Spyros-Kokolakis/publication/280244291_Privacy_attitudes_and_privacy_behaviour_A_review_of_current_research_on_the_privacy_paradox_phenomenon/links/5a1bdb5a4585155c26ae08e2/Privacy-attitudes-and-privacy-behaviour-A-review-of-current-research-on-the-privacy-paradox-phenomenon.pdf)
[^15]: Barry Schwartz, [The_Social_Psychology_of_Privacy](https://www.researchgate.net/profile/Barry-Schwartz-2/publication/17491080_The_Social_Psychology_of_Privacy/links/583315c408aef19cb81c8c80/The-Social-Psychology-of-Privacy.pdf)
[^16]: Stephen T. Margulis, [Privacy as a Social Issue and Behavioral Concept](http://www.sfu.ca/~palys/Margulis-2003-PrivacyAsASocialIssue&BehavioralConcept.pdf)
