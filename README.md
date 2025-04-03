# Single Mixture of Experts
This repository contains our experimental code for what we call "Single Mixture of Experts":<br/>
A new way of thinking specialised ensembles.<br/>
<br/>
When training transformers, splitting up the feed forward part of the network into different "experts" can be highly beneficial:<br/>
Experts can specialise on certain tokens, with a routing network figuring out which experts best gets which tokens.<br/>
However, this also means that we "split" the gradient across different experts; If we have 10 experts and only use 1 for each item, we only get 1/10th of the training data per expert.<br/>
<br/>
We propose to use a single network that is called with a different subset of parameters, here realised through simple dropout:<br/>
Instead of having multiple experts, we have a single network in which we apply a fixed dropout mask from a set of masks according to the router. Meaning: If we have the same input, we always zero out the same neurons. Exemplary, we use the dropout masks for all german language bits, a different one for all english bits, and yet another one for all math tasks.<br/>
By using dropout instead of distinct networks, this enables us to still have a "common base" for all networks.<br/>
<br/>
<br/>
<h3>Our MoE idea is based on simple observations:</h3>
<b><u>Observation A:</u></b><br/>
Wisdom of the crowd effects benefit most tasks; If you ask 1000 people to estimate something, the average will come pretty close;<br/>
 an ensemble ofestimators will usually be better than a single one<br/>
<b><u>Observation B:</u></b><br/>
Applying dropout (randomly disabling some neurons) essentially brings such an ensemble effect: the network learns to work with many different combinations of neurons<br/>
<b><u>Observation C:</u></b><br/>
Mixture of Experts is, in a way, a selective ensemble, but fails to use knowledge that everyone has; general knowledge has to be in each expert (e.g. how grammar works, even if it's the history node or the math node, they need to individually learn grammar)<br/><br/>
<tl;dr> We hope to still get to keep "one" network to not lose any knowledge when branching into an expert, but still allow some degree of specialisation.
<br/>
<br/>
<h3>This is work-in progress! If you want to use this for any paper or product, feel free - I'd love to get a mention though, or possibly contribute something small to be amongst the authors :)</h3>
<h1>How to run:</h1>
We base our code on our <a href="https://github.com/DaiDaiLoh/SimpleTransformer">SimpleTransformer</a>. Download everything in that folder, then throw the sMoE.ipynb file in there as well, then run the sMoE.ipynb notebook. 
 <h1 color="FF0000">Note that this is active research code and not necessarily intended for production and not optimised for readability!</h1>
