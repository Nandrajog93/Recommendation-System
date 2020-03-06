# Recommendation-System

`4 types of Recommendaiton system.`

1) Knowledge based Recommendaiton system 
2) Content-based Recommendaiton system 
3) Collaborative filtering recommendation system
4) Latent factor analysis


### Knowledge Based Recommedantion System

`Recommending movies based on "weighted_rating".` 


`Weighted rating function to compute the IMDB weighted rating for each movie.`


### Content based recommendation system


`Main idea` - Recommend items to the user similar to previous items rated highly or watched by the user.

Example:
1. Movies on Netflix:

• Recommend courses taught by the same tutor, or similar kind of content.

2. Websites, blogs, news:

• Articles with similar content.

`Plan of action`

Here we're gonna start with users and find out the user profile.
for example, we might look at the content that the user has rated highly or the set of the content user has watched more frequently.
Based on those items we are going build item profile. Item profile is the description of the item.
for example: If User X enrolled in big data course then there will be a high chance that he might like to study SQL courses as well.

`Item profiles`

1. For each item, create an item profile.
2. The profile is a set of features.
Videos: Metadata & tags. Movies: Author, title, actor. 3. Convenient to think of item profile as a vector.
Now we have an item profile next task is to create a user profile.

`User profiles`

1. User has rated items with profile i1.....,i(n), where i1....i(n) are vectors

2. Now the simplest way to construct the user profile from a set of item profiles is just
to take a weighted average of rated item profiles.

3. Variant: Normalize weights using an average rating of the user.

Now we have an Item profile and User profile we can recommend certain items.
The key step in this is to take a pair of user profile and item profile and figure out what the rating for that user and items pair likely to be.
Both are vectors in high dimensional space.
We can calculate the similarities of vectors using cosine similarities, so the way we make predictions as follows.

Given the user X, we compute the cosine similarities between that user and all the item in catalogue & then we pick the item with the highest cosine similarity and recommend that user.

`Pros: Content-based Approach`

1) The biggest pro on content-based recommendation approach is that you don't need data about other users to make a recommendation to a specific user.
2) Able to recommend to users with unique tastes.
3) Able to recommend new or unpopular items so we don't have a so-called first rater
problem.

`Cons: Content-based Approach`

1) Finding the appropriate feature is hard

2) Overspecialization.
• Never recommend items outside the user's content profile
• People might have multiple interests
• Unable to exploit quality judgements of other users
(There might be a certain video content that is widely popular across a cross-section of users.
However, the current user has not expressed interest in that kind of content therefore, the content-based approach will never recommend that content to that user.)

3) Cold start problem for new users
(Generally, the recommendation system start new users with some kind of average profile based on a system-wide average & over time user profile evolves as user rates more & more items)


### Use-User Collaborative filtering recommendation system



The basic idea behind collaborative filtering is very simple.
Suppose we have user X to whom you want to make recommendations. What collaborative method does it find a group of other users, whose likes and dislikes are similar to user X

1. Consider user X
2. Find set N of other users whose ratings are "similar" to X's rating.
3. Estimate X's ratings based on ratings of users in N.

`Collaborative filtering is of 2 types:`

1) User-User collaborative filtering 2) Item-Item collaborative filtering

`User-User collaborative filtering`

For example, suppose you're doing a movie recommendation. Now this group of users like the same movies that X likes & dislike the same movies that X dislikes.
We call this set of users, the neighbourhood of users X. Once we find the neighbourhood of users similar to user X, we find other movies that are liked by a lot of users in set N and recommend those items to the users X.
This is called user-user collaborative filtering.

Item-Item collaborative filtering

1. For item i, find other similar items.
2. Estimate rating for item i based on ratings for similar items
3. Use the same similarity metrics & prediction function as we used in the user-user
model.

In theory, Item-Item collaborative filtering & user-user collaborative filtering are dual approaches but in practice, Item-Item collaborative filtering outperforms user-user collaborative filtering in many use cases because items are "simpler" than "users".

• The item belongs to a small set of "genres", users have varied tastes.
• Items similarity is more meaningful than user similarity.

Therefore, it turns out that the notion of item similarity is inherently more meaningful than the notion of user similarity.

`Pros: Collaborative filtering`

1. Works for any kind of items without requiring any feature selection.
This is the biggest advantage of collaborative filtering because it turns out to be a tough problem to find the right set of features and it obviates this need for feature selection for complex things such as images, videos, music so on.

`Cons: Collaborative filtering`

1. Cold Start
• Need enough users in the system to find a match
we need to find enough set of similar items for a given item or a set of similar users for a given user but if there are not enough users in the system, it's hard to find a match.
2. Sparsity
• The user/rating matrix is sparse
• Hard to find users that have rated the same items.
3. First rater
• Cannot recommend an unrated items • New items, Esoteric items.
4. Popularity bias
• Tends to recommend popular items.

Recommending popular items works well but if every item that's recommended is popular can completely crowd out a unique recommendation that can be made for a specific user.

We can overcome the above difficulties by designing Hybrid methods

1. Add the content-based method to collaborative filtering.
• Add item profile for new item problem & make a recommendation of new items to
users.
• We can also take new users and use demographic information about new users to
build a synthetic profile for them & that deal with the new user problem.
2. Implement two or more different recommenders and combine predictions perhaps
using the linear model.


### Latent factor recommendation system 


Latent Matrix Factorization is an incredibly powerful method to use when creating a Recommender System. Ever since Latent Matrix Factorization was shown to outperform other recommendation methods in the Netflix Recommendation contest, its been a cornerstone in building recommender systems.

Latent factor recommendation system tackling the Recommendation problem.

Given a set of m users and n items, and set of ratings from the user for some items, try to recommend the top items for each user. There are many flavours and alternate deviations of this problem, most of which add more dimensions to the problem, like adding tags. What makes Latent Matrix Factorization powerful is that it yields really strong results from the core problem, and can be a good foundation to build from.

`The Approach:`

First, we initialize 2 two matrices from a gaussian distribution (random initialisation). The first one will be a m x k matrix P while the second will be a k x n matrix Q. When these two matrices multiply with each other, they result in an m x n matrix, which is exactly the size of our R matrix in which we are trying to predict.
Dimension k is one of our hyper-parameters, which represents the number of latent factors we’re using to estimate the R matrix.

With our Matrices P, Q, we’ll optimize their values by using Stochastic Gradient
Descent. 
Therefore, you’ll have two more hyper-parameters to optimize, learning rate and epochs. For each Epoch, we’re going to iterate through every known value in our original m x n matrix.

Then, we’ll get an error or residual value e by subtracting the original value by the dot product of the original value in user’s row in P and its item’s column in Q. we’ll update both of the matrices P and Q simultaneously by adding the current row for P and Q by the learning rate times the product of the error times the other Matrix’s values.
Therefore, we will solve the recommendation as an optimization problem. Find P & Q which minimize the sum of squared error & we are going to predict missing or unknown values.

`Pros: Latent factor`

1) Act as Dimensionality reduction
when we factorize a m x n matrix into two m x k matrix and k x n matrix we are reducing "n" items to "k" factors.
K factor can be b/w 10-250
2) The key is that recommending based on factors is more robust than just using movie similarities, maybe a user hasn’t seen a particular "Content" but the user might have seen other "content" that is related to previous content via some latent factors and those can be used.

`Cons: Latent factor`

1) The main problem is the Cold start problem. 
2) Can be computational expensive

