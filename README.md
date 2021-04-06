# Election_Analysis

## Project Overview
A Colorado Board of Elections employee has given you the following tasks to complete the election audit of a recent congressional election.

1. Calculate the total number of voters cast.
2. Get a complete list of candidates who received votes. 
3. Calculate the total number of votes each candidate received.
4. Calculate the percentage of votes each candidate won.
5. Determine the winnder of the election based on popular vote. 

## Resources
- Data Source: election_results.csv
- Soft ware: Python 3.6.1, Visual Studio Code, 1.38.1

## Overview of Election Audit
The election commission requested that we gather additional data for them. This time they wanted the following:
- The voter turnout for each county
- The percentage of votes from each county out of the total count 
- The county with the highest turnout
The results are to be reported in a ".txt" file named "election_results.txt"
The purpose of this report is to help the election commission map out where the majority of votes are coming from, and who they support the most. This type of data is useful for not only reporting on the current election, but also helping future candidates map out their chances. 

## Election-Audit Results
- There were "369,711" votes cast in the election.
- County Votes:
    - Jefferson: 10.5% (38,855)
    - Denver: 82.8% (306,055)
    - Arapahoe: 6.7% (24,801)
- Denver County had the largest amount of votes
- The candidate results were:
    - Charles Casper Stockham received "23.0%" of the vote and "85,213" number of votes.
    - Diana DeGette received "73.8%" of the vote and "272,892" number of votes.
    - Raymon Anthony Doane received "3.1%" of the vote and "11,606" number of votes.
- The winner of the election was:
    - Candidate (Diana DeGette), who received "73.8%" of the vote and "272,892" number of votes.
## Challenge Summary
The results displayed as the following:
Election Results:![election_analysis](https://github.com/Hamza97anh/Election_Analysis/blob/ea36846afc387660a81b97eb4bc48954bc335741/Resources/election_analysis.PNG)

# The code used to produce the results. 
---------------------------------------------------------------------------------------
### -*- coding: UTF-8 -*-
"""PyPoll Homework Challenge Solution."""

### Add our dependencies.
import csv
import os

### Add a variable to load a file from a path.
file_to_load = os.path.join("Resources", "election_results.csv")
### Add a variable to save the file to a path.
file_to_save = os.path.join("analysis", "election_analysis.txt")

### Initialize a total vote counter.
total_votes = 0

### Candidate Options and candidate votes.
candidate_options = []
candidate_votes = {}

### 1: Create a county list and county votes dictionary.
county_options = []
county_votes = {} 


### Track the winning candidate, vote count and percentage
winning_candidate = ""
winning_count = 0
winning_percentage = 0

### 2: Track the largest county and county voter turnout.
largest_county = ""
largest_count = 0
largest_percentage = 0


### Read the csv and convert it into a list of dictionaries
with open(file_to_load) as election_data:
    reader = csv.reader(election_data)

    # Read the header
    header = next(reader)

    # For each row in the CSV file.
    for row in reader:

        # Add to the total vote count
        total_votes = total_votes + 1

        # Get the candidate name from each row.
        candidate_name = row[2]

        # 3: Extract the county name from each row.
        county_name = row[1]

        # If the candidate does not match any existing candidate add it to
        # the candidate list
        if candidate_name not in candidate_options:

            # Add the candidate name to the candidate list.
            candidate_options.append(candidate_name)

            # And begin tracking that candidate's voter count.
            candidate_votes[candidate_name] = 0

        # Add a vote to that candidate's count
        candidate_votes[candidate_name] += 1

        # 4a: Write an if statement that checks that the
        # county does not match any existing county in the county list.
        if county_name not in county_options:

            # 4b: Add the existing county to the list of counties.
            county_options.append(county_name)

            # 4c: Begin tracking the county's vote count.
            county_votes[county_name] = 0

        # 5: Add a vote to that county's vote count.
        county_votes[county_name] += 1


### Save the results to our text file.
with open(file_to_save, "w") as txt_file:

    # Print the final vote count (to terminal)
    election_results = (
        f"\nElection Results\n"
        f"-------------------------\n"
        f"Total Votes: {total_votes:,}\n"
        f"-------------------------\n\n"
        f"County Votes:\n")
    print(election_results, end="")

    txt_file.write(election_results)

    # 6a: Write a for loop to get the county from the county dictionary.
    txt_file.write(election_results)
        # 6b: Retrieve the county vote count.
    for county_name in county_votes:
        # 6c: Calculate the percentage of votes for the county.
        votes = county_votes[county_name]
        vote_percentage = float(votes) / float(total_votes) * 100
        county_results = (
            f"{county_name}: {vote_percentage:.1f}% ({votes:,})\n")

         # 6d: Print the county results to the terminal.
        print(county_results)
         # 6e: Save the county votes to a text file.
        txt_file.write(county_results)
         # 6f: Write an if statement to determine the winning county and get its vote count.
        if (votes > largest_count) and (vote_percentage > largest_percentage):
            largest_count = votes
            largest_county = county_name
            largest_percentage = vote_percentage

    # 7: Print the county with the largest turnout to the terminal.
    largest_county_summary = (
        f"-------------------------\n"
        f"Largest county: {largest_county}\n"
        f"-------------------------\n")
    print(largest_county_summary)
    # 8: Save the county with the largest turnout to a text file.
    txt_file.write(largest_county_summary)

    # Save the final candidate vote count to the text file.
    for candidate_name in candidate_votes:

        # Retrieve vote count and percentage
        votes = candidate_votes.get(candidate_name)
        vote_percentage = float(votes) / float(total_votes) * 100
        candidate_results = (
            f"{candidate_name}: {vote_percentage:.1f}% ({votes:,})\n")

        # Print each candidate's voter count and percentage to the
        # terminal.
        print(candidate_results)
        #  Save the candidate results to our text file.
        txt_file.write(candidate_results)

        # Determine winning vote count, winning percentage, and candidate.
        if (votes > winning_count) and (vote_percentage > winning_percentage):
            winning_count = votes
            winning_candidate = candidate_name
            winning_percentage = vote_percentage

    # Print the winning candidate (to terminal)
    winning_candidate_summary = (
        f"-------------------------\n"
        f"Winner: {winning_candidate}\n"
        f"Winning Vote Count: {winning_count:,}\n"
        f"Winning Percentage: {winning_percentage:.1f}%\n"
        f"-------------------------\n")
    print(winning_candidate_summary)

    # Save the winning candidate's name to the text file
    txt_file.write(winning_candidate_summary)
--------------------------------------------------------------------------------
## Election-Audit Summary
This script manages to summarizes and sort an excel sheet into 13 lines the effectivly provide a brief overview of thie election results. You can see exactly which county has the most active voters, and how much of the votes each candidate got. By large margine. Denver was the largest county, and therefore future candidates can know where to focus the majority of their campaign if they see that as a fit stratgy. 
This code can be modified to sort through other elections in the same manner with a few tweeks of the script. Simply changing the name of the .csv sheet where the data is pulled from and the rows to be calculated should provide the desired results if necessary. 
