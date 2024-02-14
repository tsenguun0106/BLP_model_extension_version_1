# BLP_model_extension_version_1
Here, I implement practical and novel extensions to the BLP model. BLP model is very popular in Econometrics. However, it is not used widely in industry due to some limitations regarding this model. In this repo, I will implement some novel and practical extensions to the original BLP model. 

## Core methodology

$U_{ij} = \alpha p_j + \gamma b_j + \varepsilon_j + \epsilon_{ij}$

In the above equation, I demonstrate the household utility function for product $j$ and household $i$. Here, $p$ denotes the price, $b$ denotes the product attributes, $\varepsilon_j$ denotes the unobserved product fixed effect such as branding effect, and $\epsilon_{ij}$ denotes the random shock specific to product $j$ and household $i$. 

$\epsilon_{ij}=\zeta_{ig} + (1 - \sigma_g) \upsilon_{ij}$

The random shock, $\epsilon_{ij}$, follows the above data-generating process as an assumption. $\zeta_{ig}$ represents the product group $g$ specific shock to the product $i$, and $\sigma_g$ indicates the product group g (to which, the product $i$ belongs) nesting parameter or competitiveness degree of product group g. The higher the value of $\sigma_g$ is, the more competitive products in the product group $g$ are against each other. Moreover, we assume that $ \upsilon_{ij}$ follows the Type-1 extreme value distribution. 

Using the above two equations, we can derive the following equations:

$I_g = (1- \sigma_g) \ln \Big( \sum_{j \in J_g} \Big( \frac{ \alpha p_j + \gamma b_j + \varepsilon_j }{1-\sigma_g} \Big) \Big) $

$I = \ln \\sum_{g \in G} \exp ( I_g )$

Using equations for $I_g$ and $I$, we can derive the following product share formulas:

$s_g = \frac{\exp(I_g)}{\exp(I)}$

Here, $s_g$ denotes the total market share of product group $g$. 

$s_{j/g} = \frac{\exp \Big( \frac{ \alpha p_j + \gamma b_j + \varepsilon_j }{1-\sigma_g} \Big) }{\exp \Big( \frac{I_g}{1 - \sigma_g} \Big)}$

Here, $s_{j/g}$ denotes the share of product $j$ in the product group $g$. 

$s_j = s_{j/g} s_g$

Here, $s_j$ illustrates the market share of product $j$. 

### Price elasticity $\eta_{jk}$:

Equation 1: $\frac{\alpha}{1 - \sigma_g} p_k ( 1 - ( 1 - \sigma_g ) s_k - \sigma_g s_{k/g} )$ if $j = k$ and $j, k \in g$

Equation 1 demonstrates the self-price elasticity of product $j$. When $\alpha$ is larger, the self-price elasticity magnitude will be bigger. 

Equation 2: $\frac{-\alpha}{1 - \sigma_g} p_k ( ( 1 - \sigma_g ) s_k + \sigma_g s_{k/g} )$ if $j \neq k$ and $j, k \in g$

Equation 2 expresses the cross-price elasticity within the same product group. 
Since $s_{k/g}$ is greater than $s_k$, the larger the value of $\sigma_g$, the greater the magnitude of cross-price elasticity within the same product group. 

Equation 3: $-\alpha p_k s_k$ if $j \neq k$, $j \in g, k \in h$, and $g \neq h$

Equation 3 indicates the cross-price elasticity between products from different product groups. 

### Product from the segment with a low competitiveness degree (self-price elasticity): 

From the above equations, we can see that the product group competitiveness parameter $\sigma_g$ is critical for determining the magnitude of price elasticity. In the below graph, we can observe that when $\sigma_g$ is lower or closer to 0, the self-price elasticity is near-linear. 

<img src="https://github.com/tsenguun0106/BLP_model_extension_version_1/assets/60633314/f1834e0c-126c-4426-8a85-de53cb16549d" width="450px">

### Product from the segment with a high competitiveness degree (self-price elasticity): 

The following graph indicates how the self-price elasticity looks when the product group competitiveness parameter $\sigma_g$ is large or close to 1. When the price value is low, the self-price elasticity will be near flat and close to 0. What does it mean? Essentially it means that when a certain product's price is relatively lower compared with the prices of other products in the same product group, this product will not lose much share even if you increase its prices slightly. However, once the price of this product reaches the certain point (closer to the average of prices of products in the same product group), the self-price elasticity becomes very steep. This means that it is losing its comparative price advantage over other products in the same product group. And even if you increase its price by a small amount, this product can lose a lot of share to other products in the same product group. 

<img src="https://github.com/tsenguun0106/BLP_model_extension_version_1/assets/60633314/5cfe956b-1653-444e-b434-babf9d5d1916" width="450px">

### Product from the segment with a low competitiveness degree (cross-price elasticity): 

The below graph expresses the cross-price elasticity magnitude when the product group competitiveness degree is low. We can see that the magnitude of cross-price elasticity is very small and almost zero. This means that when the product group's competitiveness degree is lower, the price competition between products in that product group is less intense, and each product owns its specific customer base or market share with more confidence. 

<img src="https://github.com/tsenguun0106/BLP_model_extension_version_1/assets/60633314/36b1934d-4c2d-4021-bad5-98fd341218dc" width="450px">

### Product from the segment with a high competitiveness degree (cross-price elasticity): 

The following graph illustrates the cross-price elasticity magnitude when the product group competitiveness degree is large. We can see that the magnitude of cross-price elasticity is significant. This means that when the product group's competitiveness degree is greater, the price competition between products in that product group is very intense, and a product in this group can lose a lot of share by increasing the price slightly. 

<img src="https://github.com/tsenguun0106/BLP_model_extension_version_1/assets/60633314/0b416d29-0640-4556-be59-d617ef743e3a" width="450px">


## Extension idea: 

1. Product clustering

2. Heterogenous price effect across product groups

3. Heterogenous product group's competitiveness degree $\sigma_g$



