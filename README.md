###  IFT6758 Batch 5 Milestone Project

## Data Acquisition 

## Cleaning the Data

After saving the data, we only need to work with a portion of it. As such, we will need to look at the parts that are interesting.

Taking a sample game, .
We should probably keep track of the team ids, which are found like so:

```
game_id = game_data['gameData']['game']['pk']

# get team id for home and away teams
home_team_id = game_data['gameData']['teams']['home']['id']
away_team_id = game_data['gameData']['teams']['away']['id']

# get id for season in which game was played
game_season = game_data['gameData']['game']['season']
```

Looking at each play, they looks like this:

```
{'about': {'dateTime': '2016-10-12T23:19:59Z',
           'eventId': 8,
           'eventIdx': 9,
           'goals': {'away': 0, 'home': 0},
           'ordinalNum': '1st',
           'period': 1,
           'periodTime': '01:11',
           'periodTimeRemaining': '18:49',
           'periodType': 'REGULAR'},
 'coordinates': {'x': -77.0, 'y': 5.0},
 'players': [{'player': {'fullName': 'Mitchell Marner',
                         'id': 8478483,
                         'link': '/api/v1/people/8478483'},
              'playerType': 'Shooter'},
             {'player': {'fullName': 'Craig Anderson',
                         'id': 8467950,
                         'link': '/api/v1/people/8467950'},
              'playerType': 'Goalie'}],
 'result': {'description': 'Mitchell Marner Wrist Shot saved by Craig Anderson',
            'event': 'Shot',
            'eventCode': 'OTT8',
            'eventTypeId': 'SHOT',
            'secondaryType': 'Wrist Shot'},
 'team': {'id': 10,
          'link': '/api/v1/teams/10',
          'name': 'Toronto Maple Leafs',
          'triCode': 'TOR'}}
{'about': {'dateTime': '2016-10-12T23:29:09Z',
           'eventId': 27,
           'eventIdx': 43,
           'goals': {'away': 1, 'home': 0},
           'ordinalNum': '1st',
           'period': 1,
           'periodTime': '08:21',
           'periodTimeRemaining': '11:39',
           'periodType': 'REGULAR'},
 'coordinates': {'x': -70.0, 'y': 1.0},
 'players': [{'player': {'fullName': 'Auston Matthews',
                         'id': 8479318,
                         'link': '/api/v1/people/8479318'},
              'playerType': 'Scorer',
              'seasonTotal': 1},
             {'player': {'fullName': 'Zach Hyman',
                         'id': 8475786,
                         'link': '/api/v1/people/8475786'},
              'playerType': 'Assist',
              'seasonTotal': 1},
             {'player': {'fullName': 'William Nylander',
                         'id': 8477939,
                         'link': '/api/v1/people/8477939'},
              'playerType': 'Assist',
              'seasonTotal': 1},
             {'player': {'fullName': 'Craig Anderson',
                         'id': 8467950,
                         'link': '/api/v1/people/8467950'},
              'playerType': 'Goalie'}],
 'result': {'description': 'Auston Matthews (1) Wrist Shot, assists: Zach '
                           'Hyman (1), William Nylander (1)',
            'emptyNet': False,
            'event': 'Goal',
            'eventCode': 'OTT27',
            'eventTypeId': 'GOAL',
            'gameWinningGoal': False,
            'secondaryType': 'Wrist Shot',
            'strength': {'code': 'EVEN', 'name': 'Even'}},
 'team': {'id': 10,
          'link': '/api/v1/teams/10',
          'name': 'Toronto Maple Leafs',
          'triCode': 'TOR'}}
```

From here, we see we want the following fields for each play:

```
col_names = ['about/dateTime', 'about/period', 'about/periodTime', 'about/periodType', 'coordinates', 'players', 
             'result/secondaryType', 'result/eventTypeId',
            'team/id', 'team/name', 'team/triCode']
col_names_goal = ['result/emptyNet', 'result/strength/code']
```
