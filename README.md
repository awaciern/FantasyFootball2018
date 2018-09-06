# FantasyFootball2018
This project attempts to formulate player rankings and draft strategy for drafting a fantasy football team. The player rankings generated compare a player's projected fantasy score to that of an "average starter" for a league containing a certain number of theams.

## Theory
Building the optimal fantasy football team is about gaining a statistical edge over your oponents. This can be achieved by drafting the player available that gives you the greatest difference in projected points between them and the "average starter" at their fantasy position.

The "average starter" is determined by taking the average projected score for a starter at a certain position in a league. This depends on the number of players at each position that can start and earn points each week and the number of teams in the league. 

For this project I assumed the following number of starters at each position (this is a pretty standard set used by most leagues):
* 1 Quarterback (QB)
* 2 Running Backs (RB)
* 2 Wide Recievers (WR)
* 1 Tight End (TE)
* 1 Flex (RB/WR/TE)
* 1 Defense/ Special Teams (D/ST)
* 1 Kicker 

The player ranking analysis was performed for leagues of different numbers of teams based on the fantasy leagues I was in this year (8, 10, and 16). To understand an "average starter" let's say the league has n teams. An average starter at each position would be determined by the following:
* QB: Average projected score for the top n QBs (since 1 QB starts per team)
* RB: Average projected score for the top 2.5n RBs (since 2 RBs start per team and the Flex tends to be a RB or WR)
* WR: Average projected score for the top 2.5n RBs (since 2 RBs start per team and the Flex tends to be a RB or WR)
* TE: QB: Average projected score for the top n TEs (since 1 TE starts per team)
* D/ST: Average projected score for the top n D/STs (since 1 D/ST starts per team)
* K: Average projected score for the top n Ks (since 1 K starts per team)

Once the "average starter" at a position is determined, a player's "value" can be found by finding the difference between his projected score and that of the "average starter" at his position. This "value" or "adjusted score" can be used to build fantasy football rankings to draft by. These rankings target finding the maximum statistical advantage a player can provide you over an opponent. 

## Downloading and Running the Project
You can download this repository using the command `git clone <repo name>`. This project runs using python 3 and excel. All the required python packages are contained in the requirements.txt file; you can install these packages using the command `pip install -r requirements.txt `.

## Web Scraping Using Python Scripts
I scraped the data for this project from ESPN's fantasy player projections for 2018 (using python web scrapping) and Pro Football Reference's fantasy data for 2017 (downloaded as an excel file). This data was collected using the python scripts *get_espn_proj.py* and *get_prev_pts.py*. These scripts can be ran to build the basis for the PlayerData excel file. The filename addresses will need to be changed to those for your machine first.

*Note: D/ST and Kicker Fantasy data for 2017 was not available on Pro Football Reference and had to be manually entered from ESPN.

## PlayerData Excel Spreadsheet Content
The PlayerData excel spreadsheet contains the data, analysis, and rankings. All analysis and calculations were performed manually in excel. 

Each position (QB, RB, WR, TE, D/ST, K) has its own sheet containing the data and analysis used to build the rankings. The position sheets have the following columns:
* Player: Player name
* ESPN_Proj: ESPN's projected 2018 fantasy score for that player
* Prev_Yr_Pts: Pro Football Reference's 2017 fantasy score for that player
* My_Adj: My manual score adjustment for a specific player (due to rookies, injuries, or just my bias)
  Ex: Saquon Barkley has a +120 My_Adj becuase as a rookie he has no stats from last year a (and I just like him)
* Score: Projected fantasy score (calculated by [AVG(ESPN_Proj, Prev_Yr_Pts) + My_Adj])
* N_Adj_Score: Difference between that player's projected score and that of an "average starter" (where N is the number of teams in the league), representation of that player's "value"
* Avg Starter Score for # Teams: The "average starter" score for that position for a league of a certain number of teams

For each N, there is a corresponding sheet (N_Ranks) that contains the rankings of all players by their Adj_Score. These are the final rankings that show a player's "value"; they should be used for drafting. The N_Ranks sheets contain the following columns:
* Player: Player name
* Position: Position that player is
* Score: Projected fantasy score
* Adj_Score: Difference between that player's projected score and that of an "average starter", representation of that player's "value"

## PPR Note
There is a seperate folder titled *PPR*. This folder contains the same python scripts and PlayerData excel spreadsheet, except these are built for PPR scoring leagues.

## Usage for Drafting and Auto-Drafting
In theory, the rankings produced by these projects should give you a complete draft guide. The player with the top "adjusted score" or "value" left when you pick should be the one draft in order to obtain the highest statistical edge over your opponent. However, this is problematic as it may lead you to drafting too many players at certain positions and not enough at others.

I would recommend using these rankings as a reference guide when drafting. Draft the top player in the rankings when it makes sense, and if you need to draft or avoid drating a ceratin postion, look at the rankings by position or group of positions. I drafted two fantasy teams using this method.

If you are auto-drafting, simply putting in your rankings to your fantasy site can be problematic. You will likely end up with too many of one position (especially QBs and TEs, as they tend to dominate the middle round rankings since other users will not be selecting as many). I would recommed setting how many players of each position you want to draft (ESPN lets you do this). I drafted one fantasy team using auto-draft with the "adjusted score" rankings plugged in and the number of players at each position I wanted (2 QBs, 5 RBs, 5 WRs, 2 TEs, 1 D/ST, 1 K - feel free to change this to your prefernce). 

## D/ST and Kicker Problem
One problem with the rankings this project generates is that it values Defenses/ Special Teams and Kickers way more than typical fantasy rankings. Since it is just looking for a statistical advantage over the "average starter", the best D/STs and Ks have the potential to be ranked very highly. However, typical fantasy players won't draft a D/ST or K before most of their starters have been filled out.

My solution to this was to manually deduct from the "adjusted score" of D/STs and Ks. I applied a certain score deduction to all D/STs and Ks so that the first one was ranked at a point I deemed acceptable to draft (still higher than most would consider).

Perhaps the rankings generated by this project indicate that D/STs and Ks are severely undervalued by fantasy football users. However, I wanted to take advantage of being able to get very good D/STs and Ks in later rounds than the rankings valued them at. 

## Fututre Improvements
1. Data:
The data used in the project was very rudimentary, minimal, and biased (only ESPN projections last year's scores, and my manual adjustments were used to determine a player's projected score). Ideally, more comprehensive and unbiased data would be used to build the player projections

2. Draft Logic:
A draft logic program should be created to determine the best player to draft when accounting for the players and positions that have already been drafted. This would also enable flawless auto-drafting.

3. Drafting An Entire League:
How would an entire league of teams drafting using these rankings turn out?
