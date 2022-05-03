# Notions of Privacy

> The purpose of this document is to list definitions of privacy and related notions, sourced from literature, and provide fundamental understanding about the key concepts of interest for blindnet. 
> 
> We are interested in privacy from a perspective of builders of computer systems, who have to account for the human, its psychology and relationships with other humans and with the machines. 
> 
> In this document, we are not interested in the general perspectives related to politics, democracy and justice other than those views and findings that directly impact the building of a software system made for humans.


## Definition
Among the many definitions proposed in scientific literature, we use the following one:

> **“Privacy is the selective control of access to the self”** - *Irwin Altman[^1]*

This definition captures the essential features of the concept, in particular:
- Privacy is about the **self**.

The *self* is a very important element of human experience playing *"an integral part in human motivation, cognition, affect, and social identity"*[^2]. 

The self is not the same as identity. While the *self is the totality of the individual*[^3], the *identity is an individual’s sense of self defined by (a) a set of physical, psychological, and interpersonal characteristics that is not wholly shared with any other person and (b) a range of affiliations (e.g., ethnicity) and social roles*[^4].

Some scientists challenge the ability of an individual to know the *self*. Under this view the self might only be intelligible through its manifestations or consequences. It is generally accepted that the self is developed over time. Also, undoubtably, in part *"the self emerges through interaction with others"*[^5].

Due to the relational provenance of the knowledge of the self, privacy is one of the key features of the relationship of oneself with the surrounding world (other humans and artefacts) through which the knowledge of the self is formed. Privacy is a "factor of connection to oneself and to others"[^6].


- Privacy is about **control of access**.

As relationships play a key role in shaping the view on the self, it is of crucial importance for the individual to control the access to self, and thus maintain control over the change of the self. That is the function of Privacy.

- Privacy is **selective**.

It is not an absolute binary "come in" vs. "go away". It is a nuanced choice to control access to parts of the *self*.

## Genesis and Function

Privacy seems to trace its origins in biological processes. "Withdrawal from others is ubiquitous across the animal kingdom"[^7]. Researchers make an analogy with cell membrane[^1] that selectively allows material inputs and outputs, similarly as privacy selectively regulates external stimulation to one's self or the flow of information to others[^7].

Biology research suggests that, in social species, privacy might have emerged as the cost-benefit balance between the advantages offered by the life in a group and the interests of the individual's competition over scarce resources. The practice of withholding information or actively sending deceiving signals might have had origins in a survival mechanism i.e. sending away the individuals competing for the same resources. *"By increasing another individual's misinformation about the environment, an animal may increase its own fitness"*[^7].

In such primitive groups, privacy emerges as a strategy to establish **information asymmetry**[^8] and compensate for the power disbalance among individuals. It is thus possible that the need for privacy in modern society remains still linked to the power differential. Without privacy and the information asymmetry it creates, an individual is made vulnerable and its ability to ensure fitness for survival is diminished.

Compelling animals to remain in contact contrary to their own privacy inclinations, in laboratory settings, has resulted in physiological changes, reproductive failure and adrenal dysfunction[^7].

Beyond the privacy of an individual, privacy also has a group-preserving function in the relationship between one group to another[^15].

## Privacy and Other Topics

### Privacy and Information Asymmetry

Information asymmetry[^8] is clearly a key concept for privacy as identified by biological studies of privacy in animal societies. 

In the context of a power differential, where an individual interacts with a more powerful entity, the need for management of information asymmetry is twofold:
- reduce the information given by the less powerfull
- increase the transparency about what the more powerful does with the information obtained. [^9]

Indeed, in order to selectively control the access to self, the individual has to know what the other party will do if given access to a part of the self. This two-way understanding of the information asymmetry that privacy seeks to create is the ground on which the legislation around *data minimization*, *transparency of treatment* and *consent* is formed.


### Privacy vs Loneliness/Isolation
Humans are social species, hardwired for connection. 

>**"Connection is the energy that exists between people when they feel seen, heard and valued; when they can give and receive without judgement; and when they derive sustenance and strength from the relationship."** —*Brené Brown*

It is crucial to development; without it, social animals experience distress and face severe developmental consequences[^10].

Privacy is not a tool to reduce connection and favor isolation (which leads to loneliness - correlated with negative effects on health[^11]). On the contrary, privacy is a necessary element of connection making connection compatible with survival in the natural context of power differential and scarce resources.

### Privacy and Trust
> **“Trust is choosing to make something important to you vulnerable to the actions of someone else.”** - *Charles Feldman*[^20]

Privacy is strongly linked with trust. Because privacy is about the access to *self*, and self is clearly of great importance, an individual is expected to choose a particular level of privacy in relation to the level of trust.

### Privacy and Identity

As we derive the knowledge of self from our relationships with others, the freedom to engage and disengage from those relationships and selectively allow access to self is crucial to our ability to keep our identity safe. 

At the psychological level:
- privacy supports social interaction,
- social interaction provides feedback on our competence to deal with the world,
- our competence to deal with the world affects our self-definition[^1][^16].

Inability to obtain privacy has important psychological consequences ranging from embarrassment and stigma to de-individuation and dehumanization[^16].

### Privacy Paradox
The privacy paradox is a phenomenon in which online users state that they are concerned about their privacy but behave as if they were not.[^12] Anecdotal and empirical evidence indicate that individuals are willing to trade their personal information for relatively small rewards[^14].

However, as we have seen, privacy regulates the conflict of the need for connection with the need for competition, survival and overcoming the power diferential. Habits, and other needs, indeniably play a role in the persons choice of privacy related behavior and may yeald behavior inconsistent with the persons beliefs and interests (as outlined by the *privacy paradox*)[^18].

The existance of the privacy paradox is not indicative of a false concern for privacy, but rather of the context not favoring behavior aligned with this concern, as is common with attitude-behavior gap[^13]. Researchers consider privacy-oblivious behavior to be a result of technological limitations as much as a consequence of users’ deficiencies[^19].

### Privacy Fatigue
Privacy fatigue reflects a sense of weariness toward privacy issues, in which individuals believe that there is no effective means of managing their personal information on the internet[^21].

This fatigue, brought on by casual data breaches and the complexity of online privacy control, can reduce users’ attention to privacy issues. Yet, being consistently exposed to a mismatch between what one hopes for and what the environment affords leads to increased psychological strain[^21].

Privacy fatigue is closely related to the concept of *learned helplessness*[^23]. Learned helplessness is the behavior exhibited by a subject after enduring repeated aversive stimuli beyond their control. The subject affected by this phenomenon discontinues attempts to escape or avoid the aversive stimulus, even when such alternatives are unambiguously presented. Learned helplessness is linked to a degraded self-efficacy - the individual's belief in their innate ability to achieve goals. Researchers suggest that clinical depression and related mental illnesses may result from a real or perceived absence of control over the outcome of a situation[^24].

Indeed, privacy is related to identity, and to our perception of our own competence to deal with the world[^1][^16]. Repetetive exposure to technological limitations[^19], as well as the privacy paradox attitude-behavior gap[^12] might situate the explanation of privacy fatigue in the scope of learned helplessness.

## Privacy in Software Systems

Software Systems, and especially the ones operating over the internet, put an individual in a situation of *need* to control the access to self, naturally enabled by the context of use of such systems. The user has to balance the need for connection (ranging from simple information gathering, over social interactions to economic transactions) with the need for protection of the self from unwanted connection, harm and abuse.

Having control (having the system respond predictably to user's actions) is one of the key features a user can expect from a properly designed human-computer interaction[^17].

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
[^14]: Spyros Kokolakis [Privacy attitudes and privacy behaviour: A review of current research on the privacy paradox phenomenon](https://www.researchgate.net/profile/Spyros-Kokolakis/publication/280244291_Privacy_attitudes_and_privacy_behaviour_A_review_of_current_research_on_the_privacy_paradox_phenomenon/links/5a1bdb5a4585155c26ae08e2/Privacy-attitudes-and-privacy-behaviour-A-review-of-current-research-on-the-privacy-paradox-phenomenon.pdf)
[^15]: Barry Schwartz, [The_Social_Psychology_of_Privacy](https://www.researchgate.net/profile/Barry-Schwartz-2/publication/17491080_The_Social_Psychology_of_Privacy/links/583315c408aef19cb81c8c80/The-Social-Psychology-of-Privacy.pdf)
[^16]: Stephen T. Margulis, [Privacy as a Social Issue and Behavioral Concept](http://www.sfu.ca/~palys/Margulis-2003-PrivacyAsASocialIssue&BehavioralConcept.pdf)
[^17]: Shneiderman, [Eight Golden Rules of Interface Design](http://www.cs.umd.edu/~ben/goldenrules.html)
[^18]: Alessandro Acquisti, [Privacy in Electronic Commerce and the Economics of Immediate Gratification](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.580.5737&rep=rep1&type=pdf)
[^19]: Jochen Peter and Patti M. Valkenburg, [Adolescents’ Online Privacy: Toward a Developmental Perspective](https://www.researchgate.net/profile/Patti-Valkenburg/publication/279190144_Adolescents'_Online_Privacy_Toward_a_Developmental_Perspective/links/567028d208ae2b1f87acd4ce/Adolescents-Online-Privacy-Toward-a-Developmental-Perspective.pdf)
[^20]: Charles Feltman, The Thin Book of Trust: An Essential Primer for Building Trust at Work
[^21]: Hanbyul Choia, Jonghwa Parka, Yoonhyuk Jung, [The role of privacy fatigue in online privacy behavior](https://iranarze.ir/wp-content/uploads/2018/04/E6393-IranArze.pdf)
[^23]: [Learned Helplessness](https://en.wikipedia.org/wiki/Learned_helplessness)
[^24]: Seligman ME (1975). Helplessness: On Depression, Development, and Death. San Francisco: W. H. Freeman
