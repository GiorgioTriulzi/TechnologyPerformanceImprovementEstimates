# TechnologyPerformanceImprovementEstimates
This repository contains the code used in the paper "Estimating Technology Performance Improvement Rates by Mining Patent Data", coauthored with Jeff Alstott and Chris Magee, published by Technological Forecasting and Social Change and freely available at https://www.sciencedirect.com/science/article/pii/S0040162520309264.

Patent data used by the code is available at http://dx.doi.org/10.17632/f4fj887y67.1. Processed patent citation data is available at https://zenodo.org/record/3902550#.Xu-DlWhKiUk. Raw data from the USPTO is available at https://www.patentsview.org/download/. The content of the data files as well as the methods used to create them are described in the article G. Triulzi, C.L. Magee, "Functional performance improvement data and patent sets for 30 technology domains with measurements of patent centrality and estimations of the improvement rate", published by Data in Brief, available at https://doi.org/10.1016/j.dib.2020.106257. If you use the data, please cite both articles. 

<p>The code is structured as a series of Jupyter Notebooks, which use two datasets available on <a href="https://data.mendeley.com/datasets/f4fj887y67/1">Mendeley Data</a> and <a href="https://zenodo.org/record/3902550#.Xu-DlWhKiUk">Zenodo</a>.</p>
<ul>
<li>Notebook: Compute entropy of assignees in domains
<ul>
<li>What it does: for each of the 30 technology domains, it computes the normalized entropy of the share of patents by assignee over time, from 1976 to 2015. Entropy is normalized as explained in the <a href="https://www.sciencedirect.com/science/article/pii/S0040162520309264#ecom0001">paper</a>.</li>
<li>Inputs:
<ul>
<li>Domains_patent_info.csv (<a href="https://data.mendeley.com/datasets/f4fj887y67/1">available on the Mendeley Data repository</a>)</li>
<li>PERFORMANCE_DOMAINS_K_Kr2.csv (<a href="https://data.mendeley.com/datasets/f4fj887y67/1">available on the Mendeley Data repository</a>)</li>
<li>assignee.tsv (available at <a href="https://www.patentsview.org/download/">https://www.patentsview.org/download/</a>)</li>
<li>rawassignee.tsv (available at <a href="https://www.patentsview.org/download/">https://www.patentsview.org/download/</a>)</li>
</ul>
</li>
<li>Output:
<ul>
<li>DF_Normalized_Entropy_Domains_over_time.csv</li>
</ul>
</li>
</ul>
</li>
<li>Notebook: Compute Normalized Knowledge Obsolescence Index at patent and domain levels
<ul>
<li>What it does: it computes a normalized index of knowledge obsolescence based on the age profile of citations made by patents belonging to each of the 30 domains. The normalization procedure is explained in the <a href="https://www.sciencedirect.com/science/article/pii/S0040162520309264#ecom0001">paper</a>.</li>
<li>Inputs:
<ul>
<li>Domains_patent_info.csv (<a href="https://data.mendeley.com/datasets/f4fj887y67/1">available on the Mendeley Data repository</a>)</li>
<li>All_patents_info.csv (<a href="https://data.mendeley.com/datasets/f4fj887y67/1">available on the Mendeley Data repository</a>)</li>
<li>CITATION_INFO_no_neg_citlag.csv (<a href="https://zenodo.org/record/3902550#.Xu-DlWhKiUk">available on the Zenodo repository</a>)</li>
</ul>
</li>
<li>Output:
<ul>
<li>observed_vs_expected_citation_age_patent_level.csv</li>
<li>DataFrame_Normalized_Obsolescence_Domains_over_time.csv</li>
</ul>
</li>
</ul>
</li>
<li>Notebook: Monte Carlo Cross Validation (with paper figures)
<ul>
<li>What it does: for a set of candidate patent-based predictors of the technology performance improvement rate (TIR), the code computes the predictor using data only up to a year (from 1980 to 2015), randomly sample half of the technology domains, train a regression to predict TIR and test it on the remaining half. It then produces a figure showing the correlation over time between the observed log of the TIR (a.k.a. the parameter &ldquo;K&rdquo;) and the predictor, the coefficient of the predictor and the intercept. Note that notebooks &ldquo;Compute entropy of assignees in domains &ldquo; and &ldquo;Compute Normalized Knowledge Obsolescence Index at Patent and Domain Levels&rdquo; should be run before notebook &ldquo;Monte Carlo Cross Validation (with paper figures)&rdquo; as the latter uses inputs produced by the former two.</li>
<li>Inputs:
<ul>
<li>Domains_patent_info.csv (<a href="https://data.mendeley.com/datasets/f4fj887y67/1">available on the Mendeley Data repository</a>)</li>
<li>All_patents_info.csv (<a href="https://data.mendeley.com/datasets/f4fj887y67/1">available on the Mendeley Data repository</a>)</li>
<li>PERFORMANCE_DOMAINS_K_Kr2.csv (<a href="https://data.mendeley.com/datasets/f4fj887y67/1">available on the Mendeley Data repository</a>)</li>
<li>DF_Normalized_Entropy_Domains_over_time.csv (output of code &ldquo;Compute entropy of assignees in domains&rdquo;)</li>
<li>DataFrame_Normalized_Obsolescence_Domains_over_time.csv (output of code &ldquo;Compute Normalized Knowledge Obsolescence Index at Patent and Domain Levels&rdquo;)</li>
<li>CITATIONS_DOMAINS.csv (<a href="https://zenodo.org/record/3902550#.Xu-DlWhKiUk">available on the Zenodo repository</a>)</li>
</ul>
</li>
<li>Output:
<ul>
<li>DF_stability_prediction_over_time_MONTE_CARLO_COMPARISON.csv</li>
<li>Figure 3 and S6 from the <a href="https://www.sciencedirect.com/science/article/pii/S0040162520309264#ecom0001">paper</a>.</li>
</ul>
</li>
</ul>
</li>
<li>Notebook: Estimate TIR for new domains
<ul>
<li>What it does: It runs a regression that uses the best possible predictor identified by the Monte Carlo cross validation exercise to estimate TIRs for the 30 domains based on that predictor only. It then used the estimated coefficients of the regression and the values of the predictor for estimating TIR of 5 out-of-sample domains related to Bio-electronic Medicine for which we only have patent data (no available observation of the empirical TIR). This notebook can be used to estimate the yearly performance improvement rate for any new technology domain. You only need a list of US patent numbers for the new domain. If you input a patent dataset that has more than one domain it will also compute the likelihood that one is faster than the other(s).</li>
<li>Inputs:
<ul>
<li>Domains_patent_info.csv (<a href="https://data.mendeley.com/datasets/f4fj887y67/1">available on the Mendeley Data repository</a>)</li>
<li>All_patents_info.csv (<a href="https://data.mendeley.com/datasets/f4fj887y67/1">available on the Mendeley Data repository</a>)</li>
<li>PERFORMANCE_DOMAINS_K_Kr2.csv (<a href="https://data.mendeley.com/datasets/f4fj887y67/1">available on the Mendeley Data repository</a>)</li>
<li>PATENT_SET_BIOEL_MED.csv (available <a href="https://www.dropbox.com/s/wmj7968li4137wr/PATENT_SET_BIOEL_MED.csv?dl=0">here</a>)</li>
</ul>
</li>
<li>Output:
<ul>
<li>REGRESSION_DATA.xlsx</li>
<li>TABLE_estimated_k_meanSPNPcited_1year_before_randomized_zscore_RPbyYear.xlsx</li>
<li>Figure &ldquo;density_estimated_rate_new_domains&rdquo; in PDF and TIFF formats</li>
<li>Figure &ldquo;likelihood_domain_faster_than_other_domain&rdquo; in PDF and TIFF formats</li>
</ul>
</li>
</ul>
</li>
</ul>
<p>An accompanying code that can be used to compute patent centrality indicators normalized by randomizing the US patent citation network is available on my co-author page at: <a href="https://github.com/jeffalstott/patent_centralities">https://github.com/jeffalstott/patent_centralities</a>.</p>
