# First Set of Equivalencies

1. **¬(φ U ψ) ≡ (¬φ R ¬ψ)**

   The "Until" (U) operator means φ holds until ψ becomes true. Negating this means that it's **not** the case that φ holds until ψ becomes true, which is equivalent to saying that either:

   - ¬φ always holds, or
   - ψ never becomes true.
   
   This is exactly what the "Release" (R) operator means when you apply it to ¬φ and ¬ψ: "¬φ is released by ¬ψ" means that ¬φ holds until ¬ψ becomes true, but ¬ψ might never become true, in which case ¬φ must hold globally. Hence, the negation of an "until" is equivalent to a release of the negated formulas.

   **Proof Idea:**
   - **¬(φ U ψ)** means that it is **not true** that "φ holds until ψ becomes true," implying that either ψ never becomes true or ¬φ holds before ψ becomes true.
   - The formula **(¬φ R ¬ψ)** states that "¬φ holds until ¬ψ is released," meaning that if ¬ψ doesn't happen, ¬φ holds forever.

2. **¬(φ R ψ) ≡ (¬φ U ¬ψ)**

   The "Release" operator (R) means ψ must hold either globally or at the point when φ becomes false. The negation of this is that ψ does **not** hold globally and φ becomes false before ψ can be true. This is the definition of the "Until" operator (U) applied to the negations of φ and ψ.

   **Proof Idea:**
   - **¬(φ R ψ)** means it's **not true** that ψ holds until φ is released (either ψ holds globally or φ is false when ψ becomes true).
   - The formula **(¬φ U ¬ψ)** captures that "¬φ holds until ¬ψ becomes true," meaning ¬ψ becomes true before φ can hold, which is the negation of the release condition.

3. **F φ ≡ T U φ**

   The "Future" (F) operator means "eventually φ will be true." This is equivalent to saying that "True holds until φ becomes true" (since "True" is always true, φ must eventually occur).

   **Proof:**
   - **F φ** means φ will be true at some point in the future.
   - **T U φ** means "True" holds until φ becomes true. Since "True" always holds, φ will inevitably become true at some point.

4. **G φ ≡ ¬T R φ**

   The "Global" (G) operator means "φ holds at every point in time." This is equivalent to saying that it's **not** true that "True is released by φ" (i.e., True holds until φ does not hold, which implies φ holds globally).

   **Proof Idea:**
   - **G φ** means φ holds at every point in time.
   - **¬T R φ** means "it is not true that True is released by φ," i.e., φ must hold always without release, meaning φ is globally true.

5. **φ U ψ ≡ φ W ψ ∧ F ψ**

   "Until" (U) says that φ holds until ψ becomes true. This is the same as saying φ weakly holds until ψ (W) and ψ eventually becomes true (F ψ). The weak until (W) allows the possibility that ψ never becomes true, but if ψ **must** become true, then the two expressions are equivalent.

   **Proof Idea:**
   - **φ U ψ** means "φ holds until ψ becomes true."
   - **φ W ψ ∧ F ψ** means "φ weakly holds until ψ becomes true (i.e., φ holds as long as ψ doesn't become true) and ψ **eventually** becomes true."

---

# Second Set of Equivalencies

1. **φ W ψ ≡ φ U ψ ∨ G φ**

   The weak until operator (W) allows φ to hold as long as ψ does not become true, but ψ might never become true. This is equivalent to saying either:

   - φ holds until ψ becomes true (φ U ψ), or
   - φ holds globally (G φ), in the case where ψ never becomes true.
   
   **Proof Idea:**
   - **φ W ψ** means "φ holds until ψ becomes true, or if ψ never becomes true, φ holds forever."
   - **φ U ψ ∨ G φ** captures that either "φ holds until ψ becomes true," or "φ holds globally if ψ never becomes true."

2. **φ W ψ ≡ ψ R (ψ ∨ φ)**

   Weak until can be transformed using the "Release" operator. The intuition here is that weak until (W) allows the possibility that ψ never becomes true, which corresponds to the idea that ψ "releases" φ, meaning ψ holds or φ continues to hold.

   **Proof Idea:**
   - **φ W ψ** allows φ to hold until ψ becomes true or ψ never becomes true.
   - **ψ R (ψ ∨ φ)** means ψ holds globally or until φ becomes true. The release condition matches the weak until by ensuring that ψ is in control and φ can persist.

3. **φ R ψ ≡ ψ W (ψ ∧ φ)**

   Release (R) means ψ holds either until φ becomes true or ψ persists globally. This is the same as weak until applied to ψ and the conjunction of ψ and φ, since both must hold together until the release happens.

   **Proof Idea:**
   - **φ R ψ** means ψ holds globally or until φ is released.
   - **ψ W (ψ ∧ φ)** means ψ weakly holds until both ψ and φ hold together, ensuring that the release happens correctly.

# CTL Equivalencies and Proofs

To prove these Computation Tree Logic (CTL) equivalencies, we'll go through both the notation and the reasoning behind them, along with the formal steps. Here’s a guide to break them down:

## CTL Operators:
- **A**: "For all paths"
- **E**: "There exists a path"
- **X**: "Next state"
- **F**: "Eventually"
- **G**: "Globally"
- **U**: "Until"
- **R**: "Release"
- **W**: "Weak until"

In these formulas:
- **ϕ** is a CTL formula (often representing some condition or proposition).

### 1. $$AX \phi \equiv \neg EX \neg \phi$$

This states that "for all paths, in the next state, ϕ holds" is equivalent to "there does not exist a path where in the next state, ¬ϕ holds."

**Explanation:**
- $$AX \phi$$: ϕ holds in the next state in all possible paths.
- $$\neg EX \neg \phi$$: It's not possible for there to be a path where in the next state ¬ϕ holds (i.e., ϕ must hold in the next state on all paths).
- These are logically equivalent because in both cases, we are asserting that in every possible next state, ϕ holds.

### 2. $$AF \phi \equiv A[true U \phi]$$

This equivalency expresses that "on all paths, eventually ϕ will hold" is the same as saying "for all paths, ϕ will hold at some future point."

**Explanation:**
- $$AF \phi$$: On all paths, at some point in the future, ϕ will become true.
- $$A[true U \phi]$$: Along all paths, ϕ will eventually hold after (or until) any number of true steps.
- These are equivalent because both statements ensure that ϕ must eventually become true on all paths, whether directly or indirectly through the "until" operation.

### 3. $$EF \phi \equiv E[true U \phi]$$

This states that "there exists a path where ϕ eventually holds" is equivalent to "there exists a path where ϕ holds after or until some condition."

**Explanation:**
- $$EF \phi$$: There exists a path where ϕ eventually becomes true.
- $$E[true U \phi]$$: There exists a path where ϕ eventually becomes true after some arbitrary number of true conditions.
- Again, these are equivalent since both are ensuring the eventuality of ϕ on at least one path.

### 4. $$AG \phi \equiv \neg EF \neg \phi$$

This equivalence says that "ϕ holds globally on all paths" is the same as saying "there does not exist a path where eventually ¬ϕ holds."

**Explanation:**
- $$AG \phi$$: Along all paths, ϕ always holds at every state.
- $$\neg EF \neg \phi$$: There is no path where ¬ϕ holds at some point.
- These are logically equivalent since one says ϕ always holds and the other says it's never the case that ¬ϕ holds on any path.

### 5. $$EG \phi \equiv \neg AF \neg \phi$$

This expresses that "there exists a path where ϕ holds globally" is equivalent to "there does not exist a path where ¬ϕ eventually holds."

**Explanation:**
- $$EG \phi$$: There is at least one path where ϕ holds in all future states.
- $$\neg AF \neg \phi$$: It is not the case that for all paths, ¬ϕ eventually holds (meaning ϕ holds forever along some path).
- These are equivalent because both describe a path where ϕ never fails.

### Proof Example for $$A[\phi U \psi] \equiv \neg (E[\neg \psi U (\neg \psi \land \neg \phi)] \lor EG \neg \psi)$$

1. Start with the definition of $$A[\phi U \psi]$$, which means that for all paths, ϕ holds until ψ becomes true.
2. The right-hand side:
   - $$E[\neg \psi U (\neg \psi \land \neg \phi)]$$ represents the existence of a path where ψ never becomes true and ϕ fails.
   - $$EG \neg \psi$$ means there exists a path where ψ never becomes true.
   - Taking the negation of the disjunction asserts that ϕ must hold until ψ becomes true.
3. Therefore, both sides express the same thing: along all paths, ϕ holds until ψ becomes true.

### 6. **Release and Weak Until Equivalents**:

- **$$A[\phi R \psi] \equiv \neg E[\neg \psi U \neg \phi]$$**: "For all paths, ψ releases ϕ" is equivalent to "there does not exist a path where ¬ψ holds until ¬ϕ."
  
- **$$E[\phi R \psi] \equiv \neg A[\neg \psi U \neg \phi]$$**: Similar reasoning applies here, with duality between "exists" and "for all."

- **Weak Until**:
  - Weak until (W) is equivalent to release (R) or until (U) depending on its context and whether the condition on the right must eventually happen. For example:
    - $$A[\phi W \psi] \equiv A[\psi R (\phi \lor \psi)]$$: All paths satisfy "weak until."
    - $$E[\phi W \psi] \equiv E[\psi R (\phi \lor \psi)]$$: There exists a path satisfying "weak until."

By going through these equivalencies using logical negation and duality, we can better understand the underlying reasoning of Computation Tree Logic.



![[Pasted image 20241007114631.png]]
![[Pasted image 20241007114731.png]]
![[Pasted image 20241007114743.png]]