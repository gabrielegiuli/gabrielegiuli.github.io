---
layout: page
permalink: /teaching/qip_ii/ps4
title: 4. Non-Unitary Processes
---

We talked about how every process in quantum mechanics is *unitary*, thus any quantum state $\vert\psi\rangle$ evolves according to the Schrodinger equation

$$
i\hbar \frac{\mathrm{d}}{\mathrm{d}t}|\psi\rangle = \hat{H}|\psi\rangle
$$

where $\hat{H}$ is the Hamiltonian of the system. Now while it is true that quantum mechanics is unitary in its evolution, it is not always practical/possible to solve the full system's Schrodinger equation.

In the case of a qubit, we saw how this equates to trajectories on the surface of the Bloch sphere.

As an example, let's try to write down what is happening to an atom undergoing spontaneous emission.
We can write down a state Ansatz as

$$
|\psi(t)\rangle = a(t)|1, \mathbf{0}\rangle + \sum_k b_k(t)|0, \mathbf{1}_k\rangle
$$

Notice that the electromagnetic field is quantised, however the photon can be emitted in any possible direaction, thus we need to consider all the possible *modes* that we can excite. If we want to write down the full (*pure*) state, we need to record all of this information.

Not only this is cumbersome, it is also impossible to do. How would I create a detector that not only "sees" without any loss, but also tells us perfectly well where the photon went. The solution, is to use the *density matrix formalism*. Here are the basic properties:

$$
\begin{align*}
\rho &= |\psi\rangle\langle\psi| \ \text{(for a pure state)} \\
\rho &= \sum_i p_i |\psi_i\rangle\langle\psi_i| \\
\langle A \rangle &= \mathrm{Tr}(\rho A)
\end{align*}
$$

The great thing about density matrices is that we can *trace out* the degrees of freedom that we are not interested about, namely

$$ 
\rho_A = \mathrm{Tr}_B(\rho_{AB})
$$

While it would be awesome to apply this idea to the example above, we do not have enough time to do that here. Therefore we will have to resort to a simpler case scenario. Suppose we generate a Bell pair between two qubits $A$ and $B$, namely

$$
|\psi_{AB}\rangle = \frac{1}{\sqrt{2}}(|0_A0_B\rangle + |1_A1_B\rangle)
$$

Then suppose that qubit $A$ is sent to Alice and qubit $B$ is sent to Bob. Now suppose that Bob always measures his qubit before Alice does. 

> *What is the probability that Bob measures 1 and what is the probability that Bob measures 0?*

Now that Bob has measured his qubit value, Alice would also like to measure hers.

> *What is the state of the qubits $\vert\psi\rangle_{AB}$ after Bob did his measurement? What is the probability that Alice measures 1 or 0 given Bob's measurement?*

Well after the measurement, the state becomes

$$
|\psi_{AB}^\prime\rangle = \begin{cases}
|00\rangle, \ \text{if Bob has measured 0} \\
|11\rangle,  \ \text{if Bob has measured 1} 
\end{cases}
$$

Therefore Alice still observes $0$ and $1$, 50% of the times she measures it, but this is no longer a quantum probability... Take some time to absorb this concept. This is exactly what happens in our example with the spontaneous emission. The *Environment* (Bob) measures the emitted photon, and collapses the wafefunction for us, converting quantum proababilities to classical ones.

Let's continue, let's try to apply the DM formalism

$$
\begin{align*}
\rho_{AB} &= |\psi_{AB}\rangle\langle \psi_{AB}| \\
&= \frac{1}{2}(|0_A0_B\rangle\langle0_A0_B| + |0_A0_B\rangle\langle1_A1_B| + |1_A1_B\rangle\langle0_A0_B| + |1_A1_B\rangle\langle1_A1_B|)
\end{align*}
$$

Now since we want to write the density matrix state from the perspective of Alice, we assume we have no knowledge of what Bob obtained in his experiment. Thus we trace out the Bob degree of freedom.

$$
\begin{align*}
\rho_A &= \mathrm{Tr}_B(\rho_{AB}) = \sum_{i = 0,1} \langle i_B|\rho_{AB}|i_B\rangle \\
&= \frac{1}{2}(|0_A\rangle\langle 0_A| + |0_B\rangle\langle 0_B|)
\end{align*}
$$

Et voila, comparing the result above, we see that we observe a distribution of 50% observing state $1$ and 50% observing state $0$ from Alice's perspective.

## Evolution of Densitry Matrices
Corresponding to the Schrodinger Equation, states expressed in the density matrix formalism evolve according to a specific rule, the Lindblad Master Equation

$$
\frac{\mathrm{d}\rho}{\mathrm{d}t} = -\frac{i}{\hbar}[\hat{{H}}, \rho] + \sum_{i} \frac{\gamma_i}{2}\left[2\hat{L}_i\rho\hat{L}_i^\dagger - \{\rho, \hat{L}_i^\dagger \hat{L}_i\}\right]
$$

Where $\hat{H}$ is still our good old Hamiltonian and it accounts for the _unitary dynamics_, and $\hat{L}_i$ are called jump operators, and they represent the _non-unitary dynamics_.

This form is extremely useful when desribing any type of noise, as we do not have access to the action of the noise (random by definition). In addition, it is useful to describe non-unitary processes, such as _pumping_, that we discussed about last week and cooling. 

It is interesting to extend the qpicture of the Bloch sphere to density matrices. In this case, the trajectories can go through the sphere itself.

## Optical Bloch Equations
We now consider a single atom driven with a Rabi rate $\Omega$, detuning $\delta$ and subject to spontaneous decay at rate $\Gamma$. 
For instance, in the case of a single atom that is subject to spontaneous decay, we have

$$
\begin{align*}
\hat{H} &= \hbar\Delta|e\rangle\langle e| + \frac{\hbar\Omega}{2}\left(\overbrace{|e\rangle\langle g| + |g\rangle\langle e|}^{\sigma_x}\right) \\
\hat{L} &= |g\rangle\langle e| \\
\end{align*}
$$

The LME becomes 

$$
\frac{\mathrm{d}\rho}{\mathrm{d}t} = -i\Delta\Big[|e\rangle\langle e|, \rho\Big] -\frac{i\Omega}{2}\Big[|e\rangle\langle g|, \rho\Big] -\frac{i\Omega}{2}\Big[|g\rangle\langle e|, \rho\Big]  + \frac{\Gamma}{2}\Big[2|g\rangle\langle e| \rho |e\rangle\langle g| - \{\rho, |e\rangle\langle e\}\Big]
$$

Now we note that $\rho$ itself is a $2\times 2$ matrix defined as

$$
\rho = \begin{pmatrix}
\rho_{gg} & \rho_{ge}\\
\rho_{eg} & \rho_{ee}
\end{pmatrix}
$$

We notice that $\rho_{ee} = \langle e |\rho | e\rangle$ and so on, therefore if we continue, we will get to the point where

$$
\begin{align}
\frac{d\rho_{gg}}{dt} &= \Gamma \rho_{ee} + \frac{i}{2} \left( \Omega^* \rho_{eg} - \Omega \rho_{ge} \right) \\
\frac{d\rho_{ee}}{dt} &= -\Gamma \rho_{ee} + \frac{i}{2} \left( \Omega \rho_{ge} - \Omega^* \rho_{eg} \right) \\
\frac{d\rho_{ge}}{dt} &= -\left( \frac{\Gamma}{2} + i\Delta \right) \rho_{ge} + \frac{i}{2} \Omega^* \left( \rho_{ee} - \rho_{gg} \right) \\
\frac{d\rho_{eg}}{dt} &= -\left( \frac{\Gamma}{2} - i\Delta \right) \rho_{eg} + \frac{i}{2} \Omega \left( \rho_{gg} - \rho_{ee} \right)
\end{align}
$$

These are called optical bloch equations.

### Driven Dissipated Rabi Flops
Let us now consider the case when we are on resonance $\Delta = 0$ and we are not driving $\Omega = 0$, the equations reduce to

$$
\begin{align}
\frac{d\rho_{gg}}{dt} &= \Gamma \rho_{ee} \\
\frac{d\rho_{ee}}{dt} &= -\Gamma \rho_{ee} \\
\frac{d\rho_{ge}}{dt} &= -\frac{\Gamma}{2} \rho_{ge}\\
\frac{d\rho_{eg}}{dt} &= -\frac{\Gamma}{2} \rho_{eg}
\end{align}
$$

We see that all information about coherence is lost (bottom two terms) and the steady state tends (unsurprisingly) to the ground state.

By extension, if we are driving the flops, we would expect to have some shifted steady state, and spiral close to this point.
