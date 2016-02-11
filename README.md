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