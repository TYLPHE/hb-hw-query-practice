# Querying with SQLAlchemy

5/4 Homework

1. Find the user with the email cats@gmail.com.
```python
    cat1 = db.session.query(User).filter_by(email = 'cats@gmail.com').all()
    cat2 = User.query.filter(User.email == 'cats@gmail.com').all()
    cat3 = User.query.filter_by(email = 'cats@gmail.com').all()
```
2. Find any movies with the exact title “Cape Fear”.
```python
    movie1 = db.session.query(Movie).filter_by(title = 'Cape Fear').all()
    movie2 = Movie.query.filter(Movie.title == 'Cape Fear').all()
    movie3 = Movie.query.filter_by(title = 'Cape Fear').all()
```
3. Find all users with the zipcode 90703.
```python
    zip1 = db.session.query(User).filter_by(zipcode = '90703').all()
    zip2 = User.query.filter(User.zipcode == '90703').all()
    zip3 = User.query.filter_by(zipcode = '90703').all()
```
4. Find all ratings of with the score of 5.
```python
    # q1 can be looped in a for loop
    q1 = db.session.query(Movie).options(db.joinedload(Movie.ratings)).all()
    
    # q2 will return a list of Movies that had 5 stars. 
    # Looping causes multiple queries
    q2 = Movie.query.join(Rating).filter_by(score = 5).all()
```
After looking at the solution, I learned that Ratings can be filtered by score. Because Ratings are linked to Movie, we can do Rating.movie.title to find the title of the movie.
```python
    ratings_of_five = Rating.query.filter_by(score=5).all()
```
5. Find the rating for the movie whose id is 7, from the user whose id is 6.
```python
    q = Rating.query.join(User, Movie).filter( (User.user_id == 6) & (Movie.movie_id == 7) ).all()
```

After looking at the solution, I learned that Rating already has user_id and movie_id...wow
```python
    rating = Rating.query.filter_by(user_id=6, movie_id=7).first()
```
6. Find all ratings that are larger than 3.
```python
    q = Rating.query.filter(Rating.score > 3).all()
```
