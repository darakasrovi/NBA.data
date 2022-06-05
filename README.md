# NBA.data
from nba_api.stats.static import players 
import pandas as pd
player_dict = players.get_players()
player_dict_df = pd.DataFrame(player_dict)



#how to get individual player
pg = [player for player in player_dict if player ['full_name'] == 'Paul George'][0]
pg_id = pg['id']


from nba_api.stats.static import teams
team_dict = teams.get_teams()

#how to get individual team
clippers = [team for team in team_dict if team ['full_name'] == 'Los Angeles Clippers'][0]
clippers_id = clippers['id']

from nba_api.stats.endpoints import playergamelog
from nba_api.stats.library.parameters import SeasonAll 

gamelog_pg = playergamelog.PlayerGameLog(player_id='202331',season = '2020')
gamelog_pg_df = gamelog_pg.get_data_frames()[0]

gamelog_pg_all = playergamelog.PlayerGameLog(player_id='202331',season = SeasonAll.all)
gamelog_pg_df_all = gamelog_pg_all.get_data_frames()[0]


from nba_api.stats.endpoints import shotchartdetail

from pandas import DataFrame
import matplotlib as mpl
import matplotlib.pyplot as plt

BBplayers = players.get_players()
BBteams = teams.get_teams()

print(type(players))
print(BBplayers[0])
print(len(BBplayers))


#how to get shot chart 
George = [player for player in BBplayers if player['full_name'] == 'Paul George'][0]
Pg_id = George['id']
print(Pg_id)


Clippers = [name for name in BBteams if name['full_name']=='Los Angeles Clippers'][0]
Clippers_id = Clippers['id']
print(Clippers_id)
print(type(Clippers_id))


PG_ShotsChart = shotchartdetail.ShotChartDetail(player_id='202331',team_id=1610612746)
PG_ShotsChart_df = PG_ShotsChart.get_data_frames()[0]



print(PG_ShotsChart)
