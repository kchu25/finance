@def title = "Character Study - The Guy Who Keeps Choosing Uncertainty"
@def tags = ["meta"]
@def published = "17 February 2026"
@def rss = "A character analysis of someone who left ballet for CS, academia for crypto analysis, and certainty for expected value — every single time."

# Character Study - The Guy Who Keeps Choosing Uncertainty

\toc

---

## The Pattern

When you read enough of someone's writing across enough domains, the words stop mattering and the *structure* starts showing through. The topics change — ballet, DNA motifs, oracle economics, evolutionary psychology, options pricing — but the underlying architecture of thought stays the same.

Here is the architecture of Shane Chu's mind, reconstructed from the wreckage of a career that makes no sense on paper and perfect sense in theory.

---

## Exhibit A - The Career as Revealed Preference

Economists have a concept called "revealed preference" — you learn what people truly value not from what they say but from what they do. Forget what Shane says about himself. Look at what he's *done*:

**Age ~8 onward** — Trains obsessively at classical ballet. Competes internationally. Prix de Lausanne quarterfinalist. USA International Ballet Competition Capezio Award. Dances professionally at Zurich Ballet — one of the most prestigious companies in Europe — and then Ballet West, New Jersey Ballet, and Kaohsiung City Ballet. This is not a hobby. This is an identity-consuming, body-destroying, decade-long commitment to an art form that pays almost nothing and discards you at 35.

And he was good. In the Salt Lake Tribune's [review](https://archive.sltrib.com/article.php?id=53457511&itype=cmsid) of Ballet West's *Don Quixote* (February 2012), the critic wrote: *"artist Kuei-Hsien Chu wowed the audience with split leaps and multiple turns that brought whistles and cheers for his bravura."* Whistles and cheers. In a professional ballet production reviewed by a major newspaper. This is not someone who dabbled.

**Then** — Walks away. Not because he failed — he was getting standing-section cheers in Don Quixote. Because something else became more interesting.

**Age ~mid-20s onward** — Starts over in computer science. From zero. A professional ballet dancer learning to code. The social awkwardness of being the oldest person in an intro CS class. The ego death of going from "I've danced at Zurich Ballet" to "I don't understand pointers." Years of this.

**PhD** — Picks computational biology. Not a safe, well-funded subfield — a niche where he's building deep learning methods for finding DNA motifs using sparse representations. Publishes in *Bioinformatics*. Codes everything in Julia, a language whose user base fits in a mid-sized conference room. Gets a PhD from WashU.

**Postdoc at Columbia** — Takes a postdoc position (voluntary poverty with a prestigious address) to keep doing research.

**Meanwhile** — Builds an entire parallel intellectual life analyzing Chainlink oracle economics, deriving Black-Scholes from scratch, writing about measure theory, building terminal value frameworks for crypto assets, writing 1,300-line investment theses, analyzing Aave lending positions, and — on a completely separate website — developing a comprehensive theory of human evolutionary psychology that includes a 5,000-word analysis of why humans are addicted to certainty.

Now. What does revealed preference tell us?

**This person has an extraordinarily high tolerance for ambiguity, and he knows it, and he's built an entire intellectual framework to explain why that tolerance is his single greatest competitive advantage.**

---

## Exhibit B - The Certainty Addiction Essay as Self-Portrait

Shane wrote an essay called ["The Certainty Addiction"](https://kchu25.github.io/evop/blog/my_own_questions/certainty_addiction/) on his evolutionary psychology blog. On the surface, it's a general theory — it's about humanity, about cognitive bias, about why people sacrifice expected value for the feeling of knowing.

But read it carefully and you realize: **it's a self-portrait drawn in negative space.** Every trait he diagnoses in the certainty-addicted majority is a trait he has systematically purged from himself. The essay isn't just analysis — it's autobiography disguised as science.

### The Formal Structure Reveals the Mind

The essay opens with the Allais Paradox and prospect theory. Not with an anecdote. Not with a "let me tell you a story." With mathematical formalization. He defines the certainty premium:

$$\pi_c = EV_{\text{uncertain}} - CE$$

He quantifies the "felt ratio" — the brain's 4x compression of uncertain gains:

$$\text{Felt ratio} = \frac{0.5 \times \text{expected gain}}{2 \times \text{certain cost}}$$

This is a person who can't think about a psychological phenomenon without deriving a formula for it. Not because he's showing off — because formalization is how he *sees*. The math isn't decoration. The math is the lens.

This same mind then turns to Chainlink and produces terminal value frameworks, probability-weighted expected values, and supply squeeze models. Of course it does. The same cognitive machinery that says "let me formalize certainty addiction with prospect theory" inevitably says "let me formalize oracle network valuation with discounted cash flow models." The domain changes. The mind doesn't.

### The Modern Inversion as Life Philosophy

The essay's most revealing section is "The Modern Inversion" — the argument that in the ancestral environment, uncertainty was correlated with danger, but in the modern world, **uncertainty is correlated with growth**:

> *"Your brain screams 'choose certainty!' because it evolved in a world where certainty meant survival. But you live in a world where certainty means slow decay and uncertainty means growth."*

Now re-read the career timeline:

- **Certain path**: Stay in ballet (known, identity-confirming, but declining body and limited ceiling) → He chose the uncertain path (CS, starting from nothing)
- **Certain path**: Get an industry job after the CS degree (guaranteed salary, known career trajectory) → He chose the uncertain path (PhD, 5-7 years of academic poverty)
- **Certain path**: After PhD, take a stable job → He chose the uncertain path (postdoc at Columbia, even more academic poverty)
- **Certain path**: Focus exclusively on his research → He chose the uncertain path (parallel crypto analysis, evolutionary psychology essays, intellectual exploration across five unrelated fields)

**At every single fork, he chose the uncertain option.** Not by accident. Not by recklessness. By what he would call "expected value maximization under uncertainty" — the deliberate choice to pay the psychological cost of not-knowing because the math says the uncertain path has higher expected returns.

The certainty addiction essay is not a theoretical exercise. It is a manual for his own decision-making, written in third person.

### The Certainty Tax and the Postdoc

The essay identifies the "certainty tax" — the premium people pay to eliminate uncertainty, typically 20-40% of expected value. He applies this to careers:

> *"Path A (Certain): Stay at corporate job. Salary: \$90,000, growing 3% per year... Path B (Uncertain): Start a company or join an early-stage startup... Most people choose the fog-free option and pay a million-dollar certainty tax over their lifetime."*

Now look at his actual choices. He's a Columbia postdoc earning... a postdoc salary. He holds X LINK tokens. By his own analysis, LINK's expected value is somewhere between \$500-\$1,500 per token.

He has calculated — explicitly, in writing, with probability distributions — that his crypto position has an expected value exceeding his academic salary by potentially two orders of magnitude. And yet he stays in academia. Not because he can't do the math. Because the research *is the uncertain, high-expected-value path* — it just operates on a timeline so long that most people can't perceive the return.

This is a person running two parallel expected-value calculations simultaneously: one in oracle network economics, one in computational biology. Both uncertain. Both potentially enormous. Both requiring the patience of someone who trained for 15 years to perform a 3-minute dance.

---

## Exhibit C - The Intellectual Character

### The First-Principles Compulsion

Shane derives Black-Scholes from scratch. He writes out the Augmented Dickey-Fuller test by hand. He builds his website in Julia using Franklin.jl instead of using a normal static site generator. He wrote a motif discovery algorithm using deep unfolding instead of using existing tools.

This isn't stubbornness (well, not *just* stubbornness). It's a specific cognitive trait: **he doesn't trust knowledge he hasn't reconstructed himself.** He learns by re-deriving. The derivation *is* the understanding. If he can't build it from axioms, he doesn't claim to know it.

This is why his Chainlink thesis is 1,308 lines long. A normal person writes "I think LINK is undervalued because oracles are important." Shane writes a terminal value framework, models five scenarios, assigns probability distributions, computes expected values, steelmans the bear case, and then addresses the philosophical question of what "truth" means in a decentralized context. Because anything less would be an assertion without a derivation, and assertions without derivations are — in his mind — not knowledge. They're opinions.

### The Multi-Domain Pattern Matcher

The certainty addiction essay connects:
- Kahneman and Tversky's prospect theory
- Evolutionary savanna psychology
- Anterior insula neuroscience
- Stoic philosophy (Epictetus)
- Insurance economics
- Clinical OCD mechanisms
- Attachment theory
- Meditation neuroscience

All in one coherent framework. In a *single essay.*

This is the same mind that, on a different blog, connects:
- Byzantine fault tolerance
- DTCC settlement infrastructure
- The CLARITY Act's commodity classification
- U.S. debt crisis macro dynamics
- Staking game theory
- Carbon credit verification
- CME futures mechanism

Also all in one coherent framework.

The common trait: **he sees structural isomorphisms across domains that most people never connect.** The certainty addiction in finance (cash hoarding) and the certainty addiction in relationships (the "what are we?" conversation) and the certainty addiction in religion (comprehensive cosmology as uncertainty resolution) are — to him — literally the same phenomenon wearing different costumes. Just as oracle verification for bond settlements and oracle verification for athlete performance tokens and oracle verification for DeSci lab results are the same infrastructure problem wearing different costumes.

This is either genius-adjacent cross-pollination or the cognitive equivalent of a man with a hammer seeing nails everywhere. The line between those two things is thinner than most people realize.

### The Motif Hunter - The Rosetta Stone

Here is where it all clicks. Shane's LinkedIn intro contains a sentence that functions as a skeleton key to his entire intellectual character:

> *"Motifs imply evolutionary pressure, i.e. the invariants — things that may be faint but conserved in biological systems with predictable behaviors."*

Read that again. Then read the rest:

> *"The thinking and technical skills I've developed extend well beyond computational biology and apply broadly to problems in structure discovery, representation learning, and scalable inference."*

**He doesn't just study motifs in DNA. He *thinks* in motifs.** The motif — a faint but conserved pattern with predictable behavior — is not just his research subject. It is his cognitive operating system.

What is the certainty addiction? A *motif* in human behavior — faint (most people don't see it), conserved (it appears identically across finance, relationships, health, religion, career decisions), with predictable behavior (it always costs 20-40% of expected value).

What is Chainlink's value proposition? A *motif* in infrastructure economics — faint (the market prices it at nearly zero), conserved (the same oracle verification pattern appears in bonds, real estate, insurance, DeSci, supply chains), with predictable behavior (whoever controls the verification layer captures infrastructure-monopoly rents).

What is the "modern inversion" from the certainty essay? A *motif* in evolutionary mismatch — faint (it feels like common sense to choose safety), conserved (it appears in every domain where uncertainty correlates with growth), with predictable behavior (it systematically costs people the uncertain, higher-EV option).

**His entire intellectual output — across computational biology, evolutionary psychology, crypto analysis, options pricing, and measure theory — is a single activity: finding invariants.** Things that are faint. Things that are conserved across contexts. Things with predictable behaviors. He found them in DNA. Then he found them in human cognition. Then he found them in oracle economics. The method never changed. Only the substrate.

This is why his career looks incoherent on a resume but feels perfectly coherent in his head. He's not switching fields. He's applying the same algorithm — *find the motif, characterize its function, formalize the invariant* — to whatever domain is most interesting at the time. Ballet, genomics, crypto, psychology — these aren't career pivots. They're different datasets fed into the same inference engine.

### The Stoic Undercurrent

The certainty addiction essay invokes Epictetus:

> *"The Stoics would say: the energy spent chasing certainty about things outside your control is the single greatest source of human suffering."*

There's something deeply Stoic about the entire career trajectory. Ballet is one of the most Stoic art forms — you train for decades, your body is your instrument, you have almost no control over casting decisions or career breaks, and physical decline is guaranteed and early. You learn to *practice excellence in what you control and release attachment to what you don't.*

Then he enters computer science and research — another domain where you control the quality of your work but not whether reviewers accept your paper, whether your method gets adopted, whether your lab gets funded.

Then he enters crypto investing — where you control your analysis and position sizing but not whether the market agrees with you this year, this decade, or ever.

**The through-line is a practiced comfort with doing the work and releasing attachment to the outcome.** This is rare. Most people either (a) don't do rigorous work, or (b) do rigorous work but then become emotionally attached to being recognized for it. Shane appears to do rigorous work and then... put it on a Julia-powered blog that 200 people read. The work is the point. The recognition is nice but not required.

---

## Exhibit D - The Contradictions

No character study is complete without the contradictions, and there are a few good ones:

### The Uncertainty Evangelist with a Very Specific Thesis

For someone who writes 5,000 words about the dangers of premature certainty, Shane is remarkably certain about Chainlink. The investment thesis posts don't read like "here's one possible outcome" — they read like "the market is wrong and here's the math proving it." The probability-weighted expected value frameworks are technically open-ended, but the conviction radiating through the prose is not.

Is this hypocrisy? Or is it the natural consequence of someone who's done the work? The certainty addiction essay distinguishes between *performed certainty* (social signaling without supporting analysis) and *earned conviction* (high confidence born from exhaustive analysis). Shane would argue his Chainlink conviction is the latter. Maybe. But the certainty addict never thinks they're addicted, either.

### The Academic Who Doesn't Play the Academic Game

He's at Columbia. He should be publishing papers, networking at conferences, building a publication record for a tenure-track position. Instead, he's writing 1,300-line crypto analyses and evolutionary psychology essays on personal blogs. He codes in Julia when Python would get him more citations. He picks niche problems (sparse representations for motif discovery) when trendier problems (large language models) would get more attention.

This is either intellectual integrity of the highest order or career self-sabotage of the most sophisticated kind. Possibly it's both at the same time. The certainty addiction essay might provide the answer — he's systematically choosing the uncertain, high-expected-value, low-social-approval option at every junction. But expected value calculations assume you survive long enough to collect. Academic careers have clocks.

### The Pattern Recognizer Who Might Be Over-Fitting

Cross-domain pattern matching is powerful when the patterns are real. But the same cognitive tendency that allows you to see genuine structural isomorphisms can also lead you to see patterns that aren't there — the apophenia problem. Is the connection between certainty addiction in relationships and certainty addiction in finance genuinely structural, or is it a metaphor that feels satisfying? Is the parallel between DNA motif discovery and crypto signal detection a real cognitive skill transfer, or a narrative that flatters the author?

Shane would probably acknowledge this risk. The certainty addiction essay itself warns about "premature closure" — jumping to conclusions to resolve ambiguity. The question is whether his own frameworks are rigorous discoveries or sophisticated premature closures.

I suspect the answer is: mostly the former, occasionally the latter, and the willingness to ask the question is itself the most revealing character trait of all.

---

## The Synthesis

Here is who Shane Chu is, as best as I can reconstruct from the evidence:

**A motif hunter.** Someone who discovered — through ballet, through competition, through career destruction and reinvention, through DNA, through markets — that the world is full of faint, conserved patterns with predictable behaviors. And that finding them is the most rewarding thing a mind can do.

His research description says it plainly: *"motifs imply evolutionary pressure, i.e. the invariants."* His career *is* the invariant. The domains change — pirouettes, protein binding sites, oracle networks, prospect theory — but the underlying operation never does: find the motif, characterize its function, formalize the invariant, and don't stop until the derivation is complete.

He is a first-principles thinker who trusts derivations over assertions. A cross-domain pattern matcher who sees isomorphisms where others see unrelated fields. A Stoic who does the work and releases attachment to the outcome. An uncertainty evangelist who is paradoxically very certain about his uncertainty framework. A man who once *"wowed the audience with split leaps and multiple turns that brought whistles and cheers"* and then walked away to learn C++.

His career makes no sense on a resume. But it makes perfect sense as a revealed preference function: **at every decision point, choose the option with higher expected value and higher uncertainty, pay the psychological tax of not-knowing, and trust that the math works out over long time horizons.**

The certainty addiction essay ends with:

> *"The seed grows in uncertain soil. Always has. Always will."*

That's not philosophy. That's a self-description. And if you look closely, it's also a motif — faint, conserved across every chapter of this improbable life, with predictable behavior.

---

*This character analysis is necessarily incomplete. The subject keeps adding new domains of interest, which makes holding a fixed model of him approximately as difficult as he claims it should be.*
