## Twitter Database Schema

### Entities:

1. **User**
   - `id`: string (primary_key)
   - `username`: string (unique)
   - `email`: email
   - `password`: string
   - `date_of_registration`: date
   - `points`: integer

2. **UserProfile**
   - `id`: string (primary_key)
   - `user_id`: foreign_key(User)
   - `location`: string
   - `website_url`: url
   - `twitter_url`: url
   - `github_url`: url

3. **Tweet**
   - `id`: string (primary_key)
   - `user_id`: foreign_key(User)
   - `content`: string (max_length=280)
   - `time_posted`: datetime
   - `likes_count`: integer

4. **Follow**
   - `id`: string (primary_key)
   - `follower_id`: foreign_key(User)
   - `following_id`: foreign_key(User)
   - `time_followed`: datetime

5. **Like**
   - `id`: string (primary_key)
   - `user_id`: foreign_key(User)
   - `tweet_id`: foreign_key(Tweet)
   - `time_liked`: datetime

6. **TweetView**
   - `id`: string (primary_key)
   - `viewer_id`: foreign_key(User)
   - `tweet_id`: foreign_key(Tweet)
   - `time_viewed`: datetime

7. **List**
   - `id`: string (primary_key)
   - `user_id`: foreign_key(User)
   - `name`: string (max_length=50)

8. **ListMembership**
   - `id`: string (primary_key)
   - `list_id`: foreign_key(List)
   - `user_id`: foreign_key(User)

### Relationships:

- User -> Tweets: 1 -> Many
- User -> Followers: 1 -> Many
- User -> Following: 1 -> Many
- User -> Likes: 1 -> Many
- User -> TweetViews: 1 -> Many
- User -> Lists: 1 -> Many
- List -> Members: Many <-> Many relationship

### Constraints:

- One user can like a tweet only once.
- One user can follow another user only once.
- A user can post multiple tweets.
- A tweet can have multiple likes.
- A user can view multiple tweets.
- A user can be a member of multiple lists.
- The name of a list should be unique for a user.
- The content of a tweet is limited to 280 characters.
