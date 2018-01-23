# What is Machine Learning in Astronomy about? 
We discussed a bit about terminology used in this field, and that terminology was non-standard, overlapping, and perhaps not worth caring about. This pertained to statistics/Machine Learning/Data Mining (and AIdue to a question). We would adopt the position in the book that we will work on extracting information/knowledge from data.
- What is Statistics/Data Mining/Machine Learning?
    - Lots of overlap in these terms. Better to worry about the goal here.
    - Extracting Information/knowledge from data.
       - Data ? Data can mean Observations/Survey Results/Simulated Data etc. 
       - Information/Knowledge ? In the real world many connected things might continue simultaneosly, we may be interested in some part of them -> Knowledge/Information. The underlying idea is that usually we can treat  the system as proabilistic in some variables and have a trend in others. Best to go through with examples:

## Before that let us discuss examples of data types and questions in different fields
- In industry
- In Social Sciences
- In Astronomy

A number of people contributed to the discussion, and we talked about
- examples in industry/govt that are focussed on image data (google photograph location recognition, facial recognition including vehicle drivers, facial recognition used to match artwork to photographs of people. We realize that this might mean being able to match test data to images in a large training sample repository, which might have transformations like different perspectives, croppting, rotations etc.). A lot of astronomy data is images as that is the product from telescopes ... classifying astronomical sources from these images using ML techniques is a frequent and important task.
- examples of streaming data: Continually changing data like stock prices which are used by financial companies for immediate decisions. Similar (but quantitatively different) constraints apply for triggering transient observations from streaming data from a fast all  sky telescopes.
- Text Data as in scrapting web pages, content and communication, which requires processing text, and understanding language meanings and syntax through a corpus for the specific language.
- Structured/Tabular data: Probably too commonplace for mention :)
- In Astronomy : Use of neural networks in understanding the location of interaction of particles from the brightness and location of light detection. ML methods to classify galaxy properties from morphology derived from images of galaxies. 

## Examples 
A couple of concrete toy examples were used to illustrate the progression from a well defined statistical problem with a generative model (ie. well defined likelihood, and uncertainty model) to dealing with data without such information to fall back on, what kind of methods are used in such cases, and some of the consequences of using such methods. 

###  Simplest example: Generative Model in cosmology
- Simplest incarnation (wrong in principle) 
- Generative model : ie. Knowing {z_i, theta, sigma^i} we can generate mock data.
- SN Cosmology mu = m - M , mu = mu(theta) (Eqn 8.4 of text)
mu(z_i) = mu(theta, z_i) + espsion_i
epsilon_i  draws from  Normal(0, sigma^2_i) (Fig 8.5 from text)
- Many reasons why this model is wrong in principle, but let us ignore that for now.

- Q : Infer the cosmological theta from data ie. How did we find mu(theta, z)?
- A : well defined statistical procedures (Bayesian and Frequentist) to address such situations, particularly in the simple one Dimensional case as in this example. This is discussed in the book, and at least the methodology will probably come up in later classes.


### House prices vs features
Completely different, simple popular example about which we know very little. 
Q. What determines the prices of houses and how can we predict it

- Data : derives popularity due to availability of a curated tabular dataset on Boston Housing, with several
features/properties and the prices of the houses. Gets used in many data science examples, and was also on Kaggle. 

First, let us simplify this problem further and imagine a table, choosing the most important properties: 

- Number of bedrooms, area (Why these ? No one objected, so even though we don't have enough understanding tobuild models, we understand what the most important variables are. This will be often be very important) 
- `Training sample`:

| Area          | Num Bedrooms  | Price |
| ------------- |:-------------:| -----:|
| A1            | N1            | P1    |
| A2            | N2            | P2    |
| A3            | N3            | P3    |
| ..          |  ..          | ..    |
| An            | Nn            | Pn    |

But then there are other houses for which we have the first two columns but would like to predict the third. 

- Easy to think of applying the method above to houses, if we have a model (analog of mu(theta, z) ), 'fit' for the parameters in this model like we did for cosmology, and then use the 'best parameters' to do predictions. But we don't have a model. 
- Discuss Methods ?:
    - suggestion: correlations should be used 
    - some examples: Try simple methods and verify? For example start with a  model of price linear in Area and NumBedrooms, get best slopes, verify that starting model is not too crazy. 
    - Nicer methods of guessing models  both higher order polynomial and non-parametric discussed in book later.
    
#### A few things to note:
-  Correlations vs Causations: As pointed out in discussions this uses correlations in training sample to make predictions on the test sample. So this is not necessarily a causal relationship. What do we lose due to this?
    - Since it is not a causal model the model will not work in a different location. More generally, any time a variable which is fixed in the training sample but is different in the test sample, there will be a problem. 
   - More generally : __The training sample must be representative of the test sample__

### Back to the SN cosmology example:
Would we ever try the kind of methods we tried with housing prices to replace mu(theta, z) ?
- The book shows how one might try some 'guess' model of mu with z (linear/polynomial etc.), that one might try if we did not know the functional form. 
- While people in cosmology don't usually use such a model, we don't exactly know the functional form, after all the equation of state of 'dark energy' as a function of z is what many cosmological surveys would like to measure. While a linear or low order polynomial for mu is a bad fit, people do think about doing non-parametric fits to the data to get model independence. A large number of papers have been written on this.
- On the other hand, others have attempted to parameterize the  `equation of state` w = P/rho of dark energy, as the unknown variable. Here the approach is much more similar to using a low order polynomial, though more non-parametric methods have been used too.
__While we can try to use less parametric models, it is still important to understand which variables are important: mixing knowledge of the field (domain knowledge) with different methods is useful__

### House Prices Example:

We started with the two column independent variables to simplify the study. However, this could have many properties, many of which are not as easy to interpret. (eg. The Boston Dataset we talked about has many features)- What could be done in selecting features if we could not figure out the most important ones? One can have methods to select 'important features that are mostly responsible for differences in variable of interest ... in this case price.  eg.  PCA like methods which will be part of the book.

### Cosmology Example
- Let us return to the cosmology example, but increase relax the assumptions in a single way: we recognize that the absolute magnitudes of supernovae  at peak brightness is not 'known'. Instead the absolute magnitude of a supernova with specific properties is given by a data driven model. Similar to the problem of determining house prices from a training sample. 
- Unlike the case with house prices, where the training sample had the same variables as the test samples, for such cases, there are properties intrinsic to the supernovae, as well as properties that depend on the observation. For example, the same supernovae may appear different or transformed, based on where they are observed. Thus a training sample must be constructed of features that are invariant under the transformations, or the training set might need additional copies or weights to make the distributions have the right properties.

### Uncertainty Estimates
- The tradeoffs in many fields are different from Astronomy. For example, while uncertainties in ML methods may not be equally important in all applications, but are often important in Astronomy. This is beginning to be discussed in ML algorithms.


### Issues in  ML used for astronomy
    - Causality vs Correlations
    - Dealing with uncertainties
    - Mixing domain knowledge with ML algorithms
    - Symmetry of the problem, Intrinsic vs Extrinsic features
    - Representativity in training data, Data Augmentation
    - Validation/Metrics of Goodness/Overfitting

