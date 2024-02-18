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

The following graph indicates how the self-price elasticity looks when the product group competitiveness parameter $\sigma_g$ is large or close to 1. When the price value is low, the self-price elasticity will be near flat and close to 0. What does it mean? Essentially it means that when a certain product's price is relatively lower compared with the prices of other products in the same product group, this product will not lose much share even if you increase its prices slightly. However, once the price of this product reaches a certain point (closer to the average of prices of products in the same product group), the self-price elasticity becomes very steep. This means that it is losing its comparative price advantage over other products in the same product group. And even if you increase its price by a small amount, this product can lose a lot of share to other products in the same product group. 

<img src="https://github.com/tsenguun0106/BLP_model_extension_version_1/assets/60633314/5cfe956b-1653-444e-b434-babf9d5d1916" width="450px">

### Product from the segment with a low competitiveness degree (cross-price elasticity): 

The below graph expresses the cross-price elasticity magnitude when the product group competitiveness degree is low. We can see that the magnitude of cross-price elasticity is very small and almost zero. This means that when the product group's competitiveness degree is lower, the price competition between products in that product group is less intense, and each product owns its specific customer base or market share with more confidence. 

<img src="https://github.com/tsenguun0106/BLP_model_extension_version_1/assets/60633314/36b1934d-4c2d-4021-bad5-98fd341218dc" width="450px">

### Product from the segment with a high competitiveness degree (cross-price elasticity): 

The following graph illustrates the cross-price elasticity magnitude when the product group competitiveness degree is large. We can see that the magnitude of cross-price elasticity is significant. This means that when the product group's competitiveness degree is greater, the price competition between products in that product group is very intense, and a product in this group can lose a lot of share by increasing the price slightly. 

<img src="https://github.com/tsenguun0106/BLP_model_extension_version_1/assets/60633314/0b416d29-0640-4556-be59-d617ef743e3a" width="450px">


## Extension idea: 

1. Product clustering
We can create product clusters or product groups based on its fundamental attributes like taste profile, packaging info, price range, branding investment, etc. The below graph indicates one example or product clustering based on its attributes. 
<img src="https://github.com/tsenguun0106/BLP_model_extension_version_1/assets/60633314/00b89e26-d334-4736-b518-d1239004bf12" width="450px">
These product clusters or groups based on the machine learning methodology can be used to define the product groups in the BLP model. Hence, we would not need to depend on categorical variables to specify the product groups in the BLP application. In some cases, these ML model-based clusters or product groups can capture the true product similarities better and could help us to find more meaningful price and cannibalization effects. 

2. Heterogenous price effect across product groups
The original BLP model assumes one homogeneous price elasticity across different product groups. However. here I introduce the heterogeneous price elasticity across different product groups. This extension can model the true data-generating process more realistically since in reality, different product groups can have different price elasticities. 
How I estimate this heterogeneity in price elasticity by interacting the product group-specific dummy variable with the instrument variables for the endogenous price variable. The main assumptions will be that the instrument variables should vary sufficiently for the specific product group and the price variable for the specific product group should have enough variation in its movements. 

3. Heterogenous product group's competitiveness degree $\sigma_g$
Moreover, the original BLP model assumes one homogeneous competitiveness degree parameter across different product groups even though in the real world, each product group can have different levels of competitiveness degree. I also estimate this heterogeneity by interacting the product group-specific dummy variable with the nest size variable (the instrument variable for estimating the competitiveness degree parameter). The competitiveness degree parameter truly captures how competitive products are against each other in the specific product group. By estimating this heterogeneous competitiveness degree parameter, we can evaluate the price cross-elasticity and cannibalization effect more realistically. 

## Estimation example on the simulated data

Here, I simulated the synthetic data where:

- The true price effect parameter for product group 1 is -2.0 (estimated value is -1.9957).
- The true price effect parameter for product group 2 is -1.85 (estimated value is -1.8339).
- The true price effect parameter for product group 3 is -1.7 (estimated value is -1.6994).
- The true price effect parameter for product group 4 is -1.55 (estimated value is -1.5474).
- The true price effect parameter for product group 5 is -1.4 (estimated value is -1.4096).
- The true price effect parameter for product group 6 is -1.25 (estimated value is -1.2613).
- The true price effect parameter for product group 7 is -1.1 (estimated value is -1.0742).
- The true price effect parameter for product group 8 is -0.95 (estimated value is -0.9220).
- The true price effect parameter for product group 9 is -0.8 (estimated value is -0.7105).

- The true competitiveness degree parameter for group 1 is 0.1 (estimated value is 0.1009).
- The true competitiveness degree parameter for group 2 is 0.2 (estimated value is 0.2035).
- The true competitiveness degree parameter for group 3 is 0.3 (estimated value is 0.3003).
- The true competitiveness degree parameter for group 4 is 0.4 (estimated value is 0.4006).
- The true competitiveness degree parameter for group 5 is 0.5 (estimated value is 0.4980).
- The true competitiveness degree parameter for group 6 is 0.6 (estimated value is 0.5980).
- The true competitiveness degree parameter for group 7 is 0.7 (estimated value is 0.7054).
- The true competitiveness degree parameter for group 8 is 0.8 (estimated value is 0.8053).
- The true competitiveness degree parameter for group 9 is 0.9 (estimated value is 0.9120).


<img src="https://github.com/tsenguun0106/BLP_model_extension_version_1/assets/60633314/73663aeb-d7c4-40ab-93a5-565e35d31261" width="450px">

We can see that all true parameters were estimated very accurately with the suggested estimation methodology. 

# Conclusion

Here, I briefly introduced a few important extensions to the original BLP model and how these extensions can be estimated effectively. These extensions can have truly tremendous impacts on the real industry application and can help the business to strategize its pricing and product portfolio decisions efficiently. 


