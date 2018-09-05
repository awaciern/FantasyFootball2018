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

## PlayerData Excel Spreadsheet Content


## PPR Note

## Usage for Drafting and Auto-Drafting

## Limitations
