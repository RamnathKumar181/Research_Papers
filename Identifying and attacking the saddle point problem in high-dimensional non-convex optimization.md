# Identifying and attacking the saddle point problem in high-dimensional non-convex optimization

The paper highlights a very important view on a well perceived problem of non-convex optimization. They suggest that, saddle points cause more issues than local optimum and propose a new second-order optimization to address the same. Just to freshen up your memory, a saddle point is a point where the slope is 0, but is not a local extremum. This occurs when the neighborhood is not entirely on any side of the tangent space at that point. Furthermore, the ratio of the number of saddle points to local minima increases exponentially with the dimensionality N. Unfortunately, the current gradient method prioritizes reaching the local minima, and does not rapidly descend plateaus. Luckily, newton methods can descend rapidly in plateaus but are attracted towards saddle points. Hence, the motivation to attacking the saddle points.

## The prevalence of saddle points in high dimensions

Intuitively, in high dimensions, the chance that all the directions around a critical point lead upward (positive curvature) is exponentially small. There are further mathematical proofs to support the same claim along with a few experiments. Unfortunately, some of these proofs were too complex for me to grasp. Please refer to the paper if you are interested.

## Dynamics of optimization algorithms near saddle points

Given the prevalence of saddle points, it is important to understand how various optimization algorithms behave near them.

### Gradient Descent Approach

This method always points in the right direction of the saddle point. The drawback of this algorithm is the size of step it takes. Furthermore, once the algorithm reaches closer to the saddle point, there is no escape as the gradient becomes closer to zero, as the curve becomes a plateau. The proof of the gradient descent approach is quite straight forward. The goal is to prove that the error with the updated weights is lower than the error before. A simple taylor expansion is enough to solve this proof.

### Newton Approach

This method solves the issue of step size by rescaling the gradients in each direction. However, it may lead to a movement in the wrong direction, when the double differentiation of f(x) is negative. The proof of the Newton approach is by trying to minimize f(x+t), and applying the taylor expansion. Its a very simple proof. Unfortunately, there is no guarantee, that it will reach a minima as mentioned earlier.

### Trust region Approach

The idea in this approach is to make sure that the denominator in the Newton approach is always greater than zero. This ensures that the model will always move in the right direction. Unfortunately, if the damping coefficient required is very high, we will again only move in small steps. Another type is when we ignore the negative curvatures. However, such models cannot escape saddle points, as they completely ignore negative curvature.

## Attacking the saddle point Problem

A possible simple heuristic solution is to take the absolute value of the denominator. This achieves the same rescaling as newton method while preserving the direction. However, there is no justification to do the same.
Instead, the authors come up with a new approach called the saddle free newton method. This is an extension of the trust region approach with 2 important changes. We try to minimize the taylor expansion for first-order and not the second order. Hence, the information of the curvature needs to come from the distance measure. The exact math is complicated. The final result is that we need to take a step of -f|H|^-1.
Unlike gradient descent, it can move further
(less) in the directions of low (high) curvature. It is identical to the Newton method when the Hessian is positive definite, but unlike the Newton method, it can escape saddle points. Furthermore, unlike gradient descent, the escape is rapid even along directions of weak negative curvature.

## Paper link

https://arxiv.org/pdf/1406.2572.pdf
