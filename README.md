# Project 1 - Fitness Prediction in the Escherichia coli Gene Regulatory Network

## Overview

This project explores the relationship between transcription factors (TFs) and the fitness of their target genes in Escherichia coli, using data from RegulonDB and the Fitness Browser. In bacteria, fitness is typically measured as growth rate, and when a TF gene is disrupted by a transposon, the observed effect on fitness is assumed to reflect the loss of regulation on its downstream targets. The central hypothesis of the project is that the fitness of a TF mutant can be approximated by some function of the fitness values of its target genes:

<p align="center"><em>fitness(r₁) = f(fitness(t₁), fitness(t₂), ..., fitness(tₖ))</em></p>

However, the exact form of this function f is unknown. Several biologically motivated guesses are tested, each reflecting different assumptions about target gene interactions:
- The **mean** assumes redundancy across targets. In such cases, losing one gene has the same impact as losing any other, and averaging their contributions approximates the expected behavior.
- The **maximum** captures dominance by a single key target.
- The **sum** assumes independent, additive contributions. This makes it suitable when targets are involved in distinct biological processes with no epistatic interaction.
- The **product** models strong epistasis but overestimates effects when many targets are unrelated.
- The **geometric mean** corrects the product's problem but does not capture the number of interactions.

For each TF-condition pair, these five functions were computed using the fitness values of the TF's targets. The result was compared to the actual TF fitness by computing the log2 ratio of observed vs. predicted fitness. This log2 transformation allows for symmetric interpretation: a ratio near zero indicates a good match between the predicted and observed value.

To assess how well each function captures TF behavior across conditions, squared errors were computed and summarized with mean squared error (MSE). The "best function" was then assigned to each TF in two ways:
- **dominantFunc:** the most frequently best function across conditions,
- **bestGuessMSE:** the function with the lowest MSE across all conditions.

Exploratory analyses were conducted on the resulting dataset, including:
- Scatterplots and boxplots to visualize how each function performs in terms of mean error and variability,
- Correlation tests to assess whether function performance depends on the number of targets,
- Comparison of the two classification criteria (dominantFunc and bestGuessMSE)
- Principal Component Analysis (PCA) to visualize whether TFs tend to cluster by function in a reduced space,
- Relationship between the transcription factors connectivity and the function assigned.

## Results

Interestingly, no single function emerged as universally superior. PCA revealed no strong clustering by function, suggesting that TF behavior is likely TF-specific rather than governed by global patterns. This aligns with biological expectations: some TFs regulate genes involved in unrelated pathways, while others control genes that work together within the same process. Ultimately, MSE-based selection proved more reliable than frequency-based metrics, as it offers a condition-independent evaluation and better generalization when the context is unknown. Future extensions of the project could include regression-based models or machine learning approaches to more accurately approximate the true functional mapping between TFs and their targets.

## Repository Contents

This repository includes two R Markdown files that document the full analysis:
- preprocessing.Rmd: contains the data loading and preprocessing steps, including the filtering and cleaning of the data, the computation of all five aggregation functions and MSE for each transcription factor across experimental conditions.
- analysis.Rmd: includes all downstream analyses, such as exploratory plots, correlation tests, assignment of the best function per TF, PCA and three-dimensional plots, focus on the role of the number of targets and operons, and interpretation of the results.

## Contact
For any additional questions or feedback, please contact [Luca Lepore](mailto:luca.lepore99@outlook.com)