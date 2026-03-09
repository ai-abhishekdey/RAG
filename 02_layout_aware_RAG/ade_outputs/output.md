<a id='9cecb2a4-1de1-40de-b8de-93758c2d702c'></a>

Mizo Phone Recognition System

<a id='ea829261-dc7d-47f8-8c10-2bb620b3e22a'></a>

Abhishek Dey¹, Wendy Lalhminghlui², Priyankoo Sarmah²,³ , K. Samudravijaya³,
S. R. Mahadeva Prasanna³,⁴,⁵, Rohit Sinha³,⁴ and S. R. Nirmala¹

<a id='d7d0826a-9756-46e8-9858-ac20919ac2bb'></a>

1Department of Electronics and Communication Engineering,
GUIST, Gauhati University, Guwahati -781014, India.
2Department of Humanities and Social Sciences,
3Center for Linguistic Science and Technology,
4Department of Electronics and Electrical Engineering,
Indian Institute of Technology Guwahati, Guwahati -781039, India.
5Department of Electrical Engineering,
Indian Institute of Technology Dharwad, Dharwad -580011, India.
Email: abhishekdey.gu@gmail.com,
{wendy, priyankoo, samudravijaya, prasanna, rsinha} @iitg.ernet.in, nirmalasr3@gmail.com

<a id='fa34fd82-b362-436f-b54d-19df562453f8'></a>

Abstract—In this work, we present the creation of a speech corpus in an under-resourced language, namely, Mizo, and report the development of a phone recognition system using state-of-the-art acoustic modelling techniques. The speech corpus consists of Mizo passages spoken by 81 native Mizo speakers. A set of 36 phonetic units have been identified for representing the acoustic phonetic characteristics of the speech signal. Over the past few decades, the Hidden Markov Model (HMM) based acoustic modelling technique is most widely used to capture the temporal variations in the speech data. However, the state observation probabilities in the HMM were generated through multivariate Gaussian Mixture Models (GMMs). Additionally, we have explored two new frameworks in developing the Mizo phone recognition system, namely, the Deep Neural Network (DNN) and the Subspace Gaussian Mixture Model (SGMM). Phone Error Rates (PERs) of 18.1% and 17.5% are observed in DNN-HMM and SGMM-HMM based approaches, respectively, without utilizing any language constraint. PER reduced to 13.9% and 15.7%, respectively, after incorporating the language model information.

<a id='4008d466-5ffc-43bf-b2b5-ba6e92e18005'></a>

Index Terms: Mizo language, Phone Recognition System, ASR, DNN.

<a id='5771930e-5cbd-4f6b-a78e-467a11ebb566'></a>

I. INTRODUCTION

Accurate and reliable phone recognition is the founda-
tion of robust speech recognition. Considering the impor-
tance of phone recognition in applications such as Automatic
Speech Recognition (ASR) and Language Identification (LID)
systems, research was carried out for many major Indian
languages such as Assamese, Manipuri, Bengali, Malayalam
etc. [1]-[5]. The Manipuri, Assamese and Bengali Phone
Recognition Systems (PRS) also facilitated language identifi-
cation [2] using the maximum log-likelihood scores derived
from the PRS. Phone recognition systems were developed
for Bengali and Odia languages [3]. The number of phonetic
units were 35 and 32 in Bengali and Oriya systems respec-
tively.In the study reporting the development of Assamese
PRS [1], acoustic phonetic units were trained using reading
mode speech data collected from native Assamese speak-
ers, and tested with speech data recorded in three different
speaking modes, namely, reading, lecture and conversation.

<a id='390ad665-02e2-4ac6-9864-112690f8629c'></a>

Phone recognition accuracies of 47.3%, 45.3% and 36.1%
were reported for the read, lecture and conversation modes,
respectively. It is to be noted that most of these systems
were developed without utilizing any language or contextual
information.

<a id='e5e344a1-9e8a-4334-9e1d-b2b77c7a33d0'></a>

A typical speech recognition system uses Hidden Markov Models (HMMs) to model the temporal nature of speech signal while the spectral variations are modelled using multivariate Gaussian Mixture Models (GMMs). In recent years, two new acoustic modelling techniques have been reported in the liter-ature namely, Deep Neural Network (DNN) [6], [7] and Sub-space Gaussian Mixture Model (SGMM) [8], [9]. Both these frameworks have outperformed the GMM based approach. DNN employs multiple hidden layers in an artificial neural network to capture non-linear mapping between attributes of speech signal and phone classes. This leads to a much improved modeling of the acoustic variations resulting in better recognition performance. However, large amount of training data is required to learn the parameters of the DNN. On the other hand, SGMM gives a more compact representation, and provides better results when the amount of training data is small. This motivated us to explore the potential of SGMM and DNN based approaches in the development of the phone recognition system for Mizo.

<a id='849851ea-3d0f-42c1-8e04-c1bcc2d87b33'></a>

In this work, we report the creation of a read speech corpus
in Mizo, a Tibeto-Burman language, spoken mainly in the
Mizoram province of North-East India. After identifying and
manually annotating the phonetic units in Mizo, we develop a
phone recognition system using the state-of-the-art acoustic
modelling techniques and study the influence of language
model in the overall performance of the system.

<a id='d51c5393-6f51-4dcf-9791-fac2f901fca5'></a>

The remainder of the paper is organized as follows: In
Section II, linguistic background of Mizo is briefly stated.
Section III describes the Mizo speech corpus used in this work.
In Section IV, the development of the Mizo phone recognition
system is described. In Section V, we discuss the results of
the experimental studies. Section VI concludes the paper.

<!-- PAGE BREAK -->

<a id='5b3b2e13-6fae-400a-948f-f945420b8c25'></a>

II. LINGUISTIC BACKGROUND OF MIZO

Mizo belongs to the Tibeto-Burman language family spo-
ken by about 700,000 speakers in Mizoram and its neighbour-
ing states such as Manipur, Meghalaya, Tripura and Assam. It
is also spoken in parts of Bangladesh and Myanmar. Mizo
is a tone language with four contrasting tones namely, High,
Falling, Rising and Low [10]-[12]. Figure 1 gives an illustra-
tion of the four Mizo tones.

<a id='0583e0e3-11c4-4975-8910-c1d315365d66'></a>

<::line chart: The chart displays four contrastive tones (H, F, R, L) in Mizo. The y-axis is labeled "F0 in Hz" with values ranging from 135 to 175. The x-axis is labeled "Duration in percentage values" with percentages from 0% to 100%. The lines represent: H (solid line, generally high and stable), F (dashed line, starting high and gradually decreasing), R (thick solid line, starting low, dipping slightly, then rising significantly), and L (dotted line, starting mid-range and gradually decreasing). Figure 1: The four contrastive tones in Mizo obtained from 5,529 tokens spoken by 19 speakers.::>

<a id='74f35022-2bfc-4322-842d-61482ece3f49'></a>

The Mizo phone set used in this study consists of 36 acoustic phonetic units. Table I lists the phonetic units in International Phonetic Alphabet (IPA) notation [13] along with their mapping in the ASCII format. The Mizo phone set may be classified into 6 broad categories: vowels, stops, fricatives, complex sounds (A), complex sounds (B) and sonorants. Table II lists the different phones that fall into respective broad categories.

<a id='13c15dce-3068-4727-a372-a537ebbbe76a'></a>

### III. SPEECH DATABASE PREPARATION

The speech corpus used in this work was collected from 81 native Mizo speakers. The speech samples were recorded in the field and in a recording booth in quiet environment using a Shure SM10A head-mounted, close talk microphone connected to a Tasacam DR100-MKII recorder. The sampling frequency was 16 kHz and the resolution was 16 bits/sample. The recorded speech files were divided into small segments of 3-5 secs duration, depending on the pauses. They were manually annotated, using Praat [14], with information into different tiers: phone, word, sentence and tone. The segmented speech files were listened to carefully and the phone boundaries were manually marked and transcribed using the Mizo phone set defined in Table I.

<a id='f3dd3bda-33ae-48e5-b192-79205f15e16c'></a>

The entire speech corpus is divided into two parts in approximately 8:2 proportion. The major portion is used for training the acoustic models while the minor portion is used for evaluating the efficacy of the trained phone models. It was ensured that the speakers in the training set are different from those in the testing set. The descriptive statistics of the speech corpus is provided in Table III. The reading material used in the corpus consists of 9 different passages. The average number of sentences in a passage is 38. Each speaker read at least two passages.

<a id='b8e0208a-edce-4502-9542-aca8423cd4f2'></a>

**Table I:** *Inventory of phonetic units*
<table id="1-1">
<tr><td id="1-2">Phonetic units in IPA</td><td id="1-3">Phonetic units in ASCII</td></tr>
<tr><td id="1-4">a</td><td id="1-5">a</td></tr>
<tr><td id="1-6">b</td><td id="1-7">b</td></tr>
<tr><td id="1-8">ɔ</td><td id="1-9">c</td></tr>
<tr><td id="1-a">d</td><td id="1-b">d</td></tr>
<tr><td id="1-c">e</td><td id="1-d">e</td></tr>
<tr><td id="1-e">f</td><td id="1-f">f</td></tr>
<tr><td id="1-g">h</td><td id="1-h">h</td></tr>
<tr><td id="1-i">l (with dot below)</td><td id="1-j">hl</td></tr>
<tr><td id="1-k">m (with dot below)</td><td id="1-l">hm</td></tr>
<tr><td id="1-m">n (with diacritic)</td><td id="1-n">hn</td></tr>
<tr><td id="1-o">rj (with diacritic)</td><td id="1-p">hng</td></tr>
<tr><td id="1-q">r (with diacritic)</td><td id="1-r">hr</td></tr>
<tr><td id="1-s">i</td><td id="1-t">i</td></tr>
<tr><td id="1-u">k</td><td id="1-v">k</td></tr>
<tr><td id="1-w">kʰ</td><td id="1-x">kh</td></tr>
<tr><td id="1-y">l</td><td id="1-z">l</td></tr>
<tr><td id="1-A">m</td><td id="1-B">m</td></tr>
<tr><td id="1-C">n</td><td id="1-D">n</td></tr>
<tr><td id="1-E">ŋ</td><td id="1-F">ng</td></tr>
<tr><td id="1-G">0</td><td id="1-H">0</td></tr>
<tr><td id="1-I">p</td><td id="1-J">p</td></tr>
<tr><td id="1-K">pʰ</td><td id="1-L">ph</td></tr>
<tr><td id="1-M">r</td><td id="1-N">r</td></tr>
<tr><td id="1-O">s</td><td id="1-P">s</td></tr>
<tr><td id="1-Q">t</td><td id="1-R">t</td></tr>
<tr><td id="1-S">tʰ</td><td id="1-T">th</td></tr>
<tr><td id="1-U">tl (with subscript dot)</td><td id="1-V">tl</td></tr>
<tr><td id="1-W">tɬʰ</td><td id="1-X">tlh</td></tr>
<tr><td id="1-Y">tr (with subscript dot)</td><td id="1-Z">tr</td></tr>
<tr><td id="1-10">trʰ</td><td id="1-11">trh</td></tr>
<tr><td id="1-12">ts</td><td id="1-13">ts</td></tr>
<tr><td id="1-14">tsʰ</td><td id="1-15">tsh</td></tr>
<tr><td id="1-16">u</td><td id="1-17">u</td></tr>
<tr><td id="1-18">v</td><td id="1-19">v</td></tr>
<tr><td id="1-1a">?</td><td id="1-1b">X</td></tr>
<tr><td id="1-1c">Z</td><td id="1-1d">Z</td></tr>
</table>

<a id='c3c7fac0-4bf3-4738-85b8-1f6655a435f6'></a>

**Table II:** *Broad categories of Mizo phone set*
<table id="1-1e">
<tr><td id="1-1f">Category</td><td id="1-1g">Phones</td></tr>
<tr><td id="1-1h">Vowels</td><td id="1-1i">a, e, i, o, u</td></tr>
<tr><td id="1-1j">Stops</td><td id="1-1k">b, c, d, k, kh, p, ph, t, th, x</td></tr>
<tr><td id="1-1l">Fricatives</td><td id="1-1m">f, h, s, v, z</td></tr>
<tr><td id="1-1n">Complex Sound (A)</td><td id="1-1o">hl, hm, hn, hng, hr</td></tr>
<tr><td id="1-1p">Complex Sound (B)</td><td id="1-1q">tl, tlh, tr, trh, ts, tsh</td></tr>
<tr><td id="1-1r">Sonorants</td><td id="1-1s">r, l, m, n, ng</td></tr>
</table>

<a id='fb662b48-82f2-4853-b8e0-b1f8a4ec9c01'></a>

IV. DEVELOPMENT OF PHONE RECOGNITION SYSTEM

In this section, we discuss the different methodologies
that are adopted in developing the Mizo PRS. The system is
developed using the Kaldi Speech Recognition Toolkit [15]. In
this work, we explore different acoustic modelling approaches,
namely, GMM-HMM, DNN-HMM and SGMM-HMM using
Kaldi.

<!-- PAGE BREAK -->

<a id='391c885e-61f3-4c0d-b799-413a3fe03d66'></a>

Table III: *Statistics of speech corpus*
<table id="2-1">
<tr><td id="2-2"></td><td id="2-3">Training</td><td id="2-4">Testing</td></tr>
<tr><td id="2-5">Speech Data (Hrs)</td><td id="2-6">5.5</td><td id="2-7">1.5</td></tr>
<tr><td id="2-8">No. of utterances</td><td id="2-9">7394</td><td id="2-a">1568</td></tr>
<tr><td id="2-b">Total Speakers</td><td id="2-c">62</td><td id="2-d">19</td></tr>
<tr><td id="2-e">Male Speakers</td><td id="2-f">31</td><td id="2-g">12</td></tr>
<tr><td id="2-h">Female Speakers</td><td id="2-i">31</td><td id="2-j">7</td></tr>
</table>

<a id='7bc86fac-bc44-4e82-ba42-fd6f366ab9ce'></a>

A. Feature extraction and acoustic modelling

Experimental evaluations are carried out using one of the most widely used feature set, the Mel-Frequency Cepstral Coefficients (MFCC) [16]. The MFCC feature vectors are computed from Hamming windowed frames of 25 ms duration with a frame shift of 10 ms and pre-emphasis factor of 0.97. Each feature vector consists of energy and 12 MFCCs (C0-C12). In addition to the 13 dimensional static MFCC features, the Δ and ΔΔ variants are also used in this work. The velocity and acceleration components are appended, in order to capture the dynamic characteristics of the vocal tract system.

<a id='46f11d11-a989-4ead-9d09-ce207cda280e'></a>

In the current Mizo PRS, the acoustic evidence for a
phone is derived following 6 different approaches. The base
Mizo PRS is initialized with a context-independent monophone
acoustic model using 39 dimensional MFCC feature vectors.
Each of the 36 phonetic units listed in Table I is modelled by a
3 state left-to-right HMM model where the probability density
function of each state is a GMM with 8 mixtures. This PRS
is labelled as **Monophone** system.

<a id='75cfef33-de79-4929-81ae-c28b5a940dfb'></a>

In order to capture contextual information, cross-word
triphone acoustic models are trained with decision tree-based
state tying. This system is labelled as **Tri1** system. The
next PRS, labelled **Tri2**, does not explicitly use the dynamic
information. Instead, the 13 dimensional static MFCC feature
vectors are spliced in time in order to capture the dynamic
information implicitly from feature vectors of the neighbouring
frames. Four frames to the left and 4 frames to the right of
the central frame are spliced thereby making the total feature
dimension to 117 (13×9). The dimension of the spliced feature
vector is then reduced from 117 to 40 through Linear Discrim-
inant Analysis (LDA) [17], [18]. The resulting feature vectors
are further decorrelated using Maximum Likelihood Linear
Transform (MLLT) [19], [20]. The derived feature vectors are
normalized using cepstral mean and variance normalization.
The extracted features are further normalized using feature-
space Maximum Likelihood Linear Regression (fMLLR) [21].
The next advanced system, labelled as **Tri3**, employs Speaker
Adaptive Training (SAT) [22] using fMLLR transformations.

<a id='914aa5ea-3af4-4491-8e6a-ebfbd2567c48'></a>

We also explored the DNN based acoustic modeling. A feed forward deep neural network is trained using multiple hidden layers that takes time-spliced feature vectors with LDA+MLLT+fMLLR as input, and computes the posterior probabilities over HMM states as output. The specification of the parameters used in training the DNN is detailed in table IV.

<a id='52965175-23b6-455a-82df-82b286d125c6'></a>

In conventional GMM-HMM systems, each state in HMM
is modelled by an independent GMM. As a result, a large
number of model parameters are required to be estimated. This
problem is well addressed by the SGMM [8] based acoustic

<a id='62f160b2-6807-44fa-8e5e-c12157f8a470'></a>

Table IV: *Parameter specifications of DNN based model*
<table id="2-k">
<tr><td id="2-l">Parameter</td><td id="2-m">Specification</td></tr>
<tr><td id="2-n">No. of Hidden Layers</td><td id="2-o">3</td></tr>
<tr><td id="2-p">Initial learning rate</td><td id="2-q">0.01</td></tr>
<tr><td id="2-r">Final learning rate</td><td id="2-s">0.0015</td></tr>
<tr><td id="2-t">No. of epochs</td><td id="2-u">20</td></tr>
<tr><td id="2-v">Hidden layer dimension</td><td id="2-w">1024</td></tr>
<tr><td id="2-x">Mini batch size</td><td id="2-y">128</td></tr>
</table>

<a id='58a17a7b-3d24-43b5-8985-40fef0df2d5c'></a>

modelling framework. In this approach, complex distribution
of parameters are represented in a compact way. Here, the
HMM states globally share a common structure, and only the
state-dependent parameters are required to be estimated. As
a result, the total number of parameter estimation is reduced,
which makes it possible to learn the model parameters with
limited amount of training data.

<a id='fa70a5c4-5af4-4088-8fbc-b05460a4eb8c'></a>

B. Language modelling

In the current work, we have also studied the influence of language model in the overall performance of the PRS. The goal of a PRS is to estimate the sequence of phones $\hat{\mathbf{O}}$, whose likelihood of matching a given sequence of feature vectors $\mathbf{F}$ is maximum. Mathematically it is represented in the following way:

$$\hat{\mathbf{O}} = \underset{\mathbf{o}}{\text{argmax}}P(\mathbf{O}|\mathbf{F}) \quad (1)$$

Using Bayes' rule, the term $P(\mathbf{O}|\mathbf{F})$ can be simplified as:

$$P(\mathbf{O}|\mathbf{F}) = \frac{P(\mathbf{F}|\mathbf{O})P(\mathbf{O})}{P(\mathbf{F})} \quad (2)$$

<a id='c8df45d4-23d2-46cc-8f73-760eb9fd8f09'></a>

The likelihood P(F|O) in Equation 2 is determined by the acoustic model, while the prior probability P(O) is determined by the language model. P(F) represents the prior probability of the feature sequence, which is independent of the acoustic and linguistic evidence and can be ignored in the maximization operation. In the present work, the prior probability of the phone sequence P(O) is estimated using statistical bi-gram language model [23]. The bi-gram probabilities are estimated from the phone level transcription of the training data. In practical speech recognition systems, the overall likelihood of the acoustic and linguistic evidence is computed as:

logP(F|O) + αlogP(O) + β|O|

<a id='2910d3b3-72e4-4160-8a59-992834c3e133'></a>

Here, $\alpha$ is the language model scaling factor and $\beta$ is the phone insertion penalty [24].

<a id='17e092e2-fee3-4a0b-aa1a-f20f2f4d3803'></a>

V. RESULTS AND DISCUSSION
The Mizo phone recognition system is trained with 7394 utterances collected from 62 native Mizo speakers and eval-uated on a testing set comprising of 1568 utterances. For evaluating the performance of the PRS, the decoded hypothesis is compared with the original reference transcription and the Phone Error Rate (PER) is computed using Equation 3.

<a id='7ec4e838-aa73-4c38-b8b1-7fe242c17d81'></a>

PER = \frac{S + D + I}{N} \times 100 (3)

<!-- PAGE BREAK -->

<a id='a124d24b-2277-433e-b1ee-d82642849ae9'></a>

Table V: PERs of 6 variants of Mizo PRS, with and without the influence of Language Model (LM)
<table id="3-1">
<tr><td id="3-2" rowspan="2">Acoustic Model</td><td id="3-3" colspan="2">Without LM</td><td id="3-4" colspan="2">With LM</td><td id="3-5" rowspan="2">Relative Improvement in PER (%)</td></tr>
<tr><td id="3-6">Im-scale</td><td id="3-7">PER (%)</td><td id="3-8">Im-scale</td><td id="3-9">PER (%)</td></tr>
<tr><td id="3-a">Monophone</td><td id="3-b">0</td><td id="3-c">34.3</td><td id="3-d">1.8</td><td id="3-e">25.7</td><td id="3-f">25.1</td></tr>
<tr><td id="3-g">Tri1</td><td id="3-h">0</td><td id="3-i">28.4</td><td id="3-j">2.4</td><td id="3-k">20.9</td><td id="3-l">26.4</td></tr>
<tr><td id="3-m">Tri2</td><td id="3-n">0</td><td id="3-o">23.1</td><td id="3-p">2.4</td><td id="3-q">17.8</td><td id="3-r">22.9</td></tr>
<tr><td id="3-s">Tri3</td><td id="3-t">0</td><td id="3-u">21.9</td><td id="3-v">2.4</td><td id="3-w">17.6</td><td id="3-x">19.6</td></tr>
<tr><td id="3-y">DNN</td><td id="3-z">0</td><td id="3-A">18.1</td><td id="3-B">1.8</td><td id="3-C">13.9</td><td id="3-D">23.2</td></tr>
<tr><td id="3-E">SGMM</td><td id="3-F">0</td><td id="3-G">17.5</td><td id="3-H">1.8</td><td id="3-I">15.7</td><td id="3-J">10.3</td></tr>
</table>

<a id='8030d7be-959a-4569-b33c-a7ddd01b5712'></a>

Here, S is the number of substitution errors, D is the number
of deletion errors, I is the number of insertion errors and N is
the total number of phone labels in the reference transcription.

<a id='c8da6990-466c-4d36-ba2b-77c568569005'></a>

Table V shows the PERs of 6 variants of Mizo PRS. The first row of the table shows the PERs of the monophone system. The next 3 rows show the PERs for the 3 types of context-dependent PRS. The 5th row shows the PER of the system when DNN replaced GMMs to model acoustic characteristics of triphone HMMs. The last row corresponds to the case when SGMM replaced conventional GMM to model triphone HMMs.

<a id='97118a5f-1552-4819-bb98-192337d7592e'></a>

Initially, the experimental evaluations are conducted by setting the language model scaling factor (a) to 0 and phone insertion penalty (3) to 1. By doing this, the overall likelihood of the hypothesis is evaluated without any language constraint. It is observed that the performance of DNN and SGMM based systems are much better than the GMM based system. It is interesting to note that the SGMM based system outperforms all the other systems. The better performance of SGMM system can be attributed to the fact that the amount of speech data used in training the acoustic models is not very large.

<a id='9a1be9e3-9d0f-4a5b-999f-3a53794eaef0'></a>

In order to study the influence of language model, the language model scaling factor (α) is varied from 0 to 3 in steps of 0.2 keeping the phone insertion penalty (β) constant at 1. The phone error rates decreased with increasing value of α. The changes are found to be prominent when the value of α is in the range of 1.5-2.5. Beyond 2.5, the performance is saturated. The phone error rates for optimum language model scaling factor (α) is shown in the fifth column of Table V, and the relative improvements after incorporating the language model is shown in the sixth column of Table V. The gradual changes in the PER profiles are shown in Figure 2. A larger reduction in PER of the Mizo PRS is demonstrated when the value of lm-scale is increased to 1.8 as seen in Figure 2.

<a id='f110d137-df42-478d-a167-04baceb74cf1'></a>

VI. SUMMARY AND CONCLUSION

In this work, the development and evaluation of a Mizo PRS is presented. We have described the process of data collection for the speech corpus and the process of manual annotation of the collected speech data. Using the labelled data, different acoustic models are trained. In addition to the conventional GMM based approach, we also explored the DNN and SGMM based modelling approaches in the development of the Mizo PRS. The performances of both DNN and SGMM based systems are found to be significantly better than the

<a id='86344ef4-d815-4758-9c16-297173f1b028'></a>

<::transcription of the content
: chart::
This is a line chart titled "PER Profiles with the variations of Im-scale".
The Y-axis is labeled "PER(%)" and ranges from 10 to 35.
The X-axis is labeled "Im-scale" and ranges from 0 to 3.
The chart displays six data series, each represented by a distinct line style and marker, as described in the legend:
- Monophone (purple line with circles)
- Triphone (brown line with squares)
- LDA+MLLT (green line with diamonds)
- SAT (blue line with upward triangles)
- DNN (red line with downward triangles)
- SGMM (magenta line with stars)
Figure 2: PER Profiles with the variations of Im-scale
::>

<a id='e4e01bc0-8679-4dd7-8b67-6849897f0dea'></a>

GMM based approach. Since the amount of training data is
limited, the SGMM based system performed better than the
DNN based system without language model. It is observed
that by incorporating the language model information along
with acoustic evidence, the overall performance of the phone
recognition system improves.

<a id='3260c7ea-dde0-4fc9-892f-77b18e7db911'></a>

ACKNOWLEDGMENT

The speech corpus used in this work was developed for an ongoing project titled "Acoustic and Tonal Features based Analysis of Mizo", funded by the Department of Electronics & Information Technology (DeitY), Ministry of Communication & Information Technology (MC&IT), Government of India.

<a id='9acb4950-b53c-474a-82e8-0e7ee5015217'></a>

# REFERENCES

1.  B. D. Sarma, M. Sarma, M. Sarma, and S. R. M. Prasanna, "Development of Assamese Phonetic Engine: Some issues," in *2013 Annual IEEE India Conference (INDICON)*, Dec 2013, pp. 1–6.
2.  L. J. S. Sushanta Kabir Dutta, Salam Nandakishor, "Development of Manipuri phonetic engine and its application in language identification," *International Journal of Engineering and Technical Research (IJETR)*, vol. Volume-3,Issue-8,, August 2015.
3.  K. E. Manjunath, K. S. Rao, and D. Pati, "Development of phonetic engine for Indian languages: Bengali and Oriya," in *2013 International Conference Oriental COCOSDA held jointly with 2013 Conference on Asian Spoken Language Research and Evaluation (O-COCOSDA/CASLRE)*, Nov 2013, pp. 1–6.
4.  G. Deekshitha and L. Mary, "Prosodically guided phonetic engine," in *2015 IEEE International Conference on Signal Processing, Informatics, Communication and Energy Systems (SPICES)*, Feb 2015, pp. 1–5.

<!-- PAGE BREAK -->

<a id='b8a94d2d-2d96-4bc5-baef-1efbd9b404d5'></a>

[5] L. Babykutty, A. George, and L. Mary, "Development of multilingual phonetic engine for four Indian languages," in 2016 International Conference on Next Generation Intelligent Systems (ICNGIS), Sept 2016, pp. 1–3.
[6] G. E. Hinton, L. Deng, D. Yu, G. Dahl, A. R. Mohamed, N. Jaitly, A. Senior, V. Vanhoucke, P. Nguyen, T. Sainath, and B. Kingsbury, "Deep Neural Networks for Acoustic Modeling in Speech Recognition," Signal Processing Magazine, vol. 29, no. 6, pp. 82–97, November 2012.
[7] G. Dahl, D. Yu, L. Deng, and A. Acero, "Context-dependent pre-trained deep neural networks for large vocabulary speech recognition," IEEE Transactions on Speech and Audio Processing, vol. 20, no. 1, pp. 30–42, 2012.
[8] D. Povey, L. Burget, M. Agarwal, P. Akyazi, K. Feng, A. Ghoshal, O. Glembek, N. K. Goel, M. Karafit, A. Rastrow, R. C. Rose, P. Schwarz, and S. Thomas, "Subspace gaussian mixture models for speech recognition," in 2010 IEEE International Conference on Acoustics, Speech and Signal Processing, March 2010, pp. 4330–4333.
[9] R. C. Rose, S.-C. Yin, and Y. Tang, "An investigation of subspace modeling for phonetic and speaker variability in automatic speech recognition," in Proc. ICASSP, May 2011, pp. 4508–4511.
[10] P. Sarmah and C. R. Wiltshire, "A preliminary acoustic study of Mizo vowels and tones," J. Acoust. Soc. Ind, vol. 37, no. 3, pp. 121–129, 2010.
[11] B. D. Sarma, P. Sarmah, W. Lalhminghlui, and S. M. Prasanna, "Detection of Mizo tones," in Sixteenth Annual Conference of the International Speech Communication Association, 2015.
[12] P. Sarmah, L. Dihingia, and W. Lalhminghlui, "Contextual variation of tones in Mizo," in Sixteenth Annual Conference of the International Speech Communication Association, 2015.
[13] I. P. Association, Handbook of the International Phonetic Association: A guide to the use of the International Phonetic Alphabet. Cambridge University Press, 1999.
[14] P. Boersma, "Praat, a system for doing phonetics by computer." Glot International, vol. 5, no. 9/10, pp. 341–345, 2001.
[15] D. Povey, A. Ghoshal, G. Boulianne, L. Burget, O. Glembek, N. Goel, M. Hannemann, P. Motlicek, Y. Qian, P. Schwarz, J. Silovsky, G. Stemmer, and K. Vesely, "The kaldi speech recognition toolkit," in IEEE 2011 Workshop on Automatic Speech Recognition and Understanding. IEEE Signal Processing Society, Dec. 2011, iEEE Catalog No.: CFP11SRW-USB.
[16] S. Davis and P. Mermelstein, "Comparison of parametric representations for monosyllabic word recognition in continuously spoken sentences," IEEE Transactions on Acoustics, Speech, and Signal Processing, vol. 28, no. 4, pp. 357–366, Aug 1980.
[17] R. Haeb-Umbach and H. Ney, "Linear discriminant analysis for improved large vocabulary continuous speech recognition," in Proceedings of the 1992 IEEE International Conference on Acoustics, Speech and Signal Processing Volume 1, ser. ICASSP'92. Washington, DC, USA: IEEE Computer Society, 1992, pp. 13–16. [Online]. Available: http://dl.acm.org/citation.cfm?id=1895550.1895555
[18] H. Abbasian, B. Nasersharif, A. Akbari, M. Rahmani, and M. S. Moin, "Optimized linear discriminant analysis for extracting robust speech features," in 2008 3rd International Symposium on Communications, Control and Signal Processing, March 2008, pp. 819–824.
[19] M. Gales, "Maximum likelihood linear transformations for hmm-based speech recognition," Computer Speech & Language, vol. 12, no. 2, pp. 75 – 98, 1998. [Online]. Available: http://www.sciencedirect.com/science/article/pii/S0885230898900432
[20] R. A. Gopinath, "Maximum likelihood modeling with gaussian distributions for classification," in Acoustics, Speech and Signal Processing, 1998. Proceedings of the 1998 IEEE International Conference on, vol. 2, May 1998, pp. 661–664 vol.2.
[21] C. Leggetter and P. Woodland, "Maximum likelihood linear regression for speaker adaptation of continuous density hidden Markov models," Computer Speech & Language, vol. 9, no. 2, pp. 171 – 185, 1995. [Online]. Available: http://www.sciencedirect.com/science/article/pii/S0885230885700101
[22] T. Anastasakos, J. McDonough, and J. Makhoul, "Speaker adaptive training: A maximum likelihood approach to speaker normalization," in Proceedings of the 1997 IEEE International Conference on

<a id='32a47193-ad6b-4b75-850a-da779fbed5ee'></a>

Acoustics, Speech, and Signal Processing (ICASSP '97)-Volume
2 - Volume 2, ser. ICASSP '97. Washington, DC, USA:
IEEE Computer Society, 1997, pp. 1043-. [Online]. Available:
http://dl.acm.org/citation.cfm?id=839274.839489

[23] P. F. Brown, P. V. deSouza, R. L. Mercer, V. J. D. Pietra, and
J. C. Lai, "Class-based n-gram models of natural language," *Comput.
Linguist.*, vol. 18, no. 4, pp. 467-479, Dec. 1992. [Online]. Available:
http://dl.acm.org/citation.cfm?id=176313.176316

[24] M. Gales and S. Young, "The application of hidden markov
models in speech recognition," *Foundations and Trends in Signal
Processing*, vol. 1, no. 3, pp. 195-304, 2008. [Online]. Available:
http://dx.doi.org/10.1561/2000000004