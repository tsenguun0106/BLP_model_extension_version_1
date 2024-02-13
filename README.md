# BLP_model_extension_version_1
Here, I implement practical and novel extensions to the BLP model. BLP model is very popular in Econometrics. However, it is not used widely in industry due to some limitations regarding this model. In this repo, I will implement some novel and practical extensions to the original BLP model. 

## 1. Extension idea 1: 

$U_{ij} = \alpha p_j + \gamma b_j + \varepsilon_j + \epsilon_{ij}$

$\epsilon_{ij}=\zeta_{ig} + (1 - \sigma_g) \upsilon_{ij}$

$I_g = (1- \sigma_g) \ln \Big( \sum_{j \in J_g} \Big( \frac{ \alpha p_j + \gamma b_j + \varepsilon_j }{1-\sigma_g} \Big) \Big) $

$I = \ln \\sum_{g \in G} \exp ( I_g )$

$s_g = \frac{\exp(I_g)}{\exp(I)}$

$s_{j/g} = \frac{\exp \Big( \frac{ \alpha p_j + \gamma b_j + \varepsilon_j }{1-\sigma_g} \Big) }{\exp \Big( \frac{I_g}{1 - \sigma_g} \Big)}$


### Price elasticity $\eta_{jk}$:

$\frac{\alpha}{1 - \sigma_g} p_k ( 1 - ( 1 - \sigma_g ) s_k - \sigma_g s_{k/g} )$ if $j = k$ and $j, k \in g$

$\frac{-\alpha}{1 - \sigma_g} p_k ( ( 1 - \sigma_g ) s_k + \sigma_g s_{k/g} )$ if $j \neq k$ and $j, k \in g$

$-\alpha p_k s_k$ if $j \neq k$, $j \in g, k \in h$, and $g \neq h$




### Product from the segment with a low competitiveness degree (self-price elasticity): 

<img src="https://github.com/tsenguun0106/BLP_model_extension_version_1/assets/60633314/f1834e0c-126c-4426-8a85-de53cb16549d" width="450px">

### Product from the segment with a high competitiveness degree (cross-price elasticity): 

<img src="https://github.com/tsenguun0106/BLP_model_extension_version_1/assets/60633314/5cfe956b-1653-444e-b434-babf9d5d1916" width="450px">

### Product from the segment with a low competitiveness degree (cross-price elasticity): 

<img src="https://github.com/tsenguun0106/BLP_model_extension_version_1/assets/60633314/36b1934d-4c2d-4021-bad5-98fd341218dc" width="450px">

### Product from the segment with a high competitiveness degree (cross-price elasticity): 

<img src="https://github.com/tsenguun0106/BLP_model_extension_version_1/assets/60633314/0b416d29-0640-4556-be59-d617ef743e3a" width="450px">


