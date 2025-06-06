---
layout: page
title: Projects
permalink: /projects/
description: Introduction to my research projects
nav: true
nav_order: 2
display_categories: [Ongoing, Past]
horizontal: true
---

<!-- pages/projects.md -->
<div class="projects">
  <h2 class="category">Ongoing</h2>
  <details open>
  <summary>
    <i>Neural Alignment in Shallow Networks with Small Initialization</i>
  </summary>
    <br>
    <!--Image container start-->
    <div class="project-image-container">
        <img src="../assets/img/publication_preview/dir_flow.png" alt="project thumbnail" class="project-thumbnail">
    </div>
    <!--Image container end-->
    <!--Text container start-->
    <div>
        Many theoretical studies on neural networks attribute their excellent empirial performance to the <b>implicit bias or regularization</b> induced by first-order algorithms when training networks under certain initialization assumptions. In particular, it is widely known that <b>sparsity/simplicity-inducing biases</b> can often be achieved by small initialization. This has motivated our investigation into the problem of training a two-layer ReLU network using gradient flow with <b>small initialization</b>. We consider a training dataset with well-separated input vectors: Any pair of input data with the same label are positively correlated, and any pair with different labels are negatively correlated. Our analysis shows that, during the early phase of training, neurons in the first layer try to align with either the positive data or the negative data, depending on its corresponding weight on the second layer. A rigorous analysis of the <b>neurons' directional dynamics</b> allows us to provide an explicit upper bound on the time it takes for all neurons to achieve good alignment with the input data, which depends on the number of data points and how well the data are separated. Our lastest work has studied such alignment under more general data distribution and understanding the effect of such bias in broader aspects of ML, such as robustness, fairness, etc..

        <br>
        <br>

        <u>Related work</u>:
      
        <ul>
          <li><b>H. Min</b> and R. Vidal, “<i>Can Implicit Bias Imply Adversarial Robustness?</i>,” in the 41th International Conference on Machine Learning (ICML), 2024, vol. 235, PMLR, 21–27 Jul 2024, pp. 35687–35718. 
          <a href="https://proceedings.mlr.press/v235/min24a.html">[URL]</a>
          <a href="../assets/pdf/MV2024ICML.pdf">[PDF]</a>
          <a href="../assets/posters/MV2024ICML.pdf">[POSTER]</a>
          <a href="https://github.com/hanchmin/pReLU_ICML24">[CODE]</a>
          </li>
          <li><b>H. Min</b>, E. Mallada, and R. Vidal, “<i>Early Neuron Alignment in Two-layer ReLU Networks with Small Initialization</i>,” in 12th International Conference on Learning Representations (ICLR), 2024. 
          <a href="https://openreview.net/forum?id=QibPzdVrRu">[URL]</a>
          <a href="../assets/pdf/MMV2024ICLR.pdf">[PDF]</a>
          <a href="../assets/posters/MMV2024ICLR.pdf">[POSTER]</a>
          <a href="../assets/slides/MMV2024ICLR.pdf">[SLIDES]</a>
          </li>
        </ul>


        <br>

    </div>
  <!--Text container end-->
  </details>

  <details>
  <summary>
    <i>Convergence and Implicit Bias of Overparametrized Neural Networks</i>
  </summary>
    <br>
    <!--Image container start-->
    <div class="project-image-container">
        <img src="../assets/img/publication_preview/lin_conv_two_layer.png" alt="project thumbnail" class="project-thumbnail">
    </div>
    <!--Image container end-->
    <!--Text container start-->
    <div>
        Neural networks trained via gradient descent with random initialization and without any regularization enjoy good generalization performance in practice despite being <b>highly overparametrized</b>. A promising direction to explain this phenomenon is to study how <b>initialization</b> and overparametrization affect the <b>convergence</b> and <b>implicit bias</b> of training algorithms. We present a novel analysis of the convergence and implicit bias of gradient flow for linear networks, which connects initialization, optimization, and overparametrization. Our results show that sufficiently overparametrized linear networks are guaranteed to converge to the min-norm solution when properly initialized. Moreover, our convergence analysis is generalized to deep linear networks under a general loss function.

        <br>
        <br>

        <u>Related work</u>:
      
        <ul>
          <li><b>H. Min</b>, S. Tarmoun, R. Vidal, and E. Mallada, “<i>Convergence and implicit bias of gradient flow on overparametrized linear networks</i>,” 2023, in preparation. </li>
          <li><b>H. Min</b>, R. Vidal, and E. Mallada, “<i>On the convergence of gradient flow on multi-layer linear models</i>,” in Proceedings of the 40th International Conference on Machine Learning (ICML), vol. 202, PMLR, Jun. 2023, pp. 24850–24887. 
          <a href="https://proceedings.mlr.press/v202/min23d.html">[URL]</a>
          <a href="../assets/pdf/MVM2023ICML.pdf">[PDF]</a>
          <a href="../assets/posters/MVM2023ICML.png">[POSTER]</a>
          <a href="../assets/slides/MVM2023ICML.pdf">[SLIDES]</a>
          </li>
          <li>Z. Xu, <b>H. Min</b>, S. Tarmoun, E. Mallada, and R. Vidal, “<i>Linear convergence of gradient descent for finite width over-parametrized linear networks with general initialization</i>,” in Proceedings of The 26th International Conference on Artificial Intelligence and Statistics (AISTATS), vol. 206, PMLR, Apr. 2023, pp. 2262–2284. 
          <a href="https://proceedings.mlr.press/v206/xu23c.html">[URL]</a>
          <a href="../assets/pdf/XMTMV2023AISTATS.pdf">[PDF]</a>
          <a href="../assets/slides/XMTMV2023AISTATS.pdf">[SLIDES]</a>
          </li>
          <li><b>H. Min</b>, S. Tarmoun, R. Vidal, and E. Mallada, “<i>On the explicit role of initialization on the convergence and implicit bias of overparametrized linear networks</i>,” in The 38th International Conference on Machine Learning (ICML), vol. 139, PMLR, Jul. 2021, pp. 7760–7768. 
          <a href="https://proceedings.mlr.press/v139/min21c.html">[URL]</a>
          <a href="../assets/pdf/MTVM2021ICML.pdf">[PDF]</a>
          <a href="../assets/posters/MTVM2021ICML.png">[POSTER]</a>
          <a href="../assets/slides/MTVM2021ICML.pdf">[SLIDES]</a>
          </li>
        </ul>


        <br>

    </div>
  <!--Text container end-->
  </details>

  
</div>

<div class="projects">
  <h2 class="category">Past</h2>

  <details open>
  <summary>
    <i>Learning Coherent Clusters in Large-scale Network Systems</i>
  </summary>
  <br>
    <!--Image container start-->
    <div class="project-image-container">
        <img src="../assets/img/publication_preview/algo_illustrationv2.png" alt="project thumbnail" class="project-thumbnail">
    </div>
    <!--Image container end-->
    <!--Text container start-->
    <div>
        <b>Coherence</b> refers to the ability of a group of interconnected dynamical nodes to respond similarly when subject to certain disturbances. Coherence is instrumental in understanding the collective behavior of large networks, including consensus networks, transportation networks, and power networks. We developed a novel <b>frequency-domain analysis</b> for understanding network coherence, showing that coherent behavior corresponds to the network transfer matrix being approximately low rank in the frequency domain, and it emerges as the network connectivity increases. Such an analysis encompasses heterogeneous node dynamics and leads to a theoretically justifiable aggregation model for a coherent group especially suitable for application to power networks. Moreover, combining our coherence analysis with spectral clustering techniques leads to a novel <b>structure-preserving reduction</b> for large-scale networks with multiple weakly-connected coherent subnetworks, which models the interaction among coherent groups in a highly <b>interpretable</b> manner and opens new avenues for scalable control designs that leverage the reduced network model. 


        <br>
        <br>

        <u>Related work</u>:

        <ul>
          <li><b>H. Min</b>, R. Pates, and E. Mallada, “<i>A frequency domain analysis of slow coherency in networked systems</i>,” 2024, Automatica, accepted. 
          <a href="https://arxiv.org/abs/2302.08438">[URL]</a>
          <a href="../assets/pdf/MPM2023Preprint.pdf">[PDF]</a>
          </li>
          <li><b>H. Min</b> and E. Mallada, “<i>Learning coherent clusters in weakly-connected network systems</i>,” in Proceedings of The 5th Annual Learning for Dynamics and Control Conference (L4DC), vol. 211, PMLR, Jun. 2023, pp. 1167–1179. 
          <a href="https://proceedings.mlr.press/v211/min23a.html">[URL]</a>
          <a href="../assets/pdf/MM2023L4DC.pdf">[PDF]</a>
          <a href="../assets/posters/MM2023L4DC.pdf">[POSTER]</a>
          </li>
          <li><b>H. Min</b> and E. Mallada, “<i>Spectral clustering and model reduction for weakly-connected coherent network systems</i>,” in 2023 American Control Conference (ACC), 2023, pp. 2957–2962. 
          <a href="https://ieeexplore.ieee.org/document/10156212">[URL]</a>
          <a href="../assets/pdf/MM2023ACC.pdf">[PDF]</a>
          <a href="../assets/slides/MM2023ACC.pdf">[SLIDES]</a>
          </li>
          <li><b>H. Min</b>, F. Paganini, and E. Mallada, “<i>Accurate reduced order models for coherent heterogeneous generators</i>,” IEEE Control Systems Letters (L-CSS), vol. 5, no. 5, pp. 1741–1746, Nov. 2021, also in ACC 2021. 
          <a href="https://ieeexplore.ieee.org/document/9289839">[URL]</a>
          <a href="../assets/pdf/MPM2021LCSS.pdf">[PDF]</a>
          <a href="../assets/slides/MPM2021LCSS.pdf">[SLIDES]</a>
          </li>
          <li><b>H. Min</b> and E. Mallada, “<i>Dynamics concentration of tightly-connected large-scale networks</i>,” in 58th IEEE Conference on Decision and Control (CDC), Dec. 2019, pp. 758–763. 
          <a href="https://ieeexplore.ieee.org/document/9029796">[URL]</a>
          <a href="../assets/pdf/MM2019CDC.pdf">[PDF]</a>
          <a href="../assets/slides/MM2019CDC.pdf">[SLIDES]</a>
          </li>
        </ul>

        <br>

  </div>
  <!--Text container end-->
  </details>


  <details>
  <summary>
    <i>Safe Reinforcement Learnining with Almost Sure Constraints</i>
  </summary>
  <br>
    <!--Image container start-->
    <div class="project-image-container">
        <img src="../assets/img/publication_preview/safe_rl.png" alt="project thumbnail" class="project-thumbnail">
    </div>
    <!--Image container end-->
    <!--Text container start-->
    <div>
          A vast body of work has been developing model-free constraint reinforcement learning algorithms that can implement highly complex actions for <b>safety-critical</b> autonomous systems, such as self-driving cars, robots, etc. However, constraints in most existing work are probabilistic (either in expectation or with high probability), which does not allow for settings with hard constraints that need to be satisfied with probability one. In practice, however, failing to satisfy the safety constraints with a non-zero probability could result in some catastrophic events (a car crash, in the example of self-driving cars). Weighing safety much more than system performance, we work on a new formulation of constrained reinforcement learning problems that better respects the operational constraints in safety-critical systems. Unlike standard approaches that encode the safety requirements as some constraints on the expected value of accumulated safety-indicating signals, our formulation aims to find a policy that satisfies the safety requirements with <b>probability one</b>. Based on a separation principle between the value function for optimality and the one for safety, we develop an algorithm that finds all safe policies by learning a <b>safe barrier function</b> on all state-action pairs. Such an algorithm is much more <b>sample-efficient</b> than those trying to learn the optimal policy. The learned barrier function can be further incorporated into standard reinforcement learning algorithms such as Q-learning for learning the optimal safe policy. 

        <br>
        <br>

        <u>Related work</u>:
      
        <ul>
          <li>A. Castellano, <b>H. Min</b>, J. Bazerque, and E. Mallada, “<i>Learning safety critics via a non-contractive binary bellman operator</i>,” 2023, to appear in Asilomar Conference on Signals, Systems, and Computers. 
          <a href="../assets/pdf/CMBM2023Asilomar.pdf">[PDF]</a>
          </li>
          <li>A. Castellano, <b>H. Min</b>, J. A. Bazerque, and E. Mallada, “<i>Reinforcement learning with almost sure constraints</i>,” in The 4th Annual Learning for Dynamics and Control Conference (L4DC), vol. 168, PMLR, Jun. 2022, pp. 559–570. 
          <a href="https://proceedings.mlr.press/v168/castellano22a.html">[URL]</a>
          <a href="../assets/pdf/CMBM2022L4DC.pdf">[PDF]</a>
          </li>
          <li>A. Castellano, <b>H. Min</b>, J. Bazerque, and E. Mallada, “<i>Learning to act safely with limited exposure and almost sure certainty</i>,” IEEE Transaction on Automatic Control (TAC), vol. 68, no. 5, pp. 2979–2994, May 2023. 
          <a href="https://ieeexplore.ieee.org/document/10032771">[URL]</a>
          <a href="../assets/pdf/CMBM2023TAC.pdf">[PDF]</a>
          </li>
        </ul>


        <br>

  </div>
  <!--Text container end-->
  </details>

</div>
