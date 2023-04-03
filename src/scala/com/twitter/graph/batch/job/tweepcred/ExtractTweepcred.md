[View code on GitHub](https://github.com/misbahsy/the-algorithm/src/scala/com/twitter/graph/batch/job/tweepcred/ExtractTweepcred.scala)

The `ExtractTweepcred` class is a Scalding job that calculates the "tweepcred" score for Twitter users based on their pagerank and other user information. The `ExtractTweepcred` class takes in several command-line arguments, including the input pagerank file, user mass TSV file, and output files for the pagerank and tweepcred scores. There is also an optional argument to enable post-adjustment of the pagerank scores based on the number of followers and followings of each user.

The `ExtractTweepcred` class first reads in the input pagerank file and maps each record to a tuple with zero followers and followings. It then reads in the user information from the `MostRecentCombinedUserSnapshotSource` and filters out any deactivated users or users with an ID of 0. For each valid user, it creates a tuple with the user ID, pagerank mass input of 0.0, number of followers, and number of followings. These tuples are then converted to a `Pipe` with columns for the user ID, mass input, number of followers, and number of followings.

The `ExtractTweepcred` class then combines the input pagerank and user information `Pipe`s by grouping them by the user ID and taking the maximum mass input, number of followers, and number of followings for each user. The resulting `Pipe` contains one record per user with the maximum mass input, number of followers, and number of followings.

The `ExtractTweepcred` class then writes the pagerank scores to the output pagerank file by discarding the number of followers and followings columns from the combined `Pipe`.

If post-adjustment is enabled, the `ExtractTweepcred` class then calculates the adjusted pagerank scores by mapping each record to a new mass input value based on the `Reputation.adjustReputationsPostCalculation` method, which takes in the original mass input, number of followers, and number of followings. The adjusted pagerank scores are then normalized by dividing each score by the sum of all scores. If post-adjustment is not enabled, the `ExtractTweepcred` class simply discards the number of followers and followings columns from the combined `Pipe`.

Finally, the `ExtractTweepcred` class calculates the tweepcred scores by mapping each mass input value to a scaled reputation score using the `Reputation.scaledReputation` method. The tweepcred scores are then written to the output tweepcred file, as well as two other files for the current and today's tweepcred scores.

Overall, the `ExtractTweepcred` class is a key component of the larger project to calculate and analyze the tweepcred scores of Twitter users. It takes in the necessary input files and command-line arguments, combines the pagerank and user information, calculates the adjusted pagerank scores if enabled, and finally calculates the tweepcred scores and writes them to output files.
## Questions: 
 1. What is the purpose of this code and what inputs/outputs does it expect? 
- This code calculates tweepcred from a given pagerank file and outputs the results to specified locations. It expects inputs for the pagerank file, user mass tsv file, and output locations for the pagerank and tweepcred files.

2. What is the significance of the POST_ADJUST variable and how does it affect the output? 
- POST_ADJUST is a boolean variable that determines whether to reduce pagerank for users with low followers compared to number of followings based on existing reputation code. If it is true, the code will adjust the reputations post-calculation and normalize the mass input. If it is false, the code will discard the num_followers and num_followings columns.

3. What is the purpose of the getInputPagerank function and how is it used in the code? 
- The getInputPagerank function reads in a Tsv file for the pagerank and maps the first and second columns to 'src_id' and 'mass_input', respectively. It is used in the code to get the input pagerank and map it to the 'num_followers' and 'num_followings' columns.