# Lecture 1 - Introduction to Information Theory

[[slides](http://www.inference.org.uk/mackay/itprnn/slides/l1/)]
[[video](http://videolectures.net/mackay_course_01/)]

## The Fundamental Problem
- This field was invented to enable reliable communications over unreliable channels
- Received signal <img alt="$\simeq$" src="tex/svgs//457d781a27eac74101aa836bf74a4205.png?invert_in_darkmode" align=middle width="12.785520000000004pt" height="15.24665999999999pt"/> transmitted signal <img alt="$+$" src="tex/svgs//df33724455416439909c33a7db76b2bc.png?invert_in_darkmode" align=middle width="12.785520000000004pt" height="19.178279999999994pt"/> noise
- We would like communications where received message <img alt="$=$" src="tex/svgs//591ff9c1652b7e605ef0190a9713c140.png?invert_in_darkmode" align=middle width="12.785520000000004pt" height="14.155350000000013pt"/> transmitted message

## Solutions
### Physical
- Adapting physics to improve the channel
- e.g. better insulation, adding cooling, etc.

### Systems
- Accepting noise and the unreliable channel
- Adding encoding and decoding to make it reliable

### Encoding
Source <img alt="$\underline{s}$" src="tex/svgs//9249f20c9bf4301753cb9a7ac0e8ee28.png?invert_in_darkmode" align=middle width="7.705549500000004pt" height="14.155350000000013pt"/> <img alt="$\rightarrow$" src="tex/svgs//e5d134f35dc4949fab12ec64d186248a.png?invert_in_darkmode" align=middle width="16.438455000000005pt" height="14.155350000000013pt"/> Encoder <img alt="$\rightarrow$" src="tex/svgs//e5d134f35dc4949fab12ec64d186248a.png?invert_in_darkmode" align=middle width="16.438455000000005pt" height="14.155350000000013pt"/> Coded Transmission <img alt="$\underline{t}$" src="tex/svgs//8b6884394064102a3556fe7f39831eaf.png?invert_in_darkmode" align=middle width="5.936155500000004pt" height="20.222069999999988pt"/> <img alt="$\rightarrow$" src="tex/svgs//e5d134f35dc4949fab12ec64d186248a.png?invert_in_darkmode" align=middle width="16.438455000000005pt" height="14.155350000000013pt"/> Channel <img alt="$+$" src="tex/svgs//df33724455416439909c33a7db76b2bc.png?invert_in_darkmode" align=middle width="12.785520000000004pt" height="19.178279999999994pt"/> Noise <img alt="$\underline{n}$" src="tex/svgs//0bf172a7b92eeb1ad5cf65897c15e950.png?invert_in_darkmode" align=middle width="9.867000000000003pt" height="14.155350000000013pt"/> <img alt="$\rightarrow$" src="tex/svgs//e5d134f35dc4949fab12ec64d186248a.png?invert_in_darkmode" align=middle width="16.438455000000005pt" height="14.155350000000013pt"/> Received Message <img alt="$\underline{r}$" src="tex/svgs//920855b602a808c9f2d8aad22396c75e.png?invert_in_darkmode" align=middle width="7.873024500000003pt" height="14.155350000000013pt"/> <img alt="$\rightarrow$" src="tex/svgs//e5d134f35dc4949fab12ec64d186248a.png?invert_in_darkmode" align=middle width="16.438455000000005pt" height="14.155350000000013pt"/> Decoder <img alt="$\rightarrow$" src="tex/svgs//e5d134f35dc4949fab12ec64d186248a.png?invert_in_darkmode" align=middle width="16.438455000000005pt" height="14.155350000000013pt"/> Decoded Message <img alt="$\underline{\hat{s}}$" src="tex/svgs//c12d9c10db59af43083becc9e0503655.png?invert_in_darkmode" align=middle width="8.875680000000004pt" height="22.831379999999992pt"/>

## Binary Symmetric Channels
![Representation of a binary symmetric channel](images/bsc.png)

We will use the binary symmetric channel (BSC) as a toy problem. <img alt="$f$" src="tex/svgs//190083ef7a1625fbc75f243cffb9c96d.png?invert_in_darkmode" align=middle width="9.817500000000004pt" height="22.831379999999992pt"/> is the probability of a single bit being flipped. For all the following problems, we will assume <img alt="$f = 0.1$" src="tex/svgs//78c9437456c4fc7a51be7f80dc4f6e3a.png?invert_in_darkmode" align=middle width="52.739775pt" height="22.831379999999992pt"/>.

<p align="center"><img alt="$$\begin{aligned} P(y=0 | x=0) &amp;= 1-f \\&#10;P(y=1 | x=0) &amp;= f \\&#10;P(y=0 | x=1) &amp;= f \\&#10;P(y=1 | x=1) &amp;= 1-f&#10;\end{aligned}$$" src="tex/svgs//5cf42419d75b04fe5f3c969f024ac4ac.png?invert_in_darkmode" align=middle width="168.55245pt" height="90.41092499999999pt"/></p>

## Question 1
_If <img alt="$10000$" src="tex/svgs//fa35043f335bc43f27e21bc02c268be9.png?invert_in_darkmode" align=middle width="41.09605500000001pt" height="21.18732pt"/> bits are stored on a disk drive, and each bit is independently read, how many are flipped?_  
This falls under the binomial distribution, so we have:

<p align="center"><img alt="$$\begin{aligned}&#10;\mu &amp;= np = 10000 \times 0.1 = 1000 \\&#10;\sigma^2 &amp;= npq = 1000 \times 0.1 \times 0.9 = 900&#10;\end{aligned}$$" src="tex/svgs//a0458d710e7af5592853fd144f7845f0.png?invert_in_darkmode" align=middle width="248.90249999999997pt" height="40.485884999999996pt"/></p>

## Question 2
_For a saleable 1GB drive, how small does <img alt="$f$" src="tex/svgs//190083ef7a1625fbc75f243cffb9c96d.png?invert_in_darkmode" align=middle width="9.817500000000004pt" height="22.831379999999992pt"/> need to be, assuming the drive is used for 5 years at 1GB/day?_

<p align="center"><img alt="$$ \begin{aligned} \#\text{bits} &amp; = 5 \times 365 \times 8 \times 10^9\ \text{bits} \\&#10;&amp; \approx 10^{13}\ \text{bits} \end{aligned}$$" src="tex/svgs//5528bfe43ffd0396c1bb417a15e808b2.png?invert_in_darkmode" align=middle width="219.42854999999997pt" height="40.898714999999996pt"/></p>

But if we want a <img alt="$1\%$" src="tex/svgs//930f16f65c521e0e55d346532bbc4cc6.png?invert_in_darkmode" align=middle width="21.917940000000005pt" height="24.65759999999998pt"/> chance of dissapointment, we will need to set <img alt="$f \simeq 10^{-15}$" src="tex/svgs//83f75cbac2d1fcacdb2b893af01eb2ac.png?invert_in_darkmode" align=middle width="71.55257999999999pt" height="26.76201000000001pt"/>.  
To have <img alt="$1000$" src="tex/svgs//675eeb554f7b336873729327dab98036.png?invert_in_darkmode" align=middle width="32.87691pt" height="21.18732pt"/> happy customers under this new constraint, we will further neet to set <img alt="$f \simeq 10^{-18}$" src="tex/svgs//4cbe4df9402b4f8e94ec703ebe892677.png?invert_in_darkmode" align=middle width="71.55257999999999pt" height="26.76201000000001pt"/>. This is usually the standard in industry.

We will aim for <img alt="$f \simeq 10^{-15}$" src="tex/svgs//83f75cbac2d1fcacdb2b893af01eb2ac.png?invert_in_darkmode" align=middle width="71.55257999999999pt" height="26.76201000000001pt"/> for now.

## Example Encoders
### Parity Coding
- Set a parity bit <img alt="$p$" src="tex/svgs//2ec6e630f199f589a2402fdf3e0289d5.png?invert_in_darkmode" align=middle width="8.270625000000004pt" height="14.155350000000013pt"/> as the sum of some preceding bits <img alt="$s$" src="tex/svgs//6f9bad7347b91ceebebd3ad7e6f6f2d1.png?invert_in_darkmode" align=middle width="7.705549500000004pt" height="14.155350000000013pt"/>
- <img alt="$01011101$" src="tex/svgs//bf905e9e70a6184637ca8f4c38f1bc39.png?invert_in_darkmode" align=middle width="65.75381999999999pt" height="21.18732pt"/> would have parity bit <img alt="$1$" src="tex/svgs//034d0a6be0424bffe9a6e7ac9236c0f5.png?invert_in_darkmode" align=middle width="8.219277000000005pt" height="21.18732pt"/> appended to it

### Repetition Codes
- Repeat the source message a number of times

For <img alt="$R_3$" src="tex/svgs//b2992ba5af2f58c3526dc9f42bd6ac69.png?invert_in_darkmode" align=middle width="19.034070000000003pt" height="22.46574pt"/>:

<p align="center"><img alt="$$\begin{aligned}&#10;s &amp;\rightarrow t \\&#10;0 &amp;\rightarrow 000 \\&#10;1 &amp;\rightarrow 111&#10;\end{aligned}$$" src="tex/svgs//ea169dd320b62097e5a11223277841bd.png?invert_in_darkmode" align=middle width="58.447455pt" height="59.425905pt"/></p>

The decoder under this scheme is a simple majority voting decoder (MVD):

<p align="center"><img alt="$$\begin{aligned}&#10;r &amp;\rightarrow \hat{s} \\&#10;000 &amp;\rightarrow 0 \\&#10;001 &amp;\rightarrow 0 \\&#10;110 &amp;\rightarrow 1 \\&#10;111 &amp;\rightarrow 1&#10;\end{aligned}$$" src="tex/svgs//fb8c8f8ee3593ed2bcc1f226a0e82ac9.png?invert_in_darkmode" align=middle width="59.103825pt" height="110.04559499999999pt"/></p>

![Representation of applying R_3 and MVD to transmit over a BSC](images/bsc_r3.png)

And here is a worked example:

<p align="center"><img alt="$$\begin{aligned}&#10;s &amp;= 0\ 1\ 1\ 0\ 1 \\&#10;t &amp;= 000\ 111\ 111\ 000\ 111 \\&#10;n &amp;= 000\ 100\ 000\ 101\ 000\quad &amp;\text{(1 causes a flip)} \\&#10;r &amp;= 000\ 011\ 111\ 101\ 111 \\&#10;\hat{s} &amp;= 0\ 1\ 1\ 1\ 1\quad &amp;\text{(error in 4th bit)}&#10;\end{aligned}$$" src="tex/svgs//dd3f6a63bbdc04fcaf76961891c8d32b.png?invert_in_darkmode" align=middle width="331.4652pt" height="113.33338499999998pt"/></p>

Repetition codes work, but they are not good enough for <img alt="$f \simeq 10^{-15}$" src="tex/svgs//83f75cbac2d1fcacdb2b893af01eb2ac.png?invert_in_darkmode" align=middle width="71.55257999999999pt" height="26.76201000000001pt"/>. We'll see why below.

## Inference
1. Product Rule: <img alt="$P(s,r) = P(s)P(r|s) = P(r)P(s|r)$" src="tex/svgs//9696241addaaefa1afb1682a42d1c8d7.png?invert_in_darkmode" align=middle width="250.69885499999995pt" height="24.65759999999998pt"/>
2. Sum Rule: <img alt="$P(r) = \sum_{s}P(s,r) = P(s=0|r) + P(s=1|r)$" src="tex/svgs//cd2e443507cf811822bc4d6f09132c92.png?invert_in_darkmode" align=middle width="324.85315499999996pt" height="24.65792999999999pt"/>

From the above two rules, we can try solving for the posterior probability of <img alt="$s$" src="tex/svgs//6f9bad7347b91ceebebd3ad7e6f6f2d1.png?invert_in_darkmode" align=middle width="7.705549500000004pt" height="14.155350000000013pt"/>:

<p align="center"><img alt="$$P(s|r) = \frac{P(r|s)P(s)}{P(r)}$$" src="tex/svgs//a818c3724f6ce8f5a71c7339f6f694cb.png?invert_in_darkmode" align=middle width="148.751625pt" height="38.834894999999996pt"/></p>

Note that we refer to <img alt="$P(r|s)$" src="tex/svgs//e8e69acb3d2bab1396b0451aaff4f9d5.png?invert_in_darkmode" align=middle width="45.766875000000006pt" height="24.65759999999998pt"/> as the likelihood of <img alt="$s$" src="tex/svgs//6f9bad7347b91ceebebd3ad7e6f6f2d1.png?invert_in_darkmode" align=middle width="7.705549500000004pt" height="14.155350000000013pt"/>, and <img alt="$P(s)$" src="tex/svgs//133bf4410d30ceb9008d37d7ba7b9d65.png?invert_in_darkmode" align=middle width="33.327690000000004pt" height="24.65759999999998pt"/> as the prior probability of <img alt="$s$" src="tex/svgs//6f9bad7347b91ceebebd3ad7e6f6f2d1.png?invert_in_darkmode" align=middle width="7.705549500000004pt" height="14.155350000000013pt"/>.

### Question 3
_If we receive <img alt="$r = 011$" src="tex/svgs//207bf1dbf39dbcd28415e4148580f7ae.png?invert_in_darkmode" align=middle width="54.44835pt" height="21.18732pt"/>, what are the probabilities for the source message?_

We first calculate the likelihoods of <img alt="$s$" src="tex/svgs//6f9bad7347b91ceebebd3ad7e6f6f2d1.png?invert_in_darkmode" align=middle width="7.705549500000004pt" height="14.155350000000013pt"/>:

<p align="center"><img alt="$$\begin{aligned}&#10;P(r|s=0) &amp;= f^2(1-f)\quad \text{(2 bits flipped)} \\&#10;P(r|s=1) &amp;= f(1-f)^2\quad \text{(1 bit flipped)}&#10;\end{aligned}$$" src="tex/svgs//a55a1b31c092ee99e90e51d278c1f798.png?invert_in_darkmode" align=middle width="289.7631pt" height="45.00837pt"/></p>

We can also place a prior <img alt="$P(s=0) = P(s=1) = 0.5$" src="tex/svgs//7f589b95418741d1fa4680d523af1dd5.png?invert_in_darkmode" align=middle width="191.769105pt" height="24.65759999999998pt"/>, and calculate the posterior straightforwardly:

<p align="center"><img alt="$$\begin{aligned}&#10;P(s=1|r=011) &amp;= \frac{f(1-f)^2 \times 0.5}{f(1-f)^2 \times 0.5 + f^2(1-f) \times 0.5} \\&#10;&amp;= 1-f = 0.9&#10;\end{aligned}$$" src="tex/svgs//5f46cffab7e5e606b2f1ba4cc14e2bc6.png?invert_in_darkmode" align=middle width="384.86249999999995pt" height="63.466919999999995pt"/></p>

<img alt="$P(s=1|r) &gt; P(s=0|r)$" src="tex/svgs//70de8570601653323ab1cd743f4d9fec.png?invert_in_darkmode" align=middle width="173.724705pt" height="24.65759999999998pt"/>, so we have verified that this scheme produces the best choice (<img alt="$\hat{s} = 1$" src="tex/svgs//c5f4c67125b1bcbfe916a2323db7b59f.png?invert_in_darkmode" align=middle width="37.842420000000004pt" height="22.831379999999992pt"/>).

## Forward Probability
We have so far described this system:

<p align="center"><img alt="$$s \xrightarrow{R_3} t \xrightarrow[f]{BSC} MVD \rightarrow \hat{s}$$" src="tex/svgs//af8d604633c0f5c8e63b2e76a19b8caf.png?invert_in_darkmode" align=middle width="178.101pt" height="30.332114999999998pt"/></p>

What is the probability that <img alt="$P(\hat{s} \neq s)$" src="tex/svgs//ba020d8210026fd621ff76574ea89c84.png?invert_in_darkmode" align=middle width="62.9508pt" height="24.65759999999998pt"/> for a single bit (<img alt="$P_b$" src="tex/svgs//2f58d43ed8079cf63f2df3cb116dd7e1.png?invert_in_darkmode" align=middle width="16.334505000000004pt" height="22.46574pt"/>)?  
This would only happen when there are 2 or 3 flips in a block.

<p align="center"><img alt="$$P(\hat{s} \neq s) = f^3 + 3f^2(1-f) \approx 3f^2 $$" src="tex/svgs//ff7e23f60cbd21b13966e8832b4d4119.png?invert_in_darkmode" align=middle width="244.98209999999997pt" height="18.312359999999998pt"/></p>

## Question 4
_For <img alt="$R_N$" src="tex/svgs//d03e5299fcd6df02c3a8aa9475a66034.png?invert_in_darkmode" align=middle width="24.12762pt" height="22.46574pt"/>, what <img alt="$N$" src="tex/svgs//f9c4988898e7f532b9f826a75014ed3c.png?invert_in_darkmode" align=middle width="14.999985000000004pt" height="22.46574pt"/> is needed to deliver <img alt="$P_b \approx 10^{-15}$" src="tex/svgs//77f6c401e1e08394582db49ca96e716d.png?invert_in_darkmode" align=middle width="78.891615pt" height="26.76201000000001pt"/> under our system?_  
<img alt="$N = 61$" src="tex/svgs//f69d6499a03c679630df099fd2eb48b0.png?invert_in_darkmode" align=middle width="53.35605pt" height="22.46574pt"/>

As we add more repetition, we also proportionally reduce the rate of the channel (i.e. the effective data transmission throughput).

![Graph comparing rate vs p_b of repetition codes 1-61](images/rate_vs_pb.png)

## 7,4 Hamming Code
Going back to the idea of using parity bits, we add 3 parity bits for every 4 source bits, as follows:  
Select <img alt="$t_5$" src="tex/svgs//e889e7c76c7f4caae51cd398cc74acca.png?invert_in_darkmode" align=middle width="12.488685000000004pt" height="20.222069999999988pt"/> such that the parity of <img alt="$s_1 + s_2 + s_3 + t_5$" src="tex/svgs//f57b10c72dec9b9fe1df652d34eb5e37.png?invert_in_darkmode" align=middle width="118.00206pt" height="20.222069999999988pt"/> is even.  
Select <img alt="$t_6$" src="tex/svgs//ca3000ee87cb130f95eaa14d33b72855.png?invert_in_darkmode" align=middle width="12.488685000000004pt" height="20.222069999999988pt"/> such that the parity of <img alt="$s_2 + s_3 + s_4 + t_6$" src="tex/svgs//c12e6027c2f587abec29b9b7a5a5a03f.png?invert_in_darkmode" align=middle width="118.00206pt" height="20.222069999999988pt"/> is even.  
Select <img alt="$t_7$" src="tex/svgs//a268cb77170c32b8f247c9ce5a0815be.png?invert_in_darkmode" align=middle width="12.488685000000004pt" height="20.222069999999988pt"/> such that the parity of <img alt="$s_1 + s_3 + s_4 + t_7$" src="tex/svgs//0f24a5b25efd44806369ea13e16b234b.png?invert_in_darkmode" align=middle width="118.00206pt" height="20.222069999999988pt"/> is even.

The decoding process is:  
1. Find the groups which are not of even parity.
2. Find the bit which is inside the incorrect groups, but outside the correct groups.
3. Correct the suspected flipped bit.

### Example
<p align="center"><img alt="$$\begin{aligned}&#10;s &amp;= 1000 \\&#10;t &amp;= 1000\ 101 \\&#10;n &amp;= 0100\ 000\quad \text{(1 causes a flip)} \\&#10;r &amp;= 1100\ 101 \\&#10;\hat{t} &amp;= 1000\ 101\quad \text{(flipped bit corrected)} \\&#10;\hat{s} &amp;= 1000\quad&#10;\end{aligned}$$" src="tex/svgs//b8130b99025e6e9ab57692975f0e3d74.png?invert_in_darkmode" align=middle width="269.77665pt" height="136.165755pt"/></p>

Under this system, any single bit flip is detected and corrected. However, if two or more flips occur, then <img alt="$\hat{s} \neq s$" src="tex/svgs//331bc28fc4aa94ff4a47a92f1645e93a.png?invert_in_darkmode" align=middle width="37.328610000000005pt" height="22.831379999999992pt"/>.

Additionally, for this system it is known that <img alt="$p_{block\ error} \simeq 21f^2$" src="tex/svgs//daae165a7c2bc663f9f2e48e3cf8a3fc.png?invert_in_darkmode" align=middle width="131.02947pt" height="26.76201000000001pt"/> and <img alt="$p_b \simeq 9f^2$" src="tex/svgs//ffd0462cb444a06456c29c6e29162485.png?invert_in_darkmode" align=middle width="61.380165pt" height="26.76201000000001pt"/>.

What is achievable from an encoder-decoder system however? Conventional understanding was that some boundary passing through the origin existed; Shannon proved that for every channel, the boundary actually intersects the x-axis at a non-zero point. This rate is called the capacity <img alt="$C$" src="tex/svgs//9b325b9e31e85137d1de765f43c0f8bc.png?invert_in_darkmode" align=middle width="12.924780000000005pt" height="22.46574pt"/> of the channel in question.

![Graph of the capacity of a BSC](images/channel_capacity.png)

<p align="center"><img alt="$$C_{BSC(f)} = 1 - H_2(f)$$" src="tex/svgs//670512ffd3ecfad9f08bf87d207a569b.png?invert_in_darkmode" align=middle width="153.84237pt" height="18.173595pt"/></p>
<p align="center"><img alt="$$H_2(f) = f\log_2\frac{1}{f} + (1-f)\log_2\frac{1}{1-f}$$" src="tex/svgs//7c0f478fd35705ef3f7dfdaf444cc836.png?invert_in_darkmode" align=middle width="268.41704999999996pt" height="36.186479999999996pt"/></p>

<img alt="$H_2$" src="tex/svgs//912631c954499428b64ab8d828ac8cb6.png?invert_in_darkmode" align=middle width="20.216955000000006pt" height="22.46574pt"/> is the binary entropy function.

This is Shannon's Noisy Channel Coding Theorem, and proving this will be the focus of the next few lectures.

_All figures are from the linked slides for this lecture._
