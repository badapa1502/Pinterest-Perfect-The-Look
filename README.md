# Pinterest-Perfect-The-Look

## Complete the Look: Scene-based Complementary Product Recommendation
The objective is to recommend visually compatible products based on real-world scene images rather than solely the product images. This involves a comparison of both global style and local relevant regions within the scene.

## Methodology
- Firstly, we consider the global style feature vector, which is extracted from the final layers of convolutional / recurrent neural networks which we apply on a scene image. This vector is then transformed to a lower-dimensional embedding (f_s) using a certain encoding mechanism (two-layer feedforward neural network, autoencoders), and this global embeddings represents the overall style of the scene. Similarly, a global feature vector is obtained for the product and transformed into an embedding f_p.
- Global compatibility is then measured by computing the L2 norm between the two embeddings (scene-level style embedding f_s with the product’s global style embedding f_p).
- For capturing a more refined, local, region-specific style, feature maps will be extracted from the intermediate convolutional layers; containing information about different spatial areas of the scene. These local feature maps are then converted into local style embeddings f_i.
- After creating the local style embeddings, we will use category-aware attention mechanism to determine which local regions are most relevant for recommending a product of a particular category. This mechanism assigns weights a_i to each region based on its relevance to the product category. The weights are determined based on the proximity of the local region to the product category embedding.
- Local compatibility is computed as the weighted sum of the L2 norm between each region's embedding f_i and product embedding f_p, with the weights being the attention weights calculated above.
- The overall hybrid compatibility is then defined as a combination of both global and local distances; allows the model to consider both the overall style of the scene and the compatibility of specific regions with the product being recommended. 

## Dataset
- Link to dataset: https://github.com/kang205/STL-Dataset
- Basic Statistics: Scenes: 47,739, Products: 38,111, Scene-Product Pairs: 93,274

Pinterest Shop The Look (STL) datasets include STL-Fashion and STL-Home. STL-Fashion is a fashion-focused dataset that consists of real-world scene photographs (such as street photography and selfies) combined with catalog-style product images that are labelled with product category labels and bounding boxes. STL-Home takes this concept to the interior design area, offering home decor scenes as well as product photos like rugs, lamps, and furniture. The authors make a subset of the datasets and preprocessing scripts available on GitHub to help with experimentation and model development, even if the complete datasets are proprietary and not publicly accessible. We are still looking into what dataset size would be computationally feasible to work with.
