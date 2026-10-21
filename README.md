# Route-Resilience
Extracts occlusion-robust road networks using a context-aware Transformer. It mathematically heals broken pixel masks and translates them into routable vector graphs to simulate urban bottlenecks, infrastructure collapse, and disaster resilience.


OVERVIEW 

Standard satellite road extraction often fails in dense urban and forested environments, producing fragmented pixel masks that are useless for real-world navigation or disaster response. Developed for ISRO PS-4, Route Resilience is an end-to-end deep learning and graph-theoretic pipeline designed to solve this "spectral blindness."
Our framework uses a context-aware MiT-B2 Transformer to accurately extract road networks hidden beneath tree canopies and cloud shadows. It then mathematically heals disconnected road segments using a Disjoint Set Union (DSU) bridging algorithm, translating raw pixel predictions into a continuous, routable vector graph. Finally, the system runs automated stress tests—such as urban flood rerouting and centrality ablation—to identify critical intersection bottlenecks and quantify the overall resilience of the infrastructure.


PROBLEM STATEMENT

Spectral Blindness & Occlusion
Topological Disconnection
Lack of Actionable Resilience Modeling
Geospatial Processing Overhead


PIPELINE

Data Ingestion: Rapidly ingests lightweight .jpg imagery (DeepGlobe dataset) and applies synthetic urban occlusions like tree shadows and cloud cover 
-->Context-Aware Segmentation: Processes tiles through a MiT-B2 Transformer to logically infer continuous road features hidden beneath visual obstacles
-->Topological Optimization: Trains using a hybrid clDice loss suite that penalizes centerline disconnections rather than simple area mismatches
-->Dynamic Calibration: Applies 4-fold Test-Time Augmentation (TTA) to auto-tune the optimal probability threshold for maximum accuracy
-->Morphological Thinning: Reduces the raw binary road predictions into 1-pixel wide skeletonized centerlines
-->DSU-MST Healing: Automatically bridges disconnected road gaps using a Disjoint Set Union algorithm based on Euclidean proximity and angular collinearity
-->Vector Translation: Assembles the mathematically healed centerlines into a functional, routable NetworkX spatial graph.
-->Bottleneck Identification: Computes Betweenness Centrality across the graph to map critical "Gatekeeper" intersections
-->Disaster Stress Testing: Simulates localized infrastructure failures (e.g., urban flooding) to calculate detour factors and a global 
-->Resilience Index ($R$).Automated Export: Headlessly generates and saves the cleaned masks, .graphml routing vectors, analytical JSON reports, and diagnostic dashboards.


MODELS & LIBRARIES USED

MiT-B2(Mix Transformer B2 Backbone) , CBAM (Convolutional Block Attention Module) , Differential clDice , pytorch , openCV , scikit & scipy , NetworkX , numpy , matplotlib , pandas.


KEY FINDINGS 

Significant Topological Healing Gains: The collinear bearing-constrained Disjoint Set Union (DSU-MST) algorithm successfully bridged shadow-induced road breaks up to 55 pixels wide, achieving up to a +90.3% increase in the Largest Connected Component (LCC) on blind test tiles ; automated flood inundation simulations demonstrated detour penalties inflating travel distances up to 1.60x when high-centrality intersections were submerged ; 

RESULTS

Strict val iou : 0.7093 , relaxed val iou : 0.93  , strict test iou : 0.7077, relaxed test iou : 0.9190 .


