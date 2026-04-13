# IMDB Review Dataset (as introduced in Maas et al., 2011)

> **Scope note:** This data card is filled **only from information stated in the paper**
> “Learning Word Vectors for Sentiment Analysis” (ACL 2011) and the dataset URL given in the paper.
> Whenever the paper does not provide enough detail, the field is marked **Not specified in the paper**.

Write a short summary describing your dataset (limit
200 words). Include information about the content
and topic of the data, sources and motivations for the
dataset, benefits and the problems or use cases it is
suitable for.

The paper introduces a publicly released **IMDB movie review dataset** for sentiment analysis. The dataset contains **50,000 movie reviews** collected from IMDB, with an **even number of positive and negative reviews**. To focus on clear polarity classification, the dataset includes only **highly polarized reviews**: reviews with score **≤ 4/10** are labeled negative, and reviews with score **≥ 7/10** are labeled positive; **neutral reviews are excluded**. The dataset is evenly split into **25,000 training** and **25,000 test** reviews, and uses **disjoint sets of movies** for training and testing to reduce leakage from movie-specific words and repeated content patterns. The dataset was introduced as a **more robust benchmark** than smaller prior sentiment datasets and is suitable for **research on sentiment classification, benchmark evaluation, and sentiment-aware representation learning**.

#### Dataset Link
- Dataset page: http://www.andrew-maas.net/data/sentiment
- Paper: https://aclanthology.org/P11-1015.pdf

#### Data Card Author(s)
- **Andrew L. Maas et al., Stanford University:** (Owner; proxy based on dataset/paper authors, since the paper does not name separate data card authors)

## Authorship
### Publishers
#### Publishing Organization(s)
- Stanford University

#### Industry Type(s)
- Academic - Tech

#### Contact Detail(s)
- **Publishing POC:** Andrew L. Maas et al. (exact POC not designated in the paper)
- **Affiliation:** Stanford University
- **Contact:** [amaas, rdaly, ptpham, yuze, ang, cgpotts]@stanford.edu
- **Mailing List:** Not specified in the paper
- **Website:** http://www.andrew-maas.net/data/sentiment

### Dataset Owners
#### Team(s)
- Stanford University research team (exact lab/group name not specified in the paper)

#### Contact Detail(s)
- **Dataset Owner(s):** Andrew L. Maas; Raymond E. Daly; Peter T. Pham; Dan Huang; Andrew Y. Ng; Christopher Potts
- **Affiliation:** Stanford University
- **Contact:** [amaas, rdaly, ptpham, yuze, ang, cgpotts]@stanford.edu
- **Group Email:** Not specified in the paper
- **Website:** http://www.andrew-maas.net/data/sentiment

#### Author(s)
- Andrew L. Maas, Author, Stanford University, 2011
- Raymond E. Daly, Author, Stanford University, 2011
- Peter T. Pham, Author, Stanford University, 2011
- Dan Huang, Author, Stanford University, 2011
- Andrew Y. Ng, Author, Stanford University, 2011
- Christopher Potts, Author, Stanford University, 2011

### Funding Sources
#### Institution(s)
- DARPA Deep Learning program
- National Science Foundation (NSF)
- Office of Naval Research (ONR)

#### Funding or Grant Summary(ies)
This work is reported as supported by the **DARPA Deep Learning program** under contract **FA8650-10-C-7020**, an **NSF Graduate Fellowship** awarded to Andrew L. Maas, and **ONR grant No. N00014-10-1-0109** to Christopher Potts.

**Additional Notes:** Funding is stated in the paper acknowledgments.

## Dataset Overview
#### Data Subject(s)
- Non-Sensitive Data about people
- Others: Publicly available user-written movie reviews and rating-derived sentiment labels

#### Dataset Snapshot
Category | Data
--- | ---
Size of Dataset | Not specified in the paper
Number of Instances | 50,000 reviews
Number of Fields | Not specified in the paper
Labeled Classes | 2 (positive, negative)
Number of Labels | 50,000 binary sentiment labels (1 per review)
Average Labeles Per Instance | 1
Algorithmic Labels | Binary polarity labels derived by thresholding IMDB scores
Human Labels | Original IMDB review scores / ratings supplied by reviewers
Other Characteristics | Class-balanced; max 30 reviews per movie; neutral reviews excluded; train/test use disjoint movie sets

**Above:** Snapshot of the IMDB review benchmark dataset introduced in the paper.

**Additional Notes:** The paper also mentions using 25,000 labeled IMDB reviews for learning word representations, and a variant using 50,000 additional unlabeled reviews.

#### Content Description
Each instance is a **movie review text** from IMDB paired with a **binary sentiment polarity label**. The dataset is intended for document-level sentiment classification. Labels are based on IMDB review scores: **negative if score ≤ 4/10**, **positive if score ≥ 7/10**. Neutral reviews are excluded.

**Additional Notes:** The paper does not enumerate the exact serialized fields of the released files.

#### Descriptive Statistics
Statistic | Field Name | Field Name | Field Name
--- | --- | --- | ---
count | Not specified | Not specified | Not specified
mean | Not specified | Not specified | Not specified
std | Not specified | Not specified | Not specified
min | Not specified | Not specified | Not specified
25% | Not specified | Not specified | Not specified
50% | Not specified | Not specified | Not specified
75% | Not specified | Not specified | Not specified
max | Not specified | Not specified | Not specified
mode | Not specified | Not specified | Not specified

**Above:** Detailed descriptive statistics are not reported in the paper.

**Additional Notes:** Only aggregate dataset-level characteristics are stated.

### Sensitivity of Data
#### Sensitivity Type(s)
- User Content
- Others: The paper does not specify whether usernames, account identifiers, or metadata are included in the released files

#### Field(s) with Sensitive Data
**Intentional Collected Sensitive Data**

(S/PII were collected as a part of the
dataset creation process.)

Field Name | Description
--- | ---
None reported | The paper does not describe collection of direct identifiers or sensitive personal attributes

**Unintentionally Collected Sensitive Data**

(S/PII were not explicitly collected as a
part of the dataset creation process but
can be inferred using additional
methods.)

Field Name | Description
--- | ---
Review text | Free-form user text could potentially contain incidental personal information, but this is not discussed in the paper

**Additional Notes:** Privacy handling is not described in the paper.

#### Security and Privacy Handling
The paper does not report specific privacy filtering, redaction, anonymization, or access-control procedures for the released dataset.

**Method:** Not specified in the paper

**Additional Notes:** Because the dataset consists of public user-generated text, downstream users should review privacy considerations independently.

#### Risk Type(s)
- Not specified in the paper

#### Supplemental Link(s)
**Dataset Page:** http://www.andrew-maas.net/data/sentiment

**Paper:** https://aclanthology.org/P11-1015.pdf

#### Risk(s) and Mitigation(s)
The paper does not provide a formal risk analysis. A likely residual risk is that some free-text reviews may contain incidental personal information or platform-specific artifacts. The paper’s main documented mitigation is **benchmark design** rather than privacy design: using **disjoint sets of movies** for training and testing to reduce leakage from movie-specific correlations.

**Risk type:** Leakage / benchmark contamination risk + mitigated by disjoint movie splits

**Additional Notes:** Privacy and fairness risks are not analyzed in the paper.

### Dataset Version and Maintenance
#### Maintenance Status
**Limited Maintenance / Static benchmark release** (inferred from the paper’s description of a public benchmark release; exact maintenance policy is not specified)

#### Version Details
**Current Version:** 1.0 (paper-associated release)

**Last Updated:** Not specified in the paper

**Release Date:** 06/2011 (paper publication timeframe; exact dataset release date not separately stated)

#### Maintenance Plan
The paper describes the dataset as a released public benchmark for future work, but does not specify a versioning or maintenance process.

**Versioning:** Not specified in the paper

**Updates:** Not specified in the paper

**Errors:** Not specified in the paper

**Feedback:** Dataset website is provided, but no process is specified in the paper

**Additional Notes:** Treat as a static benchmark unless later documentation says otherwise.

#### Next Planned Update(s)
**Version affected:** 1.0

**Next data update:** Not specified in the paper

**Next version:** Not specified in the paper

**Next version update:** Not specified in the paper

#### Expected Change(s)
**Updates to Data:** Not specified in the paper

**Updates to Dataset:** Not specified in the paper

**Additional Notes:** None.

## Example of Data Points
#### Primary Data Modality
- Text Data

#### Sampling of Data Points
- Dataset page: http://www.andrew-maas.net/data/sentiment

#### Data Fields
Field Name | Field Value | Description
--- | --- | ---
review_text | Free-form text | User-written IMDB movie review
sentiment_label | positive / negative | Binary label derived from score thresholds
original_score | 1–10 scale (used during construction) | IMDB rating used to derive sentiment polarity; the paper does not explicitly state whether this field is included in the public release

**Above:** Conceptual fields inferable from the paper.

**Additional Notes:** The paper does not print an example review.

#### Typical Data Point
A typical data point is a **single IMDB movie review document** paired with a **binary sentiment label**. Reviews are selected to be **highly polarized**, meaning the underlying IMDB score falls clearly into either the negative or positive range.

```text
{
  "review_text": "[movie review text]",
  "sentiment_label": "positive or negative"
}
```

**Additional Notes:** Example is schematic because the paper does not reproduce a real review instance.

#### Atypical Data Point
Atypical cases are not explicitly cataloged in the paper. Relative to the dataset design, an atypical source review would be a **neutral review** (score 5 or 6), but such reviews are **excluded** from the released benchmark.

```text
{
  "review_text": "[neutral review text]",
  "sentiment_label": "excluded from dataset"
}
```

**Additional Notes:** This describes the exclusion rule rather than an included outlier example.

## Motivations & Intentions
### Motivations
#### Purpose(s)
- Research

#### Domain(s) of Application
`Natural Language Processing`, `Sentiment Analysis`, `Text Classification`, `Representation Learning`

#### Motivating Factor(s)
- To learn word vectors that capture both **semantic** and **sentiment** information
- To exploit abundant **document-level sentiment labels** available in online reviews
- To provide a **larger and more robust benchmark** than smaller prior movie-review datasets
- To reduce train/test correlation caused by multiple reviews of the same movie appearing across folds in earlier benchmarks

### Intended Use
#### Dataset Use(s)
- Safe for research use

#### Suitable Use Case(s)
**Suitable Use Case:** Binary document-level sentiment classification on movie reviews

**Suitable Use Case:** Research on sentiment-aware word representations or feature learning

**Suitable Use Case:** Benchmark evaluation where disjoint movie splits are important to reduce leakage

**Additional Notes:** The paper also uses the data to induce sentiment-aware word vectors.

#### Unsuitable Use Case(s)
**Unsuitable Use Case:** Multi-class rating prediction across the full 1–10 rating scale, because the benchmark excludes neutral reviews and collapses sentiment to two classes

**Unsuitable Use Case:** Domain-general sentiment modeling outside movie reviews without checking transfer performance

**Unsuitable Use Case:** Tasks requiring demographic, author, or rich metadata fields, because such information is not described in the paper

**Additional Notes:** These limitations follow directly from the dataset construction choices stated in the paper.

#### Research and Problem Space(s)
The dataset is intended to support research on **sentiment classification** and **sentiment-aware word representation learning**. The paper specifically motivates the dataset as a more robust benchmark that emphasizes **genuine sentiment features** rather than movie-specific lexical cues caused by overlap between training and test examples.

#### Citation Guidelines
**Guidelines & Steps:** Cite the ACL 2011 paper that introduces the dataset. When relevant, also cite the dataset website listed in the paper.

**BiBTeX:**
```bibtex
@inproceedings{maas2011learning,
  title={Learning Word Vectors for Sentiment Analysis},
  author={Maas, Andrew L. and Daly, Raymond E. and Pham, Peter T. and Huang, Dan and Ng, Andrew Y. and Potts, Christopher},
  booktitle={Proceedings of the 49th Annual Meeting of the Association for Computational Linguistics: Human Language Technologies},
  pages={142--150},
  year={2011},
  address={Portland, Oregon},
  publisher={Association for Computational Linguistics}
}
```

**Additional Notes:** The paper is the primary citable source for the dataset.

## Access, Rentention, & Wipeout
### Access
#### Access Type
- External - Open Access

#### Documentation Link(s)
- Dataset Website URL: http://www.andrew-maas.net/data/sentiment
- Paper URL: https://aclanthology.org/P11-1015.pdf

#### Prerequisite(s)
No prerequisites, training requirements, or approval steps are described in the paper.

#### Policy Link(s)
- Dataset page: http://www.andrew-maas.net/data/sentiment

Code to download data:
```text
Not specified in the paper.
```

#### Access Control List(s)
**Access Control List:** Not specified in the paper; the dataset is described as publicly released.

**Additional Notes:** None.

### Retention
#### Duration
Not specified in the paper.

#### Policy Summary
**Retention Plan ID:** Not specified

**Summary:** Not specified in the paper

#### Process Guide
No retention process is described in the paper.

**Additional Notes:** None.

#### Exception(s) and Exemption(s)
**Exemption Code:** `PUBLIC_DATA` (reasonable classification based on the public release described in the paper)

**Summary:** The dataset is described as publicly released for research, but no formal retention policy is given in the paper.

**Additional Notes:** This exemption code is a practical classification, not a statement from the paper.

### Wipeout and Deletion
#### Duration
Not specified in the paper.

#### Deletion Event Summary
**Sequence of deletion and processing events:**
- Not specified in the paper

**Additional Notes:** None.

#### Acceptable Means of Deletion
- Not specified in the paper

#### Post-Deletion Obligations
**Sequence of post-deletion obligations:**
- Not specified in the paper

**Additional Notes:** None.

#### Operational Requirement(s)
**Wipeout Integration Operational Requirements:**
- Not specified in the paper

#### Exceptions and Exemptions
**Policy Exception bug:** Not specified

**Summary:** Not specified in the paper

**Additional Notes:** None.

## Provenance
### Collection
#### Method(s) Used
- Others: Collected from publicly available IMDB reviews; the exact harvesting pipeline is not described in the paper

#### Methodology Detail(s)
**Collection Type**

**Source:** IMDB movie reviews

**Platform:** IMDB, an online movie review platform

**Is this source considered sensitive or high-risk?** Not specified in the paper

**Dates of Collection:** Not specified in the paper

**Primary modality of collection data:**
- Text Data

**Update Frequency for collected data:**
- Static

**Additional Links for this collection:**
- Dataset page: http://www.andrew-maas.net/data/sentiment

**Additional Notes:** The paper states that the authors constructed a collection of 50,000 reviews from IMDB and capped the number of reviews at 30 per movie.

#### Source Description(s)
- **Source:** Publicly available movie reviews from IMDB
- **Source:** User-provided IMDB review scores used to derive sentiment polarity labels

**Additional Notes:** The paper does not describe any additional upstream sources.

#### Collection Cadence
**Static:** Data was collected once and released as a benchmark.

#### Data Integration
**Source**

**Included Fields**

Data fields that were collected and are included in the dataset.

Field Name | Description
--- | ---
review_text | Movie review text from IMDB
sentiment_label | Binary polarity label derived from rating thresholds

**Additional Notes:** Exact serialized file schema is not specified in the paper.

**Excluded Fields**

Data fields that were collected but are excluded from the dataset.

Field Name | Description
--- | ---
neutral reviews | Reviews with score 5 or 6 are excluded
extra same-movie reviews | More than 30 reviews per movie are not included

**Additional Notes:** Disjoint movie splits are used between train and test.

#### Data Processing
**Collection Method or Source**

**Description:** The authors construct a balanced sentiment dataset from IMDB reviews.

**Methods employed:** Threshold ratings into positive and negative classes; exclude neutral reviews; cap reviews per movie at 30; create disjoint movie sets for train/test; for representation learning, use 5,000 most frequent tokens while ignoring the 50 most frequent terms, do not apply stemming, do not apply traditional stop-word removal, and allow some non-word sentiment tokens.

**Tools or libraries:** Not specified in the paper.

**Additional Notes:** The paper also mentions a training variant with 50,000 additional unlabeled reviews.

### Collection Criteria
#### Data Selection
- **Collection Method of Source:** Select IMDB movie reviews with no more than 30 reviews per movie
- **Collection Method of Source:** For benchmark classification, include only highly polarized reviews
- **Collection Method of Source:** Use disjoint movie sets for training and testing

**Additional Notes:** These are the main documented criteria.

#### Data Inclusion
- **Collection Method of Source:** Include reviews with score **≤ 4/10** as negative
- **Collection Method of Source:** Include reviews with score **≥ 7/10** as positive
- **Collection Method of Source:** Include an even number of positive and negative reviews

**Additional Notes:** The released benchmark is balanced.

#### Data Exclusion
- **Collection Method of Source:** Exclude neutral reviews (scores 5 or 6)
- **Collection Method of Source:** Exclude reviews beyond the per-movie cap of 30
- **Collection Method of Source:** Avoid movie overlap between training and test sets

**Additional Notes:** These exclusions are central to the paper’s benchmark design.

### Relationship to Source
#### Use & Utility(ies)
- **Source Type:** IMDB reviews are used to build a benchmark for sentiment classification and to provide document-level supervision for sentiment-aware word vector learning

**Additional Notes:** The source platform supplies both free-text reviews and review scores.

#### Benefit and Value(s)
- **Source Type:** Larger than the 2,000-review Pang and Lee benchmark
- **Source Type:** Reduced train/test contamination through disjoint movie splits
- **Source Type:** Balanced positive/negative classes support clearer benchmark comparison

**Additional Notes:** The paper explicitly motivates these advantages.

#### Limitation(s) and Trade-Off(s)
- **Source Type:** Domain limited to movie reviews
- **Source Type:** Neutral sentiment is removed, so the benchmark does not cover the full rating spectrum
- **Source Type:** The paper does not provide rich metadata, demographic information, or collection-time details

### Version and Maintenance
#### First Version
- **Release date:** 06/2011 (paper timeframe; exact date not separately specified)
- **Link to dataset:** http://www.andrew-maas.net/data/sentiment
- **Status:** Limited Maintenance / Static benchmark release (not explicitly specified)
- **Size of Dataset:** Not specified in the paper
- **Number of Instances:** 50,000

#### Note(s) and Caveat(s)
The paper presents this as the benchmark release and does not describe earlier versions.

**Additional Notes:** None.

#### Cadence
- Static

#### Last and Next Update(s)
- **Date of last update:** Not specified in the paper
- **Total data points affected:** Not specified in the paper
- **Data points updated:** Not specified in the paper
- **Data points added:** Not specified in the paper
- **Data points removed:** Not specified in the paper
- **Date of next update:** Not specified in the paper

#### Changes on Update(s)
- **Source Type:** Not specified in the paper

**Additional Notes:** None.

## Human and Other Sensitive Attributes
#### Sensitive Human Attribute(s)
- Not specified in the paper

#### Intentionality
**Intentionally Collected Attributes**

Human attributes were labeled or collected as a part of the dataset creation
process.

Field Name | Description
--- | ---
None reported | The paper does not report collecting demographic or sensitive human attributes

**Additional Notes:** None.

**Unintentionally Collected Attributes**

Human attributes were not explicitly collected as a part of the dataset
creation process but can be inferred using additional methods.

Field Name | Description
--- | ---
review_text | Author style, background, or other attributes may be inferable from free text, but this is not analyzed in the paper

**Additional Notes:** None.

#### Rationale
The paper’s goal is sentiment analysis and sentiment-aware representation learning, not human-attribute analysis.

#### Source(s)
- **Human Attribute:** Not specified in the paper

**Additional Notes:** None.

#### Methodology Detail(s)
**Human Attribute Method:** Not specified in the paper

**Collection task:** Not specified in the paper

**Platforms, tools, or libraries:**
- Not specified in the paper

**Additional Notes:** None.

#### Distribution(s)
Human Attribute | Label or Class | Label or Class
--- | --- | ---
Count | Not specified | Not specified

**Above:** No human-attribute distributions are reported in the paper.
**Additional Notes:** None.

#### Known Correlations
[`review_text`]

**Description:** The paper discusses **movie-specific lexical correlation** as a benchmark concern in earlier datasets, not demographic correlation.

**Impact on dataset use:** Disjoint movie splits are used to reduce memorization of movie-specific words.

**Additional Notes:** This is the only explicitly discussed correlation risk.

#### Risk(s) and Mitigation(s)
**Human Attribute**

The paper does not discuss fairness or demographic risk analysis.

**Risk type:** Inference risk from free text + not analyzed in the paper

**Trade-offs, caveats, & other considerations:** Use with caution for any human-attribute inference task.

**Additional Notes:** None.

## Extended Use
### Use with Other Data
#### Safety Level
- Unknown

#### Known Safe Dataset(s) or Data Type(s)
**Dataset or Data Type:** Not specified in the paper.

#### Best Practices
Use the dataset primarily as a **standalone benchmark** for sentiment classification unless there is a clearly justified reason to join it with other data.

**Additional Notes:** The paper does not provide data-joining guidance.

#### Known Unsafe Dataset(s) or Data Type(s)
**Dataset or Data Type:** Not specified in the paper.

#### Limitation(s) and Recommendation(s)
The paper does not discuss joining with other datasets. Because the data are free-text reviews, joining with author or account metadata could change the privacy and leakage profile.

**Additional Notes:** This is a downstream-use recommendation, not a statement from the paper.

### Forking & Sampling
#### Safety Level
- Conditionally safe to fork and/or sample

#### Acceptable Sampling Method(s)
- Random Sampling
- Stratified Sampling

#### Best Practice(s)
Maintain **class balance** and, when possible, preserve **movie-level disjointness** between train and test partitions.

**Additional Notes:** These recommendations follow the paper’s benchmark design logic.

#### Risk(s) and Mitigation(s)
Sampling that ignores movie identity may reintroduce benchmark leakage through movie-specific words.

**Risk Type:** Train/test contamination risk + mitigate by grouping/splitting at the movie level

**Additional Notes:** None.

#### Limitation(s) and Recommendation(s)
The benchmark is intentionally designed to prevent memorization of movie-specific lexical cues. Any fork or sample that breaks this constraint may inflate performance.

**Limitation Type:** Split design + preserve disjoint movie sets where possible

**Additional Notes:** None.

### Use in ML or AI Systems
#### Dataset Use(s)
- Training
- Testing
- Validation

#### Notable Feature(s)
**Exploration Demo:** Dataset page listed in the paper.

**Notable Field Name:** Sentiment label is binary and derived from highly polarized scores only.

**Notable Field Name:** Dataset is balanced across positive and negative classes.

**Notable Field Name:** Training and test sets use disjoint movie sets.

**Above:** These are the main benchmark characteristics emphasized in the paper.

**Additional Notes:** The paper also uses 10-fold cross-validation on other datasets for comparison.

#### Usage Guideline(s)
**Usage Guidelines:** Use as a benchmark for document-level sentiment classification and sentiment-aware representation learning. Preserve the documented split logic and note that the task is binary polarity classification, not full-scale rating prediction.

**Approval Steps:** Not specified in the paper.

**Reviewer:** Not specified in the paper.

**Additional Notes:** None.

#### Distribution(s)
Set | Number of data points
--- | ---
Train | 25,000
Test | 25,000
Validation | Not separately provided in the paper
Dev | Not separately provided in the paper

**Above:** Official split information explicitly stated in the paper.

**Additional Notes:** Hyperparameters were cross-validated on the training set.

#### Known Correlation(s)
`movie identity`, `review_text`

**Description:** Earlier smaller benchmarks contained correlated reviews from the same movie across train/test folds. The new IMDB dataset is designed to avoid this issue.

**Impact on dataset use:** Reported results better reflect genuine sentiment generalization rather than memorization of movie-specific words.

**Risks from correlation:** Breaking the disjoint-by-movie split can inflate performance estimates.

**Additional Notes:** This is a central motivation in the paper.

#### Split Statistics
Statistic | Train | Test | Valid | Dev
--- | --- | --- | --- | ---
Count | 25,000 | 25,000 | Not specified | Not specified
Class balance | Balanced positive/negative | Balanced positive/negative | Not specified | Not specified
Movie overlap | Disjoint from test | Disjoint from train | Not specified | Not specified

**Above:** Split statistics directly supported by the paper.

## Transformations
### Synopsis
#### Transformation(s) Applied
- Converting Data Types
- Others (Please specify): Rating-threshold label derivation, vocabulary filtering, train/test splitting by movie

#### Field(s) Transformed
**Transformation Type**

Field Name | Source & Target
--- | ---
original_score | 1–10 IMDB score -> binary sentiment polarity (for the benchmark)
original_score | 1–10 IMDB score -> continuous value in [0, 1] (for model training described in the paper)
vocabulary | Full vocabulary -> 5,000 most frequent tokens, excluding the top 50 most frequent terms (for word representation learning)

**Additional Notes:** These are the key transformations explicitly described.

#### Library(ies) and Method(s) Used
**Transformation Type**

**Method:** Threshold rating scores to derive labels; linearly map star values to [0,1] for supervised sentiment training; restrict vocabulary; do not apply stemming; do not use traditional stop-word removal; allow some non-word sentiment tokens.

**Platforms, tools, or libraries:**
- Not specified in the paper

**Transformation Results:** Produced a balanced binary sentiment benchmark and a training setup for sentiment-aware word vectors.

**Additional Notes:** None.

### Breakdown of Transformations
#### Cleaning Missing Value(s)
Not specified in the paper.

#### Method(s) Used
Not specified in the paper.

#### Comparative Summary
Not specified in the paper.

#### Residual & Other Risk(s)
Not specified in the paper.

#### Human Oversight Measure(s)
Not specified in the paper.

#### Additional Considerations
Not specified in the paper.

#### Cleaning Mismatched Value(s)
Not specified in the paper.

#### Method(s) Used
Not specified in the paper.

#### Comparative Summary
Not specified in the paper.

#### Residual & Other Risk(s)
Not specified in the paper.

#### Human Oversight Measure(s)
Not specified in the paper.

#### Additional Considerations
Not specified in the paper.

#### Anomalies
Not specified in the paper.

#### Method(s) Used
Not specified in the paper.

#### Comparative Summary
Not specified in the paper.

#### Residual & Other Risk(s)
Not specified in the paper.

#### Human Oversight Measure(s)
Not specified in the paper.

#### Additional Considerations
Not specified in the paper.

#### Dimensionality Reduction
Not specified as a dataset transformation in the paper.

#### Method(s) Used
Not specified in the paper.

#### Comparative Summary
Not specified in the paper.

#### Residual & Other Risks
Not specified in the paper.

#### Human Oversight Measure(s)
Not specified in the paper.

#### Additional Considerations
Not specified in the paper.

#### Joining Input Sources
Not specified in the paper.

#### Method(s) Used
Not specified in the paper.

#### Comparative Summary
Not specified in the paper.

#### Residual & Other Risk(s)
Not specified in the paper.

#### Human Oversight Measure(s)
Not specified in the paper.

#### Additional Considerations
Not specified in the paper.

#### Redaction or Anonymization
Not specified in the paper.

#### Method(s) Used
Not specified in the paper.

#### Comparative Summary
Not specified in the paper.

#### Residual & Other Risk(s)
Not specified in the paper.

#### Human Oversight Measure(s)
Not specified in the paper.

#### Additional Considerations
Not specified in the paper.

#### Others (Please Specify)
The paper explicitly describes the following dataset-construction transformations:
- Thresholding review scores into positive/negative labels
- Excluding neutral reviews
- Capping reviews per movie at 30
- Enforcing disjoint movie sets between train and test
- Restricting vocabulary for representation learning experiments

#### Method(s) Used
Rule-based filtering and thresholding, as described in the paper.

#### Comparative Summary
These transformations are used to create a more robust sentiment benchmark and reduce leakage from movie-specific overlap.

#### Residual & Other Risk(s)
A stricter benchmark may reduce ecological validity for real-world rating distributions because neutral reviews are excluded.

#### Human Oversight Measure(s)
Not specified in the paper.

#### Additional Considerations
None.

## Annotations & Labeling
#### Annotation Workforce Type
- Human Annotations (Non-Expert)
- Machine-Generated Annotations

#### Annotation Characteristic(s)
**Annotation Type** | **Number**
--- | ---
Number of unique annotations | 50,000 review-level labels
Total number of annotations | 50,000
Average annotations per example | 1
Number of annotators per example | 1 reviewer-provided rating per included review (as implied by the source platform)
Quality metrics | Not specified in the paper

**Above:** Annotation information inferable from IMDB review ratings and the paper’s label-derivation rules.

**Additional Notes:** Binary labels are derived from original user scores.

#### Annotation Description(s)
**(Rating-derived polarity labels)**

**Description:** Original IMDB review scores are used to derive sentiment labels. Reviews with score **≤ 4** are treated as negative and reviews with score **≥ 7** are treated as positive. Neutral reviews are excluded.

**Link:** http://www.andrew-maas.net/data/sentiment

**Platforms, tools, or libraries:**
- IMDB: source of public ratings and review text
- Label derivation rules: described in the paper

**Additional Notes:** The paper also maps ratings to [0,1] for the sentiment component of model training.

#### Annotation Distribution(s)
**Annotation Type** | **Number**
--- | ---
Positive reviews | 25,000 (50%)
Negative reviews | 25,000 (50%)

**Above:** The released benchmark is class balanced.

**Additional Notes:** Exact train/test class counts are not separately enumerated, but the dataset is evenly divided and class-balanced overall.

#### Annotation Task(s)
**(Sentiment labeling)**

**Task description:** Assign document-level sentiment polarity to movie reviews using user-provided IMDB ratings.

**Task instructions:** Negative if score ≤ 4/10; positive if score ≥ 7/10; exclude neutral reviews.

**Methods used:** Rule-based thresholding of original ratings.

**Inter-rater adjudication policy:** Not specified in the paper.

**Golden questions:** Not specified in the paper.

**Additional notes:** None.

### Human Annotators
#### Annotator Description(s)
**(Rating source users)**

**Task type:** Original rating of movie reviews on IMDB

**Number of unique annotators:** Not specified in the paper

**Expertise of annotators:** Non-expert public users / reviewers

**Description of annotators:** IMDB reviewers who wrote the source reviews and supplied the underlying scores

**Language distribution of annotators:** Not specified in the paper

**Geographic distribution of annotators:** Not specified in the paper

**Summary of annotation instructions:** Not specified in the paper

**Summary of gold questions:** Not specified in the paper

**Annotation platforms:** IMDB

**Additional Notes:** The dataset creators derive labels from these ratings; they do not report a separate manual annotation campaign.

#### Annotator Task(s)
**(User-provided rating task)**

**Task description:** Submit a movie review and corresponding score on IMDB.

**Task instructions:** Not specified in the paper

**Compensation:** Not specified in the paper

**Quality assurance:** Not specified in the paper

**Additional Notes:** None.
