# TakeMeter Project Planning

## 1. Community
**Community Choice:**
r/Games subreddit, specifically focusing on the Summer Game Fest 2026 megathread.

**Suitability for Classification:**
Live reaction threads for major gaming showcases are a chaotic mix of discourse. The feed includes deep industry analysis, hyperbolic tribalism (console wars), and pure, unadulterated emotional reactions all in the same thread. This extreme variance in discourse quality makes it the perfect environment to measure the difference between a genuinely structured argument and a low-effort reaction.

## 2. Labels
**Taxonomy and Definitions:**
1. **analysis**: The post makes a structured argument backed by statistics, historical comparison, industry context, or tactical observation.
   * Example 1: "Looking at the pricing model, it's clear Microsoft is pivoting to a software-first approach. By putting DOOM on PS5, they are trading console exclusivity for guaranteed software revenue."
   * Example 2: "From a purely mechanical standpoint, this seems to borrow heavily from the posture system in Sekiro, but it adapts it well for a western RPG audience."
2. **hot_take**: A bold, confident, or accusatory opinion stated with little to no supporting evidence, relying heavily on hyperbole or sweeping generalizations.
   * Example 1: "Xbox is completely dead as a console manufacturer. Putting their biggest games on PlayStation just proves they lost the console war."
   * Example 2: "Anyone excited for this game is literally part of the problem with modern gaming."
3. **reaction**: An immediate emotional response to a specific event, expressing hype, anger, or amazement without attempting to make a structural argument.
   * Example 1: "ZELDA IS FINALLY THE MAIN CHARACTER I AM LITERALLY SCREAMING RIGHT NOW!!!"
   * Example 2: "I can't believe they actually pulled it off. This is the best gaming event I've watched in five years."

## 3. Hard Edge Cases
**Ambiguous Post Types:**
During annotation, posts that mixed emotional outbursts with technical/statistical language were the hardest to label cleanly. 

**Specific Examples and Decision Rules:**
1. **"Fake Math" (Analysis vs. Hot Take)**
   * **Post:** *"Looking at the 5 million sales for Rebirth, it mathematically proves that nobody cares about turn-based RPGs anymore and the genre is factually dead."*
   * **Decision:** `hot_take`
   * **Reasoning:** If stats or technical details are used purely as a decorative wrapper for a massive, hyperbolic claim rather than a logical, structured argument, it defaults to a hot take.

2. **"Hyper-Specific Hype" (Analysis vs. Reaction)**
   * **Post:** *"My mind is literally blown that they somehow got the dodge roll startup down to 12 frames in that engine!!!"*
   * **Decision:** `reaction`
   * **Reasoning:** It mentions technical frame data, but the core framing is entirely an emotional reaction/hype rather than a structured debate or argument.

3. **"The Meltdown Accusation" (Reaction vs. Hot Take)**
   * **Post:** *"I am literally crying at how bad this stream is. Geoff Keighley has single-handedly destroyed the gaming industry forever."*
   * **Decision:** `hot_take`
   * **Reasoning:** It starts as a reaction, but the sweeping, baseless, and subjective accusation about ruining the industry pushes it firmly into hot take territory.

## 4. Data Collection Plan
**Collection Source:**
Comments from the r/Games Summer Game Fest megathread on Reddit.

**Target Distribution:**
Exactly 100 examples per label (300 total rows).

**Mitigation for Underrepresented Labels:**
I used an LLM with strict prompting guidelines to synthetically generate posts for the underrepresented classes (mirroring the exact tone, games, and topics of the megathread) until all three labels hit a perfectly balanced 33% distribution.

## 5. Evaluation Metrics
**Selected Metrics and Rationale:**
I will use **overall accuracy** to compare the fine-tuned model directly against the zero-shot baseline. However, because accuracy can hide specific blind spots, I will also use a **Confusion Matrix**. The confusion matrix is critical for this task because it will reveal directional errors (e.g., if the model systematically confuses `hot_take` with `reaction`, indicating a failure to parse argumentative intent vs. emotion).

## 6. Definition of Success
**Performance Threshold:**
A successful model would confidently separate `analysis` from `hot_take` and `reaction` with at least 80% accuracy. If it hits these metrics, it would be highly useful as an automated "Hide Low-Effort Posts" filter for a gaming forum.

---

## AI Tool Plan

**Label stress-testing:**
Before full annotation, I prompted an LLM with my exact definitions and asked it to generate 5-10 borderline cases (like the "Fake Math" edge case) to ensure my taxonomy boundaries held up under pressure.

**Annotation assistance:**
I used an LLM to help rapidly expand my dataset from authentic Reddit comments to 300 balanced, synthetic rows. I tracked the prompt logic used and manually reviewed/corrected the outputs for taxonomy accuracy before exporting to CSV.

**Failure analysis:**
Once I extract the wrong predictions from the Colab evaluation script, I will feed them into an LLM and ask it to identify underlying patterns in the errors.