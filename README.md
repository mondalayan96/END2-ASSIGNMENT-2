# END2-ASSIGNMENT-2

![](RackMultipart20210513-4-6foywv_html_84a73c66ed52ec91.png)

**For Forward Propagation:**

Inputs: i1, i2

Activation function: Softmax.

Actual Output = t1, t2

1st Layer:

1. h1 = w1\*i1 + w2\*i2
2. a\_h1 = σ(h1) = 1/(1+e-h1)
3. h2 = w3\*i1 + w2\*i2
4. a\_h2 = σ(h2) = 1/(1+e-h2)

2nd Layer:

1. 1 = w5\*a\_h1 + w6\*a\_h2
2. a\_o1 = σ(a\_o1) = 1/(1+e-a\_o1)
3. 2 = w7\*a\_h1 + w8\*a\_h2
4. a\_o2 = σ(a\_o2) = 1/(1+e-a\_o2)

Error:

1. Error(E1) = 0.5\*(t1-a\_o1)2
2. Error(E2) = 0.5\*(t1-a\_o2)2
3. Total Error(E\_total) = E1 + E2

**Backward Propagation:**

In backward propagation, we start from the output layer and propagate backwards, updating weights and biases for each layer. We adjust the weights and biases throughout the network, so that we get the desired output in the output layer. To update each node after every iteration, we need to calculate the error generated with respect to that node which is calculated with the help of the gradient. After each iteration of the epoch we observe that the total error is decreasing.

To update w5 we need to calculate ∂E\_Total/ ∂w5

Thus, ∂E\_Total/ ∂w5 = ∂(E1+E2) / ∂w5 As, E\_total = E1 + E2

= ∂E1 / ∂w5 + ∂E2 / ∂w5 = ∂E1/ ∂w5 (As w5 is not involved in the updation of E2 in forward propagation)

By chain rule we can write,

∂(E1+E2)/ ∂w5 = ∂E1/ ∂w5 = ∂E1/∂a\_o1 \* ∂a\_o1/∂w5

= ∂E1/∂a\_o1 \* ∂a\_o1/∂o1 \* ∂o1/∂w5 (As w5 is involved in updation of o1, which in turn affects the updation of a\_o1, which produces the output E1 )

= ∂( 0.5\*(t1-a\_o1)2) / ∂a\_o1 \* ∂σ(o1)/∂o1 \* ∂o1/∂w5

= (a\_o1 - t1) \* a\_o1\*(1 - a\_o1) \* ∂ (w5\*a\_h1 + w6\*a\_h2)/ ∂w5

= (a\_o1 - t1) \* a\_o1\*(1 - a\_o1) \* a\_h1

Thus, **∂E\_Total/∂w5 = (a\_o1 - t1) \* a\_o1\*(1 - a\_o1) \* a\_h1**

- **w5 = w5 - learning\_rate \*(∂E\_Total/∂w5)**
- **w5 = w5 - ղ \* (a\_o1 - t1) \* a\_o1\*(1 - a\_o1) \* a\_h1**

1. To update w6 we need to calculate ∂E\_Total/ ∂w6

Thus, ∂E\_Total/ ∂w6 = ∂(E1+E2) / ∂w6 As, E\_total = E1 + E2

= ∂E1 / ∂w6 + ∂E2 / ∂w6 = ∂E1/ ∂w6 (As w6 does not involve in updating of E2 in forward propagation)

By chain rule we can write,

∂(E1+E2)/ ∂w6 = ∂E1/ ∂w6 = ∂E1/∂a\_o1 \* ∂a\_o1/∂w6

= ∂E1/∂a\_o1 \* ∂a\_o1/∂o1 \* ∂o1/∂w6 (As w6 is involved in updation of o1, which in turn affects the updation of a\_o1, which produces the output E1)

= ∂( 0.5\*(t1-a\_o1)2) / ∂a\_o1 \* ∂σ(o1)/∂o1 \* ∂o1/∂w6

= (a\_o1 - t1) \* a\_o1\*(1 - a\_o1) \* ∂ (w5\*a\_h1 + w6\*a\_h2)/ ∂w6

= (a\_o1 - t1) \* a\_o1\*(1 - a\_o1) \* a\_h2

Thus, **∂E\_Total/∂w6 = (a\_o1 - t1) \* a\_o1\*(1 - a\_o1) \* a\_h2**

- **w6 = w6 - learning\_rate \*(∂E\_Total/∂w6)**
- **w6 = w6 - ղ \* (a\_o1 - t1) \* a\_o1\*(1 - a\_o1) \* a\_h2**

1. To update w7 we need to calculate ∂E\_Total/ ∂w7

Thus, ∂E\_Total/ ∂w7 = ∂(E1+E2) / ∂w7 As, E\_total = E1 + E2

= ∂E1 / ∂w7 + ∂E2 / ∂w7 = ∂E2/ ∂w7 (As w7 does not involve in updating of E1 in forward propagation)

By chain rule we can write,

∂(E1+E2)/ ∂w7 = ∂E2/ ∂w7 = ∂E2/∂a\_o2 \* ∂a\_o2/∂w7

= ∂E2/∂a\_o2 \* ∂a\_o2/∂o2 \* ∂o2/∂w7 (As w7 is involved in updation of o2, which in turn affects the updation of a\_o2, which produces the output E2)

= ∂( 0.5\*(t2-a\_o2)2) / ∂a\_o2 \* ∂σ(o2)/∂o2 \* ∂o2/∂w7

= (a\_o2 – t2) \* a\_o2\*(1 - a\_o2) \* ∂ (w7\*a\_h1 + w8\*a\_h2)/ ∂w7

= (a\_o2 – t2) \* a\_o2\*(1 - a\_o2) \* a\_h1

Thus, **∂E\_Total/∂w7 = (a\_o2 – t2) \* a\_o2\*(1 - a\_o2) \* a\_h1**

- **w7 = w7 - learning\_rate \*(∂E\_Total/∂w7)**
- **w7 = w7 - ղ \* (a\_o2 – t2) \* a\_o2\*(1 - a\_o2) \* a\_h1**

1. To update w8 we need to calculate ∂E\_Total/ ∂w8

Thus, ∂E\_Total/ ∂w8 = ∂(E1+E2) / ∂w8 As, E\_total = E1 + E2

= ∂E1 / ∂w8 + ∂E2 / ∂w8 = ∂E2/ ∂w8 (As w8 does not involve in updating of E1 in forward propagation)

By chain rule we can write,

∂(E1+E2)/ ∂w8 = ∂E2/ ∂w8 = ∂E2/∂a\_o2 \* ∂a\_o2/∂w8

= ∂E2/∂a\_o2 \* ∂a\_o2/∂o2 \* ∂o2/∂w8 (As w8 is involved in updation of o2, which in turn affects the updation of a\_o2, which produces the output E2)

= ∂( 0.5\*(t2-a\_o2)2) / ∂a\_o2 \* ∂σ(o2)/∂o2 \* ∂o2/∂w8

= (a\_o2 – t2) \* a\_o2\*(1 - a\_o2) \* ∂ (w7\*a\_h1 + w8\*a\_h2)/ ∂w8

= (a\_o2 – t2) \* a\_o2\*(1 - a\_o2) \* a\_h2

Thus, **∂E\_Total/∂w8 = (a\_o2 – t2) \* a\_o2\*(1 - a\_o2) \* a\_h2**

- **w8 = w8 - learning\_rate \*(∂E\_Total/∂w7)**
- **w8 = w8 - ղ \* (a\_o2 – t2) \* a\_o2\*(1 - a\_o2) \* a\_h2**

1. To update w4 we need to calculate ∂E\_Total/ ∂w4

By chain rule we can write,

∂(E\_Total) / ∂w4 = ∂E\_Total/∂a\_h2 \* ∂a\_h2/∂w4

= ∂E\_Total/∂a\_o2 \* ∂a\_o2/∂o2 \* ∂o2/∂a\_h2 \* ∂a\_h2/∂h2 \* ∂h2/∂w4 (As w4 is involved in updation of h2, which is involved in the updation of a\_h2,

which is involved in updation of o1 and o2, which is involved in updation of

a\_o1 and a\_o2 respectively, which in turn affects updation of E\_Total)

= (a\_o2-t2) \* a\_o2\*(1-a\_o2) \* w8 + (a\_o1-t1) \* a\_o1\*(1-a\_o1) \* w6 \*

a\_h2 \* (1-a\_h2) \* i2

Thus, **∂E\_Total / ∂w4 = (a\_o2-t2) \* a\_o2\*(1-a\_o2) \* w8 + (a\_o1-t1) \* a\_o1\*(1-a\_o1) \* w6 \***

**a\_h2 \* (1-a\_h2) \* i2**

- **w4 = w4 – learning\_rate \* (∂E\_Total/∂w4)**
- **w4 = w4 – ղ \* (a\_o2-t2) \* a\_o2\*(1-a\_o2) \* w8 + (a\_o1-t1) \* a\_o1\*(1-a\_o1) \* w6**

**\* a\_h2 \* (1-a\_h2) \* i2**

1. To update w3 we need to calculate ∂E\_Total/ ∂w3

By chain rule we can write,

∂(E\_Total) / ∂w3 = ∂E\_Total/∂a\_h2 \* ∂a\_h2/∂w3

= ∂E\_Total/∂a\_o2 \* ∂a\_o2/∂o2 \* ∂o2/∂a\_h2 \* ∂a\_h2/∂h2 \* ∂h2/∂w3 (As w3 is involved in updation of h2, which is involved in the updation of a\_h2,

which is involved in updation of o1 and o2, which is involved in updation of

a \_o1 and a\_o2 respectively, which in turn affects updation of E\_Total)

= (a\_o2-t2) \* a\_o2\*(1-a\_o2) \* w8 + (a\_o1-t1) \* a\_o1\*(1-a\_o1) \* w6 \*

a\_h2 \* (1-a\_h2) \* i1

Thus, **∂E\_Total / ∂w3= (a\_o2-t2) \* a\_o2\*(1-a\_o2) \* w8 + (a\_o1-t1) \* a\_o1\*(1-a\_o1) \* w6 \***

**a\_h2 \* (1-a\_h2) \* i1**

- **w3 = w3 – learning\_rate \* (∂E\_Total/∂w3)**
- **w3 = w3– ղ \* (a\_o2-t2) \* a\_o2\*(1-a\_o2) \* w8 + (a\_o1-t1) \* a\_o1\*(1-a\_o1) \* w6**

**\* a\_h2 \* (1-a\_h2) \* i1**

1. To update w2 we need to calculate ∂E\_Total/ ∂w2

By chain rule we can write,

∂(E\_Total) / ∂w2 = ∂E\_Total/∂a\_h1 \* ∂a\_h1/∂w2

= ∂E\_Total/∂a\_o1 \* ∂a\_o1/∂o1\* ∂o1/∂a\_h1 \* ∂a\_h1/∂h1 \* ∂h1/∂w1 (As w2 is involved in updation of h1, which is involved in the updation of a\_h1,

which is involved in updation of o1 and o2 respectively , which is involved in updation of

a\_o1 and a\_o2, which in turn affects updation of E\_Total)

= (a\_o1-t1) \* a\_o1\*(1-a\_o1) \* w5 + (a\_o2-t2) \* a\_o2\*(1-a\_o2) \* w7 \*

a\_h1 \* (1-a\_h1) \* i2

Thus, **∂E\_Total / ∂w2= (a\_o1-t1) \* a\_o1\*(1-a\_o1) \* w5 + (a\_o2-t2) \* a\_o2\*(1-a\_o2) \* w7****\***

**a\_h1 \* (1-a\_h1) \* i2**

- **w2 = w2 – learning\_rate \* (∂E\_Total/∂w2)**
- **w2= w2– ղ \* (a\_o1-t1) \* a\_o1\*(1-a\_o1) \* w5 + (a\_o2-t2) \* a\_o2\*(1-a\_o2) \* w7 \***

**\* a\_h1\* (1-a\_h1) \* i2**

1. To update w1 we need to calculate ∂E\_Total/ ∂w1

By chain rule we can write,

∂(E\_Total) / ∂w1 = ∂E\_Total/∂a\_h1 \* ∂a\_h1/∂w1

= ∂E\_Total/∂a\_o1 \* ∂a\_o1/∂o1\* ∂o1/∂a\_h1 \* ∂a\_h1/∂h1 \* ∂h1/∂w1 (As w1is involved in updation of h1, which is involved in the updation of a\_h1,

which is involved in updation of o1 and o2, which is involved in updation of

a\_o1 and a\_02 respectively, which in turn affects updation of E\_Total)

= (a\_o1-t1) \* a\_o1\*(1-a\_o1) \* w5 + (a\_o2-t2) \* a\_o2\*(1-a\_o2) \* w7 \*

a\_h1 \* (1-a\_h1) \* i1

Thus, **∂E\_Total / ∂w1= (a\_o1-t1) \* a\_o1\*(1-a\_o1) \* w5 + (a\_o2-t2) \* a\_o2\*(1-a\_o2) \* w7****\***

**a\_h1 \* (1-a\_h1) \* i1**

- **w1 = w1 – learning\_rate \* (∂E\_Total/∂w1)**
- **w1= w1– ղ \* (a\_o1-t1) \* a\_o1\*(1-a\_o1) \* w5 + (a\_o2-t2) \* a\_o2\*(1-a\_o2) \* w7 \***

**\* a\_h1\* (1-a\_h1) \* i1**