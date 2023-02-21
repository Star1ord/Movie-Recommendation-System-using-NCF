# Movie-Recommendation-System-using-NCF
Introduction

Problem

It’s really hard to find a great movie that would suit you. You waste a lot of time trying to find it. Nowadays, there tones of movies and you just can’t decide which one to watch.

Literature review:
How to make a movie recommender: creating a recommender engine using Keras and TensorFlow. This tutorial uses ANN for a recommendation system. Trains the model using ANN and in the result outputs top k movies for particular user from the dataset.
Movie-Recommendation-System-Using-KNN-Algorithm. This solution uses KNN and I initially planned to use it. But I couldn’t find elements of DL here. Simple ML.
MovieLens-Hybrid-Movie-Recommendation-System. This project has an NCF model. Uses “timestamps”, rating-based and uses “user_id” to identify unique reviews. I took the idea of my project from here.
NLP-based Movie Recommendation System it’s similar to [1] solution. Uses NLP to output top movies that’s similar to the movie we entered.

Current Work(Most of the explanation are on the notebook)

I’ve found a dataset on MovieLens(25M Dataset). 
Based on the solutions and tutorials above I decided to use NCF model.
I preprocessed the dataset
Split it using Leave-one-out methodology
Dropped the unnecessary columns for the project
Converted explicit feedback(ratings column) to implicit feedback. Converted them to 1’s
With 4:1 ratio created negative review samples. That was done to movies that weren’t interacted with by the user.
I’ve created Pytorch Dataset class to facilitate training of my model.
In notebook, explained how NCF model works and provided illustrations, example + article
Created the NCF model itself
Instantiated it and trained for 5 epochs and 1 google collab gpu.
Explained how evaluation for recommendation system works on bullet list
Evaluated model with Hit Ratio 25. Result: 90%.
Data and Methods
Information about the data (probably analysis of the data with some visualisations)
MovieLens Dataset contains 25million rows with 4 columns. 
userId, movieId, rating and timestamp
 
Here is the dataset:

62,000 users and 25m ratings:

Source of the picture above
Description of the ML models you used with some theory
Model - Neural Collaborative Filtering (NCF)
Article
User Embeddings
An embedding is a low-dimensional space that captures the relationship of vectors from a higher dimensional space.
Ex.: User loves 2 genres - Comedy and thrillers movies.
1st dimension is - how much he loves comedy movies. 2nd dimension is - how much he loves thriller movies.


Let's say, Nurzhas loves thrillers, but doesn't likes thrillers. So, in graph, he would look like this:

Other user, Yerasyl is opposite of Nurzhas.
This is known as 2d embedding. Here we can easily track preferences of users in 2d linespace.
More dimensions = more traits of users. In this model exactly, I used 8d model.
Learned Embeddings
Seperate movie embegging will be used to represent the traits of movies(in lowerd dimension).
How to automatically get weights for embeddings? Answers is - Collaborative Filteging.
By using the ratings dataset, we can identify similar users and movies, creating user and item embeddings learned from existing ratings.
Model Architecture
User and movie(item) embeddings are key to the model.
Let's walk through the model architecture using the following training sample:

userId
movieID
interacted
17
4
1

here that's positive review, because user interacted with movie.

The user input vector and item input vector are fed to the user embedding and item embedding respectively, which results in a smaller, denser user and item vectors.
The embedded user and item vectors are concatenated before passing through a series of fully connected layers, which maps the concatenated embeddings into a prediction vector as output.
Finally, we apply a Sigmoid function to obtain the most probable class.
Results
Evaluating our Recommender System
I simulated it's evaluation for 25 items that could be recommended for user.
User have 99 items that he didn't click on.
We combine it with 1 test item(remember Avatar movie?)
Run the model, and rank them according to their probabilities.
I chose top 25 movies from this 100 initial items. If the test movie is there, then out model works.
Repeat it for all users. The Hit Ratio is then the average hits.
This is Hit Ratio 25, and it's used in most of the modern recommendation systems.

To put this into context, what this means is that 90% of the users were recommended the actual item (among a list of 25 items) that they eventually interacted with.

One of those items will be next movie that  you will watch.
Discussion
Critical review of results 
I tried evaluating it with accuracy or RMSE, but it didn't fit the recommendation system evaluation.
Why? Because, user don't have to click on every item that he sees. Instead, we need him to click on one of the many items. As long as users obey this pattern, our system works great.
Model showed great results on evaluation, 
Next steps
 I’ve used one csv of a huge dataset. From now on, I can continue it by actually showing movie titles for every user. I should look more on different solutions, especially MovieLens-Hybrid-Movie-Recommendation-System, so I could further develop the idea of this project.





