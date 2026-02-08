# Project

# Theory

## Fairness metrics

It is extremely difficult to concretely define the concept of fairness. Because of this, there are many metrics associated with this concept. We can divide this metrics into two classes, whether they measure **individual** (similar individuals should have similar outcomes) or **group** fairness (the model shouldn't discriminate against certain groups). We will focus on the latter metrics. There are three broad notions of group fairness:

- **Independence**: Decisions should be independent of any sensitive attribute.
- **Separation**: Disparities on groups should be completely justified by the target variable, assuming that you can trust that the target variable is correctly labeled i.e. is not biased.
- **Sufficiency**: Similar to separation, but taking into account the predicted variable instead of the target.

### Independence

Decisions should be independent from any protected attributes (demographic parity):

$$P(\hat{Y} = 1 \mid A = a) = P(\hat{Y} = 1 \mid A = b), \quad \forall a, b \in \mathcal{A}$$

There are situations where independence doesn't directly relate to fairness. For example, women may have a bigger admission rate into a degree than men because they might have better grades in general. In order to achieve independence, or demographic parity, the model **should favor the group** with lower admission rates, i.e. **treating groups differently**, and this might not be fair. For this reason, we have to be very careful with enforcing demographic parity, and it has to be justified, for example, we can't trust that the target variable is correctly labelled, or there is historical bias in the data.

Another criteria for independence named **Conditional demographic parity** could be more suitable in most situations. In the last example, we could say that we have achieved conditional demographic parity if the predicted variable (admission) is independent of the protected attribute (sex) for individuals with the same grades.

### Separation

Disparities between groups should be completely justified by the target variable:

$$P(\hat{Y}=1 \mid A = a, Y=y) = P(\hat{Y} = 1 \mid A = b, Y=y),\quad \forall a,b\in \mathcal{A}, y\in{0, 1}$$

This can be a good fairness metric **if the target variable is free of any bias**.



There are two relaxed versions of separation:

- **Predictive equality**: Same false positive rates across groups. $FPR = \dfrac{FP}{FP+TN}$
- **Equality of opportunity**: Same false negative rates. $FNR = \dfrac{FN}{FN + TP}$

Depending on the problem, one may prioritize one or the other.

- Predictive equality may be prioritized when you want to minimize the risk of innocent people being arrested (False positive) between groups.
- Equality of opportunity may be prioritized when accepting people into a degree, i.e. both groups should have equal opportunities.

In conclusion, separation might be a good fairness metric if the data can be trusted, specifically the target variables.

### Sufficiency

When the model has the same precission across sensitive groups, it has achieved predictive parity:

$$P(Y=1 \mid A=a, \hat{Y} = 1) = P(Y=1 \mid A=b, \hat{Y} = 1),\quad \forall a,b\in \mathcal{A}$$

If we require the last condition to also hold true for $Y=0$, then the sufficiency criterion is satisfied.

The main difference between sufficiency and separation is in the point of view: while in separation, the observations are grouped according to the target variable, in sufficiency they are grouped according to the predicted value.

## Incompatibilities between metrics

- If the target variable is binary and there is a group imbalance, then **independence** and **separation** are incompatible.
- If there is a group imbalance, **sufficiency** and **independence** are also incompatible.
- Separation and sufficiency can both hold either when there is an imbalance in sensitive groups.

Chouldechova (2017) showed that, if the true recidivism rate is different for black and white people, then Predictive Parity and Equality of Odds cannot both hold, thus implying that a reflection on which of the two (in general of the many) notions is more important to be pursued in that specific case must be carefully considered.

