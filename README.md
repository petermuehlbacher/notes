# https://sivers.org/book/FluentForever
first 625: http://fluent-forever.com/wp-content/uploads/2014/05/625-List-Thematic.pdf
* start off with “minimal pair testing” (e.g. having to differentiate sounds like niece and knees)
* use Google images, not translations
* to memorize genders(/tones/…) imagine the masculine terms exploding, feminine catching fire, neuter shattering like glass (similar for tone colors)
* good at remembering when images are violent/sexual/funny
* cloze card types for functional words like “of”, “what”, …
* for 10 ways to form plural, pick 10 nouns and use the person-action-object system (Tiger essen Fleisch)
* also use this to learn verb/noun/adjective/adverb patterns
* submit sentences to lang8 and put corrections in flash cards
* TV series are easier than films (read ahead on Wikipedia, no subs)
* card types should also ask for mnemonic (e.g. “What’s a phrase that includes [word]?”)

# http://arxiv.org/pdf/1511.06444.pdf
universality in halting time for spin glasses and deep neural networks

# http://arxiv.org/pdf/1301.3537.pdf
super short abstract:
* pooling operators are for local invariance
* 1 layer of convolutions is for learning 1 one-parameter-group invariance (or rather: convolutions leave already learned group invariance untouched and the training learns the invariance)
* deep networks are basically doing group factorisation that’s stable w.r.t. perturbations of the group

my notes:

* the problem: find signal representation $\Phi$ (e.g. classifier) that is
	* invariant under some transformation group $G$ (e.g. rotation), i.e. $\Phi(x)=\Phi(gx)$ for all $g\in G$ and
	* is “stable” to perturbations (i.e. transformations $h$ that are “close” to the transformation group $G$ which can be thought of as a low dimensional manifold), i.e. $||\Phi(\varphi(h,x))-\Phi(x)||\leq C||x||d(h,G)$
* approach: take convolutional networks and think of them in terms of signal processing, i.e.
  * inputs $x\in X$ = signals $x\in L^2(\Omega)$
  * convolution kernels = filter bank $\{\psi_\lambda\}_\lambda, \lambda\in\Lambda_1$
  * the first layer maps $x(\cdot)\mapsto \{x*\psi_\lambda(\cdot)\}_\lambda =: z^{(1)}(\cdot,\lambda)$ (which is the set of **convolutions** with kernels $\psi_\lambda$ - think of them as some very localised bump functions, centered around points distributed in $\Omega_0$), applies some operator $M$ and then applies some **pooling operator** $P$, which, in terms of signal processing, can be thought of as low-pass filter, followed by downsampling (see Wikipedia for a quick explanation)
* the special case of one-parameter transformation groups $G=\{U_t\}_{t\in\mathbb R}, U_t\in L^2(\Omega), \lim U_t z = U_{t_0}z, U_{t+s}=U_tU_s$ (e.g. translations, frequency transpositions, dilations):
  * due to Stone’s theorem there is some s.a. $A$ such that $U_t=\exp(itA)$
  * in the finite dimensional case we can write $U_tz = O^{-1}\text{diag}(\exp(it\omega) Oz(\omega))$, implying that the group action is a linear phase change in the basis that diagonalizes $A$
  * hence, a representation that is invariant under the action of $\{U_t\}_t$ can be obtained with a single layer of a fully connected(?) neural network
* how does this help?
  * using the change of basis given by $O$ we can write the group action as some linear phase change; if we also apply the inverse Fourier transform this becomes a translation operator $T_s:z(\cdot)\mapsto z(\cdot -s)$, which lets us measure deformations ($\tilde T_s: z(\cdot)\mapsto z(\cdot -\tau(s))$ such that $d(\tilde T_s,T_s)\ll 1$) in a convenient way by analyzing the regularity of $\tau$
  * thus the key to obtaining group invariant representations is not to find die eigenvectors of $A$ (yielding the change of basis given by $O$), but rather measurements that are “close” to diagonalising $A$ and are localised where deformations occur(?) - this can be done with convolutions with compactly supported filters

# Properties of the Fourier transform
* diagonalises the derivative (i.e. turns it into a multiplication operator if expressed in its basis), which in turn let’s us define pseudo-differential operators via non-polynomial symbols
* Fourier transform is like a projection onto eigenspaces of Laplace operator → in a compact domain (with suitable regularity) those are discrete → get a sum = Fourier _series_
	* using the above idea one can generalize Fourier transforms not only to higher dimensional setting and manifolds, but also to graph settings (see graph Laplacian)
* translation = phase change (think of a shift by π/2 in 1D and what this does to the coefficients of a Fourier _series_)
  * in a space-time metric (having signature 1,1,1,-1) we can “place” a particle at some point in space-time by multiplying the creation operator with some exponential in the right basis (i.e. the one of the Fourier transform) where the spatial part has the inverse sign of the time part because of this metric

# Braess’ paradox (http://ist.ac.at/fileadmin/user_upload/pdfs/Talks/2016/02/Talk_Timme.pdf)
* the paradox: given some (directed) graph with a flow (e.g. traffic network) removing edges could improve the “overall situation” (e.g. on average you do not drive as long as before if a street is closed)
* note that this also implies the converse: adding a street doesn’t necessarily make the traffic situation better overall
* one take on this paradox (from a dynamical systems point of view): knowing the capacity of all the edges and the nodes one gets a system of constraints for every closed loop in order to satisfy some stability condition, but if one introduces another edge that divides a circle in two we get two systems of constraints that may not be compatible → no more stable solution (= traffic jam)

# http://www.huffingtonpost.com/2015/05/13/andrew-ng_n_7267682.html
* “The idea is that innovation is not these random unpredictable acts of genius, but that instead one can be very systematic in creating things that have never been created before. […] learn a lot, read a lot, talk to experts.”
* on early influences: moved around, visited many different colleges and interned at different labs → many different points of view
* don’t “follow your passion” (which usually gets amended to “follow your passion of all the things that happen to be a major at the university you’re attending”); often “you first become good at something, and then you become passionate about it. And I think most people can become good at almost anything. So when I think about what to do with my own life, what I want to work on, I look at *two criteria*. The first is whether it’s an *opportunity to learn*. Does the work on this project allow me to learn new and interesting and useful things? The second is the *potential impact*. **The world has an infinite supply of interesting problems. The world also has an infinite supply of important problems. I would love for people to focus on the latter.**”
* “one pattern of mistakes I’ve made in the past, hopefully much less now, is doing projects where you do step one, you do step two, you do step three, and then you realize that step four has been impossible all along”
* “”if you seriously study half a dozen papers a week and you do that for two years, after those two years you will have learned a lot. […] But that sort of investment, if you spend a whole Saturday studying rather than watching TV, there’s no one there to pat you on the back or tell you you did a good job. Chances are what you learned studying all Saturday won’t make you that much better at your job the following Monday. There are very few, almost no short-term rewards for these things. But it’s a fantastic long-term investment. […] People that count on willpower to do these things, it almost never works because willpower peters out. Instead I think people that are into creating habits — you know, studying every week, working hard every week — those are the most important. Those are the people most likely to succeed.”
* “I don’t work on preventing AI from turning evil for the same reason that I don’t work on combating overpopulation on the planet Mars”, more urgent: “[…] when the U.S. transformed from an agricultural to a manufacturing and services economy, we had people move from one routine task, such as farming, to a different routine task, such as manufacturing or working call service centers. A large fraction of the population has made that transition, so they’ve been okay, they’ve found other jobs. But many of their jobs are still routine and repetitive. The challenge that faces us is to find a way to scalably teach people to do non-routine non-repetitive work. Our education system, historically, has not been good at doing that at scale. The top universities are good at doing that for a relatively modest fraction of the population. But a lot of our population ends up doing work that is important but also routine and repetitive. That’s a challenge that faces our educational system.”
* “One thing about speech recognition: most people don’t understand the difference between 95 and 99 percent accurate. Ninety-five percent means you get one-in-20 words wrong. That’s just annoying, it’s painful to go back and correct it on your cell phone. Ninety-nine percent is game changing. If there’s 99 percent, it becomes reliable.”

# http://www.paulgraham.com/hs.html
great text, you should read it!
* if you don’t have a clear goal (which is usually the case) work forward from promising situations instead
* if you have to choose, take those options that will give you the most promising range of options afterward
* work on hard problems (“Writing novels is hard. Reading novels isn’t. Hard means worry: if you’re not worrying that something you’re making will come out badly, or that you won’t be able to understand something you’re studying, then it isn’t hard enough.”) → also get to know interesting people and get big ideas
* “Put in time how and on what? Just pick a project that seems interesting: to master some chunk of material, or to make something, or to answer some question. Choose a project that will take less than a month, and make it something you have the means to finish. Do something hard enough to stretch you, but only just, especially at first. If you're deciding between two projects, choose whichever seems most fun. If one blows up in your face, start another. Repeat till, like an internal combustion engine, the process becomes self-sustaining, and each project generates the next one.”
* “Don’t disregard unseemly motivations. One of the most powerful is the desire to be better than other people at something.”

# https://terrytao.wordpress.com/2008/08/07/on-time-management/
* “Another thing is that my ability to do any serious mathematics fluctuates greatly from day to day; sometimes I can think hard on a problem for an hour, other times I feel ready to type up the full details of a sketch that I or my coauthors already wrote, and other times I only feel qualified to respond to email and do errands, or just to take a walk or even a nap. I find it very helpful to organise my time to match this fluctuation: for instance, if I have a free afternoon, and feel inspired to do so, I might close my office door, shut off the internet, and begin typing on a languishing paper; or if not, I go and work on a week’s worth of email, referee a paper, write a blog article, or whatever else seems suited to my current levels of energy and enthusiasm. It is fortunate in mathematics that a large fraction of one’s work (with the notable exception of teaching, which one then has to build one’s schedule around) can be flexibly moved from one time slot to another in this manner. [A corollary to this is that one should deal with tasks before they become so urgent that they have to be done immediately, thus disrupting one’s time flexibility.]”
* “A half-hearted system is probably worse than no system at all. A corollary to this is not to try to make an overly ambitious system ab nihilo that one is unlikely to follow faithfully; it is probably better to let such systems evolve over time.“
* “Sometimes one should abandon one’s own rules and allow for serendipity. There have been many times, for instance, when I had planned to work on something during my lunch hour (grabbing something quick to eat), when I was interrupted by a colleague or visitor to go out to eat. It has often happened that I got a lot more out of that lunch (mathematically or otherwise) than I would have back at the office, though not in the way I would have anticipated.”

# http://arxiv.org/pdf/1405.4537v1.pdf
* def: stream is a map $\gamma$ from a totally ordered set $I$ to some state space
* there is a canonical way to convert discrete streams to continuous paths (path: $I$ interval and some regularity conditions like right continuity)
* from now on “wlog”: $\gamma:[J_-,J_+]\rightarrow E$ will continuously map an interval $J$ to some Banach space $E$
* def: bounded $p$-variation ($p\geq 1$) iff $sup_{\dots<u_i < u_{i+1}<\dots\in J}\sum_i\|\gamma_{u_{i+1}}-\gamma_{u_i}\|^q <\infty$ for $q=1$ and $q=p$
TO BE CONTINUED

# http://math.ucr.edu/home/baez/rosetta.pdf
great paper for everybody who is interested in (yet not familiar with) category theory - summary may follow

# uses of 的 (中文)
* possessive particle: 我的女 = my daughter
* attributive (connecting adjective and noun): 红色的菜 = red vegetables 
