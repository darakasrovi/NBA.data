# NBA.data
from nba_api.stats.static import players 
import pandas as pd
player_dict = players.get_players()


#how to get individual player
pg = [player for player in player_dict if player ['full_name'] == 'Paul George'][0]
pg_id = pg['id']


from nba_api.stats.static import teams
team_dict = teams.get_teams()

#how to get individual team
wolves = [team for team in team_dict if team ['full_name'] == 'Minnesota Timberwolves'][0]
wolves_id = wolves['id']

from nba_api.stats.endpoints import playergamelog
from nba_api.stats.library.parameters import SeasonAll 

gamelog_pg = playergamelog.PlayerGameLog(player_id='202331',season = '2020')
gamelog_pg_df = gamelog_pg.get_data_frames()[0]

gamelog_pg_all = playergamelog.PlayerGameLog(player_id='202331',season = SeasonAll.all)
gamelog_pg_df_all = gamelog_pg_all.get_data_frames()[0]

from nba_api.stats.endpoints import leaguegamefinder
wolves_games = leaguegamefinder.LeagueGameFinder(team_id_nullable=wolves_id).get_data_frames()[0]
