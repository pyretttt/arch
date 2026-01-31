# VAE
***
$p(x)$: The true distribution of $x$. IT's never known. The whole universe of diffusion models is to find ways to draw samples from $p(x)$
$p(z)$: Distribution of the latent variable. Typically, we make it a zero-mean unit-variance gaussian $N(0, 1)$. One reason is that linear transformation of a Gaussian remains a Gaussian.
$p(z | x)$: The conditional distribution associated with the **encoder**, which tells us the likelihood of $z$ when given $x$. We have no access to it. $p(z | x)$ is not itself an encoder, but the encoder has to do something so that it will be consistently with $p(z | x)$
$p(x | z)$: The conditional distribution associated with the **decoder**, which tells us the posterior probability of getting $x$ given $z$. We have no access to it.
$q_{\phi}(z | x)$: The proxy for $p(z | x)$, which is also the distribution associated with the encoder. For example it can defined as
$$\begin{align}
(\mu, \sigma^{2}) = EncoderNetwork(x) \\
q_{\phi} = N(x; \mu, diag(\sigma^{2}))
\end{align}$$
$p_{\theta}(x | z)$: The proxy for $p(x | z)$, which is also the distribution associated with the decoder. For example
$$\begin{align}
f_{\theta}(z) = DecoderNetwork(z) \\
p_{\theta}(x | z) = (x | f_{\theta}(z), \sigma_{dec}^2I)
\end{align}$$

###### Evidence-Lower-Bound
***
**Definition** _(Evidence Lower Bound)_. Evidence Lower Bound is defined as
$$\begin{align}
ELBO(x) := E_{q_{\phi}(z | x)}\left[ \log\left( \frac{p(x, z)}{q_{\phi}(z | x)} \right) \right]
\end{align}$$
In a nutshell **ELBO** is a lower bound for the prior distribution $\log(p(x)) \geq ELBO(x)$.
$$\begin{align}
\log(p(x)) = \dots  \\
= E_{q_{\phi}(z | x)}\left[ \log\left( \frac{p(x, z)}{q_{\phi}(z | x)} \right) \right] + D_{KL}(q_{\phi}(z | x) || p(z | x)) \\
\geq E_{q_{\phi}(z | x)}\left[ \log\left( \frac{p(x, z)}{q_{\phi}(z | x)} \right) \right] \\
= ELBO(x)
\end{align}$$

**Remark**. _(Why we need ELBO)_. ELBO is lower bound for $\log(p(x))$. Thereof if we are able to maximize ELBO, then we can maximize $\log(p(x))$. The question is how good ELBO is? As seen from inequality it turns to equality if $q_{\phi}(z | x)$ is equal to $p(z | x)$. So, part of the game is to ensure $q_{\phi}(z | x)$ is close to $p(z | x)$


**Definition**. _(Decomposition of Log-Likelihood)_. The log likelihood $\log(p(x))$ can be decomposed as
$$\begin{align}
\log(p(x)) = E_{q_{\phi}(z | x)}\left[ \log\left( \frac{p(x, z)}{q_{\phi}(z | x)} \right) \right] + D_{KL}(q_{\phi}(z | x) || p(z | x))
\end{align}$$
_Proof_.
$$\begin{align}
\log(p(x)) = \log(p(x)) \int q_{\phi}(z | x) dz  \\
= \int \log(p(x)) q_{\phi}(z | x) dz   \\
= E_{q_{\phi}(z | x)}[\log(p(x))]
\end{align}$$
Next thing to note that $p(x) = \frac{p(x, z)}{p(z | x)}$
$$\begin{align}
E_{q_{\phi}(z | x)}[\log(p(x))] = E_{q_{\phi}(z | x)}\left[ \log\left( \frac{p(x, z)}{p(z | x)} \right) \right] \\
= E_{q_{\phi}(z | x)}\left[ \log\left( \frac{p(x, z)}{p(z | x)} \cdot \frac{q_{\phi}(z | x)}{q_{\phi}(z | x)} \right) \right]  \\
= E_{q_{\phi}(z | x)}\left[ \log\left( \frac{p(x, z)}{q_{\phi}(z | x)} \cdot \frac{q_{\phi}(z | x)}{p(z | x)} \right) \right]  \\
= \overbrace{ E_{q_{\phi}(z | x)}\left[  \log\left(  \frac{p(x, z)}{q_{\phi}(z | x)}  \right) \right] }^{ ELBO } + \overbrace{ E_{q_{\phi}(z| x)} \frac{q_{\phi}(z | x)}{p(z | x)}] }^{ D_{KL}(q_{\phi}(z | x) || p(z | x)) }
\end{align}$$


**Theorem**. _(Interpretation of ELBO)_. Why ELBO is even useful? It defines lower bound for $\log(p(x))$ involving $p(x, z)$. Let's look at it interpretation:
$$\begin{align}
ELBO(x) = E_{q_{\phi}(z | x)}\left[ \log\left( \frac{p(x|z) p(z)}{q_{\phi}(z|x)} \right) \right] \\
 = \underbrace{  E_{q_{\phi}(z | x)}\left[ \log\left( \overbrace{p(x | z)}^{ \text{A Gaussian} } \right) \right] }_{ \text{How good decoder is} } - \underbrace{ D_{KL}(\overbrace{ q_{\phi}(z | x) }^{ \text{a Gaussian} } || \overbrace{ p(z) }^{ \text{a Gaussian} }) }_{ \text{How good encoder is} }  \\
= E_{q_{\phi}(z | x)}[ \log( {\color{red} { p_{\phi}(x | z) }} ) ]  - D_{KL}( q_{\phi}(z | x)  || p(z)
\end{align}$$
where in last equation replaced $p(x | z)$ with $p_{\phi}(x | z)$.=

[[diffusion_models_stanley_chan.pdf#page=21&selection=0,0,4,1|Example 2.1. Let’s consider a Gaussian mixture model]]