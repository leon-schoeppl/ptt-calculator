#### 1. Overview
Automated analysis of probabilistic truth-table tasks for studies on reasoning under uncertainty. Written as research assistant on [BMBF project <01UL1906X>](https://homepages.uni-regensburg.de/~pfn23853/LogWissUns.html) of Dr. Dr. Niki Pfeifer. At this point (Feb 2022) so-called dice tasks (see **3.**), and a slightly more general analysis for up to 10-case setups (see **2.**) have been implemented.

***
#### 2. PTT-Calculator
The current  version can be accessed for testing in the browser [here](https://leon-schoeppl.shinyapps.io/ptt-calculator/), hosted by *shinyapps.io*. If you want to actually work with the software, please download it and run it locally.

This small program is meant to assist in creating studies in which participants are asked to evaluate the probability point-values or uncertainty intervals of sentences featuring two propositions (the antecedent *A* and the consequent *C*) connected by various sentence-connectives. Participants are shown a sentence of the form 'A [sentence connective] C', as well as all the possible outcome-cases ('A ∧ C', 'A ∧ ¬C', '¬A ∧ C' or'¬A ∧ ¬C'), some of which remain hidden ('?'). They are then asked to determine with which probability (intervals) they assume the sentence to hold. 

The *PTT-Calculator* aims to automatically calculate the uncertainty intervals or probability point-values of such sentences for a variety (of interpretations) of sentence connectives, which I attempted to group according to their natural language counterparts. In addition, for each setup the program also calculates the values of 10 different measures of argument strength (or factual support) between the antecedent and the consequent. Keep in mind that not all of these probabilistic measures share the same domain.

**How to use:** 
First, select the type of sentence connective you are interested in, or the placeholder '[any connective]' in case you are interested in all interpretations. Next, select a total number of cases, and choose how many of them make both the antecedent and consequent true ('A ∧ C'), only one of the two ('A ∧ ¬C' or '¬A ∧ C'), neither ('¬A ∧ ¬C') and how many of them are hidden ('?'). Finally, decide whether to include the calculation of halfway interpretations (see Pfeifer 2013b, Pfeifer forthcoming) and notions of inferential strength (see Pfeifer 2013a, Sprenger & Hartmann 2010). Press 'Calculate Task' to create and view tables containing the desired data. For easy of use, the program can also display the formulae used for each output, and offers each output-table as pre-generated LaTeX code.

**How it works:**
Calculation of task setups featuring no uncertainty - that is, no [?] cases - is pretty straight-forward. Here, one can simply determine the probabilities required (e.g., P(A), P(¬C), P(A ∧ C) and so on) by counting up the relevant cases and dividing them by the total number of cases in the task. For tasks featuring uncertainty though, the application opens a grid - akin to a propositional logic truth table - containing every possible variation *behind the hidden sides*. As each [?] side essentially functions as two boolean variables (A or ¬A and C or ¬C), this amounts to a *2n times 2^(2n)* grid, where *n* equals the number of [?] sides in given task. Reading out this grid then allows calculation of the probabilities required (e.g., P(A), P(¬C), P(A ∧ C) and so on) for each of the *2^(2n)* no-uncertainty-setups compatible with the task at hand. The application then calculates the interpretations and notions of factual support for each of these possibilities individually, in order to return the correct minimal, maximal, median and mean values.

***
#### 3. Dice Task Subroutine
Dice tasks constitute that subset of probabilistic truth table tasks which is restricted to 6 sides of a die, each featuring a symbol and a color. Participants ought to evaluate the probability intervals of conditional sentences like: “If the side facing up shows *antecedent* (A), then the side shows *consequent* (C).”. *A* and *C* are independent, so if one is a symbol, the other is a color (and vice versa). In-completeness of probabilistic knowledge is introduced by leaving some sides of the dice blank, which is marked by *?*.

This R-subroutine calculates and prints the uncertainty intervals identified by different interpretations of natural language conditionals in dice tasks. In addition, it calculates the connection between antecedent and consequent in terms of different notions of argument strength. The function expects as input two boolean vectors of equal length, representing the color and symbol of each visible side, respectively. Vectors shorter than 6 values leave open some uncertainty, leading to probability intervals rather than point values. Written using R version 4.1.0 (2021-05-18).

**Example:** The experiment shows 2 sides of a die, the first a white triangle, the second a black square. Every other side is marked with a question mark. The conditional in question is “If the side facing up shows a triangle, the side shows black.”. This means that the first side makes the antecedent of the conditional true, but not the consequent, and the second side vice versa. Thus, you input (True, False) as the antecedent vector, and (False, True) as the consequent vector, leaving open the remaining four sides.

For more detailed explanations and application examples, see Pfeifer 2013a, Pfeifer 2013b, Pfeifer & Tulkki 2017.

***
#### 4. Dice Task Shiny-App
This little Shiny application does the exact same thing as the Dice Task Subroutine, but comes with a UI. Quickly accessible for testing in the browser [here](https://leon-schoeppl.shinyapps.io/dicetask/), hosted by *shinyapps.io*. If you want to actually work with the software, please download it and run it locally.

***
#### 5. References
* Hartmann, S., & Sprenger, J. (2010). *Bayesian epistemology*.
* Howson, C., & Urbach, P. (1993). *Scientific Reasoning: the Bayesian Approach*, Open Court. Lasalle, IL.
* Pfeifer, N. (2013a). On argument strength. In F. Zenker (Ed.), *Bayesian argumentation. The practical side of probability* (p. 185-193). Dordrecht: Synthese Library Vol. 362 (Springer).
* Pfeifer, N. (2013b). The new psychology of reasoning: A mental probability logical perspective. *Thinking & Reasoning*, 19(3-4), 329-345.
* Pfeifer, N. & Tulkki, L. (2017). Abductive, causal, and counterfactual conditionals under incomplete probabilistic knowledge. In Gunzelmann, G., Howes, A., Tenbrink, T., &, Davelaar, E. (Eds.). *Proceedings of the 39th Cognitive Science Society Meeting* (p. 2888-2893).

