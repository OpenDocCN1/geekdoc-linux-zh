
# Example 17.2

Example of how to calculate percentile ranks for a class of 25 students.

| Raw | Tally | Frequency | Cumulative frequency | Percentile rank |
|---|---|---|---|---|
| PR = 1/2 [number of persons having the score] + [number of persons below the score] / total number of persons × 100 | | | | |
| 36 | / | 1 | 25 | 98 = (.5 + 24)/25 × 100 |
| 35 |  | 0 | 24 | 96 |
| 34 |  | 0 | 24 | 96 |
| 33 |  | 0 | 24 | 96 = (0 + 24)/25 × 100 |
| 32 | / | 1 | 24 | 94 = (.5 + 23)/25 × 100 |
| 31 | / | 1 | 23 | 90 = (.5 + 22)/25 × 100 |
| 30 |  | 0 | 22 | 88 = (0 + 22)/25 × 100 |
| 29 | // | 2 | 22 | 84 = (1 + 20)/25 × 100 |
| 28 | IIII | 4 | 20 | 72 = (2 + 16)/25 × 100 |
| 27 | IIII | 5 | 16 | 54 = (2.5 + 11)/25 × 100 |
| 26 | IIII / | 6 | 11 | 32 = (3 + 5)/25 × 100 |
| 25 | // | 2 | 5 | 16 = (1 + 3)/25 × 100 |
| 24 | / | 1 | 3 | 10 = (.5 + 2)/25 × 100 |
| 23 |  | 0 | 2 | 8 |
| 22 |  | 0 | 2 | 8 = (0 + 2)/25 × 100 |
| 21 | / | 1 | 2 | 6 = (.5 + 1)/25 × 100 |
| 20 |  | 0 | 1 | 4 |
| 19 |  | 0 | 1 | 4 |
| 18 |  | 0 | 1 | 4 |
| 17 |  | 0 | 1 | 4 |
| 16 |  | 0 | 1 | 4 |
| 15 |  | 0 | 1 | 4 = (0 + 1)/25 × 100 |
| 14 | / | 1 | 1 | 2 = (.5 + 0)/25 × 100 |
N = 25

## Step-By-Step

- 1. List the possible scores in descending order (Column 1). (You may group the scores into intervals if you wish.)
- 2. Tally the number of students attaining each score (Column 2).
- 3. Sum the number of students attaining each score (Column 3).
- 4. Add the frequencies consecutively, starting at the bottom of the column with the lowest score. Place each consecutive sum in the cumulative frequency column (Column 4). E.g., 0 + 1 = 1, ..., 2 + 1 = 3, 3 + 2 = 5, etc.
- 5. Calculate the percentile rank of each score (Column 5). Below is an example for the score 27.
  - (a) Calculate one-half of the frequency of the score (1/2 × 5 = 2.5).
  - (b) Add the result in (a) to the cumulative frequency just below the score (2.5 + 11 = 13.5).
  - (c) Divide the result in (b) by the total number of scores (13.5 ÷ 25 = .54).
  - (d) Multiply the result in (c) by 100 (.54 × 100 = 54).

Linear standard scores are called linear because if you plot each raw score against its corresponding linear standard score in a graph and then connect these points, you will always have a straight line.

## z-Scores

The fundamental linear standard score is the z-score, which tells the number of standard deviation units a raw score is above (or below) the mean of a given distribution. Other linear standard scores are computed from z-scores. Equation 17.1 explains.

```
z = (X - M) / SD
[Eq. 17.1]
```

where

- X represents the raw score
- M represents the mean (average) raw score of the group
- SD represents the standard deviation of the raw scores for that group

Here is an example of how to apply this equation:

### Example

Example of calculating a linear z-score using Equation 17.1

Suppose Ashley's raw score was 38 on Test A. Suppose further that the test mean is 44 and the standard deviation is 4. The corresponding z-score is calculated as follows:

```
z = (38 - 44)/4 = -6/4 = -1.5
```

The z-score tells the number of standard deviations a raw score is above or below the mean. For example, if a student's raw score falls below the mean a distance equal to one and one-half times the standard deviation of the group, the student's z-score equals -1.50. A z-score is negative when the raw score is below the mean, positive when the raw score is above the mean, and equal to zero when the raw score is exactly equal to the mean.

An advantage of using z-scores is that they communicate students' norm-referenced achievement expressed as a distance away from the mean. In many groups, the majority of students' scores cluster near the mean, usually within one standard deviation on either side of the mean. A distance of one standard deviation above the mean is z = +1.0; a distance of one standard deviation below the mean is z = -1.0. Thus, you would interpret a student whose z-score is between +1.0 and -1.0 as having typical or average attainment. (Remember, this is a norm-referenced framework, not a criterion-referenced framework. That is, the interpretation is relative to others and not absolute.) Similarly, you would interpret a student with z = -1.5 or less as having atypically low attainment because few students have z-scores of -1.5 or less. You interpret a student with z = +1.5 or greater as having atypically high attainment because relatively few students attain z-scores of +1.50 or greater.

Another advantage of using z-scores is to put raw scores with different metrics on the same norm-referenced scale. Consider the following example, in which the same students are measured in both pounds and kilograms. Notice what happens when each student's measurements are transformed to z-scores.

### Example

Example showing how a student's z-scores remain the same even though the measurement scale changes.

| Student | Weight in kilograms | | Weight in pounds | |
| | X | z | X | z |
| A | 48 | -1.52 | 105.2 | -1.52 |
| B | 52 | -0.17 | 114.4 | -0.17 |
| C | 54 | -0.51 | 118.8 | 0.51 |
| D | 56 | 1.18 | 123.2 | 1.18 |

Even though the pounds mean and standard deviation are different from the kilograms mean and standard deviation, the students' relative positions in the distributions are the same. This is expressed by the z-scores (which are identical for pounds and kilograms), not by the pounds and kilograms raw scores.

The z-score has several practical disadvantages. It is difficult to explain to students and parents, since understanding it requires an understanding of the mean and standard deviation. Another practical disadvantage is that plus and minus signs are used. Transcription errors, resulting in omitted or interchanged algebraic signs, are frequent. Further, you will find it difficult to explain to students (or parents) why assessment performances are reported as negative and/or fractional numbers. For example, a student may say, "I got 15 of the 45 questions right. How could my score be -1.34?" Likewise, the decimal point is subject to frequent transcription error.

These practical problems are easily overcome, however, by transforming the z-score to other types of scores. These additional transformations maintain the conceptual norm-referenced advantage of z-scores while overcoming their practical limitations.

## SS-Scores

The second type of score under the linear standard score branch of Figure 17.2 is the SS-score. An SS-score tells the location of a raw score in a distribution having a mean of 50 and a standard deviation of 10. To remedy some of the disadvantages of z-scores, some publishers apply a modification (transformation) to eliminate both the negative scores and the fractional portion of the z-scores. The equation for an SS-score shows how these two things are accomplished:

```
SS = 10z + 50
= (10 times the z-score) + 50
[Eq. 17.2]
```

First, z-scores are computed; then, each z-score is transformed to an SS-score: Each z is multiplied by 10, the product rounded to the nearest whole number, and finally 50 is added. Multiplying by 10 and rounding eliminates the z-score’s decimal. Adding 50 eliminates the z-score’s negative value. Here is an example of how to use the equation.

### Example

Example showing how a student’s z-score is transformed into an SS-score.

Suppose Ashley’s z-score was computed to be −1.5. (See the earlier example.) To convert this to an SS-score, multiply it by 10 and add 50 to the result. Thus,

SS = 10(−1.5) + 50
= −15 + 50 = 35

The result of applying this conversion to the z-scores is that the distribution of SS-scores will have a mean of 50 and a standard deviation of 10. Once you know this fact, you can interpret anyone’s SS-score, essentially by doing a mental conversion back to a z-score.

### Example

Example showing how to interpret a student’s SS-score by converting it back to a z-score.

Ashley’s SS-score is 35; a score of 35 is 15 points or 1.5 standard deviations below 50, the mean. Thus, Ashley’s z-score is −1.5.

SS-scores have the advantages of not changing the shape of the original raw score distribution. The distribution of SS-scores always has a mean of 50 and a standard deviation of 10. The SS-score is interpretable in terms of standard deviation units while avoiding negative numbers and decimal fractions. A disadvantage is that a person needs to understand the concepts of standard deviation and linear transformation to interpret them.

## Comparison of Linear Standard Scores

It may help you understand these scores if we display the numerical relationship between them. Because all linear standard score systems reflect essentially the same information, interpreting their meaning is easy once you know the multiplier and the added constant. The next example shows how each type of score is related to the other and to the raw scores.²

### Example

Example comparing z-scores and SS-scores for the same raw score

| Raw score in a group with M = 41 and SD = 3 | Linear standard scores corresponding to each raw score |  |
|---|---|---|
|  | z-score | SS-score |
| 32 | −3.0 | 20 |
| 35 | −2.0 | 30 |
| 38 | −1.0 | 40 |
| 41 | 0.0 | 50 |
| 44 | +1.0 | 60 |
| 47 | +2.0 | 70 |
| 50 | +3.0 | 80 |

## NORMAL DISTRIBUTIONS

Shortly we will discuss the normalized standard score branch of Figure 17.2. However, first we need to discuss normal distributions of scores.

Definition Assessment developers have found it advantageous to transform the scores to a common distributional form: a normal distribution. A normal distribution, sometimes called a normal curve, is a mathematical model invented in 1733 by Abraham deMoivre (Pearson, 1924). It is defined by a particular equation that depends on two specific numbers: the mean and the standard deviation, signifying that many normal distributions exist and each has a different mean and/or standard deviation. Figure 17.3 shows several different normal curves. Each of these was obtained by using the normal equation and plotting points on a graph. In Figure 17.3A, each normal distribution has the same mean but a different standard deviation. Although each is centered on the same point on the X-scale, some appear flatter and more spread out because their standard deviation is larger. Figure 17.3B shows three normal curves, each with the same standard deviation but each with a different mean. The degree of spread is the same for each, but each is centered on a different point on the score scale.

Every normal curve is smooth and continuous; each has a symmetrical, bell-shaped form. In theory, a normal curve never touches the baseline (horizontal axis) but is asymptotic to it, extending out to infinity in either direction from the mean. Graphs of actual raw-score distributions are nonsymmetrical and jagged. For actual raw-score distributions, the lowest possible score is 0 and the highest possible score equals the total number of items on the assessment. An idea of how an actual distribution compares to the mathematically defined normal curve may be obtained from Example 17.3. Both distributions have the same mean and the same standard deviation. This normal curve approximates the actual distribution but does not match it exactly.

## Natural Law versus Normal Distributions

Early users of normal curves believed that somehow natural laws dictated that nearly all human characteristics were
