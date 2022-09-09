# MLBD_01
MRes project
\documentclass[12pt]{extarticle}
\usepackage{graphicx}
\bibliographystyle{unsrt}
\usepackage{geometry}
\usepackage{gensymb}
\usepackage{subcaption}
%\usepackage{amsmath}
\usepackage[indent=10pt]{parskip}
\geometry{
 a4paper,
 total={170mm,257mm},
 left=25mm,
 top=25mm,
 }
\graphicspath{ {./figures/} }
 
 
\begin{document}
\begin{center}


\vspace{4cm}
\huge{\textbf{\textrm{DNN Regression: Neural Network Application in Higgs Boson CP State Measurement}}}
\vspace{7cm}

\large{\textit{Qintong Li}}
\vspace{1cm}

\large{Student ID: 02158205}

\large{Project ID: MLBD\_01}
\vspace{1cm}

\large{Supervised by: Prof. David Colling}

\large{Assessed by: Dr. Daniel Winterbottom}
\vspace{1cm}

\large{Word Count: 8211}

\large{Submitted: September 9th 2022}
    
\end{center}

\newpage
\section*{Layperson's summary - Exploring the Invisible Land in an Apple}

I still remember the first time I read the book called The Map of the Invisible. The author asked a question at the beginning of the book: imagine you have an apple, you cut it in half, then cut it in half again, and again, and keep doing that. What will you end up with? I guess it is pretty normal to have such a stage in life, being curious about the most basic but eccentric questions. As time passed, most people forgot about these 'stupid' thoughts and started to focus on more 'important' things in life. Fortunately, you are not one of them. You are still wondering whether there is an answer to that question. Congratulations, this is the first step before entering the gate of particle physics.

Let's go back to the question about the apple. After billions of cutting, we end up with a set of minor constituents called atoms. If the same logic can be applied to this element, what will be inside it? Will there be anything inside? The answer is yes. The model of atoms was discovered and finalized a century ago by Thompson, Rutherford and Schr\" {o}dinger. Atoms were proved to consist of sub-atomic particles. However, this is still not the end of this path. 

"...Discoveries in this field since the 1930s have resulted in a remarkable insight into the fundamental structure of matter: Everything in the universe is found to be made from a few basic building blocks called fundamental particles. Our best understanding of how these particles are encapsulated in the Standard Model(SM) of particle physics." Quoted from the website of CERN introducing the establishment of SM. 

Nevertheless, by then, there was one last missing puzzle in SM: the Higgs boson. It was predicted in the 1960s and finally discovered in 2012 at CERN's Large Hadron Collider. Analysing the properties of this particle became one of the principal interests in this field. This project is also designed for the same purpose.

This goal can be achieved by reconstructions of observables. The decay products of the Higgs boson can be an excellent point to start with for the reconstructions. The obstacle in this process is to predict the kinematics of neutrinos, as it is the so-called invisible particle and is not detectable. This project uses ML techniques, especially Deep Neural Networks, to predict neutrinos without building any explicit physics model. This model used Monte Carlo truth as the learning target. This way, further analysis of the observables can be carried out based on the prediction. 

Apart from fundamental observables such as mass, spin and parity, the CP state is another essential property to explore. An angle between two decaying planes of Higgs decaying products is defined as acoplanarity angle. It was cumbersome to evaluate data for too many distinct acoplanarity angle sensitivities. ML techniques can then be implemented again to simplify the process.

We can see that the improvement of equipment and technical tools sizably accelerated the development of science in the history of particle physics. From the discovery of the Higgs boson to the breakthrough in its further analysis, each step is significant and cheerful. No matter how little knowledge we have at each stage, extracting as much information as possible from the limited condition. We grabbed all the chances like beasts. This will always be the spirit on the way to this endless road. 

Hope the thoughts of wondering about the result of cutting apples never fade in your mind.



\newpage
\section*{Abstract}

Machine learning(ML) techniques are finding increasing applications in high-energy physics data analysis. Extracting as much information as possible from low-level variables and implementing ML techniques with this information has become a principal interest in this field. This allows an algorithm to learn the results without explicit physics models. This paper discusses how much improvement can be introduced by ML techniques, especially by implementing DNN, to the measurement of CP-sensitive observable $\phi_{CP}$ of the Higgs boson. By implementing a multi-output DNN regressor to predict the momentum of neutrinos decayed from $\tau$ leptons, the discrimination between the CP-even(scalar) and CP-odd(pseudo-scalar) improved vastly when both $\tau$ leptons undergo $\pi$ decays. More improvements can be expected for other decay modes once the reconstruction of $\phi_{CP}$ is correct.


\tableofcontents


\section{Introduction}
Machine learning(ML) techniques have been rapidly finding a place in high-energy physics data analysis such as data selection, data classification and further predictions \cite{r24}. Various applications of ML techniques allow improvements in reconstructing high-level physics quantities without specific physics models. It shows the probability of having a general model and improves the efficiency of data analysis. This study addressed the application of ML techniques, especially Deep Neural Network(DNN), in measuring the Higgs boson CP state. 


\subsection{Measurement of CP states}

After the discovery of the Higgs boson by LHC experiments in 2012 \cite{r1,r2}, a large and growing amount of literature has investigated other basic quantum numbers such as mass \cite{r3}, spin \cite{r4,r5} and parity \cite{r5} which is crucial for studying the feature of Higgs boson. Its CP state is one of the most significant properties of Higgs boson that help us achieve a better understanding of this particle\cite{r6}. 

Extensive research has been conducted to measure the CP state of the Higgs boson\cite{r6}. For example, the Standard Model predicts that the Higgs boson is purely CP even. Therefore, any CP odd measurements will imply physics beyond Standard Model and worth carrying analysis. 
 
As was stated in 1993 by Kr\"{a}mer \cite{r10}, one way to achieve that can be accomplished by measuring the transverse spin correlations. One of the most powerful methods to do that is through its decay to $\tau$ leptons \cite{r7}. This is based on the sensitivity of the transverse spin to the parity of the Higgs. This sensitivity can be indicated by angular correlations of secondary decay products, particularly in the distribution of the products from $\tau$ decays.
 
However, the main limitation of this method is the validity of detecting the loss of neutrinos and evaluating the detector precision \cite{r6}. Therefore, based on Kr\"{a}mer's work, Bower improved the method of measuring the parity of the Higgs in 2002 \cite{r11}. Even though it does not need to adapt the measurements from LHC and the reconstruction of $\tau$ rest-frames, the method only applied to the dominant $\tau$ decay channels \cite{r6}. This is because it is relatively easier to define the acoplanarity angle in this decay mode. In light of this study, extending to other decay modes has become particularly important for the next stage.
 
In addition, the secondary decay products $\pi^0$, $\pi^{\pm}$ and most importantly, the neutrinos. The neutrinos are the so-called Invisibles and cannot be detected directly from the collision \cite{r25}. One crucial step before analyzing the Higgs boson's property is reconstructing the neutrinos with valuable features such as the directions and angular-related information, which will be mentioned later in the study.
 
In most of the following publications \cite{r7,r13,r14,r15,r16}, a well-established idea is that the promising potential improvement in achieving sensitivity to Higgs CP states can be starting to use information in $\tau$ decay vertex. For example, Ralph J\'{o}zefowicz and his colleagues have concentrated only on the sensitivity to CP states during Higgs decaying through analyzing acoplanarity angles \cite{r6}. Instead of exploring the effect of the decay vertex, they studied more essential details in the cascade $\tau$ decay. Based on Bower's work, they improved the definition of acoplanarity angle and split the events into more groups so that it can be used to discriminate more decay modes \cite{r6}.



\subsection{History applications of ML techniques}

When the analysis of decaying modes was extended from $\pi\pm\pi^0$ to $3\pi$, it is found that part of the sensitivity could have been lost in the decays due to the more complicated nature of decay with $3\pi$ product. Deep Learning Neural Network classification was then introduced to quantify this effect. More details and formal discussion can be found in \cite{r18}. This new inclusion increases the available fraction of $H\rightarrow\tau\tau$ decay rate from 6.5 $\%$ to 11.9 $\%$, for the analysis discussed here only considered either $\tau$ decay to 3 charged $\pi$ or $\tau$ decay to $\pi\pm\pi^0$. The improvement is promising as they almost doubled available statistics \cite{r6}.
 
The accomplishment of machine learning techniques in this field was approved by extensive literature. As it was supported by Barberio in 2017 \cite{r23}, although it is currently challenging to differentiate the pseudo-scalar Higgs boson state from the scalar ones, which are favoured in measurements of CP states, the Deep Learning techniques have been applied in this study to extract the sensitivity as much as possible. Lasocha also pointed out in 2020 that machine learning offered a significant breakthrough in distinguishing scalar and pseudo-scalar Higgs states by their complex multidimensional signatures \cite{r8}.

\subsubsection{Mixing Angle $\alpha_{cp}$}
However, a closer look at the literature on the condition when applying machine learning techniques to this field reveals several gaps and shortcomings. For example, it did not discuss the possible contamination of the background signals or mis-reconstructed signals while training the Deep Learning Neural Network formally \cite{r6,r8}. Lasocha's work also commented that the machine learning techniques applied in this study have limitations concerning the measurement of the hypothetical mixing angle of Higgs boson parity states as part of the study. This significant quantity was also defined in J\' {o}zefowicz's research and widely used in the
following studies \cite{r6}.
 
Lasocha investigated the same topic and extended it to the potential of determining the preferred mixing angle of the Higgs boson decays by DNN \cite{r8}. Based on J\'{o}zefowicz's work, Lasocha's research mainly focused on the discussion of the distinction between two different machine learning techniques in Deep Neural Networks: classification and regression, when both of them are used to distinguish the preferred mixing angle of Higgs boson events.
 
The preferred mixing angle was defined for the clarity of the discussion on the DNN results: $\alpha_{CP} = 2\phi_{CP}$. The $\alpha_{CP} = 0,2\pi$ indicate scalar state and the $\alpha_{CP} = \pi$ to pseudo-scalar one \cite{r8}. Therefore, it is obvious that some important information about the Higgs boson CP state is encoded in the angles between the decay products and the angle $\phi_{CP}$ between the two $\tau$ lepton decay planes in the H rest frame. An illustration of $\phi_{CP}$ of a single $\pi$ decay is shown in Figure 1 \cite{r9}.

\begin{figure}[h!]
  \centering
  \includegraphics[scale=0.5]{phi_cp.png}
  \caption{The decay planes of two $\tau$ leptons decaying to a single $\pi^{\pm}$. The angle $\phi_{CP}$ is the angle between the decay planes in the H rest frame.}
  \label{fig:phi_cp}
\end{figure}

To be compatible with the previous studies \cite{r6}, all the data sources were consistent with J\'{o}zefowicz's work. The extended part of the research and the results such as spin weight of different CP mixing angles $\alpha_{CP}$ were also calculated and stored.

\subsubsection{The first successful measurement of Higgs CP state}
The latest breakthrough in this field is the first successfully measured CP structure of the Yukawa coupling between the Higgs boson and $\tau$ leptons by CMS collaboration in 2021 \cite{r9}.
It showed the consistency of experimental measurements and the Standard Model prediction. Machine learning techniques DNN were also significantly applied in the analysis.
 
The data used for this study is collected at pp collision when centre-of-mass energy $\sqrt{s}$ is equal to 13 TeV by the CMS detector at the LHC, corresponding to an integrated luminosity
of 137 $fb^{-1}$. This is consistent with the research done by J\'{o}zefowicz and Lasocha. A similar method of using mixing angles was applied in this study.
  
Based on previous studies, CMS collaboration developed a more concise and efficient method and defined an effective mixing angle $\alpha^{H\tau\tau}$ between CP-even and CP-odd $\tau$ Yukawa couplings. The effective mixing angle $\alpha^{H\tau\tau}$ is defined as \cite{r9}:

\begin{equation}\label{1}
\tan{\alpha^{H\tau\tau}} = \frac{\tilde\kappa_{\tau}}{\kappa_{\tau}}
\end{equation}

, where $\tilde\kappa_{\tau}$ and $\kappa_{\tau}$ are coupling strength modifiers.
  
The most noticeable development of this study was its deployment of machine learning techniques. The first application was similar to previous studies, the Deep Neural Network (DNN) called `DEEPTAU` for $\tau$ lepton reconstruction.
 
Another improvement of this research was the experimental techniques developed for this analysis. The multivariate analysis discriminant (MVA) was deployed to identify $\tau$ decay modes. After establishing this technique, the other application of the machine learning technique is a boosted decision tree (BDT). It was implemented to optimize the performance in discriminating the $\tau$ decay modes. This decision tree was trained by XGBoost framework \cite{r9}.
 
Unlike the previous study, most research has been carried out only with binary classification because they focused on separating scalar and pseudo-scalar Higgs states \cite{r6,r8}. The machine learning techniques improved in this study could identify multiple features of events at once. Both multi-class neural networks and multi-class BDT algorithm combined with the XGBoost package were used to optimize the performance of categorization \cite{r9}.
 
The effective mixing angle was found to be $-1 \pm 19 \degree$
as $0 \pm 21 \degree$ at the 68.3\% confidence level. The results also disfavoured the pure CP-odd scenario at 3.0 standard deviations. The results showed compatibility with predictions from the standard model Higgs boson. More importantly, as the leading uncertainties were statistical, the precision would increase as the data accumulated. The limitation of this literature has not yet been evaluated academically for its advance. However, this research offered limited explanations in specific analysis with machine learning techniques compared to previous literature.

\subsection{Focus of this study and parametrisation of CP states}
Experimental data consists typically of events to the magnitude of $10^6$. Each event represents a particle in a multidimensional coordinate space. This is usually presented by four-momenta and other observable quantities of each detected particle in this event. Studying distributions of these quantities and the ones constructed from these quantities is one of the main goals of this research. Based on the analysis of these distributions, looking for physically meaningful interpretations of the results is also crucial for making a reasonable conclusion. In this case, ML techniques can be implemented to reduce the complexity of the problem.

However, using only low-level variables as input for the ML algorithm is inadequate to capture all information that can reconstruct the wanted quantity. Mixing the low-level inputs with the high-level ones becomes the seemingly best strategy. Similar methods were presented in these studies \cite{r29,r30}.

Nevertheless, this previous literature not only provided opportunities for developing the implementations of ML techniques but also the prerequisites of future studies in related studies \cite{r24}. With the help of results from previous studies, we reconstructed the core variable: polarimetric vectors of two $\tau$ and their decayed products by using the predicted information made by the DNN model. The polarimetric vector can be considered as an estimation of the most likely direction of the spin vector of the $\tau$ lepton in the $\tau$ lepton rest frame \cite{r26}. We start by reconstructing the $\tau$ lepton momenta required to compute the polarimetric vectors.

The reconstruction of neutrinos is an inevitable step before starting reconstructing the $\tau$ lepton momenta. Therefore, reconstructing partial neutrino information, especially the four-momenta (6 variables in total), becomes the first step to obtaining the polarimetric vector. As Lasocha mentioned in their latest studies, only limited input information(hadronic visible decay products) was provided in their previous study. This limitation might be overcome by adding more high-level variables and hence being able to reconstruct the neutrinos (Invisibles) momenta approximately and other event kinematics (the momenta of visible $\tau$ decay products, overall missing energy met) \cite{r24}. The case in this study can be divided into the following steps:

\begin{enumerate}
    \item Reconstruct the four-momenta of the decay products from each $\tau$ leptons, i.e., $\pi^0$ and $\pi^{\pm}$.
    \item Compute the $\tau$ lepton mass from Monte Carlo truth and the one from reconstructed level information and missing transverse energy met for each event.
    \item Build data set for inputs and output target.
    \item Build DNN model with a customized loss function
    \item Train model to predict the neutrino four-momenta(6 variables).
    \item Compute polarimetric vectors for each decay and obtain the acoplanarity angle. 
\end{enumerate}

After step 1 and step 2, all the baseline information constructed from the Monte Carlo truth is ready to be compared to the result obtained by DNN models. The process can be considered an approach to achieving high-level variables from essential low-level variables without explicit physics models \cite{r24}. A similar strategy is applied by the following literature \cite{r27,r28}. By accomplishing these steps, the framework is ready for DNN implementation. Therefore, steps 3 and 4 start to build the DNN model customized to this case. 

Once the DNN regressor makes prediction the neutrino four-momenta, it can be used to obtain the acoplanarity angle $\phi_{CP}$ with the help of the polarimetric vector method. The performance of the DNN model is also compared to traditional methods. The improvement and limit will be discussed in the conclusion.

This paper will be organised as follows. The Source of data and prepossessing of the H signals are outlined in the first part of Methods, followed by the reconstruction methods for CP-sensitive observables. After that, an essential variable Acoplanarity angle is presented in the next part of the Methods. With all the essential background fully outlined, the main structure of the DNN model is presented in the last bit of the Methods. In the Result part, the separation of Higgs signals from Drell-Yan background signals, linear regression for neutrino kinematics and the reconstruction of Acoplanarity angles are listed respectively. A conclusion and the improvement of this study are discussed in the end.

\section{Methods}

\subsection{Source of Data}
Some of the valuable databases in numerical studies were also listed here as background information. The signal and relevant background processes are modelled with Monte Carlo simulated events samples. The signal samples with an H produced through gluon-gluon fusion (ggH), vector boson fusion (VBF), or in association with a W or Z vector boson (denoted as WH or ZH, or VH when combined) are generated at next-to-leading order (NLO) in perturbative quantum chromodynamics (QCD) with the POWHEG 2.0 \cite{r33}-\cite{r35} event generator \cite{r9}. 

The decay of the H does not depend on its production. These samples are simulated without accounting for the $\tau$ spin correlations. After the samples have been generated, the TAUSPINNER package \cite{r21} is used to calculate event weights that can be applied to the simulated signal samples to model $\tau$ polarisation effects for a boson with CP-mixing angles of 0, 45, and 90\degree. There is no normalisation effect from the re-weighting procedure, i.e. the integrated $H\rightarrow\tau\tau$ cross-section of the signal samples is invariant under rotations in $\alpha^{H\tau\tau}$.

Monte Carlo generated events are processed through a simulation of the CMS detector based on GEANT4 \cite{r32} and reconstructed with the same algorithms as the ones used for data. This is also referred to as generator-level information for later.

\subsection{Separating $H\rightarrow\tau\tau$ signal from Drell-Yan background by $\tau$-polarisation}

Before applying any ML technique, an analysis to separate the Higgs signal from the background, the background signal is generated from the Drell-Yan process. The energy fraction of the decay products from each $\tau$ leptons is plotted in both 1D and 2D distributions for different decay modes. This is based on the theory presented by Moretti in 2002 \cite{r31}. It was shown in this study that the correlation between the $\tau$-polarisation can serve as a distinctive way to separate the $H\rightarrow\tau\tau$ signal from the Drell-Yan background. The $\tau$-polarisation is defined as the two decay modes we are interested in at the generator and reconstructed level:

\begin{equation}\label{2}
R_{i,gen} = \frac{E_{\pi}}{E_{\tau}} = \frac{E_{\pi}}{E_{\pi}+E_{\nu}}
\end{equation}

\begin{equation}\label{3}
R_{i,gen/reco} = \frac{E_{\rho}}{E_{\tau_{vis}}} = \frac{E_{\pi^{\pm}}}{E_{\pi^{\pm}}+E_{\pi^{0}}}
\end{equation}

, where the numbering i will be addressed later in the Results section.

By showing the 2D distribution of the selected events, the different distribution patterns can be used to distinguish the $H\rightarrow\tau\tau$ signal from the Drell-Yan background.

\subsection{Methods for CP sensitive observables reconstruction}
    \subsubsection{Impact Parameter method}
The transverse impact parameter here is defined as the minimal distance between the primary vertex and the point on the track \cite{r36}. For each $\tau$ lepton, the impact parameter and its charged-particle momentum vector can be used to define a plane. This plane is constructed in the laboratory frame and only represents the plane of a single charged pion and neutrino instead of the genuine $\tau$ lepton frame\cite{r9}. 

    \subsubsection{Neutral-pion method}
    

This method can be applied to hadronic decay channels where at least one $\tau$ lepton decays involving more than one outgoing hadron. We describe the method applied to the inter-
mediate $\rho$ meson decay. For the $\rho$ meson decays, the vector $\lambda$ is replaced by the four-momentum vector of the $\pi^{0}$, which means we use the planes spanned by the $\rho$ decay products to define the $\phi_{CP}$ observable \cite{r9}. 

    \subsubsection{Polarimetric vector method}
This method can be applied to all decay channels. Only two decay modes of the $\tau$ leptons are considered in this case: $\tau^{\pm}\rightarrow \pi^{\pm}\nu$ and $\tau^{\pm}\rightarrow\rho^{\pm}\nu$, followed by $\rho^{\pm}\rightarrow\pi^{\pm}\pi^{0}$. Decay mode $\tau^{\pm}\rightarrow a_{1}^{\pm}\nu$ is also considered but not completed due to time limitations, which will be specified more in the conclusion part. The first two decay modes form four possible hadronic final-state configurations, each accompanied by a corresponding neutrino pair. This variable is defined as \cite{r37}:

\begin{equation}\label{4}
h^i = \mathcal{N}(2(q \cdot N)q^i - q^2N^i)
\end{equation}

, where $\mathcal{N}$ is a normalization function, q is the difference of the $\pi^{\pm}$ and $\pi^{0}$ four-momenta and N is the four-momentum of the $\tau$ neutrino (all defined in the $\tau$ rest frame). The term $q \cdot N$ is defined as:

\begin{equation}\label{5}
q \cdot N = (E_{\pi^{\pm}}-E_{\pi^{0}})m_{\tau}
\end{equation}


\subsection{Acoplanarity angle $\phi_{CP}$}

To compute $\phi_{CP}$, the process is shown in the following equations(6-10) as the methods of calculating the polarimetric vector $\vec h_{1,2}$ are outlined in the last section:

\begin{equation}\label{6}
\vec{k}_{1,2} = \frac{\vec h_{1,2} \times \vec h_{1,2}}{|\vec h_{1,2} \times \vec h_{1,2}|}
\end{equation}

, where $\vec{k_{1,2}}$ can now be used to reconstruct $\phi_{CP}$. Nevertheless, before that, $\phi^{*}$ is calculated without applying the phase shift.

\begin{equation}\label{7}
\phi^{*} = arccos(\vec k_{1}\cdot \vec k_{2})
\end{equation}

\begin{equation}\label{8}
O^{*} = -(\vec h_1 \times \vec h_2)\cdot \vec h_1
\end{equation}

, where $\phi^{*}$ is $\phi_{CP}$ before phase shifting and $O^{*}$ is the PV sign that is used to apply the corresponding phase shift. $\phi_{CP}$ can be shifted in the methods presented in equation (9):

\begin{equation}\label{9}
\phi_{CP} =\left\{
                \begin{array}{ll}
                  \phi^{*} &ifO^{*} \geq 0\\
                  2\pi - \phi^{*} &if O^{*} \leq 0
                \end{array}
              \right.
\end{equation}

Another valid angular variable to approximate the energy fraction is defined similarly in this process. This will be discussed more in Results.

\begin{equation}\label{10}
C_{1,2} = \vec h_{1,2}\cdot \vec n_{1,2}
\end{equation}
, where $\vec n_{1,2}$ are the unit vectors for the decayed products from the $\tau$ leptons in the laboratory frame.


After fully computing the acoplanarity angle, its distribution can be used to identify the CP properties of Higgs by comparing the distribution applied with scalar weight and pseudo-scalar.

Figure 2 shows the normalised distribution of $\phi_{CP}$ at the generator level. $\phi_{CP}$ here is calculated in the rest frame of the H, for the scalar, pseudo-scalar and the $\phi_{CP}$ distribution from Drell–Yan processes. These distributions are for one of the scenarios where both $\tau$ leptons decay to a charged pion and a neutrino \cite{r9}.

It is important to note that the distribution of $\phi_{CP}$ for the Drell–Yan background is constant. The acoplanarity angle $\phi_{CP}$ was initially introduced in the context of $e^{+}e^{-}$ collisions \cite{r10,r38}, where $\phi_{CP}$ can be calculated in the H rest frame. In this study, the methods for estimating $\phi_{CP}$ have been extended and optimised for hadronic collisions \cite{r39}. Throughout this study, the angle between the $\tau$ decay planes is denoted as $\phi_{CP}$ , irrespective of the frame in which it is calculated.

\begin{figure}[h!]
  \centering
  \includegraphics[scale=0.5]{gen_phi.png}
  \caption{The normalised distribution of $\phi_{CP}$ between the $\tau$ lepton decay planes in the H rest frame at the generator level.}
  \label{fig:gen_phi}
\end{figure}

    
\subsection{Main structure of the multi-output NN Regressor}
In this study, the ML algorithm is applied to analyze the CP state in the decay channel $H\rightarrow\tau\tau$. 
    \subsubsection{Pre-selection of data}
Before analyzing the DNN model, pre-selection data is a fundamental prerequisite to optimizing the model's efficiency. The data set includes the information of decay mode flags: decay mode 1(dm-1) stands for leading $\tau$ decay mode and decay mode 3(dm-2) stand for sub-leading $\tau$ decay mode. As was stated in the previous section, only hadronic decay is discussed in this study. Therefore, $dm = 11$ is excluded in the data set, while $dm = 0,1 and 10$ represent single charged pion decay ($\pi$ mode), neutral pi decay ($\rho$ mode) and 3-prong decay (a1 mode).

    \subsubsection{Input variables and targets}
The input with a dimension of 72 for the DNN model is categorized as:
\begin{enumerate}
    \item Single charged $\pi$ and neutral $\pi$ (four-momenta) kinematics decays from each $\tau$.
    \item Missing energy met in x and y direction(Cartesian coordinate).
    \item Impact parameters for both taus in Cartesian coordinate.
    \item Secondary vertex information.
    \item Reconstructed tau kinematics.
\end{enumerate}

The 6 output targets are also listed here for each tau, 12 in total:
\begin{enumerate}
    \item Neutrino momentum in Cartesian coordinate(3 variables for each tau). Energy is the magnitude of the 3-vector.
    \item deltaRapidityPhi: $\Delta R = \Delta\phi^2 + \Delta\eta^2$, where $\phi$ is the spherical polar angle (from 0 to $\pi$, inclusive) and $\eta$ is the rapidity which is a kind of spherical polar angle \cite{r40}. This quantity is defined to specify the difference between the neutrino vector and the visible decay product vectors.
    \item Scalar product between the visible decay product and neutrino for each tau, which can also be treated as the projection of neutrino vector on visible decay product direction.
    \item Cross product magnitude between the visible decay product and neutrino for each tau can also be treated as the distance between the neutrino and visible product vectors.
\end{enumerate}

After the $\phi_{CP}$ is computed, the weight for the scalar and pseudo-scalar event included in the same data set will be applied for separation.

    \subsubsection{Define customised loss function}

A loss function is a method of evaluating how well the algorithm models the data set. During training, the loss calculated by the loss function in each epoch tells how well the model is trained. If the predictions are off, the loss function should output a higher number and vice versa. Loss functions are also related to model accuracy, another critical component in evaluating the performance of the ML models.

A normal inner-built loss function such as MAE is usually given in the structure for a baseline model. For each prediction made by the model, the loss function will measure the absolute difference between the predictions and the given target values. For example, MAE in mathematical notation can be defined as:

\begin{equation}\label{11}
MAE = \frac{1}{N} \sum^{n}_{j=1}{|y_{pred}-y_{true}|}
\end{equation}

Therefore, checking whether the loss function is well designed for the specific case is also essential. Due to the complexity of the case, giving a simple MSE or MASE loss function for the DNN regressor model is not capable of achieving the goal of regressing multiple variables. A more complicated loss function is defined to customize the study. 

In this case, we have 12 outputs instead of only one. Due to the nature of each predicted physics quantity, the impact of each quantity on the final reconstruction is different. Therefore, to penalize each quantity equally or add bias to the preferred target, applying individual weight to each target value is important. This is addressed in more detail in Appendix A. Similarly to the MAE defined above, the loss function defined in this case can be written as:

\begin{equation}\label{12}
MAE_{multi} = \frac{1}{N} \sum^{n}_{j=1,i=1} w_{i} \cdot{|y_{i,pred}-y_{i,true}|}
\end{equation}

, where $w_{i}$ is the weight for each output.

In this study, the information on neutrino kinematics is what we want to partially reconstruct at the end. However, if the information of four-momenta is the only target, it will be strongly biased towards the tau four momenta because the neutrino direction only deviates subtly from the tau direction. Therefore, adding more angular information related to the distance between the neutrino and the visible decayed products can separate these two vectors. The deltaRapidityPhi is added to address the vector difference in spherical coordinates. Similarly, the scalar and cross product are used to give information on the correlation between these two vectors.

\subsubsection{The structure of the multi-output DNN regressor}
The library used in this study to build the architecture is TensorFlow. Figure 3 is a flowchart showing the structure of the multi-output DNN regressor. 

\begin{figure}[h!]
  \centering
  \includegraphics[scale=0.5]{flowchart.png}
  \caption{A visualisation of DNN model architecture}
  \label{fig:DNN}
\end{figure}

\textbf{Activation functions}

Here, an input layer with an input dimension of 72 is followed by three Dense layers with the ReLU function as the activation function. The last layer is the output layer with a linear activation function. The activation function ReLU function in the DNN regressor and a Sigmoid function is shown in Figure 4 \cite{r41}:

\begin{figure}[h!]
\centering
  \begin{subfigure}[b]{0.5\textwidth}
      \centering
      \includegraphics[width=\textwidth]{ReLU.png}
      \caption{A plot of ReLU activation function}
      \label{fig:ReLU_funtion}
  \end{subfigure}
  \hfill
  \begin{subfigure}[b]{0.45\textwidth}
      \centering
      \includegraphics[width=\textwidth]{Sigmoid.png}
      \caption{A plot of Sigmoid activation function}
      \label{fig:linear_funtion}
  \end{subfigure}
    \caption{Activation function plots in this DNN regressor}
    \label{fig:loss_funtion}
\end{figure}

Sigmoid activates almost all neurons in the same way. This means that the activation is very intensive \cite{r41}. Figure 4 shows the advantage of using a ReLU function as the activation function compared to a Sigmoid function is evident when the NN is getting larger. The ReLU function with a value of 0 on the negative axis means that the network will run faster and makes ReLU a better choice when we got multi-layers of structure, which improves the efficiency sizably.
 
Nevertheless, the ReLU function is still not the best activation function as it might cause incapability of learning in the 0 activation region. The leaky-ReLU function gives a leaky value of 0.01, whereas the ReLU function will give a 0, which can avoid the problem encountered when using a ReLU function as an activation function. The plot of a leaky-ReLU function is shown in Figure 5.

\begin{figure}[h!]
  \centering
  \includegraphics[scale=0.5]{L_ReLU.png}
  \caption{Plot of a Leaky-ReLU function}
  \label{fig:lrelu_funtion}
\end{figure}

\textbf{Weight initializer}

The weight initializer is a critical consideration in the design of a neural network model. Weight initialization aims to prevent layer activation outputs from exploding or vanishing during the course of training. If either occurs in the process, loss gradients will either be infinite or approach 0 to be meaningful, and the network will take longer to converge or even not be able to do so \cite{r42}.

In this model, optimizer was chosen as RandomNormal. This means the initializer will generate a normal distribution of weights every time.

\section{Results}

The results in this section follow the same logic as the Methods section. After the pre-procession of data, the Higgs boson signal is separated from the Drell-Yan background using the energy fraction. Then the polarimetric vectors and the corresponding $\phi_{CP}$ are reconstructed with the neutrino information predicted by the multi-output DNN regressor. All the necessary neutrino information at the reconstructed level in this part is the prediction from the DNN regressor. Therefore, the distributions in this section are plotted at the generator level. A series of comparisons will be made for the final possible decay configurations reconstructed by different methods listed in the Methods section such as impact parameter, neutral-pion method and polarimetric vector method.


\subsection{Distributions of energy fraction for Higgs boson and Z boson}
This section discusses how to use $\tau$ polarisation to distinguish the Higgs boson signal from the Z boson signal(Drell-Yan) in this case. The method is applied for both cases when Higgs boson mass is 125 GeV and 95 GeV. 

    \subsubsection{Higgs with 125 GeV mass}
The final decay configuration discussed in this section will be:
\begin{enumerate}
    \item When both $\tau$ leptons decay into a single charged pion($\pi\pi$ decay).
    \item When both $\tau$ leptons decay into one charged pion and a neutral pion($\rho\rho$ decay).
    \item One $\tau$ lepton decays into a single charged pion, while the other decays into one charged pion and a neutral pion($\pi\rho$ decay).

\end{enumerate}

\textbf{$\pi$ decay for both $\tau$ leptons}

Figure 6 shows the distributions for Higgs and Z bosons when both $\tau$ leptons decayed from they undergo a single charged pion decay. Here, we redefine the energy fractions as $R_1$ and $R_2$, where $R_1$ is the energy fraction of leading $\tau$ lepton and $R_2$ is the energy fraction for sub-leading $\tau$ lepton. The definition was stated earlier in the Methods section in equations (2) and (3). For Higgs, there is one tau energy larger than the other (the leading tau), while for the Z boson both $\tau$ leptons decayed from it should have similar energy.

\begin{figure}[h!]
  \centering
  \includegraphics[scale=0.5]{Gen_pipi_ef.png}
  \caption{Distribution energy fraction of Higgs boson(left) and Z(right) boson}
  \label{fig:ef_pipi}
\end{figure}

\textbf{$\rho$ decay for both $\tau$ leptons}

Figure 7 is the 2D distribution for Higgs and Z boson $\rho\rho$ decay modes. As shown in the figure, Higgs boson distribution is biased towards the edges while Z boson biases towards the corners. The mass difference between them might cause this. Different weights applied to the Higgs boson distribution can also cause a difference in the distribution. The weight applied in this study is simply the weight for scalar products. The energy fraction for this final decay mode configuration is computed only from the visible decay products so it can also be applied to the reconstructed level. 

\begin{figure}[h!]
  \centering
  \includegraphics[scale=0.5]{Gen_rhorho_ef.png}
  \caption{Distribution energy fraction of Higgs boson and Z boson}
  \label{fig:ef_rhorho}
\end{figure}

\textbf{$\rho$ decay for leading $\tau$ lepton $\pi$ decay for sub-leading $\tau$}

Figure 8 shows the distribution of energy fraction $R_1$ for leading $\tau$ and $R_2$ for sub-leading $\tau$. In this final decay configuration, a 1D distribution plot is enough to determine the difference between a Higgs signal and a Drell-Yan background. 

We also applied Pt cuts on the data set to achieve better separation. The constraint is set as: transverse momentum $P_{T}>$ 40 GeV and rapidity $\eta<$ 2.3 for both $tau$ lepton decay products.

\begin{figure}[h!]
  \centering
  \includegraphics[scale=0.5]{Gen_pirho_ef.png}
  \caption{Distribution energy fraction of Higgs boson and Z boson}
  \label{fig:ef_pirho}
\end{figure}

For decay mode a1, it might be better to use the polarimetric vector. Energy fraction can tell some information about the $\tau$ spin, but if the polarimetric vector can be constructed entirely, it will imply maximal information for the decay. However, the formula to reconstruct it might be very complicated in some cases. This will be discussed later in the subsection for DNN regressor.

    \subsubsection{Higgs with 95 GeV mass}

This analysis repeats the process of the previous subsection when Higgs mass is 125 GeV. The results for final decay configuration $\pi\pi$ decay and $\rho\rho$ decay are similar to the previous case. For clarity of the study, distributions for these two decay configurations are presented in Appendix B with other repeated contents.

The distributions of energy fraction when the leading $\tau$ lepton decays into $\rho$ and the sub-leading $\tau$ lepton undergoes a $\pi$ decay is slightly different from the previous case. This is presented in Figure 9 below. The cut applied in this case is the same as the one in the previous case.

\begin{figure}[h!]
  \centering
  \includegraphics[scale=0.5]{Gen_95_rhopi.png}
  \caption{Distribution energy fraction of Higgs boson and Z boson}
  \label{fig:ef_pirho_95}
\end{figure}

Figure 9 clearly shows that the distribution for the Higgs boson in this case is flatter than the one for Higgs with 125 GeV mass. This is because the change in energy fraction will be less evident for smaller masses.

Some other simple variables are also helpful: for $\tau$ lepton decay products, the angular information with how two taus are distributed (defined as $C_{1,2}$ in this case), the definition can be found in equation (10). It is similar to something we boosted into the Z rest frame, then took the angles between one of the $\tau$ lepton and the other. This will also create separation without using the information of $\tau$ lepton decay products. The distribution for this simple variable is shown in Figure 10:

\begin{figure}[h!]
  \centering
  \includegraphics[scale=0.5]{Gen_cos1cos2.png}
  \caption{Distribution of $C_{1,2}$ for Higgs boson and Z boson}
  \label{fig:costheta}
\end{figure}

However, even if we use these variables to separate the Higgs from Z or non-Higgs, the sample separated out, or at least the properties we used for Higgs might not be identical as the case for the pure Higgs state. This means that the separation using this method introduces bias to the analysis. Therefore, more work should be done around $\phi_{CP}$ to check if the distribution of the $\phi_{CP}$ is the same in the selected sample as in the pure sample. 

\subsection{Linear regression for Higgs momentum}
The quantities above are more accessible to reconstruct than angular information, which is more difficult to define, let alone the neutrino information. Regressing the Higgs boson momentum and its components(in Cartesian coordinate) can be the first step. This step can check whether the DNN setup can learn helpful information from the lowest level of variables. The inputs for this model are similar to the final DNN regressor while the outputs are only the momentum for Higgs and its components at the generator level.
The baseline model architecture is set up as shown in Appendix B because it has a similar structure as the final DNN regressor but with a less customized setup.

    \subsubsection{Loss curves for training and testing data}
Plotting the loss for each epoch during the training process and comparing it to a testing data set is a practical and basic way to evaluate the model's performance. The shape of curves can represent the goodness of choice for learning rate. A plot of different loss curves is shown in Figure 11 to address this property \cite{r43}:

\begin{figure}[h!]
  \centering
  \includegraphics[scale=0.5]{L_curve}
  \caption{Loss curves for models with different learning rates}
  \label{fig:loss_curve}
\end{figure}

Apart from this property, comparing the curves for the training and testing sets is also informative. For example, the testing curve starts to go up after a certain point while the training curve continues to go down. This might imply the model is undergoing over-training \cite{r44}. 

With this background information, Figure 12 shows the learning curves for the baseline model used to regress the Higgs momentum and its components. 

\begin{figure}[h!]
  \centering
  \includegraphics[scale=0.8]{loss_plot}
  \caption{Loss curves for baseline model for training and testing data}
  \label{fig:loss_plot}
\end{figure}

As it is clearly shown in the plot, the testing curve is closely in line with the training curve. This means the model makes predictions under the excellent condition without over-fitting or under-fitting problems.

    \subsubsection{Linear regression for Higgs momentum and its components in 2D distribution}  
After evaluating the model's performance, the next step is presenting the result with true values as this is the ultimate goal of making the predictions. The prediction made by this baseline model is presented in Figure 13:

\begin{figure}[h!]
  \centering
  \includegraphics[scale=0.5]{H_reg}
  \caption{Linear regression plots for Higgs momentum and its three components in Cartesian coordinate. The 2D distribution is plotted as the predicted value against the true value at the generator level.}
  \label{fig:H_reg}
\end{figure}

As shown in the plots, both the total momentum and the momentum components in the x,y and z directions demonstrate the linear regression on the generator level values. Here, the total momentum is the magnitude of the components so it only has value along the positive axis. Compared with the components in the x and y direction, the momentum component in the z direction has the best prediction, while the components in the x and y direction are biased towards the origin. 
    

\subsection{Linear regression for neutrino momentum using multi-output DNN regressor}
After testing the baseline model with Higgs momentum regression, regression for neutrino momentum components can be achieved in similar methods. Apart from the analysis from the previous subsection, the predicted values are also compared to SV reconstructed values (referred to as SV-fit later) as part of the evaluation. SV-fit values here are calculated with the reconstructed level visible information and $\tau$ kinematics reconstructed by Secondary Vertex \cite{r9}. The baseline model is also adjusted to the DNN regressor with more helpful input information. More details for this model are listed in the Methods section and appendix.

\subsubsection{Evaluation of predicted neutrino momentum components}
The first step to evaluating the prediction is still plotting the 2D distributions for predicted values against true values. The distributions for the x momentum component is presented as followed in Figure 14: a similar set of 2D distribution plots are made for neutrino momentum components in Cartesian coordinate for both leading $\tau$ lepton and sub-leading $\tau$ lepton. Only the results of the momentum component in the x direction are presented in this subsection because the other two components demonstrate a similar pattern. Therefore, the rest of the results will be included in Appendix B.arefollows

\begin{figure}[h!]
  \centering
  \includegraphics[scale=0.5]{2D_xyz}
  \caption{Linear regression plots for neutrino momentum x-component in Cartesian coordinate. The 2D distribution is plotted as the predicted value against the true value at the generator level.}
  \label{fig:N_reg}
\end{figure}

As it is shown in Figure 14, the 2D distributions for neutrino momentum components are regressed better in all directions than in the baseline model. Therefore, the next evaluation step can be done using SV-fit values as a comparison. The computation of neutrino momentum components using SV-fit information can be explained by the equation below:

\begin{equation}\label{13}
SV_{neutrino} = SV_{tau} - reco_{visible}
\end{equation}

Figure 15 shows the difference distribution between predicted and true values. The true values for both differences are generator-level information. The comparison is made for the prediction obtained by the DNN regressor and the prediction made by SV-fit using equation(13). The rest of the distributions are included in Appendix B for similar reasons to the 2D distribution plots.

\begin{figure}[h!]
  \centering
  \includegraphics[scale=0.5]{svfit}
  \caption{1D distribution of the difference between true values and predicted values for neutrino momentum x-component in Cartesian coordinate. The true values are imported from the generator level and the predictions are made from the DNN model and calculated by SV-fit values.}
  \label{fig:svfit_reg}
\end{figure}

It is clearly shown that the distribution peaks at 0. The peaks for the distributions for DNN regressor predictions are sharper than the SV-fit results. The root means square errors are also used to represent the width of the distributions. The distribution widths for DNN regressor results are smaller than the ones for SV-fit results by 2 orders of magnitude.

\subsubsection{Comparison between multi-output DNN regressor and basic ML models}

Comparing the reconstructed variables from the predictions is closer to the ultimate goal to analyze the predictions further. One simple variable that can be used to evaluate the performance is the mass of $\tau$ lepton. $\tau$ lepton mass is known to be around 1.776 GeV \cite{r45}. Therefore, comparing the peak of each prediction distribution can be an effective way to compare the performance of each model. 

\begin{figure}[h!]
\centering
  \begin{subfigure}[b]{0.3\textwidth}
      \centering
      \includegraphics[width=\textwidth]{Tau_DNN.png}
      \caption{A plot of $\tau$ mass computed from the predictions made by multi-output DNN regressor}
      \label{fig:16a}
  \end{subfigure}
  \hfill
  \begin{subfigure}[b]{0.3\textwidth}
      \centering
      \includegraphics[width=\textwidth]{Tau_DTR.png}
      \caption{A plot of $\tau$ mass computed from the predictions made by Decision Tree regressor}
      \label{fig:16b}
  \end{subfigure}
  \hfill
  \begin{subfigure}[b]{0.3\textwidth}
      \centering
      \includegraphics[width=\textwidth]{Tau_Ridge.png}
      \caption{A plot of $\tau$ mass computed from the predictions made by Ridge regressor}
      \label{fig:16c}
  \end{subfigure}
    \caption{Comparison of distributions of reconstructed $\tau$ mass computed from different models}
    \label{fig:16}
\end{figure}

The result distribution for the DNN regressor is the sharpest and peaks at the true value. This means that the DNN regressor gives the best predictions so that the reconstructed $\tau$ lepton mass peaks at 1.776 GeV, while the predictions made by the other two basic ML models failed in reconstructing this variable.
    
\subsection{Reconstruction of acoplanarity angle $\phi_{CP}$}
All the evaluation above is to confirm the validity of the predictions before  reconstructing the CP-sensitive variable $\phi_{CP}$. The distribution of $\phi_{CP}$ is plotted with generator information and compared with the $\phi_{CP}$ computed from predictions made by the DNN regressor.

With the neutrino kinematics predicted in the previous section, the reconstruction of $\phi_{CP}$ and the polarimetric vectors for the decay products can be done following the process in the Methods section. The final possible decay configurations of interests are:
\begin{enumerate}
    \item $\pi\pi$ decay: Both $\tau$ leptons decay into single charged pion $\pi^{\pm}$.
    \item $\rho\rho$ decay: Both $\tau$ leptons decay into a charged pion and a neutral pion $\pi^{0}$.
    \item $\pi\rho$ decay: Leading $\tau$ lepton decays into a single charged pion $\pi^{\pm}$ while sub-leading $\tau$ lepton decays into a charged pion and a neutral pion $\pi^{0}$.
    \item $\rho\pi$ decay: Leading $\tau$ lepton decays into a charged pion and a neutral pion $\pi^{0}$ while sub-leading $\tau$ lepton decays into a single charged pion $\pi^{\pm}$.
\end{enumerate}

Figure 17 shows the $\phi_{CP}$ distribution when both $\tau$ leptons undergo $\pi$ decays. The distributions are computed by impact parameter methods, and one is reconstructed by the polarimetric vector method with DNN regressor predictions.

\begin{figure}[h!]
  \centering
  \includegraphics[scale=0.5]{reco_pipi}
  \caption{$\phi_{CP}$ distribution for scalar and pseudo-scalar reconstructed by impact parameter methods and polarimetric vector method with the prediction from DNN regressor.}
  \label{fig:phicp_p}
\end{figure}
    
In Figure 17, data of $\pi\pi$ is displayed. Events are
included from all MVA score bins in these signal categories. The average asymmetry between the scalar and pseudo-scalar distributions. The definition of the average asymmetry per bin is $\frac{|CP_{even}-CP_{odd}|}{|CP_{even}+CP_{odd}|}$ and is normalised to the total number of bins. In this equation, $CP_{even}$ and $CP_{odd}$ are the scalar and pseudo-scalar
contributions per bin \cite{r9}. 

However, the polarimetric vector methods for the rest of the decay modes configuration are not as promising as the original method. For $\rho$ decays, the simple method to reconstruct $\phi_{CP}$ is the neutral-pion method. The distribution in this scenario is displayed in Figure 18. Similar results for reconstructed $\phi_{CP}$ distribution using the polarimetric vector method for $\pi\rho$ and $\rho\pi$ decays are included in Appendix B.

\begin{figure}[h!]
  \centering
  \includegraphics[scale=0.5]{reco_rhorho}
  \caption{$\phi_{CP}$ distribution for scalar and pseudo-scalar reconstructed by neutral-pion methods and polarimetric vector method with the prediction from DNN regressor.}
  \label{fig:phicp_r}
\end{figure}
 
 The average asymmetry of these two distributions from the polarimetric method is not as good as the case when both $\phi_{CP}$ are reconstructed by the neutral-pion method. This implies that a mixed method using neutral-pion methods for $\rho$ decay and polarimetric vector methods for $\pi$ decays can be applied to the other two configurations.
 
 However, the $\phi_{CP}$ reconstructed by repeating the neutral-pion method using the reconstructed level visible decay products kinematics are not giving valid results. This might be caused by mistakes in the code. It can be corrected by plotting the same set of distributions at the generator level. This verifying process is displayed in Figure 19:

\begin{figure}[h!]
  \centering
  \includegraphics[scale=0.5]{gen_pipi}
  \caption{$\phi_{CP}$ distribution for scalar and pseudo-scalar reconstructed by neutral-pion methods using the information at generator level.}
  \label{fig:phicp_g}
\end{figure}

In Figure 19, the distribution of $\phi_{CP}$ on the left is plotted by sorting the value of $\phi_{CP}$ and applying weights sorted by the value of the acoplanarity angle computed by the neutral-pion method using generator level information. The one on the right is the distribution of $\phi_{CP}$ without this process. This is to check whether the algorithm used to compute the neutral-pion vectors will change the $\phi_{CP}$ order so that each $\phi_{CP}$ does not belong to the actual event it comes from. By sorting both the $\phi_{CP}$ values and weights in ascending order, it will reorganise the $\phi_{CP}$ so that each value corresponds to the event it comes from. Comparison between the sorted distributions and the unsorted one implies that having the wrong $\phi_{CP}$ for each event is one of the problems causing the failure of separation in this case. 

\newpage
\section{Conclusion}
For the first part of the study, separating Higgs signals from Drell-Yan background signals with energy fractions or the $C_{1,2}$ is possible at the generator level. A similar conclusion can be drawn at the reconstructed level since we have successfully predicted the kinematics information of neutrinos. Once the separation is made by classification, it is also essential to check whether the $\phi_{CP}$ reconstructed from the separated Higgs signal is the same as the one reconstructed from the pure Higgs state.

The ML techniques were first applied to this field because it was cumbersome to evaluate data for too many distinct acoplanarity angle sensitivities, then evolved as one of the backbones in identifying decay modes. It started from the application of binary classification and was developed into a multi-class neural network tool. Implementing ML techniques not only simplified the analysis but also reduced the uncertainties of the results. 

The multi-output DNN regressor implementation in this study shows promising potential for improving the reconstruction of CP-sensitive observables, especially the acoplanarity angles $\phi_{CP}$. By customizing the loss function, the performance of the regressor was improved so that the average asymmetry of the $CP_{even}$(scalar) and $CP_{odd}$(pseudo-scalar) distributions for $\pi\pi$ decays improved from the 0.135 using the impact parameter method to 0.170 using the polarimetric method with the prediction made by the regressor.

Nevertheless, this only works well for $\pi\pi$ decays. The results of other possible configurations are still far from satisfactory. Improvements can be made by checking the algorithm computing the polarimetric vectors and $\phi_{CP}$ because of the problem stated in the Results section. 

\subsection{Possible application of GNN architecture}
Apart from the potential mistake in the code, the DNN regressor can also be improved from a simple basic neural network structure to a more complicated model with more layers and appropriate structure.

Here, implementation of Graph Neural Network structure might be a possible way to go. A GNN is an optimizable transformation on all attributes of the graph (nodes, edges, global-context) that preserves graph symmetries (permutation invariance) \cite{r46}. The benefit of implementing a GNN is that it does not change the potential linkage between the inputs. The progressive transformation will be acted on the embeddings such as the information of nodes, edges and global context without changing the connectivity of the input graph.

Possible way of implementation is listed below:
\begin{enumerate}
    \item Node feature: decay products kinematics(four-momenta, missing energy), impact parameter and secondary vertex information.
    \item Edge features a one-hot encoded array showing the type of decay mode.
    \item Label for regression: same output targets stated in this study earlier in the Methods section.
\end{enumerate}

\subsection{Main achievements}
So far, most of the previous studies are predominantly focused on basic applications of machine learning and are far from optimization \cite{r6,r8,r9}. Therefore, the research gap in this field deserves to be discussed to optimize the applications and the measurements. This study critically evaluates the development of the machine learning method applied in measuring the CP state of the Higgs bosonor at least in a bid to address the gap.

Overall, previous studies highlight the need to develop machine learning techniques in the analysis of the CP structure of the Higgs boson. Considering the evidence mentioned in the study, it was evident that developing corresponding machine learning techniques can bring significant improvements in measurements and extraction of sensitivities with more amendment if time allows. 

However, due to the time limitation, some of the work in this study remains uncompleted. A more systematic and sufficient analysis is required for the training of the algorithm so that it can extract more information contained in the existing data. This is one of the toughest challenges for all researchers in this domain. Implementing a new model such as GNN might therefore be helpful to improve the performance of the results in the analysis of the CP-sensitive observables.

\newpage
\section{Acknowledgements}
I would like to thank my supervisors, Prof. David Colling and Daniel Winterbottom for guiding me through this MRes project. I also appreciate the time I spent with the HEP team. The meetings and conversations were vital in inspiring me to think outside the box from multiple perspectives to form a comprehensive and objective critique. I have been feeling supported the whole year and enjoy working with all my colleagues.
\newpage


\bibliography{ref.bib}

\newpage
\appendix
\addcontentsline{toc}{section}{Appendices}
\section*{Appendices}
\section{Important code}

All the code will be uploaded to a GitHub repository and the link will be put at the end of the appendix.

\begin{figure}[h!]
  %\centering
  \includegraphics[scale=0.75]{define_Loss_function.png}
  \caption{Code for customized loss function}
  \label{fig:loss_funtion_code}
\end{figure}

\newpage
\section{Repeated graphs}
    \subsubsection{Higgs M95}
\begin{figure}[h!]
  \centering
  \includegraphics[scale=0.5]{Gen_95_pipi.png}
  \caption{Distribution energy fraction of Higgs boson and Z boson}
  \label{fig:ef_pipi_95}
\end{figure}

\begin{figure}[h!]
  \centering
  \includegraphics[scale=0.5]{baseline_model.png}
  \caption{Flowchart of the baseline model used to predict Higgs momentum and its components}
  \label{fig:baseline}
\end{figure}

\begin{figure}[h!]
  \centering
  \includegraphics[scale=0.5]{Gen_95_rhorho.png}
  \caption{Distribution energy fraction of Higgs boson and Z boson}
  \label{fig:ef_rhorho_95}
\end{figure}

\begin{figure}[h!]
  \centering
  \includegraphics[scale=0.5]{2D_xyz_rest}
  \caption{Linear regression plots for neutrino momentum y,z-component in Cartesian coordinate. The 2D distribution is plotted as the predicted value against the true value at the generator level.}
  \label{fig:N_reg_rest}
\end{figure}

\begin{figure}[h!]
  \centering
  \includegraphics[scale=0.5]{svfit_rest}
  \caption{1D distribution of the difference between true values and predicted values for neutrino momentum y,z-component in Cartesian coordinate. The true values are imported from the generator level and the predictions are made from the DNN model and calculated by SV-fit values.}
  \label{fig:svfit_reg_rest}
\end{figure}

 \begin{figure}[h!]
  \centering
  \includegraphics[scale=0.5]{reco_pirho}
  \caption{$\phi_{CP}$ distribution for scalar and pseudo-scalar reconstructed by impact parameter methods and polarimetric vector method with the prediction from DNN regressor.}
  \label{fig:phicp_pi}
\end{figure}

\begin{figure}[h!]
  \centering
  \includegraphics[scale=0.5]{reco_rhopi}
  \caption{$\phi_{CP}$ distribution for scalar and pseudo-scalar reconstructed by impact parameter methods and polarimetric vector method with the prediction from DNN regressor.}
  \label{fig:phicp_rp}
\end{figure}


\end{document}
