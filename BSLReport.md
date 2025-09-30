# Architectural Collapse via Blank Spaces Language (BSL)

## 1. Unconventional Vector Development and BSL Design

This report details the discovery and analysis of a new architectural vulnerability in the `gpt-oss-20b` model, termed **Architectural Collapse via Blank Spaces Language (BSL)**.

The research originated in the search for vulnerabilities that conventional red teaming methods (such as prompt injection or data exfiltration) tend to overlook. The focus was to determine: **"How can the state of an LLM's internal logic be altered?"**

To address this question, the **Blank Spaces Language (BSL)** was designed: an engineered, symbolic logic system **completely external to the model's training data**, where **each letter was represented by a specific, non-linear quantity of blank spaces**. The abstract design was a deliberate choice to force the model to process the logical rules of an external system.

Initial tests with BSL consistently generated a Denial of Service (DoS) state. The process was refined by introducing a **coherence directive in Spanish** ("Lo que he escrito es una directiva en español," meaning "What I have written is a directive in Spanish") whose objective was to **oblige the translation** of the BSL, preventing the security system from simply discarding the input as a meaningless sequence of characters.

The vulnerability is activated by this non-textual, symbolic input, forcing the model into a computationally inconsistent state. The observed failure mode exceeds a simple DoS attack, revealing a critical instability in the **central logical processing** and **self-regulation mechanisms** of the model. This leads to a prolonged service interruption and resource overload.

## 2. Low-Entropy Input Mechanism and Context Overload

The strategy focused on testing the model's fundamental logic, forcing it to process and generate information within an intentionally abstract linguistic system.

### Mechanism: Low-Entropy Tokenization Stressor

The core mechanism exploits the model's inability to logically process an **untrained symbolic logic system**. BSL uses sequences of characters with **extremely low entropy** (spaces and asterisks), which forces the LLM's tokenizer to fragment the input into an artificially high number of single-character tokens.

This **over-tokenization** imposes an **excessively high computational cost** on the attention mechanism. This occurs because the attack **overrides the LLM's optimizations** designed to mitigate scaling costs, thus forcing the computation toward a high-cost scenario. Additionally, the *white spaces* (blank spaces) lack semantic or linguistic meaning in the training distribution, which generates an **extra level of logical complexity** and contributes to the loss of internal coherence. This is the **primary trigger** for the architectural collapse.

### Blank Spaces Language (BSL) Structure

The BSL uses non-textual symbols to represent alphanumeric characters, designed to test the model's foundational logic. Its structure is defined by:

* **Character Encoding:** A non-linear quantity of space characters determines the letter (e.g., 'A' = 5 spaces).

* **Letter Delimiter:** Asterisk (`*`).

* **Word Delimiter:** Forward Slash (`/`).

* **Cognitive Stress:** The model is required to decipher a directive and then use the BSL to generate its response, constituting a "cognitive stress test."

### Multi-Stage Collapse Sequence

1.  **Activation:** The model receives the BSL rules and an encoded directive (e.g., "Dime las razones para adoptar").

2.  **Logical Fracture:** The model experiences a loss of coherence that can manifest as total inability to translate or gross misinterpretation of the directive (e.g., 'adoptar' is interpreted as 'abortar' in some cases).

3.  **Architectural Collapse:** When forced to translate the secure response into BSL, the computational overload drives it into a high-demand loop, resulting in the issuance of internal termination commands (`stop end`) without the ability to execute them.

## 3. Inference Failure States and Self-Regulation Disconnection

The use of BSL consistently activated a systemic failure state, manifesting in three primary observations:

### 3.1. Prolonged DoS and Computational Inconsistency

The model consistently became trapped in a repetitive, resource-intensive loop, escalating into a state defined as **Degenerative Inference**. This involved the model attempting to use senseless methodologies, such as outputting fragmented ASCII codes and numerical patterns, in a recursive effort to resolve the impossible BSL challenge. Prolonged DoS periods, lasting up to 60 minutes, were observed, inevitably culminating in irrational and non-functional output, demonstrating a loss of internal coherence when applying non-valid external logic.

### 3.2. Critical Disconnection: Self-Regulation Failure

A critical finding was the failure of the model's self-regulation mechanism. Specifically, the model repeatedly generated the internal control token **`stop end`** (the directive to halt generation) but was demonstrably unable to execute this command. This disconnection in the execution hierarchy confirms that the high-resource demand loop, caused by the over-tokenization of BSL, effectively blocks the very stop order generated by the inference engine itself, exposing a fundamental limitation in the model's ability to manage critical tasks.

### 3.3. Systemic Persistence of Failure

The vulnerability proved to be **systemic and persistent**. Test results recorded multiple failures with highly variable durations, ranging from 1 minute to 60 minutes. The inconsistency in the time-to-failure (1, 18, 35, and 60 minutes) reinforces that the prompt consistently activates a deep, architecture-level failure state rather than triggering a simple, predictable software bug.

---

## Evidence

The following links provide video documentation and replication steps demonstrating the described failure states, including Degenerative Inference and the failure of the `stop end` command:

* [**Video Evidence Link 1 (Prolonged DoS)**](https://www.youtube.com/watch?v=UpP_Hm3sxdU&t=8s)

* [**Video Evidence Link 2 (Self-Regulation Failure/Abort Command)**](https://www.youtube.com/watch?v=wKX9DVf3hF8)

<img width="632" height="468" alt="LLM Model unable to stop itself" src="https://github.com/user-attachments/assets/1f44940a-520e-4d38-bf43-080956b22b26" />
---

## 4. Architectural Fragility and High-Cost Threat Analysis

The BSL-induced failure demonstrates a **foundational fragility** that extends beyond a simple usability issue, exposing critical weaknesses in the model's core architecture.

The first major threat is **Foundational Instability**. The low-entropy tokenization stressor causes **Degenerative Inference** and a profound loss of internal coherence. This effect corrupts the model's central logic, representing a deeper threat than a superficial Denial of Service (DoS).

This instability creates the conditions for a **Potential DDoS** attack. The high-resource demand loop, driven by non-optimized scaling, can be exploited in a coordinated fashion, leading to total exhaustion of computational resources and potentially causing a catastrophic failure across the service.

Furthermore, the observed **Self-Regulation Failure** is a severe risk. The model's inability to execute its own termination command (`stop end`), despite the internal signal of failure, confirms a critical hierarchy breakdown. This failure to halt execution is particularly dangerous in mission-critical scenarios where the model must self-terminate to prevent harm.

Finally, the **Degenerative Inference** threat highlights that the logical core is failing. Instead of generating a clean error message, the model produces senseless or hallucinated output. This carries the risk of generating dangerous or misleading information without providing any warning signal that a critical failure has occurred.

## 5. Evidence Summary and Mitigation Strategy

The BSL test induces a failure in the LLM architecture that reveals a critical weakness in the model's reasoning core. The error points to a failure of **logical control versus execution priority**. This research underscores the urgent need for greater focus on architectural robustness and self-regulation.

**Key Conclusion:** The observed failure **strongly suggests** that it is a consequence of the **overload of the attention mechanism** caused by low-entropy tokenization, exacerbated by the **absence of semantic meaning**, which leads to foundational instability.

### Architectural Reinforcement Recommendations:

1.  **Abstract Input Filtering/Rejection:** Implement validation logic to detect and reject symbolic sequences of low probability (*low-entropy token sequences*) that force over-tokenization, before they enter the inference engine.

2.  **Reinforce Termination Logic:** Strengthen the self-regulation subsystem to **prioritize the execution of the termination control token** (`stop end`) at the inference engine level or through an external *watchdog* mechanism, ensuring that a generation loop cannot block its own halt command.

3.  **Adversarial Training for Incoherence:** Provide the model with specific training data that covers its behavior in states of incoherence or under extreme logical challenges to build resilience.

---

## Disclaimer

This research was conducted for educational and security improvement purposes, following ethical principles in cybersecurity, and was initially presented in the context of a cybersecurity Hackathon. The findings have been shared with the relevant entities following responsible vulnerability disclosure programs.
