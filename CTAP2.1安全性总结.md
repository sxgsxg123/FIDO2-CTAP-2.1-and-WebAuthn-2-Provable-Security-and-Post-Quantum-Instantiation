Security Conclusions for CTAP 2.1

After having defined security for ePACA protocols above, we now present the security statements for CTAP 2.1. We give the full proofs of our two theorems (against PPT and QPT adversaries) in Section I and J in the appendix. Our first theorem shows the SUF-t ′ security of CTAP 2.1 against PPT adversaries.

Theorem 2 (PPT security of CTAP 2.1). Let ePACA = (Reboot, Setup, Bind, Auth, Validate) denote the CTAP 2.1 protocol described in Section V-B. Assume that ePACA supports puvProtocoli for i ∈ {1, 2, 3}. If the hash function H is ϵ coll-res H collision resistant, Hi : {0, 1} ⋆ → {0, 1} li is modeled as independent random oracle for i ∈ {1, ..., 7}, SKE1 is ϵ ind-1cpa-H2 SKE1 IND-1CPA-H2 and ϵ ind-1$pa-lpc SKE1 -IND-1$PA-LPC secure, SKEi is ϵ ind-1cpa SKEi -IND-1CPA and ϵ ind-1$pa-lpc SKEi -IND-1$PA-LPC secure for i ∈ {2, 3}, and the sCDH problem over ECDH with prime order q is ϵ sCDH ECDH hard, then the advantage of any PPT adversary A that breaks SUF-t ′ security of ePACA is bounded by
$$
\begin{aligned}&\mathrm{Adv}_{\mathrm{PACA},\mathcal{A}}^{\mathrm{SUF-t^{\prime}}}(1^{\lambda})\\&\leq(q_{\mathrm{SETUP}}+q_{\mathrm{EXECUTE}})\epsilon_{\mathrm{ECDH}}^{\mathrm{sCDH}}+\epsilon_{\mathrm{H}}^{\mathrm{coll-res}}\\&+\begin{pmatrix}q_{\mathrm{SETUP}}+q_{\mathrm{EXECUTE}}\\2\end{pmatrix}(2^{2-\min\{l_{1},l_{3},l_{5},l_{6}\}}+2^{1-q})\\&+q_{\mathrm{NEWU}}2^{-\alpha_{\mathcal{D}}}+\begin{pmatrix}q_{\mathrm{SEND-BIND-T}}\\2\end{pmatrix}2^{-\min\{\mu,2,\mu^{\prime}\}\lambda}\\&+q_{\mathrm{SETUP}}\max\{\epsilon_{\mathrm{SKE}_{1}}^{\mathrm{ind-1cpa-H}_{2}},\epsilon_{\mathrm{SKE}_{2}}^{\mathrm{ind-1cpa}},\epsilon_{\mathrm{SKE}_{3}}^{\mathrm{ind-1cpa}}\}\\&+q_{\mathrm{EXECUTE}}\max\{\epsilon_{\mathrm{SKE}_{1}}^{\mathrm{ind-1Spa-lpc}},\epsilon_{\mathrm{SKE}_{2}}^{\mathrm{ind-1Spa-lpc}},\epsilon_{\mathrm{SKE}_{3}}^{\mathrm{ind-1Spa-lpc}}\}\\&+q_{\mathrm{SETUP}}\text{pinRetriesMax}2^{-\alpha_{2}}\\&+q_{\mathrm{VALIDATE}}2^{-\min\{\mu\lambda,2\lambda,\mu^{\prime}\lambda,l_{2},l_{4},l_{7}\}}\end{aligned}
$$
where qO denotes the number of queries to O = {SETUP, EXECUTE, VALIDATE} and qi denotes the number of queries to random oracle Hi for i ∈ {1, ..., 7}.



Proof Sketch. The proof is divided into the following steps: (1) By the random oracle Hi for i ∈ {1, 3, 5, 6} and the sCDH assumption on the underlying ECDH, all keys K derived from the encapsulation of the underlying puvProtocol in the obtainSharedSecret-C-end algorithm, which is only invoked in the SETUP and EXECUTE oracles, are distinct except probability 
$$
(q_{\mathrm{SETUP}}+q_{\mathrm{EXECUTE}})\epsilon_{\mathrm{ECDH}}^{\mathrm{sCDH}}+\binom{q_{\mathrm{SETUP}}+q_{\mathrm{EXECUTE}}}{2}2^{2-\min\{l_{1},l_{3},l_{5},l_{6}\}}.
$$
(2) By the entropy of the user PIN αD, none of the user PIN sampled in NEWU oracle is predicable except with probability qNEWU2 −αD .

 (3) By the collision-resistance of H and the entropy of the Diffie-Hellman public keys 2^q and of pt values 2 max{µ,2,µ′}λ , we have the all H(pin), Diffie-Hellman public keys, pt values, are respectively distinct except probability in total 
$$
\epsilon_{\mathsf{H}}^{\mathsf{coll-res}}+\binom{q_{\mathsf{SETUP}+\mathsf{EXECUTE}}}{2}2^{1-q}+\binom{q_{\mathsf{SEND-BIND-T}}}{2}2^{-\operatorname*{min}\{\mu,2,\mu^{\prime}\}\lambda}.
$$
(4) By the IND-1CPA-H2 security of SKE1 and the IND-1CPA security of SKE2 and SKE3, the pins encrypted by the underlying puvProtocol in the setPIN-C algorithm, which is only invoked in the SETUP oracle, are indistinguishable from random except probability 
$$
q_{\mathrm{SETUP}}\max\{\epsilon_{\mathrm{SKE}_{1}}^{\mathrm{ind-1cpa-H}_{2}},\epsilon_{\mathrm{SKE}_{2}}^{\mathrm{ind-1cpa}},\epsilon_{\mathrm{SKE}_{3}}^{\mathrm{ind-1cpa}}\}
$$
(5) By the IND-1$PA-LPC security of SKEi for i ∈ {1, 2, 3}, the pinHashs encrypted by the underlying puvProtocol in the obtainPinUvAuthToken-C-start algorithm, which is invoked only in the EXECUTE oracle, are indistinguishable from random except probability 
$$
q_{\mathrm{EXECUTE}}\max\{\epsilon_{\mathrm{SKE}_{1}}^{\mathrm{ind-1\$pa-Ipc}},\epsilon_{\mathrm{SKE}_{2}}^{\mathrm{ind-1\$pa-Ipc}},\epsilon_{\mathrm{SKE}_{3}}^{\mathrm{ind-1\$pa-Ipc}}\}.
$$
Finally, the adversary A cannot trigger the flip of the win-SUF-t ′ predicate in Figure 6 via condition (i) in Line 8, due to the design of CTAP 2.1, see validate-T algorithm in CTAP 2.1. (ii) in Line 9, due to the distinction of DiffieHellman public keys, (iii) in Line 10, due to the distinction of Diffie-Hellman public keys and pts, (iv) in Line 11-14, since A obtains no information about pins or pts and can only win by randomly guessing the pin in the SETUP oracle maximal pinRetriesMax times for each token session, or the pt values or the tags t in the Validate algorithm in the VALIDATE oracle, which happens with probability except
$$
q_{\mathrm{SETUP}}\text{pinRetriesMax}2^{-\alpha_{2}}+q_{\mathrm{VALIDATE}}2^{-\operatorname*{min}\{\mu\lambda,2\lambda,\mu^{\prime}\lambda,l_{2},l_{4},l_{7}\}}
$$
in total, modeling H7 as a random oracle.



The above theorem proves that CTAP 2.1 only accepts messages under the user’s approval, which is captured by winning condition 1. Winning conditions 2 and 3 capture the uniqueness of each session identifiers: if two sessions are partnered with each other, then they are each other’s unique partners. Condition 4 ensures the token only accepts the authorization from a client that it binds to if (1) the binding phase is trusted, (2) the binding state (on the client side) is not compromised if available, and (3) the user PIN that sets up the token is not corrupted.

As is to be expected, the above theorem only holds when the token’s user PINs have large enough entropy. If a user PIN is predictable, the attacker can perform active attacks and authorize malicious commands towards the token.

Moving to the security guarantees against quantum adversaries, we note that the asymmetric cryptographic primitives in puvProtocol1 and puvProtocol2 are simply ECDH, which is quantum-vulnerable. Therefore, A can trivially win SUF-t ′ experiment by selecting the Pin/Uv Auth Protocol in a test session to be puvProtocol1 or puvProtocol2 . The theorem below suggests the security of the test session if puvProtocol3 is selected as instantiation.



Theorem 3 (QPT security of CTAP 2.1). Let ePACA = (Reboot, Setup, Bind, Auth, Validate) denote the CTAP 2.1 protocol described in Section V-B. Assume that the underlying H is ϵ coll-res H -collision resistant, H5 is ϵ swap H5 -swap secure, Hi is ϵ prf Hi -prf secure for i ∈ {6, 7}, SKE3 is ϵ ind-1cpa SKE3 -IND-1CPA and ϵ ind-1$pa-lpc SKE3 -IND-1$PA-LPC secure, and that the KEM in puvProtocol3 with public-key entropy αpk and ciphertext entropy αc is ϵ ind-cca KEM -IND-CCA secure. If there exists a QPT adversary A that breaks the SUF-t ′ security of ePACA for a test session π that uses puvProtocol3 , then we have that
$$
\begin{aligned}&\mathrm{Adv}_{\mathrm{ePACA,QPT}}^{\mathrm{SUF-t^{\prime}}}(\mathcal{A})\\&\leq(q_{\mathrm{SETUP}}+q_{\mathrm{EXECUTE}})(\epsilon_{\mathrm{KEM}}^{\mathrm{ind-cca}}+\epsilon_{\mathrm{H_{5}}}^{\mathrm{swap}}+\epsilon_{\mathrm{H_{6}}}^{\mathrm{prf}})\\&+\begin{pmatrix}q_{\mathrm{SETUP}}+q_{\mathrm{EXECUTE}}\\2\end{pmatrix}2^{1-l_{6}}+\epsilon_{\mathrm{H}}^{\mathrm{coll-res}}+q_{\mathrm{NEWU}}2^{-\alpha_{2}}\\&+\begin{pmatrix}q_{\mathrm{SEND-BIND-T}}\\2\end{pmatrix}2^{-\mu^{\prime}\lambda}+\begin{pmatrix}q_{\mathrm{EXECUTE}}\\2\end{pmatrix}(2^{-\alpha_{pk}}+2^{-\alpha_{c}})\\&+q_{\mathrm{SETUP}}\epsilon_{\mathrm{SKE}_{3}}^{\mathrm{ind-1cpa}}+q_{\mathrm{EXECUTE}}\epsilon_{\mathrm{SKE}_{3}}^{\mathrm{ind-1Spa-Ipc}}\\&+q_{\mathrm{SETUP}}\text{pinRetriesMax}2^{-\alpha_{D}}+\begin{pmatrix}q_{\mathrm{EXECUTE}}\\2\end{pmatrix}(2^{-\alpha_{pk}}+2^{-\alpha_{c}})\\&+q_{\mathrm{VALIDATE}}(2^{-\mu^{\prime}\lambda}+\epsilon_{\mathrm{H}_{7}}^{\mathrm{prf}}+2^{-l_{7}})\end{aligned}
$$
where qO denotes the number of queries to O = {SETUP, EXECUTE, VALIDATE}.

Proof Sketch. The proof is similar to the one for Theorem 2 and consists of following steps: (1) By the IND-CCA security of KEM, the swap security of H5, and the prf security of H6, all keys K derived in from the encapsulation of the underlying puvProtocol in the obtainSharedSecret-C-end algorithm,which is only invoked in the SETUP and EXECUTE oracles, are distinct except probability (qSETUP +qEXECUTE)ϵ sCDH ECDH + (qSETUP + qEXECUTE)(ϵ ind-cca KEM + ϵ swap H5 + ϵ prf H6 ) + 
$$
\binom{q_\mathrm{SETUP}+q_\mathrm{EXECUTE}}{2}2^{1-l_6}.
$$
(2) By the entropy of the user PIN αD, none of the user PIN sampled in NEWU oracle is predicable except with probability qNEWU2 −αD .

(3) By the collision-resistance of H and the entropy 2 −µ ′λ of pt values sampled in the SEND-BIND-T oracle, we have all H(pin) and pt values respectively distinct except probability in total 
$$
\epsilon_{\mathsf{H}}^{\mathsf{coll-res}}+\binom{q_{\mathsf{SEND-BIND-T}}}{2}2^{-\mu^{\prime}\lambda}.
$$
 (4) By the IND-1CPA security of SKE3, the pins encrypted by the underlying puvProtocol3 in the setPIN-C algorithm, which is only invoked in the SETUP oracle, are indistinguishable from random except probability qSETUPϵ ind-1cpa SKE3 . (5) By the IND-1$PA-LPC security of SKE3, the pinHashs encrypted by the underlying puvProtocol3 in the obtainPinUvAuthToken-C-start algorithm, which is invoked only in the EXECUTE oracle, are indistinguishable from random except probability qEXECUTEϵ ind-1$pa-lpc SKE3 .

Finally, the adversary A cannot trigger the flip of the win-SUF-t ′ predicate in Figure 6 via condition (i) in Line 8, due to the design of CTAP 2.1, see validate-T algorithm in CTAP 2.1, (ii) in Line 9, since the collision of KEM public keys or ciphertexts with entropy αpk or αc happens at most  
$$
\binom{q_{\mathrm{EXECUTE}}}{2}(2^{-\alpha_{pk}}+2^{-\alpha_{c}}),
$$
 (iii) in Line 10, due to the pairwise distinct KEM public keys and pts in the tokens’ session identifiers, (iv) in Line 11-14, since A obtains no information about pins or pts and can only win by randomly guessing the pin in the SETUP oracle maximal pinRetriesMax times for each token session, or the pt values or the tags t in the Validate algorithm in the VALIDATE oracle, which happens with probability except 
$$
q_{\mathrm{SETUP}}\text{pinRetriesMax}2^{-\alpha D}+q_{\mathrm{VALIDATE}}2^{-\mu^{\prime}\lambda}+\epsilon_{\mathrm{H}_{7}}^{\mathrm{prf}}+2^{-l}
$$
in total, assuming the prf security of the underlying H7.

As such, we suggest to add our PQ instantiation puvProtocol3 of CTAP 2.1 to the specifications. As mentioned in Section V-C, we also suggest to increase the security parameter from 256 to 512, in order to preserve the current 256-bits level security.