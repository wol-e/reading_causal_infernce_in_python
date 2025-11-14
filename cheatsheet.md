# Causal Inference Cherat Sheet

A collection of critical definitions, terms, ideas, concepts based on the book "Causl Inference in Python" by Matheus Focure. 

# Definitions

**_endogenous_**: Variables that are explicitly modeled

**_exogenous_**: Variables that are not explicitly modeled, basically part of the error term

For example a common notation might be like $$Y = T(x_1, u_1) + f(x_2, u_2)$$ where $u_i$ could be exogenous variables not explicitly modeled and $x_i$ are endogenous variables for which we have data available and can model them.

**_Potential Outcomes_**: Given individula outcomes $Y_i$ the potential outcomes $Y_{ti} = Y(t)_i$ are the potential outcomes given $T = t$. The observed outcome $Y(T(Y_i))_i$ is the _factual_ outcome while any potential outcome that's not observed is _counterfactual_. The _fundamental problem of causal inference_ is that ony one potential outcome can ever be observed for a given unit. 

**_Average Treatment Effect ATE_**: Given a binary tratment varaible $$\mathrm{ATE} = \mathrm E(Y_1 - Y_0) = \mathrm E(Y | do(T = 1)) - \mathrm E(Y | do(T = 0)).$$ The ATE is the average difference in the outcome when all units are treated versus all units are not treaated. Due to the fundamental problem in causal inference it can never be observed or calculated directly and one of causal inferences main opbjectives is estimating it.

**_Average Treatment Effect of the Treated ATT_**: $$\mathrm{ATT} = \mathrm E(Y_1 - Y_0 | T = 1),$$ the average treatment effect only for the treated units. Depending on selection bias, this can be very different from the ATE. Answers for example the question "What was the average uplift from the marketing campaign we ran in city XY?"

**_Conditional Treatment Effect CATE_**: $$CATE = \mathrm E(Y_1 - Y_0 | X = x)$$ where $X$ is some feature of the treated units, e.g. age. Relevant for deeper understanding effects, e.g. for personalization. ATT is a psecial case of CATE.  

For non binary treatments one can work with incremental treatment effects.

**_Bias_**: Bias is what makes correlation different from causation. $$Bias = \mathrm E(\hat \beta - \beta)$$ where $\hat \beta$ is an estimator for the parameter $\beta$ you estimate. Bias helps to understand why the ATE is (generally) different from the difference of means between treated and untreated units:
$$\mathrm E(Y|T = 1) - \mathrm E (Y|T=0) = \mathrm E(Y_1 - Y_0 | T = 1) + (\mathrm E(Y_0 | T = 1) - \mathrm E(Y_0 | T = 0)) = ATT - Bias$$
Note that the left hand side of the equation can be calculated from observed data, while the two terms on the right hand side can't. However, if for some reason we know $Bias = 0$ then the left hand side yields an estimator for the $ATT$. Additionally, if treated and untreated units are interchangeable (i.e. statistically the same) then ATT = ATE so we obtain an unbiased estimator for the ATE.

**_Independence assumption_**: Independence means the treatment assignment is independent of the _potential_ outcome: $$(Y_0, Y_1) \bot T$$ This implies $$\mathrm E(Y_i | T) = \mathrm E(Y_i).$$

**_Identification_**: Identification is the process of making assumptions on the causality and answering whether the causal effect is theoretically recoverable from the observed data under these assumptions. It precedes and is separate from estimation.
