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


